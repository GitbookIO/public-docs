---
description: Serve your docs under a subdirectory of your main domain.
---

# Custom subdirectories (Cloudflare, Vercel, AWS)

{% hint style="info" %}
Custom subdirectories are available on the Ultimate plan.
{% endhint %}

A custom subdirectory makes your docs site accessible at `example.com/docs`, rather than at a [custom domain](README.md) like `docs.example.com`. This keeps your docs URL consistent with the rest of your site, and can help SEO.

Configuring a subdirectory means setting things up in your website's backend, then finalizing the process in your GitBook site settings. The first step is the same regardless of provider:

### Configure your GitBook site

In your GitBook organization, click your docs site's name in the sidebar, then **Manage site** (or open **Settings**). Open **Domain and redirects**, and under **Subdirectory**, click **Set up a subdirectory**.

Enter the URL where you want to host your docs, specify the subdirectory (e.g. `example.com/docs`), and click **Configure**. Under **Additional configuration**, copy the **proxy URL** shown — you'll need it for whichever provider setup you follow below.

### Cloudflare

{% stepper %}
{% step %}
#### Create your Cloudflare worker

Sign into Cloudflare, go to **Workers & Pages**, click **Create**, then **Hello world** under "Start from a template." Give the worker a descriptive name (e.g. `mydocs-subpath-proxy`) and click **Deploy**.
{% endstep %}

{% step %}
#### Configure your custom domain

Click **Settings** on your worker, then **+ Add** under **Domains & Routes**. Choose **Custom domain** and enter your domain — without the subdirectory (`example.com`, not `example.com/docs`).
{% endstep %}

{% step %}
#### Update the worker code

Click **Edit code** (or **Continue to project** → **Edit code**), and replace the sample code with:

{% code lineNumbers="true" %}
```javascript
export default {
  fetch(request) { 
    const SUBDIRECTORY = '/docs';
    const url = new URL(request.url);
    const target = "<INSERT YOUR PROXY URL FROM GITBOOK>" + url.pathname.slice(SUBDIRECTORY.length);
    const proxy = new URL(
      target.endsWith('/') ? target.slice(0, -1) : target 
    )
    proxy.search = url.search;
    return fetch(new Request(proxy, request));
  }
};
```
{% endcode %}

{% hint style="info" %}
Update the URL on line 5 with the proxy URL from GitBook.
{% endhint %}

Click **Deploy**. Once it completes, visiting the URL should show your docs site.
{% endstep %}
{% endstepper %}

### Vercel

{% stepper %}
{% step %}
#### Update your vercel.json

In your Vercel app, open (or create) `vercel.json` at the root, and add:

```json
{
    "rewrites": [
        {
            "source": "/docs",
            "destination": "<INSERT YOUR PROXY URL FROM GITBOOK>"
        },
        {
            "source": "/docs/:match*",
            "destination": "<INSERT YOUR PROXY URL FROM GITBOOK>/:match*"
        }
    ]
}
```

Update the destination URLs with your proxy URL from GitBook.
{% endstep %}

{% step %}
#### Re-deploy and verify

Re-deploy your Vercel app with the updated configuration. Once it's live, visiting the URL should show your docs site.
{% endstep %}
{% endstepper %}

### AWS (CloudFront and Route 53)

{% hint style="info" %}
This covers one approach using CloudFront and Lambda@Edge. If your AWS setup differs (e.g. a load balancer with EC2 running NGINX), you may need to configure your reverse proxy differently — [contact support](../../../resources/get-support.md) for guidance.
{% endhint %}

{% stepper %}
{% step %}
#### Create your Lambda@Edge function

In the AWS Console, go to **Lambda** → **Create function** → **Author from scratch**. Name it descriptively (e.g. `gitbook-subpath-proxy`), select **Node.js** (latest version) as the runtime, leave other settings default, and click **Create function**.
{% endstep %}

{% step %}
#### Update the Lambda function code

Replace the default code with:

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
Update `target` (line 8) with your GitBook proxy URL (looks like `https://proxy.gitbook.site/sites/site_XXXX`), and `subdirectory` (line 5) if you're using something other than `/docs`.
{% endhint %}

Click **Deploy** to save.
{% endstep %}

{% step %}
#### Configure Lambda permissions for Lambda@Edge

1. In your Lambda function's **Configuration** tab, click **Permissions**.
2. Under **Execution role**, click the role name to open it in IAM.
3. Click **Trust relationships** → **Edit trust policy**, and replace it with:

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

Lambda@Edge requires a published version, not `$LATEST`:

1. Click **Actions** → **Publish new version** (optionally add a description).
2. Click **Publish**.
3. Copy the ARN of the published version (includes a version number, e.g. `arn:aws:lambda:us-east-1:123456789:function:gitbook-subpath-proxy:1`).

{% hint style="warning" %}
Lambda@Edge functions must be created in **us-east-1** (N. Virginia). Recreate your function there if you built it elsewhere.
{% endhint %}
{% endstep %}

{% step %}
#### Create your CloudFront distribution

In **CloudFront**, click **Create distribution**. Keep defaults except:

| Setting | Value |
|---|---|
| Origin type | Other |
| Custom origin | Your main website domain (e.g. `example.com`) |
| Cache policy | CachingDisabled |
| Origin request policy | AllViewerExceptHostHeader |

Click through your preferred security protections, then **Create distribution**. Wait for its status to change from "In Progress" to "Enabled" — this can take several minutes.
{% endstep %}

{% step %}
#### Associate Lambda@Edge with CloudFront

1. Open your distribution → **Behaviors** tab.
2. Select the default behavior → **Edit**.
3. Under **Function associations** → **Origin request**, select **Lambda@Edge**.
4. Paste your published Lambda function's ARN.
5. Check **Include body**.
6. Click **Save changes**.
{% endstep %}

{% step %}
#### Configure domain and DNS records

1. On the distribution's **General** tab, under **Alternate domain names**, click **Add domain** and enter your domain (e.g. `example.com`).
2. Select or create a TLS certificate, and continue.
{% endstep %}

{% step %}
#### Configure Route 53 DNS records

If you use Route 53: on the distribution's **General** tab, below your configured domain, click **Route domains to CloudFront**, then **Set up routing automatically** to create A and AAAA records.

{% hint style="info" %}
Not using Route 53? Point your domain to the CloudFront distribution's domain name (found under "Distribution domain name") in your own DNS provider instead.
{% endhint %}
{% endstep %}

{% step %}
#### Test your configuration

Once changes propagate (10–15 minutes), visit your domain with the subdirectory path (e.g. `https://example.com/docs`) — you should see your docs site.

If it doesn't load right away: wait a few more minutes for DNS, clear your browser cache or try incognito, run `nslookup yourdomain.com` to check DNS resolution, and confirm the CloudFront distribution status is "Enabled."
{% endstep %}
{% endstepper %}

#### Troubleshooting (AWS)

**Lambda function not triggering:** confirm you published a version (not `$LATEST`), that the function is in `us-east-1`, and that the trust policy includes `edgelambda.amazonaws.com`.

**DNS not resolving:** propagation can take up to 48 hours (usually faster); verify Route 53 points to the correct distribution; remove old conflicting DNS records.

**SSL certificate errors:** confirm your ACM certificate includes your custom domain, and was created in `us-east-1`.

**Subdirectory not working:** confirm `SUBDIRECTORY` in your Lambda function matches what you configured in GitBook, that `target` is correct, and check CloudFront logs for whether requests are reaching the distribution.
