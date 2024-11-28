---
description: Set up site redirects to route traffic to content anywhere on your site
icon: diamond-turn-right
---

# Site redirects

<figure><img src="../.gitbook/assets/Redirects.png" alt=""><figcaption><p>Site redirects are useful when migrating documentation or restructuring content to avoid broken links, which can impact SEO.</p></figcaption></figure>

Redirects are commonly used when you are migrating your documentation from one provider to another — like when you just moved docs to GitBook. Broken links can impact SEO so we recommend setting up redirects where needed.

In addition to [automatic redirects created by GitBook](site-redirects.md#about-automatic-redirects), you can create a redirect from any path in your site’s domain.

## Managing redirects on your site

To get started, view your site’s dashboard in GitBook and click **Settings** <picture><source srcset="../.gitbook/assets/settings-dark.png" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/settings-light.png" alt="" data-size="line"></picture> in the top-right corner. Scroll down to the **Redirects** section.

### Creating redirects

Click **Add redirect** to begin. Fill in the source path — i.e. the URL slug that you wish to redirect somewhere else — and the destination content you wish to link to. You can pick any [section](site-structure-and-navigation/site-sections.md), [variant](site-structure-and-navigation/publish-multiple-spaces-on-one-site.md), or [page](../content-editor/editor/content-structure/content-in-a-space.md) on to your site. Click **Add** to create the redirect.&#x20;

If you want to add another redirect to the same page, you can toggle the **Add another redirect** option on before you hit **Add**. When you add your redirect, the modal will remain open with the destination content set to the previous selection so you can add another URL slug immediately.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-26 at 19.58.22.png" alt=""><figcaption><p>Clicking <strong>Add redirect</strong> opens a modal with two fields — <strong>Source path</strong> and <strong>Destination content</strong>.</p></figcaption></figure>

### Editing redirects

To edit a redirect, press the **Edit** <picture><source srcset="../.gitbook/assets/edit-dark.png" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/edit-light.png" alt="" data-size="line"></picture> icon next to it in the list. Update the redirect and hit **Save**.

To delete a redirect, press the **Delete redirect** button and confirm.

<figure><img src="../.gitbook/assets/Screenshot 2024-11-26 at 20.20.04.png" alt=""><figcaption><p>Clicking the <strong>Edit</strong> icon next to a redirect opens a modal that lets you edit or delete the redirect. </p></figcaption></figure>

## About automatic redirects

Whenever pages are moved or renamed, their canonical URL changes with them. In order to keep your content accessible, GitBook automatically creates a [HTTP 301](https://en.wikipedia.org/wiki/HTTP_301) redirect from the old URL to the new one.&#x20;

Every time a URL is loaded, GitBook resolves it through the following steps:

1. Site content is resolved to its canonical URL by following any of the automatically created redirects.
2. If the URL cannot be resolved, the URL is checked against [space-level redirects](../integrations/git-sync/content-configuration.md#redirects), defined in your repository's `.gitbook.yaml` file.
3. Finally, the URL is checked against site-level redirects, created via [the process above](site-redirects.md#creating-redirects).
