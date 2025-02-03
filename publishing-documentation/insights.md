---
icon: chart-line-up
description: View analytics and insights related to your published documentation’s traffic
---

# Site insights

{% hint style="info" %}
This feature is available on [Premium and Ultimate site plans](https://www.gitbook.com/pricing).
{% endhint %}

Insights give you information on the content you've published and how it performs. It's split up between different sections — **traffic**, **pages & feedback**, **search**, **ask AI**, **links**, and **OpenAPI**.

You can find insights for individual docs sites in the docs site dashboard, and can sort it by the last day, week and month. You can download insights by hovering over the header for the data you want, and clicking **Download CSV**.

<figure><img src="../.gitbook/assets/03_02_25_advanced_site_insights.svg" alt=""><figcaption><p>The site insights dashboard.</p></figcaption></figure>

### Traffic

GitBook tracks page views to help you understand the popularity and reach of your content. Each time a user visits a page on your docs site, it is counted as a page view.&#x20;

Page views are critical for assessing the effectiveness of your content strategy and optimizing your documentation based on user interest. It’s split up between different views and profiles, including countries, languages, browsers, and more.

### Pages & Feedback

Pages & feedback allow you to see a high-level representation of how your users rate your content. You’ll see an overview of all of your site’s sections and variants, and after enabling [page rating](site-settings.md#page-ratings-pro-and-enterprise-plans) in the **Customize** menu for a site, you can see each page’s average feedback rating.

If you want to use or analyze this data further outside of GitBook, click **Download CSV** to download a `.csv` file to your device.

You can also see a list of comments left from visitors who rate your pages, to get actionable insights on how your docs can be improved.

#### How does GitBook calculate user scores?

GitBook uses a simple formula to calculate the page’s overall score:

`no. of ratings * (no. of positives - [0.5 * no. of neutrals] - [2 * no. of negatives])`

The goal of the content score is to surface the pages with the most feedback, with a bias towards negative ratings so you can see pages that need improvements. The more ratings a page has, the more the formula amplifies the sentiments of those ratings. This helps you spot pages that need attention, as well as pages that are highly-rated — to help you identify, iterate on and replicate your best content.

We cap the score at 500 (and -500) to avoid scores for commonly-rated pages reaching 10,000+.

### Search

You can measure and improve your documentation by checking which keywords are used the most by users searching your documentation. This view allows you to see what keywords are performing the best, and which ones you could improve on.&#x20;

The information here can be helpful for informing your content architecture, making certain parts of your documentation easier to find without search, or adding additional content to existing pages based on what your visitors are searching for.

### Ask AI

The [Ask AI](../creating-content/searching-your-content/gitbook-ai.md) section allows you to see what your users are asking for when using GitBook AI. This insight helps you identify common questions, uncover gaps in your documentation, and improve content to better meet user needs.&#x20;

By looking at these queries, you can refine your documentation structure, enhance discoverability, and provide more relevant information to your audience.

### Links

GitBook tracks links to help you understand how users interact with external resources in your documentation. This feature provides insights into external links, their domains, and their placement within your docs, such as in the header, footer, or sidebar. Analyzing link usage can help you optimize navigation, improve content accessibility, and refine your documentation strategy based on user engagement.

### OpenAPI

The [OpenAPI](../creating-content/openapi/) analytics view in GitBook provides insights into how users engage with your API documentation.&#x20;

It tracks interactions such as endpoint views, parameter searches, and request explorations, helping you understand which parts of your API are most accessed and where users may need more clarity. These insights enable you to refine your documentation, improve developer experience, and ensure your API content is effectively meeting user needs.

{% hint style="info" %}
**Why can’t I see any data for my site?**\
We only display data for published sites with page ratings enabled. If your site is not published or does not have page ratings enabled, you won’t see any insights.
{% endhint %}
