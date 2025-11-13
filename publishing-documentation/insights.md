---
description: View analytics and insights related to your published documentation’s traffic
icon: chart-line-up
---

# Site insights

{% include "../.gitbook/includes/premium-and-ultimate-hint.md" %}

Insights give you information on the content you've published and how it performs. It's split up between different sections — **Traffic**, **Pages & feedback**, **Search**, **Ask AI**, **Links**, and **OpenAPI**.

You can see a top-level overview of your insights on the **Overview** tab of your site’s dashboard, with a globe that shows views in the last hour by location.

Click the **Insights** tab in the site header to find more detailed insights for your site.

<figure><img src="../.gitbook/assets/18_07_25_publishing-documentation-advanced-site-insights.svg" alt="A GitBook screenshot showing the site insights dashboard"><figcaption><p>The site insights dashboard.</p></figcaption></figure>

### Filters & groups

You can add filters or group your data to view it in specific ways. For example, you could look at search data within a specific site section, or filter your traffic data by country, device, browser and more.

By combining filters and groups, you can drill down in to precise analytics data to track the events that you are important to you.

### View by custom time periods

You can use the drop-down menu on the right of the Insights screen to change the time period between the last 24 hours, 7 days, 30 days or 3 months.&#x20;

To view the data over a custom time period, click the **Select custom date range** button <picture><source srcset="../.gitbook/assets/calendar-dark.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/calendar.svg" alt=""></picture> to the right of the menu and choose your custom time period using the calendar that appears.

### Types of data

The Insights tab is split into six sections, each focused on a specific data type.

#### Traffic

GitBook tracks page views to help you understand the popularity and reach of your content. Each time a user visits a page on your docs site, it is counted as a page view.

Page views are critical for assessing the effectiveness of your content strategy and optimizing your documentation based on user interest. It’s split up between different views and profiles, including countries, languages, browsers, and more.

{% hint style="success" %}
Throughout the insights tab you will see Events and Visitor metrics. **Events** indicate the total number of instances for any given category, while **Visitors** indicates the unique users performing the actions.

In the context of page views, Events would be total amount of page views, and Visitors would be the count of distinct users performing a page view.
{% endhint %}

#### Pages & Feedback

Pages & feedback allow you to see a high-level representation of how your users rate your content. You’ll see an overview of all of your site’s sections and variants, and after enabling [page rating](site-settings.md#page-ratings-pro-and-enterprise-plans) in the **Customize** menu for a site, you can see each page’s average feedback rating.

If you want to use or analyze this data further outside of GitBook, click **Download CSV** to download a `.csv` file to your device.

You can also see a list of comments left from visitors who rate your pages, to get actionable insights on how your docs can be improved.

{% hint style="info" %}
**Why can’t I see any feedback data for my site?**\
We only display data for published sites with page ratings enabled. If your site is not published or does not have page ratings enabled, you won’t see any insights.
{% endhint %}

#### Broken URLs

Broken URLs shows any incoming links from external sources that are resulting in a ‘Page not found’ error. These may be mistyped URLs, outdated links with no redirects, or spam links.

If a broken link points to a topic that exists somewhere else in your documentation, or you simply want to direct the traffic to your primary docs, you can set up [site redirects](site-redirects.md) to point those visitors in the right direction.

#### Search

You can measure and improve your documentation by checking which keywords are used the most by users searching your documentation. This view allows you to see what keywords are performing the best, and which ones you could improve on.

The information here can be helpful for informing your content architecture, making certain parts of your documentation easier to find without search, or adding additional content to existing pages based on what your visitors are searching for.

#### Ask AI

The [Ask AI](../creating-content/searching-your-content/gitbook-ai.md) section allows you to see what your users are asking for when using GitBook AI. This insight helps you identify common questions, uncover gaps in your documentation, and improve content to better meet user needs.

You can also see how users are rating the answers that AI gives to their questions. By looking at these queries and their ratings, you can refine your documentation structure, enhance discoverability, and identify areas that would benefit from more documented information.

#### Links

GitBook tracks links to help you understand how users interact with external resources in your documentation. This feature provides insights into external links, their domains, and their placement within your docs, such as in the header, footer, or sidebar. Analyzing link usage can help you optimize navigation, improve content accessibility, and refine your documentation strategy based on user engagement.

#### OpenAPI

The [OpenAPI](../api-references/openapi/) analytics view in GitBook provides insights into how users engage with your API documentation.

It tracks interactions such as endpoint views, parameter searches, and request explorations, helping you understand which parts of your API are most accessed and where users may need more clarity. These insights enable you to refine your documentation, improve developer experience, and ensure your API content is effectively meeting user needs.
