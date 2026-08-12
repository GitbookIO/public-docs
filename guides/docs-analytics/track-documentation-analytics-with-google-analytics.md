---
description: >-
  Learn how to install and configure the Google Analytics integration so you can
  track detailed analytics from your docs site
---

# Track documentation analytics with Google Analytics

The Google Analytics integration for GitBook is available for all plans and provides an easy way to monitor your site's metrics in even more detail than you get from [the built-in insights](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/analytics/insights).

### Install and configure Google Analytics

{% stepper %}
{% step %}
### Obtain your measurement ID

To locate your measurement ID:

1. Open Google Analytics.
2. Navigate to the **Admin** section.
3. Under the **Data collection and modification** section, click **Data streams**.
4. Select the **Web** tab.
5. Click on your web data stream.
6. Find the measurement ID in the first row of the stream details. Copy it to your clipboard.

{% hint style="info" %}
A valid measurement ID starts with ‘G-’ followed by a combination of numbers and letters (e.g., ‘G-IT8OOK2K25’)&#x20;
{% endhint %}
{% endstep %}

{% step %}
### Install the integration in GitBook

Next up you need to install the Google Analytics integration directly from the [GitBook Integrations page](https://app.gitbook.com/integrations). To do this:

1. Find the Google Analytics integration in the **Integrations** page, accessible from the GitBook sidebar (or the link above).
2. Install the integration for your organization.
3. You can configure the integration for every site, but for now just choose **Install on specific site** and select the site you want from the drop-down.
4. To finish the configuration, paste in your measurement ID and click **Done**.
{% endstep %}

{% step %}
### Verify data collection

After configuration, it may take a few hours for data to start appearing in your Google Analytics dashboard.&#x20;
{% endstep %}
{% endstepper %}

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2Fwjetvhwhb2MFiWh1x2mN%2Fset-up-google-analytics.mp4?alt=media&token=e4eacbb1-2a9c-4227-837a-728cd1e9706c?autoplay=1&_loop=1" %}
Watch a quick video guide showing how to set up Google Analytics for your GitBook site.
{% endembed %}

### Troubleshooting

If no data has appeared in your Google Analytics dashboard after 48 hours:

1. Return to Google Analytics.
2. Click the **Admin** cog.
3. Navigate to **Data Streams** settings.
4. Select your data stream.
5. Check the top of the page for data reception status.&#x20;
6. Double-check that the measurement ID is correct in GitBook.
7. Ensure your site is published in GitBook and receiving traffic.&#x20;
