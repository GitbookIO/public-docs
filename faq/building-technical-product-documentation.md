---
description: Use GitBook to create technical product documentation
---

# Building technical product documentation

Documentation is a vital part of any product, and teams that nail theirs from the start get ahead of the competition earlier on. Engaging product documentation adds so much value; it increases your user's confidence in the product, improves the user experience, and increases user satisfaction.

Often, writers of product documentation face challenges related to ease of contribution, updating and maintaining information, and the look and feel of the docs. This can result in having to compromise on at least one of those aspects — but not with GitBook!

GitBook allows you to make writing beautiful documentation part of your everyday workflow.

## Key benefits and features of GitBook

* [**Import or create your content**](building-technical-product-documentation.md#import-or-create-your-content)\
  Get started in a matter of minutes with our intuitive editor.&#x20;
*   [**Make use of content blocks**](building-technical-product-documentation.md#make-use-of-content-blocks)

    Create easy to read content with blocks designed for technical authors and readers.&#x20;
*   [**Collaborate with your team**](building-technical-product-documentation.md#collaborate-with-your-team)

    Review your content in change requests while maintaining full control of each version.
* [**Match your existing Git workflow**](building-technical-product-documentation.md#match-your-existing-git-workflow)\
  Bridge the gap between collaborators who write directly in the GitBook editor, and those who prefer to write in Markdown in a GitHub or GitLab repository.
* [**Customize your documentation**](building-technical-product-documentation.md#customize-your-documentation)\
  Create beautiful docs that match _your_ brand by uploading your logo, setting a primary color, choosing a font, and more.
* [**Integrate existing tools within your docs**](building-technical-product-documentation.md#integrate-existing-tools-within-your-docs)\
  Include live code samples directly in your doc with RunKit, create graphs and diagrams with Markdown.&#x20;
*   [**Publish your documentation**](building-technical-product-documentation.md#publish-your-documentation)

    Choose from a number of visibility settings, plus you can publish on your own custom domain.

## Import or create your content

GitBook allows you to easily start creating and editing your content. In cases where you already have content written elsewhere, you can [import](broken-reference) it. We support importing from files or websites that are in markdown, HTML or Microsoft word formats, as well as importing from a number of other services.

{% content-ref url="../content-creation/import.md" %}
[import.md](../content-creation/import.md)
{% endcontent-ref %}

Alternatively, if you are just kicking off your documentation journey you can easily start writing by designing your [content structure](../content-creation/content-structure/) and inviting other [collaborators](../collaboration/collaboration/) to work with you.

## Make use of content blocks

In addition to standard text, image and list blocks, GitBook allows you to directly include more technical content. Find out more about:

* [Code blocks](../content-creation/blocks/code-block.md)
* [API blocks](../content-creation/blocks/api-method.md)
* [More block types](../content-creation/blocks/)

## Collaborate with your team

Once your initial content exists, it's important to design a contribution workflow that will ensure your documentation remains up-to-date. You can manage the access of each contributor or team of contributors through [permissions and inheritance](../account-management/member-management/permissions-and-inheritance.md), allowing for a review process before merging your content into the main branch.

Each change request is tracked and logged in the [activity tab](../content-creation/activity-history.md), which gives you an overview of the work that has been happening in the space. If you ever need to view or roll back to an older version of the content, you can do that from the [change history](../content-creation/activity-history.md#see-the-activity-of-a-specific-draft) section.

## Match your existing Git workflow

A huge benefit of GitBook is the ability to bridge the gap between contributors who prefer to collaborate in Markdown or write documentation directly in their Git repository and those who may not know Markdown or simply prefer the expanded editing capabilities.&#x20;

Thanks to our [bi-directional sync](../integrations/git-sync/bi-directional-git-integration.md), documentation is continuously updated regardless of whether it is edited in your Git repository or in GitBook, removing any potential friction or silos in your team.

{% content-ref url="../integrations/git-sync/" %}
[git-sync](../integrations/git-sync/)
{% endcontent-ref %}

## Customize your documentation

GitBook makes it easy to align your documentation with your branding. Change the logo, font, primary colour, header and footer links, light or dark mode, and more in our interactive [customizer](../publishing/customization/space-customization.md).

Additionally, each page can make use of one of three [layouts](../publishing/share/page-layouts.md): docs page, editorial post, and landing page. Combining landing pages with docs pages can help with structuring your technical product documentation in a way that helps users find what they're looking for, faster.

## Integrate existing tools within your docs

We've made it easier for your documentation to integrate closely with other tools you use for support, tracking or collaboration allowing you to build one smooth workflow.

Our [RunKit](https://github.com/GitbookIO/integrations) integration allows your users to run sample code directly from your documentation, embedding interactive JavaScript playgrounds connected to a complete Node environment right in your browser.

Our [Mermaid](https://github.com/GitbookIO/integrations) integration allows you to create diagrams and visualizations using text and code. With the integration enabled you can insert the Mermaid block into any page. You can edit the code content and preview how it looks using the live editor.

{% hint style="info" %}
When using [Git Sync](../integrations/git-sync/), all code blocks with the mermaid syntax will be replaced by diagram. All diagrams inserted from the editor will be formatted as such code blocks in Markdown.
{% endhint %}

We offer a number of [other integrations](https://github.com/GitbookIO/integrations), too, and have plans to make it easier to extend GitBook with additional integrations in the future. 🤩

## Publish your documentation

When your documentation is ready, publishing it is a breeze! Choose from [a number of options](../publishing/share/space-publishing.md), deciding based on who should have access to the published content.

For complete control, we offer [visitor authentication](../publishing/visitor-authentication.md). This feature lets _your_ server-side code handle who has access to the content.

As a finishing touch, [set a custom domain](../publishing/custom-domain/) so that your visitors can use a subdomain of your choice to access the published documentation. If your website is available at `example.com`, you might choose to set a custom domain of `docs.example.com` for your documentation.

## Start creating your product documentation today

Creating _good_ product documentation can be hard — but GitBook makes it easier! [Sign up](https://app.gitbook.com/join) or [log in](https://app.gitbook.com/) to start trying out these features right away.

