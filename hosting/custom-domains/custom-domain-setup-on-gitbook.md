---
description: Register your custom domain for your GitBook space or your whole organization.
---

# Custom domain setup on GitBook

## Organization domains

Organization domains are useful for large organizations with multiple projects they want to host on a single domain (with a subfolder per project).

> For example, if my organization domain is `docs.example.com`, all your public projects will be available under `docs.example.com/{project-id}`

To set up an organization domain, go to your organization's settings. The settings in the Domain section of the page relate to your organization's domain name.

{% hint style="info" %}
The Domain section will only appear when your organization has at least one published space.
{% endhint %}

![](<../../.gitbook/assets/General Settings.png>)

| Field             | Description                                                                                                                                                                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GitBook Subdomain | If you're not using a custom domain, this field lets you set the subdomain of gitbook.io that your content will be served from                                                                                                           |
| Custom domain     | The custom subdomain you want to serve your content from. Make sure to[ configure your DNS settings](dns-configuration.md) properly!                                                                                                     |
| Default Content   | Selects the content that will be displayed when a user goes to the domain name your space is configured to serve from. This can be a space or a collection. For more info, see [our publishing guide](../../spaces/space-visibility.md). |

## Space and Collection domains

Space domains are what you will want to use most of the time, especially if you only have personal spaces. Domain settings for published collections are the identical to those of spaces, so this information applies to both cases.

To set up a space domain, go to your space. Under the publish menu, when an option other than 'unpublished' is selected, you can open Link and Domain settings, where you can customize your space URL and add a custom domain.

![](<../../.gitbook/assets/Link Settings.png>)
