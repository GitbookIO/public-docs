---
description: >-
  We run through the process of centralizing all your existing documentation in
  a single site using site sections in GitBook
---

# Combine multiple existing sites into one using site sections

With [site sections](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure/site-sections), you can now publish multiple spaces under one docs site — featuring global search. If you already have multiple sites published separately, or you’re using [variants](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure/variants) to publish different spaces, combining them into a single docs site will give your readers a much better experience.

Below, we’ll explain the best process for building your new, centralized docs site.

{% hint style="info" %}
You’ll need to be on one of our [new pricing plans](https://www.gitbook.com/pricing) to use site sections. Please reach out to our support team if you’re interested in migrating.
{% endhint %}

{% stepper %}
{% step %}
#### Create a new Ultimate docs site

To make the transition from your existing sites smooth, it’s a good idea to create a new sandbox site where you can set up your new structure.

To do this, Click the `+` next to the **Docs sites** header in the sidebar to create a new site. For now, give it a name that’s clear that this is a WIP environment, such as “Test – Docs sections”.

<figure><img src="../.gitbook/assets/create-new-site.jpg" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Set up your new site structure

In your new docs site’s dashboard, click the **Settings** tab at the top, then choose the **Structure** section.

Here, you can organize your new site and add all the content you want. Click **Add section** to create a new site section and select your the existing space you want.

<figure><img src="../.gitbook/assets/site-structure.jpg" alt=""><figcaption></figcaption></figure>

If you want to add [variants](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure/variants) — if you have localized your docs into other languages, for example — you can do that for each individual section.

[Head to our docs](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/site-structure) to find out more about structuring your documentation.

{% hint style="success" %}
You can link a space as many sites as you like — the content of the space will be unaffected. So adding your published spaces here will have no impact on your other live sites.
{% endhint %}
{% endstep %}

{% step %}
#### Match the section slugs to existing site slugs

Once you have your site structure in place, you'll want to ensure that the section slugs match the existing site slugs that you have published today.

You can edit the slugs in the section modal.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Publish with a test domain

Once you’re happy with your site structure, the next step is to understand the impact to your existing site URLs.

To do this, we first need to set up a new custom domain that is different from the existing domain shared by your other sites. For example, if the URL being used by your current sites is `docs.company.com` you could use `docs-test.company.com` .

Once you have the test domain set up, hit **Publish** to push your site live.
{% endstep %}

{% step %}
#### Check URL mapping and add redirects where needed

Explore your new site a little and compare the URLs for each site section and variant to the URLs for your existing published sites with that same content.

If some important URLs will change in your new site, you can [add redirects](https://gitbook.com/docs/publishing-documentation/site-redirects) in your new site’s **Settings** page so they point users and search engines to the correct content. For example, if your existing docs landing page is `gitbook.com/docs/home`, you can set up a redirect from `/home` to the new landing page of your site.

When you complete your migration and change the domain of your new site to take over the old site’s custom domain, these redirects will automatically send users to the page they need.

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FLBGJKQic7BQYBXmVSjy0%2Fuploads%2FlwX6eT4UEQZculaqr0EX%2Fredirects.mp4?alt=media&token=8722b096-6f84-43a1-abdd-c22d873e38c0" %}
{% endstep %}

{% step %}
#### Customize the site to mimic your existing docs

Once you’ve set up your site’s structure and redirects, you can customize your site to give it the same look and feel to the existing published content.

{% hint style="info" %}
If your existing sites use header links or links in your table of contents to link to your other content, these links will no longer be necessary with site sections. You may want to remove the TOC links in each space.
{% endhint %}

<figure><img src="../.gitbook/assets/cusomization.jpg" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
#### Switch your custom domain to the new site

When you’re happy with all of the customization and structure, it’s time to go live.

If your custom domain is currently being shared by multiple sites, you’ll first need to remove the domain from your organization. Click **Settings** at the bottom of the GitBook sidebar and choose **Organization settings**, and remove it in the **Publishing** section. You can then set it up on the test site that you've been building. Since this will impact your live documentation, you'll want to do this quickly to minimize any downtime. Here is the breakdown of the steps:

1. Go to organization settings.
2. Remove the organization-level domain in the **Publishing** section.
3. Click **Back to the app** in the bottom-left corner and return to your docs site’s dashboard.
4. Open the site’s **Settings** page and select the **Domain and redirects** tab.
5. Configure the domain on the new site by updating the `CNAME` target value in your DNS provider.
{% endstep %}

{% step %}
#### Check your new site is working properly

That’s it! Your new site will be live on your custom domain, and you can explore it to make sure that everything looks right, works as expected, and that the redirects are all correct.
{% endstep %}
{% endstepper %}
