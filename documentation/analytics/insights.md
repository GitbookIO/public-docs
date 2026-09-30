---
description: View analytics related to your published documentation’s traffic and usage
---

# Site analytics

Site analytics gives you information on the content you’ve published and how it performs. It’s split into reports, each focused on one audience:

* [traffic.md](traffic.md "mention"): the people reading your site, the pages they land on, what they search for, and the feedback they leave.
* [agents-and-mcp.md](agents-and-mcp.md "mention"): the LLMs, coding agents, and crawlers reading your site through Markdown, `llms.txt`, and your site’s MCP server.
* [ai-insights.md](ai-insights.md "mention"): what your visitors ask GitBook Assistant, and how well your content answers them.

To open a report, go to **Analyze** in your site’s sidebar. You can also see a top-level overview of your analytics on your site’s **Overview** screen, with a globe that shows views in the last hour by location.

Incoming links that land on a “Page not found” are reported in [broken-links.md](broken-links.md "mention"), under **Improve** in the site sidebar, alongside the redirects GitBook suggests for them.

{% hint style="info" %}
If you connect **Google Analytics**, your site can show a cookies notice. To remove it, open [**Site settings → Analytics cookie**](../manage-your-site/site-settings.md#analytics-cookie) and disable or remove the **Google Analytics** integration.
{% endhint %}

## Filters

Every report has a filter bar at the top. Add a filter to narrow a report down to the data you care about: a single site section, variant, or page, or an audience defined by country, language, device, browser, referrer, campaign, or authenticated visitor status. Filters apply to every card in the report at once.

Sites using [adaptive content](../publish/adaptive-content/enabling-adaptive-content/) can also filter by visitor claims, such as a customer, plan, role, or feature access, so you can look at how one segment reads your docs.

## Time periods and comparisons

Use the time filter in any report to switch between the last 24 hours, 7 days, 30 days, or 3 months. Click **Custom range** to pick your own period in the calendar. Reports include today’s data as it arrives.

Each figure at the top of a report compares itself to the period before, so you can see what’s moving without setting anything up. To compare a whole report, open the comparison picker next to the time filter and choose **Previous period** or **Same period last year**. With a comparison on, the report changes in three ways:

* Figures show the change and the earlier value they moved from.
* Charts draw the earlier period underneath each series.
* Breakdown rows show a trend arrow, with the change and the earlier figure in its tooltip.

**Same period last year** shifts the window back 12 months and stops where the current window starts, so a range longer than a year never counts an event twice. The comparison is stored in the report’s URL along with your other filters, so you can share a compared view.

## Export data

To analyze data outside of GitBook, open the menu on a card and click **Download CSV**. To build your own reports from the underlying events, see the [Events Aggregation API guide](https://app.gitbook.com/s/LBGJKQic7BQYBXmVSjy0/docs-analytics/track-advanced-analytics-with-gitbooks-events-aggregation-api).

{% hint style="success" %}
Throughout site analytics, you see **Events** and **Visitors** metrics. **Events** indicate the total number of instances for any given category, while **Visitors** indicates the unique visitors performing the actions.

In the context of page views, Events would be the total amount of page views, and Visitors would be the count of distinct visitors performing a page view.
{% endhint %}

## Ads & sponsorship

Sites on the [sponsored site plan](../account-and-billing/plans/community/sponsored-site-plan.md) get an extra **Ads & sponsorship** report, showing impressions, clicks, click-through rate, and revenue, along with the advertisers and pages behind them.

## FAQ

<details>

<summary>Who can view site analytics?</summary>

Anyone with access to the site can view its analytics — including readers, reviewers, and editors. Creators and admins can also access the site’s settings and customization.

</details>

<details>

<summary>Where did Search, Pages &#x26; feedback, MCP, Ask AI, and Broken URLs go?</summary>

They’re still here, grouped with the audience they belong to. Search and page feedback are part of [traffic.md](traffic.md "mention"), MCP activity is part of [agents-and-mcp.md](agents-and-mcp.md "mention"), and Ask AI questions are part of [ai-insights.md](ai-insights.md "mention"). The Broken URLs report is part of [broken-links.md](broken-links.md "mention"), under **Improve**, next to the redirects GitBook suggests for those URLs.

</details>

<details>

<summary>Why is my analytics data not loading?</summary>

If the analytics dashboard isn’t loading, it’s usually because an ad blocker or privacy extension is blocking the analytics scripts. Temporarily disable the extension and reload the page, or add GitBook and the services it uses to the extension’s allowlist.

</details>

<details>

<summary>What does “Page not found” mean?</summary>

“Page not found” means visitors tried to open a page on your site that doesn’t exist. To see which URLs are broken, open [broken-links.md](broken-links.md "mention"). From there you can see how many visitors each broken link had and [create redirects](../publish/site-redirects.md) if needed.

</details>

<details>

<summary>What does “Not set” mean in referrer data?</summary>

“Not set” referrers indicate direct traffic — visitors typed your URL directly, used a bookmark, or clicked links from emails and apps that don’t pass referrer data.

</details>

<details>

<summary>What does “Authenticated visitor” mean?</summary>

The “Authenticated visitor” filter shows whether GitBook could identify a visitor when the event happened.

Visitors count as “Authenticated” when they signed in through visitor authentication or arrived with signed visitor claims, such as on sites using adaptive content. Personalization attributes passed through URL parameters or the public visitor cookie are unsigned, so those visitors count as “Anonymous”.

</details>

<details>

<summary>What does “Unknown” mean for authenticated visitors?</summary>

“Unknown” means GitBook recorded the event before tracking visitor authentication began in August 2026.

GitBook labels those older events “Unknown” rather than inferring their status. Reports covering earlier periods therefore show most traffic as “Unknown.” The “Authenticated” and “Anonymous” split is meaningful from August 2026 onward.

</details>
