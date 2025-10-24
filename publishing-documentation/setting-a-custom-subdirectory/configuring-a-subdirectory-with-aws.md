---
description: >-
  Host your documentation with a /docs subdirectory using AWS CloudFront and
  Route 53.
icon: aws
---

# Configuring a subdirectory with AWS using CloudFront and Route 53

{% include "../../.gitbook/includes/ultimate-hint.md" %}

{% hint style="info" %}
This guide covers setting up a subdirectory using AWS CloudFront and Lambda@Edge. This is one approach for AWS users. If you have a different AWS setup (such as a load balancer with EC2 instances running NGINX), you may need to configure your reverse proxy differently. Contact [support](https://gitbook.com/docs/help-center/further-help/how-do-i-contact-support) if you need guidance for alternative configurations.
{% endhint %}

{% stepper %}
{% step %}
#### Configuring your GitBook site

In your GitBook organization, click on your docs site name in the sidebar, then click **Manage site** or open the **Settings** tab. Open the **Domain and redirects** section and under ‘Subdirectory’, click **Set up a subdirectory**.

Enter the URL where you would like to host your docs. Then specify the subdirectory for docs access, e.g. `example.com/docs`, and click **Configure**.

Under **Additional configuration**, you will now see a proxy URL. You’ll use this in the next step when configuring your Lambda function. Copy it to your clipboard.
{% endstep %}

{% step %}
#### Create your Lambda@Edge function

Sign into your AWS Console and navigate to **Lambda**.

Click the **Create function** button.

Choose **Author from scratch**, then:

* Give your function a descriptive name, like `gitbook-subpath-proxy.`
* Select **Node.js** as the runtime (use the latest available version).
* Leave the architecture and other settings as default.

Click **Create function**.
{% endstep %}

{% step %}
#### Update the Lambda function code

In the Lambda function editor, replace the default code with the following:

{% code lineNumbers="true" %}
```javascript
export const handler = async (event) => {
	const request = event.Records[0].cf.request;
	
	// update if your subdirectory is not /docs
	const subdirectory = '/docs';
	
	// update with your proxy URL below
	const target = new URL('<proxy URL you got from GitBook>');

	// rewrite: /docs* -> proxy.gitbook.site
	if (request.uri.startsWith(subdirectory)) {
		request.uri = target.pathname + request.uri.substring(subdirectory.length);

		// Remove trailing slash if present
		if (request.uri.endsWith('/')) {
			request.uri = request.uri.slice(0, -1);
		}

		request.origin = {
			custom: {
				domainName: target.host,
				port: 443,
				protocol: 'https',
				path: '',
				sslProtocols: ['TLSv1.2'],
				readTimeout: 30,
				keepaliveTimeout: 5,
				customHeaders: {},
			},
		};

		request.headers['host'] = [{ key: 'host', value: target.host }];
		request.headers['x-forwarded-host'] = [{ key: 'x-forwarded-host', value: target.host }];
	}
    
	return request;
};
```
{% endcode %}

{% hint style="warning" %}
Be sure to update `target` on line 8 with the proxy URL you got from GitBook in the first step. This will look like `https://proxy.gitbook.site/sites/site_XXXX`
{% endhint %}

{% hint style="warning" %}
Also be sure to update `subdirectory` on line 5 if you’re using a different subdirectory path than `/docs`.
{% endhint %}

Click **Deploy** to save your changes.
{% endstep %}

{% step %}
#### Configure Lambda permissions for Lambda@Edge

Before you can use your Lambda function with CloudFront, you need to configure the execution role to allow Lambda@Edge to assume it.

1. In your Lambda function, click on the **Configuration** tab
2. Click **Permissions** in the left sidebar
3. Under **Execution role**, click on the role name to open it in IAM
4. Click the **Trust relationships** tab
5. Click **Edit trust policy**
6. Replace the trust policy with the following:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "edgelambda.amazonaws.com",
                    "lambda.amazonaws.com"
                ]
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

Click **Update policy** to save.
{% endstep %}

{% step %}
#### Publish your Lambda function

Lambda@Edge requires a published version (not just `$LATEST`).

1. In your Lambda function, click the **Actions** dropdown in the upper right
2. Select **Publish new version**
3. Optionally add a description like “Initial version for CloudFront”
4. Click **Publish**
5. **Important:** Copy the ARN of the published version that appears at the top of the page (it will include a version number at the end, like `arn:aws:lambda:us-east-1:123456789:function:gitbook-subpath-proxy:1`)

{% hint style="warning" %}
Lambda@Edge functions must be created in the **us-east-1** (N. Virginia) region. If you created your function in a different region, you’ll need to recreate it in us-east-1.
{% endhint %}
{% endstep %}

{% step %}
#### Create your CloudFront distribution

Navigate to **CloudFront** in the AWS Console and click **Create distribution**.

Configure the following settings. Where settings are not specified, keep the default settings.

**Specify origin**

| Setting           | Value                                          |
| ----------------- | ---------------------------------------------- |
| **Origin type**   | Other                                          |
| **Custom origin** | Your main website domain (e.g., `example.com`) |

**Cache settings**

| Setting                   | Value                     |
| ------------------------- | ------------------------- |
| **Cache policy**          | CachingDisabled           |
| **Origin request policy** | AllViewerExceptHostHeader |

Click **Next,** select your preferred security protections, then click **Next** again.

Click **Create distribution**.

Wait for the distribution to deploy (status will change from “In Progress” to “Enabled”). This may take several minutes.
{% endstep %}

{% step %}
#### Associate Lambda@Edge with CloudFront

Once your CloudFront distribution is deployed:

1. Click on your distribution ID to open its settings
2. Go to the **Behaviors** tab
3. Select the default behavior and click **Edit**
4. Scroll down to **Function associations**
5. Under **Origin request**, select **Lambda@Edge**
6. In the **Lambda function ARN** field, paste the ARN of your published Lambda function (from step 5)
7. Check **Include body** to allow the function to access request bodies if needed
8. Click **Save changes**
{% endstep %}

{% step %}
#### Configure domain and DNS records

1. On the main page of your CloudFront distribution, click the **General** tab, and under **Alternate domain names**, click **Add domain**
2. Enter the domain for which you are configuring your subdirectory e.g. `example.com` and click **Next**
3. Select your existing TLS certificate, or create a new one, if needed, and click **Next** again
{% endstep %}

{% step %}
#### Configure Route 53 DNS records from CloudFront

If you’re using Route 53 for DNS, you’ll need to create or update your DNS records to point to your CloudFront distribution.

1. While remaining on the main page for your CloudFront distribution, make sure you are on the **General** tab, then below the URL that you have configured in **Alternate domain names,** click **Route domains to CloudFront.**
2. Click on **Set up routing automatically** to create A and AAAA DNS records for your domain

{% hint style="info" %}
If you’re not using Route 53, you’ll need to update your DNS provider’s settings to point your domain to your CloudFront distribution domain name. You can find this in the CloudFront distribution details under “Distribution domain name”.
{% endhint %}
{% endstep %}

{% step %}
#### Test your configuration

Once all changes have propagated (this can take 10–15 minutes):

1. Open a browser and navigate to your domain with the subdirectory path (e.g., `https://example.com/docs`)
2. You should see your GitBook documentation site!

If the site doesn’t load immediately, try:

* Waiting a few more minutes for DNS propagation
* Clearing your browser cache or trying an incognito window
* Running `nslookup yourdomain.com` in terminal to verify DNS is resolving correctly
* Checking CloudFront distribution status is “Enabled” and not “In Progress”

{% hint style="success" %}
Congratulations! Your GitBook documentation is now accessible via your custom subdirectory.
{% endhint %}
{% endstep %}
{% endstepper %}

### Troubleshooting

**Lambda function not triggering:**

* Ensure you published a version of your Lambda function (not using `$LATEST`)
* Verify the Lambda function is in the us-east-1 region
* Check that the trust policy includes `edgelambda.amazonaws.com`

**DNS not resolving:**

* DNS changes can take time to propagate (up to 48 hours, though usually much faster)
* Verify your Route 53 records are pointing to the correct CloudFront distribution
* Check that you deleted any old conflicting DNS records

**SSL certificate errors:**

* Ensure your SSL certificate in AWS Certificate Manager includes your custom domain
* Certificates for CloudFront must be created in the us-east-1 region

**Subdirectory not working:**

* Verify the `SUBDIRECTORY` value in your Lambda function matches what you configured in GitBook
* Check that the `target` in your Lambda function is correct
* Review CloudFront logs to see if requests are reaching the distribution
