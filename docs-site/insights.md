---
description: View analytics related to your published documentation’s traffic and usage
icon: chart-line-up
---

# Site analytics

{% include "../.gitbook/includes/premium-and-ultimate-hint.md" %}

Site analytics gives you information on the content you’ve published and how it performs. It’s split into different sections — **Traffic**, **Pages & feedback**, **Agent and LLMs**, **Search**, **Ask AI**, **Links**, **MCP**, and **OpenAPI**.

You can see a top-level overview of your analytics on the **Overview** tab of your site’s dashboard, with a globe that shows views in the last hour by location.

Click **Analytics** in the site header to open site analytics for your site.

{% hint style="info" %}
If you connect **Google Analytics**, your site can show a cookies notice. To remove it, open [**Site settings → Analytics cookie**](site-settings.md#analytics-cookie) and disable or remove the **Google Analytics** integration.
{% endhint %}

<figure><img src="../.gitbook/assets/26_03_30_analytics@2x (1).png" alt="A GitBook screenshot showing the site analytics dashboard"><figcaption><p>The site analytics dashboard.</p></figcaption></figure>

### Filters & groups

You can add filters or group your data to view it in specific ways. For example, you could look at search data within a specific site section, or filter your traffic data by country, device, browser and more.

By combining filters and groups, you can drill down in to precise analytics data to track the events that you are important to you.

### View by custom time periods

You can use the time filter <picture><source srcset="../.gitbook/assets/25_09_15_calendar.svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/25_09_15_calendar_1.svg" alt=""></picture> on the right of the **Analytics** screen to change the time period between the last 24 hours, 7 days, 30 days or 3 months.

To view the data over a custom time period, click **Custom range** to choose your custom time period in the calendar.

### Types of data

Site Analytics is split into seven sections, each focused on a specific data type.

#### Traffic

GitBook tracks page views to help you understand the popularity and reach of your content. Each time a user visits a page on your docs site, it is counted as a page view.

Page views are critical for assessing the effectiveness of your content strategy and optimizing your documentation based on user interest. It’s split up between different views and profiles, including countries, languages, browsers, and more.

{% hint style="success" %}
Throughout Site Analytics, you will see Events and Visitor metrics. **Events** indicate the total number of instances for any given category, while **Visitors** indicates the unique users performing the actions.

In the context of page views, Events would be total amount of page views, and Visitors would be the count of distinct users performing a page view.
{% endhint %}

#### Pages & Feedback

Pages & feedback allow you to see a high-level representation of how your users rate your content. You’ll see an overview of all of your site’s sections and variants, and after enabling [page rating](site-settings.md#page-ratings-pro-and-enterprise-plans) in the **Customize** menu for a site, you can see each page’s average feedback rating.

If you want to use or analyze this data further outside of GitBook, click **Download CSV** to download a `.csv` file to your device.

You can also see a list of comments left from visitors who rate your pages, to get actionable insights on how your docs can be improved.

{% hint style="info" %}
**Why can’t I see any feedback data for my site?**\
We only display data for published sites with page ratings enabled. If your site is not published or does not have page ratings enabled, you won’t see any analytics data.
{% endhint %}

#### Agent & LLMs

Track traffic from LLMs, coding agents, and bots.

This view shows requests to `llms.txt`, `llms-full.txt`, and Markdown pages. You can also review which agents access your content most often.

#### Broken URLs

Broken URLs shows any incoming links from external sources that are resulting in a ‘Page not found’ error. These may be mistyped URLs, outdated links with no redirects, or spam links.

If a broken link points to a topic that exists somewhere else in your documentation, or you simply want to direct the traffic to your primary docs, you can set up [site redirects](../publishing-documentation/site-redirects.md) to point those visitors in the right direction.

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

#### MCP

See how your site content is being accessed through [MCP](../publishing-documentation/mcp-servers-for-published-docs.md) integrations. You can view MCP requests over time and see which bots and agents are accessing your site content.
