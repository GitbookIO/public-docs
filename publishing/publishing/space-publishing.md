---
description: Learn about the different options for sharing your GitBook space.
---

# Space sharing

## Sharing a space

To share a space, start by clicking the **share** button, which you'll find near the top-right corner of each space. This will open the share modal.

<figure><img src="../../.gitbook/assets/share-button-modal.gif" alt=""><figcaption><p>To share a space, start by clicking the share button. This will open the share modal.</p></figcaption></figure>

Inside the share modal, you'll see tabs on the left-hand side to choose from. The tabs available to you will depend on your permissions in the space.

### Invite members

If you have administrator permissions for the space, you'll see the option to invite members here. Inviting a member will make them a member of the organization that owns the space, and the cost for this will depend on the [plan](../../account-management/plans/) that the organization is subscribed to.

It is also possible to invite members to the organization from within the organization settings area.

{% content-ref url="../../collaboration/invite-members-to-your-organization/" %}
[invite-members-to-your-organization](../../collaboration/invite-members-to-your-organization/)
{% endcontent-ref %}

If you want your content to remain private, shared only with a specific person or group, inviting that person or people to be a member of your organization could be a great choice. They will be able to access the content when they are logged into their GitBook account.

### Publish to the web

On the other hand, your content might be suited for a much wider audience! If that's the case, you might like to publish it to the web. Spaces that are published to the web can be [indexed by search engines](../seo.md) and will be available to **anyone** on the Internet.

You'll still retain control over who can _edit_ your content, and only your primary content branch will be published, so any [change requests](../../collaboration/collaboration/change-requests.md) will remain private until merged.

### Share to an audience

In some cases, you might want to publish your content, but only permit certain people to access it. We offer a number of options for this:

1. **Publish in collection**\
   ****If the space is nested inside of a published collection, you'll see this option. A space nested inside of a collection does not _have_ to be published as part of the collection, so that you can do things like work on a new version and only publish it when it's ready. Toggle this option on to publish the space as part of the collection. You can [find out more about collection publishing](collection-publishing.md).
2. **Publish with** [**visitor authentication**](../visitor-authentication.md)\
   With visitor authentication, GitBook lets _your_ server-side code handle who has access to the content. You can [find out more about visitor authentication](../visitor-authentication.md).
3. **Publish with** [**share links**](share-links.md)\
   Share links include a private token, making it extremely difficult for anyone outside of those you share the link with to find the content. This can be a great way to share private content with those who are not members of your organization. You can [find out more about share links](share-links.md).
4. **Publish as unlisted**\
   Unlisted spaces are publicly available, but they _won't_ be indexed by search engines such as Google. They will still be accessible to anyone on the Internet who knows (or can guess) the link to your documentation. Unlisted spaces can be particularly helpful if you want to publish a beta of your docs, or do large-scale user-testing, without impacting your SEO with potentially duplicate content, etc.

### Export as PDF

This option allows you to generate a PDF copy of your content and share this with others in any way you choose. You can export one or more single pages, or the entire space in one PDF file.

### Who can access?

This tab confirms the current visibility of the space, along with who has access to it within the GitBook app. No settings can be changed here; all changes are made from within the other tabs.

