---
description: >-
  Find the broken links on your published site and in your content, and fix them
  with suggested redirects or updated links
tags:
  - beta
  - tag: new
    primary: true
---

# Broken links

{% hint style="info" %}
Broken links is in beta and available on the Ultimate site plan.
{% endhint %}

Broken links finds the URLs on your published site that visitors are reaching but that no longer exist. For each broken URL, GitBook works out which page the visitor was most likely looking for and suggests a redirect you can enable in one click, so visitors stop landing on 404 pages.

It also finds links in your content that point to external websites and no longer work, so you can fix them before visitors click them. Broken URLs on your own site are called inbound broken links, and failing links to other websites are called outbound broken links. See [Outbound broken links](broken-links.md#outbound-broken-links).

GitBook can also apply these fixes for you after each audit. See [Fixing broken links automatically](broken-links.md#fixing-broken-links-automatically).

In your site’s sidebar, go to **Improve → Broken links**.

## How it works

GitBook regularly audits every published site on a plan that includes Broken links. Each audit runs these steps:

1. Looks at the last 30 days of traffic to your site and collects the URLs that returned a 404. A URL needs to have been hit at least three times to be considered, and noise from bots and scanners, such as requests for `/wp-admin` or `.php` files, is ignored.
2. Merges similar URLs, drops any that a live redirect already covers or that resolve again because a page now exists at that path, and ranks the rest by visits. The 60 most-visited broken URLs go forward.
3. Reads your published content to find the page each visitor was most likely looking for. If a whole section has moved, GitBook groups the broken URLs under a single wildcard suggestion such as `/v1/*`. If no page fits, GitBook says so, and checks that URL again after 30 days.
4. Creates a suggested redirect for each broken URL that has a clear match, with a short explanation of why that page was chosen and a severity based on how much traffic the URL receives.

A site is audited at most once a day. Each audit starts again from your current traffic, and resolved URLs drop out, so a site with more than 60 broken URLs works through them over successive audits, most-visited first. Broken URLs that GitBook couldn’t match to any page are kept as findings too, with the reason and the pages it considered, so you can decide whether they need a new page instead of a redirect.

This section describes inbound broken links. Outbound broken links are checked separately, as described in [Outbound broken links](broken-links.md#outbound-broken-links).

Broken links builds on [site-redirects.md](../publish/site-redirects.md "mention"). Read it first if you’re not familiar with redirects.

## The two views

Broken links has two views, which you can switch between from the tabs in the header:

* **Findings** lists the broken URLs GitBook found and the redirects it suggests, ready for you to review. It also lists broken outbound links.
* **Analyze** shows the full broken URL report from your site’s analytics, including URLs that don’t have a suggestion yet.

## Reviewing findings

The **Findings** view starts with a summary of the last 30 days:

| Card                    | What it shows                                      |
| ----------------------- | -------------------------------------------------- |
| **Broken visits**       | The number of 404 responses your site returned.    |
| **Visitors affected**   | The number of unique visitors who hit a 404.       |
| **Open broken URLs**    | The number of open suggestions waiting for review. |

The list shows each finding with its status, its severity, and a title describing the broken URL and, when GitBook found one, the page it should lead to. Findings with a suggested fix are listed first.

### Severity

Severity reflects how much traffic a broken URL receives, relative to the other broken URLs on your site.

Severity has three levels:

* **High**: at least 20 visits in the last 30 days, and one of the five most-visited broken URLs on your site.
* **Medium**: a URL with steady traffic.
* **Low**: a URL hit only a handful of times in the last 30 days.

### Searching, filtering, and sorting

Type a URL, or part of one, in the search box to find a specific finding. Use the filter bar to narrow findings by **Status** or **Severity**. By default the list shows only **Open** findings, sorted by severity. Switch the sort to **Recently updated** to see the latest changes first. Opening a finding and going back keeps your search, filters, and sort.

## Fixing a broken URL

1. Select a finding in the list to open its details.
2. Read the **Motivation** section. It explains which page GitBook matched to the broken URL and why. The **Related pages** list links to the pages involved.
3. Click **Create redirect**.
4. The **Add redirect** dialog opens with the **Source path** and **destination** already filled in from the suggestion. Adjust anything you want, for example choose **Permanent redirect** if the old URL will never return.
5. Click **Enable redirect** to activate it immediately, or **Save as draft** to publish it later from your site’s redirect settings.

When you enable a redirect whose source matches an open finding, the finding is automatically marked as **Resolved**. Saving the redirect as a draft leaves the finding open until the redirect goes live.

The redirect is added to your site’s redirects. You can edit or delete it at any time from **Settings → Redirects**, or by clicking **Settings** at the top of the screen, then **Manage redirects**.

{% hint style="info" %}
Creating redirects needs admin permissions on the site, and changing a finding’s status needs edit permissions. Actions you can’t use appear disabled, with an explanation.
{% endhint %}

### Wildcard suggestions

When several broken URLs share a prefix and all belong to the same moved section, GitBook suggests a single wildcard redirect such as `/v1/*` instead of one redirect per URL. The prefilled redirect dialog has **Replace wildcard with matched text** enabled, so `/v1/installation` is sent to the matching path under the new destination. See [site-redirects.md](../publish/site-redirects.md "mention") for how wildcard redirects behave.

## Ignoring a finding

If a suggestion is not right, or the broken URL does not need a redirect, open the finding and click **Ignore**. It moves to **Ignored** and disappears from the default list. You can find it again by filtering on **Status**, and bring it back with **Restore**.

Each finding has one of these statuses, shown in the list and on the details page:

| Status                | Meaning                                                                              |
| --------------------- | ------------------------------------------------------------------------------------ |
| **Open**              | The finding is waiting for review.                                                   |
| **Awaiting approval** | GitBook drafted a fix that isn’t live yet. See [Fixing broken links automatically](broken-links.md#fixing-broken-links-automatically). |
| **Resolved**          | A redirect fixes the URL, the URL resolves again, or you resolved it without a redirect. |
| **Ignored**           | You chose to ignore the finding.                                                     |

Findings are also resolved automatically when the next audit finds that the broken URL now resolves, either because a page exists at that path again, including a translated page, or because a live redirect covers it.

## Outbound broken links

Outbound broken links are links in your content that point to external websites and are failing. Inbound broken links are URLs on your own site that visitors reach and that return a 404.

GitBook reports an outbound link only after it fails in consecutive checks, so the Findings view shows confirmed failing external links rather than one-off errors.

### Finding outbound broken links

Outbound findings appear in the same **Findings** view as inbound ones:

* Each row has an **Inbound** or **Outbound** badge.
* The **Broken outbound links** card shows how many outbound findings you have.
* Outbound rows show the target URL and a reason for the failure, such as **404 Not Found** or **Redirect error**.

To narrow the list, use the filter bar. To find a specific link, type its URL, or part of it, in the **Search for a URL...** box.

### Reviewing an outbound broken link

1. In the **Findings** view, filter **Type** by **Broken Outbound Link**.
2. Select a finding to open its details.
3. Read the **Motivation** section. It explains why GitBook reports the link, for example that it returned HTTP 404 in consecutive checks.
4. Check the **Pages** section. It lists the pages in your content that contain the link.
5. Click **Create change request(s)**. GitBook Agent creates change requests that fix the link, by updating it or removing it on the affected pages.
6. Review and merge the change requests. Once the updated link passes GitBook’s next check, the finding is resolved.

If the link doesn’t need fixing, click **Ignore** instead. The finding moves to **Ignored** and disappears from the default list.

Unlike inbound broken links, you don’t fix an outbound broken link with a redirect, because the broken URL is on another website. Fix it by editing your content instead.

## Fixing broken links automatically

GitBook can fix the broken links it finds after each audit, so you don’t have to review every finding yourself. Automatic fixes are off by default, and a site admin turns them on for each site.

### Turning on automatic fixes

1. In **Broken links**, click **Settings** at the top of the screen.
2. Turn on **Fix broken links automatically**.
3. Choose an autonomy level. **Fix clear matches** is selected by default.

The autonomy level sets how many redirects GitBook applies on its own:

| Autonomy level        | What GitBook does                                                                                           |
| --------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Suggest fixes**     | Drafts redirects for you to approve, and applies none on its own.                                           |
| **Fix clear matches** | Applies redirects from a single path to a page in the same space, and drafts the rest for you to approve.   |
| **Fix close matches** | Also applies redirects that cover a whole section or a link with heavy traffic.                             |

At every level, GitBook never redirects a link it isn’t sure about, and never merges a change request.

{% hint style="info" %}
Only site admins can change these settings. Other members see the settings with the controls disabled.
{% endhint %}

### What GitBook does after each audit

For inbound broken links, GitBook either applies a redirect or drafts one, depending on the autonomy level:

* An applied redirect is live immediately, and the finding moves to **Resolved**. The finding’s details say that GitBook Agent fixed the link.
* A drafted redirect isn’t live until an admin approves it. The finding moves to **Awaiting approval**.

GitBook skips any path that already has a redirect, so it never overwrites a redirect or a draft you created.

For outbound broken links, GitBook Agent drafts change requests that update or remove the failing links, grouping the links in the same space into one change request. These findings also move to **Awaiting approval**, and nothing changes in your content until someone merges the change request. The autonomy level doesn’t affect outbound broken links.

### Reviewing automatic fixes

To find the fixes that need a decision, filter the **Findings** view by the **Awaiting approval** status, then open a finding:

* For a drafted redirect, approve it to make the redirect live, or reject it.
* For a drafted change request, click **Review and approve** to open the change request, then review and merge it. Click **Reject** if the link doesn’t need that fix.

Once GitBook has applied at least one redirect, a **Fixed for you** card in the summary shows how many broken URLs it redirected in the last 30 days.

### Undoing an automatic fix

To undo a redirect GitBook applied, open the resolved finding and click **Reopen and delete redirect**. The redirect is deleted, the finding returns to **Open**, and GitBook doesn’t apply that fix again in later audits. A fix you reject isn’t suggested again either.

Approving, rejecting, and undoing automatic fixes need admin permissions on the site.

## Analyzing broken URLs

The **Analyze** view shows every URL that returned a 404 in the selected period, whether or not GitBook has a suggestion for it. These can be mistyped URLs, outdated links with no redirect, or spam links. Use it to find broken URLs that need a new page rather than a redirect, or to see where broken traffic comes from.

The report includes these cards:

* **Broken URL hits**, **Affected visitors**, and **Distinct URLs** for the selected period, with a trend over time.
* **Top broken URLs**, ranked by hits.
* **Broken URLs by dimension**, which lets you group broken traffic by **Referrer domain**, **Broken URL**, **Full referrer**, **Country**, or **Device**. Grouping by referrer domain is the quickest way to find an external site that links to an outdated URL, and to tell a genuine outdated link apart from crawler noise.
* **404s caused by adaptive content**, if your site uses adaptive content. These are visitors who reached a page that exists but that a condition kept them from seeing. They are excluded from the findings, since a redirect would not help.

You can filter the report using the same filters as the rest of your [site analytics](insights/), including section, language, country, device, and referrer.
