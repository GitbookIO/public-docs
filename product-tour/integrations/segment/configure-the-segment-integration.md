---
description: Install and configure the Segment integration
---

# Configure the Segment integration

## Install the integration

To start using the Segment integration, you will need to install it in your GitBook library or just on a single space. To do this, follow the steps described in the [install an integration](../install-an-integration.md) section.

Once it is installed, you will need to connect it to your chosen Segment source **to complete the installation**. To do this, you will need to configure the integration.&#x20;

## Configure the integration

After installing the integration to your space or GitBook library, you will need to connect it to your Segment source.

{% hint style="success" %}
Before proceeding, make sure you have a Segment source ready to use and its write key handy. Go back to the [Segment page](./) to read more about this.
{% endhint %}

First, head to your **Segment dashboard**, navigate to the source's settings and copy the source's **write key**:

![Copy the Segment Source's write key](<../../../.gitbook/assets/Segment Write Key.png>)

Next, go back to **GitBook** and navigate to the Segment integration's **configuration screen**:

![Segment integration's configuration](<../../../.gitbook/assets/Segment Configuration.png>)

Then, **paste** the write key in the **write key** input field in the **space configuration** section and **press enter** to save the key:

![Save the source's write key](<../../../.gitbook/assets/Segment Space Configuration.png>)

Finally, repeat the above steps for each space you need to connect to the Segment integration.

To switch to another space and save the write key, click the **space dropdown** at the top right hand corner of the **space configuration** section, and select the specific space you want to connect:

![Switch to another space to save the write key](<../../../.gitbook/assets/Segment Swtich Spaces.png>)

### Test the configuration

Once you have configured the Segment integration on your space(s), you can test that the integration is correctly configured and sends [events](gitbook-segment-event.md) anytime a visitor access a page on your published content.

First, head to one of the spaces (which is [published](../../../publishing/publishing/space-publishing.md)) that you've connected to the integration. Then copy its published URL from the **get the link** section of the space's visibility menu:

![Get the link from the space's visibility menu](../../../.gitbook/assets/Publish.png)

Next, open that link **in a new tab** and start browsing your published content. Navigate between pages to generate multiple events.

Then go to your Segment dashboard and navigate to the source you've connected to the integration.

In the source's **debugger** tab (see [this section](https://segment.com/docs/connections/sources/debugger/) of Segment's documentation to access the debugger tool), you should see `[GitBook] space_view`  events showing up:

![View the GitBook events in the source's debugger](<../../../.gitbook/assets/Segment GitBook Event.png>)
