---
description: Publish your docs publicly to the web so that everyone can access them
---

# Public publishing

If you created your docs for a public audience, you can publish it on the web. Spaces that you publish on the web can be indexed by search engines and will be available to anyone. If you don’t want your content to be indexed by search engines, you can disable that too — read more about that [below](public-publishing.md#publish-as-public).

However you publish your content, you’ll still retain control over who can _edit_ your content. And only your primary content branch will be published, so any [change requests](../../collaboration/change-requests/) will remain private until merged.

### Publish as public

To publish your docs publicly on the web head to the docs site you want to publish, click **Publish** button, and choose the **Public** option.

### **Publish without search engine indexing**

By default, your site will be indexed by search engines. You can alternatively choose to disable this — meaning the docs are still available to everyone on the web, but they _won’t_ be indexed by search engines such as Google.&#x20;

They will still be accessible to anyone with a the link to your documentation. Docs sites that aren’t indexed can be particularly helpful if you want to publish a beta version of your docs, or do large-scale user testing without impacting your SEO with potentially duplicate content.

### Page-level search indexing controls

You can also control search indexing at the individual page level. GitBook provides two types of search indexing controls:

#### Internal search indexing

Controls whether pages are indexed in GitBook's internal search engine and Ask AI feature. This affects:

* Content search within your GitBook space
* Ask AI's ability to reference the page content

**External search indexing (Web crawlers)**

Controls whether search engines and web crawlers (Google, ChatGPT, etc.) can index your pages. This affects:

* SEO and discoverability through search engines
* Web crawler access to your content

#### **Hierarchical inheritance behavior**

**Search indexing settings follow a hierarchical inheritance pattern:**

* **Parent page controls**: When you disable search indexing on a parent page, it automatically disables indexing for ALL sub-pages beneath it.
* **Children cannot override**: Sub-pages cannot re-enable search indexing if their parent page has it disabled.
* **Cascading effect**: This creates a cascading effect down the entire page hierarchy - disabling indexing on a top-level page will disable it for the entire section.

This hierarchical behavior ensures consistent indexing policies across related content sections and prevents accidental exposure of content that should remain private within a section.

{% hint style="info" %}
This feature is available on [Premium and Ultimate site plans](https://www.gitbook.com/pricing).
{% endhint %}
