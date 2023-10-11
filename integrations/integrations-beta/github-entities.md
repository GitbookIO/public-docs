---
description: >-
  The GitHub Entities integration for GitBook allows you to add useful
  information like pull requests, issues and comments to your team’s knowledge
  base.
cover: ../../.gitbook/assets/GitHub (1).png
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

# GitHub Entities

{% hint style="warning" %}
This integration is currently in beta. See our [beta information](./) for more info and learn how to gain access.
{% endhint %}

The GitHub Entities integration for GitBook allows you to synchronize repositories with GitBook and add important workflow information to your team’s knowledge base.

The GitHub integration will analyze repositories for:

* issues
* pull requests
* releases
* comments
* general metadata.

After indexing a repository, GitBook AI will index this information in your knowledge base, and use it to answer questions from you and your team — adding context to existing data.

### Install & configure the GitHub Entities integration

The GitHub Entitles integration is currently in closed beta. Once accepted to the beta, you’ll be able to install the GitHub Entities integration from the home screen in the GitBook app.

To configure the GitHub Entities integration, you’ll need to both authenticate with GitHub, and add the GitBook Entities app to your GitBook repositories:

1. **Install the GitHub Entities integration in GitBook**

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-11 at 13.34.39.png" alt=""><figcaption><p>Install the GitHub Entities integration</p></figcaption></figure>

2. **Install the GitBook Entities app to GitHub**

To configure the GitHub Entities integration correctly, you'll need to [install the GitBook Entities](https://github.com/apps/gitbook-entities/) app into your GitHub Account.

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-11 at 13.34.45.png" alt=""><figcaption><p>Install the GitBook Entities ap to GitHub</p></figcaption></figure>

3. **Select the repositories you want to sync**

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-05 at 11.17.54.png" alt=""><figcaption><p>Select repositories to index</p></figcaption></figure>

4. **Authenticate your GitHub Account**

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-11 at 13.36.09.png" alt=""><figcaption><p>Authenticate your GitHub account</p></figcaption></figure>

5. **Select your account in the GitBook integration's configuration**

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-11 at 15.35.42.png" alt=""><figcaption><p>Select your GitHub account</p></figcaption></figure>

{% hint style="warning" %}
GitHub Entities will index any and all of the repositories you grant it access to. If you’d only like to index a select few repositories, make sure to configure them as you see in step 3 above.
{% endhint %}

{% hint style="warning" %}
You may need to refresh the GitBook page after authenticating in order to see and  select your repositories to index.
{% endhint %}

### FAQ

<details>

<summary>I’m getting an error when I index my repositories</summary>

This could be because your GitHub account is not properly authenticated in your GitBook space. Head to the configuration section for the GitHub Entities integration and try to authenticate your user account again.

</details>

