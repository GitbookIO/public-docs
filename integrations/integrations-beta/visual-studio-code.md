---
description: >-
  The GitBook integration for Visual Studio Code allows you to capture and
  recall information from your team’s knowledge base.
cover: ../../.gitbook/assets/VS Code (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Visual Studio Code (alpha)

{% hint style="warning" %}
This integration is currently in alpha. See our [information page](./) for more info and learn how to gain access.
{% endhint %}

The GitBook Visual Studio Code integration allows you to collect, review, and share information to and from your company’s knowledge base. With a dedicated side panel and a list of different commands, you can easily utilize your entire team’s knowledge directly in the tool you use every day.

GitBook AI will summarize information that you or your team add to your knowledge base, turning a series of captures into a context-rich document. And when you or a colleague need to learn more about something you’ve saved, you can ask GitBook AI and get a plain-text summary, with all the background needed to dive in deeper.

### Installation & configuration

The Visual Studio Code integration is currently in closed beta. Once accepted to the beta, you’ll be able to install the Visual Studio Code integration from the home screen in the GitBook app.

After installing the integration to Visual Studio Code, you’ll need to log into your GitBook account in order to complete the configuration.

{% hint style="warning" %}
The GitBook Extension for Visual Studio Code is only available for MacOS at this time.
{% endhint %}

#### 1. Sign into GitBook with your developer token

In order for Visual Studio Code to access GitBook, you’ll need to grant your IDE access by adding a developer token. You can generate a new GitBook developer token in your [developer settings](https://app.gitbook.com/account/developer).

After you have your token, you can add it to Visual Studio Code via the Command Palette (⌘+⇧+P), under **GitBook: Sign into GitBook.**

#### 2. Select your GitBook organization

After saving your personal access token, you’ll need to choose the organization that you’d like to add your [captures](visual-studio-code.md#what-is-a-capture) to.

In the Command Palette, you can choose an organization under the **GitBook: Switch Organization** option. If you’re only part of one organization, it’ll already be selected for you.

### Add information to GitBook from VS Code

#### What is a capture?

You can add knowledge to GitBook via Visual Studio Code captures. A capture is an analyzed set of data, containing a combination of files and voice recordings that you save during a capture session. GitBook AI will combine these into a written guide and add it to your knowledge base.

### How to summon GitBook knowledge from VS Code

Using the GitBook VS Code extension, you can ask contextual questions in the side panel to access your team’s knowledge. This section also contains a list of recent captures by people on your team, so you can quickly see what others are saving to your team’s knowledge base from VS Code.

To summon information, simply open the GitBook panel, and type your query into the search bar. You’ll get a summarized result based on information in your GitBook organization.
