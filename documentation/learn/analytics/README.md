---
description: Understand site traffic and what readers are asking.
---

# Analytics

{% hint style="info" %}
Site analytics is available on all plans; advanced analytics and AI insights are available on Premium and Ultimate plans.
{% endhint %}

Site analytics gives you information on your published content and how it performs, split across several data types: **Traffic**, **Pages & feedback**, **Search**, **Links**, and more, alongside AI-powered [insights](insights/README.md) into what readers are actually asking.

See a top-level overview on your site's **Overview** screen, under **General** in the site sidebar — a globe showing views in the last hour by location. Click **Analytics** in the site header to open the full picture.

{% hint style="info" %}
If you connect Google Analytics, your site can show a cookies notice. To remove it, open **Site settings → Analytics cookie** and disable or remove the [Google Analytics](google-analytics.md) integration.
{% endhint %}

### Filters & groups

Add filters or group your data to view it in specific ways — for example, search data within a specific site section, or traffic filtered by country, device, or browser. Combine filters and groups to drill into the precise events that matter to you.

### View by custom time periods

Use the time filter on the right of the **Analytics** screen to change the period — last 24 hours, 7 days, 30 days, or 3 months — or click **Custom range** to set your own.

### Types of data

Site analytics splits into sections, each focused on a specific data type:

#### Traffic

Page views help you understand the popularity and reach of your content — every visit to a page counts as a page view, split across countries, languages, browsers, and more.

{% hint style="success" %}
Throughout site analytics, you'll see **Events** and **Visitors** metrics. Events are the total instances of a category; Visitors are the unique users performing the action. For page views, Events is the total page-view count, and Visitors is the count of distinct people viewing.
{% endhint %}

#### Pages & feedback

A high-level view of how readers rate your content, across every section and variant. After enabling [page ratings](../customization/site-settings-reference.md#features) in a site's Customize menu, see each page's average feedback rating, and download the data as a CSV. You can also see comments left by visitors rating your pages.

{% hint style="info" %}
**Why can't I see any feedback data?** GitBook only shows data for published sites with page ratings enabled.
{% endhint %}

#### Broken URLs

Shows incoming links from external sources resulting in a "Page not found" error — mistyped URLs, outdated links with no redirect, or spam. If a broken link should point somewhere else in your docs, or you just want to direct that traffic to your primary docs, set up [site redirects](../publishing/create-redirects.md).

#### Search

Measure and improve your documentation by checking which keywords users search for most, and which underperform. Use this to inform your content architecture, make parts of your documentation easier to find without search, or add content based on what visitors are looking for.

#### Links

Tracks how users interact with external links in your documentation — their domains and placement (header, footer, sidebar). Use this to optimize navigation and refine your docs strategy based on engagement.

#### OpenAPI

See how users engage with your API documentation — endpoint views, parameter searches, request explorations — helping you understand which parts of your API get used most, and where users need more clarity. See [How GitBook renders OpenAPI](../api-documentation/how-gitbook-renders-openapi.md).

#### MCP

See how your site content is accessed through MCP integrations — requests over time, and which bots and agents access your content. See [MCP server for published docs](../gitbook-ai/readers-ai/mcp-server-for-published-docs.md).
