---
description: Integrate your GitBook public documentation with your Segment pipeline.
---

# Segment

## Get started

Before proceeding, make sure you have created a **Segment Source**. You can create one from the Segment dashboard as described [in their documentation](https://segment.com/docs/connections/sources/catalog/libraries/website/javascript/quickstart/#step-1-create-a-source-in-the-segment-app). Alternatively, you can re-use an existing one if you wish to.

{% hint style="info" %}
Take note of the Segment Source's **write key** as it will be needed during the configuration of the integration.

You can locate your Source's **write key** as described [in Segment's documentation](https://segment.com/docs/connections/find-writekey/).
{% endhint %}

Once installed and configured on a Space, anytime a visitor access a page in your GitBook Published content, the GitBook Segment integration will send `[GitBook] space_view` events (read more about the event [in this section](gitbook-segment-event.md)) to the Segment Source you've chosen.

Next, you will need to install the Segment integration in GitBook and configure it to your need. For this, follow the steps described in these sections:

* **Step 1:** [Install the integration](install-the-integration.md)
* **Step 2:** [Configure the integration](configure-the-integration.md)

## Feature overview

![](<../../.gitbook/assets/Segment GitBook Event.png>)

The GitBook Segment integration empowers your teams by connecting your GitBook public documentation to your Segment pipeline.

### Automatic page view events on your public documentation

Each of your connected GitBook spaces will send a `[GitBook] space_view` event to the associated Segment source.

### Track your users' actions across all your company's websites

Each `[GitBook] space_view` includes the `anonymousId` property. If the active user has already visited one of your other company's websites, the `anonymousId` will match the one already set by Segment. Otherwise, GitBook will associate a new `anonymousId` for the user matching Segment's format.
