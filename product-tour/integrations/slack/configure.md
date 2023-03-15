---
description: Configure the Slack integration
---

# Configure the Slack integration

## Install the integration

To start using the Slack integration, you will need to install it in your GitBook library or just on a single space. To do this, follow the steps described in the [install an integration](../install-an-integration.md) section.

Once it is installed, you will need to connect it to your Slack workspace, select the channels to which the integration will be posting the status updates, and tweak other configuration options to your need, **to complete the installation** by configuring it.&#x20;

## Configure the integration

After installing the integration to your space or GitBook library, you will first need to authorize the Slack integration to connect to your Slack workspace.

<details>

<summary>Step 1: Authorize the connection</summary>

In the **configuration** section of the integration's configuration screen, click the **authorize** button.

</details>

<figure><img src="../../../.gitbook/assets/Authorize Slack Integration.png" alt="Integration settings with Configuration highlighted. The integration between Slack and GitBook requires authorization and the button is visible to the right of the text. "><figcaption></figcaption></figure>

<details>

<summary>Step 2: Grant the GitBook Slack app access to your workspace</summary>

This will open up a pop-up window requesting permission for the GitBook Slack app to access your Slack workspace.

Next, make sure to select the correct Slack workspace from the dropdown menu located at the top right-hand side of the pop-up.&#x20;

Then, click the **allow** button to grant permission and complete the authorization flow.

This will bring you back to the integration's configuration screen if the authorization was successful.

</details>

<figure><img src="../../../.gitbook/assets/Configure the integration.png" alt="Slack authorisation flow open with &#x27;Gitbook is requesting permission to access your Slack workspace&#x27;. "><figcaption></figcaption></figure>

{% hint style="info" %}
After successful authorization, the [GitBook Slack app](https://gitbook.slack.com/apps/A7DE1QCTD-gitbook?tab=more\_info) will be automatically installed in your Slack workspace.
{% endhint %}

<details>

<summary>Step 3: Choose a default Slack channel </summary>

Next, you have the option to select the default Slack channel to which the integrations will be posting messages to when no channel is selected individually for each space.

Click the **default channel** dropdown in the **configuration** section and select the default channel from the dropdown options.

</details>

<figure><img src="../../../.gitbook/assets/Select default channel.png" alt="Configuration settings of the integration settings open, with default channel settings and an arrow which expands to a search settings. One space called &#x27;general&#x27; is selected "><figcaption></figcaption></figure>

<details>

<summary>Step 4: Select configuration options for specific spaces (optional)</summary>

Next, you can select different configuration options to apply individually to each of the spaces. You can do this in the **space configuration** section.

You can for example select a specific Slack channel to which the integration will be posting the selected space updates.

Additionally, you can choose what type of space updates will trigger the delivery of messages to the selected Slack channel.

</details>

To switch to another space and configure its individual configuration options, click the **space dropdown** at the top right-hand corner and select the specific space:

<figure><img src="../../../.gitbook/assets/Install on selected spaces.png" alt="Space configuration window open, with a drop down list of spaces. The integration is already installed in &#x27;Jet-Stream Docs&#x27; but user can select other spaces to access it&#x27;s own configurations. "><figcaption></figcaption></figure>
