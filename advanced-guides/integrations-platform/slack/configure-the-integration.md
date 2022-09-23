---
description: Configure the Slack Integration
---

# Configure the integration

After installing the integration to your Space or GitBook library, you will first need to authorize the Slack integration to connect to your Slack workspace.

In the **Configuration** section of the integration's configuration screen, click the **Authorize** button:

![Authorize the GitBook Slack integration](<../../../.gitbook/assets/Slack Integration Authorize.png>)

This will open up a pop-up window requesting permission for the GitBook Slack app to access your Slack workspace.

Next, make sure to select the correct Slack workspace from the dropdown menu located at the top right hand side of the pop-up.&#x20;

Then, click the **Allow** button to grant the permission and complete the Authorization flow:

![Slack Auhorization pop-up](<../../../.gitbook/assets/Slack Auhorization Pop Up (1).png>)

This will bring you back to the integration's configuration screen if the authorization was successful.

{% hint style="info" %}
After successful authorization, the [GitBook Slack App](https://gitbook.slack.com/apps/A7DE1QCTD-gitbook?tab=more\_info) will be automatically installed in your Slack workspace.
{% endhint %}

Next, you have the option to select the default Slack channel to which the integrations will be posting messages to, when no channel is selected individually for each Spaces.

Click the **Default Channel** dropdown in the **Configuration** section and select the default channel from the dropdown options:

![Select the default Slack channel](<../../../.gitbook/assets/Slack Default Channel.png>)

Next, you can select different configuration options to apply individually to each of the Spaces.

You can do this in the **Space configuration** section:

![Space configuration options for the Slack integration](<../../../.gitbook/assets/Slack Space Configuration Options.png>)

You can for example select a specific Slack channel to which the integration will be posting the selected Space updates.

Additionally can you choose what type of Space updates will trigger the delivery of message to the selected Slack channel.

To switch to another Space and configure its individual configuration options, click the **Space dropdown** at the top right hand corner and select the specific Space:

![Switch to another Space to configure its options](<../../../.gitbook/assets/Slack Space Configuration Switcher.png>)

### Note on Link Preview

For the integration to generate nice-looking previews for links to GitBook Spaces you share in your Slack workspace, the Spaces corresponding to the links that are shared need to be connected to the integration's installation.

You can check if the integration was installed on a specific Space under the **Space configuration** section mentioned above. Use the Space dropdown at the top right hand corner to switch to the specific Space.

If it's not installed you should see an **Add to Space** button like this:

![Connect a Space to the Slack integration](<../../../.gitbook/assets/Add Integration to Space.png>)

Alternatively, you can choose to enable the integration **on all Spaces** of your GitBook library. To do this, toggle **Install on all spaces** in the **Space access** section:

![Install the Slack integration on all Spaces](<../../../.gitbook/assets/Install on all Spaces.png>)
