---
icon: sitemap
---

# Organization settings

View and manage the settings for your GitBook organization. These include member management, sign-in methods, integrations, billing and plans.

<figure><img src="../.gitbook/assets/10_01_25_organization_settings.svg" alt=""><figcaption><p>Your organization settings page.</p></figcaption></figure>

### How to access the settings for an organization

Click on the **settings** icon, then click on **\[organization name] settings**. This will take you to the general tab of that organization’s settings page, and you’ll see additional tabs containing further settings on the left-hand side.

<details>

<summary>General</summary>

**Organization profile**

You can update the logo and the name of the organization.

**GitBook AI features**

[GitBook’s AI](../creating-content/searching-your-content/gitbook-ai.md)-powered search lets your team members ask questions about your content in natural language. You can also enable GitBook AI for published content in the space [customization ](../publishing-documentation/customization.md)panel.

**Publishing**

Each published GitBook space that lives within your organization’s library will have a domain in two parts:

1. `[something].gitbook.com` (this is the GitBook subdomain) **or** your own custom subdomain
2. `/[spaceURL]` (this is set within the settings for the space itself)

You can update the GitBook subdomain here, as well as the default content, which is the space that visitors will see if they navigate to your GitBook subdomain directly.&#x20;

&#x20;Note: GitBook subdomains are a legacy feature, and you may not have access to change your subdomain at the time of reading this doc. Please refer to [custom domain setup](../publishing-documentation/custom-domain.md) and [site sections](../publishing-documentation/site-structure/site-sections.md) to learn more about structuring your docs with custom URLs.

**Actions**

From this section you can delete the organization. **Note: there is no turning back if you delete an organization!** All associated data will be deleted as well. If you want to keep any spaces or collections owned by the organization, make sure to first [move](https://docs.gitbook.com/getting-started/organizing-content/what-is-a-space#moving-a-space) them to another library.

</details>

<details>

<summary>Members</summary>

**Members tab**

[Members](member-management/) can be added to and removed from the organization as needed. You can also update the [role](member-management/roles.md) for each member.

**Teams tab**

[Teams](member-management/teams.md) are a way to group members within an organization. You can then grant access to certain things to anyone who is a member of a given team.

</details>

<details>

<summary>SSO</summary>

**Email domains**

For any domains that you specify, anyone with an email address on those domains will immediately be able to access the organization upon signing up for a GitBook account. You can decide what [role](member-management/roles.md) these members should have by default.

**SAML**

For organizations on our Enterprise plan, you can configure your SSO with any SAML solution, to give your members access to GitBook through an identity provider (IdP) of your choice. [Contact sales](mailto:sales@gitbook.com) if you’re interested in upgrading to Enterprise!

</details>

<details>

<summary>Integrations</summary>

You can check which integrations are installed for your organization and [install new integrations](../integrations/install-an-integration.md) from this page.

</details>

<details>

<summary>Plans</summary>

From this page you can view your current plan and switch from one plan to another. The toggle at the top of the page enables you to switch between viewing the prices for our plans paid yearly (with 2 months free!) or monthly, and you can then use the upgrade/downgrade button under the name of each plan to select your new plan.

Please see our [billing policy](plans/billing-policy.md) for information about how charges are calculated when you make a change during the middle of a billing period.

</details>

<details>

<summary>Billing</summary>

The billing tab takes you to our payment provider, Stripe. On their website you can securely manage your payment method and billing information. You can also [cancel your plan](cancelling-a-plan.md). If a plan has been cancelled but you change your mind before the end of the billing period, you can renew the plan to have it continue without any lapse in service.

</details>
