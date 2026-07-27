---
description: "How GitBook pricing is structured: plans, seats, and sites."
icon: money-check-dollar-pen
---

# How pricing works

GitBook pricing has two independent parts: a **site plan** (what a published docs site can do) and **seats** (how many people can collaborate). You pay for a site plan per site, and for additional users on any paid plan.

<a href="https://www.gitbook.com/pricing" class="button secondary">Visit pricing page</a>

### Site plans

| Plan | Best for | Key features | Price |
|---|---|---|---|
| **Basic** | Simple docs sites with basic customization needs | Unlimited traffic, basic customization, site insights, public publishing, preview deployments | $0/site/month, one user |
| **Premium** | Fully branded documentation | Customizable logo/theme/fonts, custom domain, advanced site insights, site redirects, page ratings, AI Search | $65/site/month + $12/user/month |
| **Ultimate** | Centralizing all your documentation | Site sections & groups, cross-site search, Authenticated Access (Azure, Auth0, Okta, and more), custom fonts, adaptive content, GitBook Assistant, AI insights, Slack/GitHub/Linear channels | $249/site/month + $12/user/month |
| **Enterprise** | Large-scale organizations | SAML SSO, migration assistance, advanced targeting, dedicated account manager, invoice & wire transfer, security reviews, custom contract | Custom pricing |

AI Search is available on Premium and Ultimate site plans. GitBook Assistant, AI insights, and channels remain Ultimate-only.

### Add-ons

| Add-on | What it does | Price |
|---|---|---|
| **Translations** | Auto-translates content into any language, only re-translating pages with changes, with custom AI instructions for tone & style, glossary support, and publishing as a language-toggle variant | $25/month |

### The Community plan

The Community plan is a free, collaborative plan for organizations that meet certain criteria. It's aimed at:

1. Non-profit organizations
2. Open source organizations
3. Education-related groups

{% hint style="info" %}
If you don't need to collaborate with others, or can collaborate via [Git Sync](../learn/git-sync/README.md) instead, our **Free** plan already covers you — it includes unlimited private content at no cost. If you also want to publish a docs site for free, choose a Basic site with limited features, or apply for a [sponsored site](#the-sponsored-site-plan), which has more features and earns you funding through small, relevant ads.
{% endhint %}

#### Eligibility criteria

Your organization should **not**:

* be a church, affiliated with one, or promote any specific religion
* be a school, college, university, etc. (student/lab/course groups are fine)
* be a government office, ministry, or function (small municipal offices are fine)
* be a private foundation
* have political affiliations, or promote a dogma or religious position
* promote discrimination on the basis of gender identity/expression, race, ethnicity, political or religious opinion, sexual orientation, or anything else
* be a cryptocurrency or gaming-related project

{% tabs %}
{% tab title="Non-profit organizations" %}
Your organization needs to be a company with official non-profit status and share a valid charitable status (501(c) or your country's equivalent).
{% endtab %}

{% tab title="Open source projects" %}
Your Git repository must:

* exist publicly on GitHub or GitLab
* be a truly open source project not associated with a for-profit or venture-backed company
* not be empty, or a fork with no activity of its own
* have a `README.md`, `CONTRIBUTING.md`, `LICENSE` (a [valid OSS license](https://choosealicense.com/)), and `CODE_OF_CONDUCT.md`
* make it easy for others to [contribute](https://docs.github.com/en/get-started/exploring-projects-on-github/finding-ways-to-contribute-to-open-source-on-github#finding-good-first-issues)
{% endtab %}

{% tab title="Education-related groups" %}
* The organization must not represent a whole school, college, or university.
* It may represent a small group related to one — a student group, lab group, or course group.

{% hint style="info" %}
Individual students who just want to keep personal and course notes should use the **Free** plan instead — it's unlimited and free, with no application needed.
{% endhint %}
{% endtab %}
{% endtabs %}

We can't share detailed reasons for a rejected application, so check the criteria above before applying — you're welcome to reapply once you can meet them.

#### How to apply

{% stepper %}
{% step %}
#### Sign up or sign in

[Sign up](https://app.gitbook.com/join) for a GitBook account, or [sign in](https://app.gitbook.com) if you already have one.
{% endstep %}

{% step %}
#### Choose an organization

Decide which organization the Community plan should apply to — an existing one, or a new one you create from the organization switcher in the sidebar.
{% endstep %}

{% step %}
#### Get the organization's URL

Click the organization's name in the sidebar and copy the URL — it looks like `app.gitbook.com/o/[string]/home`.
{% endstep %}

{% step %}
#### Contact us

Use the messenger on [our website](https://www.gitbook.com/contact) — select **Contact Support** → **I have a question about pricing** → **I want to apply to the Community plan** — or email `support@gitbook.com` with the details below for your organization type.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="Non-profit organizations" %}
* A brief description of your non-profit's purpose
* A link to your organization's public website
* Your non-profit's valid 501(c) (or equivalent) documentation
* Your organization's URL (from the steps above)
{% endtab %}

{% tab title="Open source projects" %}
* A brief description of your project's purpose
* A link to your public Git repository on GitHub or GitLab
* Your organization's URL (from the steps above)
{% endtab %}

{% tab title="Small education-related groups" %}
* Every group member, invited to the organization using their school email address (do this before applying)
* A brief description of the group and its purpose
* A link to a public website associated with the group, if you have one
* Your organization's URL (from the steps above)
{% endtab %}
{% endtabs %}

### The sponsored site plan

{% hint style="info" %}
The sponsored site plan is only available to organizations on the Community plan, and is designed specifically for open source projects — cryptocurrency, web3, and related projects aren't accepted.
{% endhint %}

The sponsored site plan gives you all of GitBook's best docs site features at no cost, in exchange for a small, relevant ad shown in the corner of your published site. Every view earns you money.

{% stepper %}
{% step %}
#### Create and publish a site

Any site created on the Community plan is eligible by default.
{% endstep %}

{% step %}
#### Submit for ad review

Your site must be [published publicly](../learn/publishing/publish-and-unpublish.md) for **seven days** first. Then, in your site's settings, open **Ads and sponsorship** and review the ads checklist before submitting.
{% endstep %}

{% step %}
#### Wait for review

Review takes up to seven days, though delays can push this out further. You'll be marked **approved** (ads go live, you start earning) or **rejected** (you can update your site and resubmit).
{% endstep %}
{% endstepper %}

Once live: a small, relevant, non-tracking ad appears in one corner of each page, and you earn money from every view. Your content stays the visual focus — only one ad per page.

<details>

<summary>Why was my site rejected?</summary>

Common reasons include: the project isn't open source or not-for-profit; it's a cryptocurrency project; the site's primary language isn't English; the content isn't high-quality; or the site doesn't reach a minimum monthly page-view threshold.

</details>

<details>

<summary>How much do I earn per view?</summary>

The CPM (cost per 1,000 views) fluctuates, so there's no fixed dollar amount per view. Once approved, your ads dashboard shows how your site performs over time.

</details>

<details>

<summary>What if I don't submit my site for review?</summary>

The sponsored site plan lets you use Ultimate-tier features to prepare your site before review. If you don't submit within one month, the site reverts to a free plan and loses those features (custom domains, customizations, and more).

</details>

<details>

<summary>What if I switch back to a free site plan?</summary>

You'll lose access to features that aren't available on the free plan — this is effectively a downgrade.

</details>

### About legacy pricing

If you signed up before GitBook's current pricing model, you may still be on legacy pricing. Some newer features are only available on current plans — [contact support](../resources/get-support.md) if you'd like to learn more or upgrade.
