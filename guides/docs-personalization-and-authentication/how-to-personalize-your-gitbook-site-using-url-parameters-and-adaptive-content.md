# How to personalize your GitBook site using URL parameters and adaptive content

{% hint style="info" %}
You’ll need an [Ultimate site](https://www.gitbook.com/pricing) with [adaptive content enabled](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/url) to follow this guide.
{% endhint %}

Adaptive content transforms your documentation from a static reference into a dynamic experience tailored to the person reading it.

With just a bit of configuration, you can show different content depending on who’s visiting — like first-time users, advanced developers, or potential customers. This guide will walk you through how to set up adaptive content using URL parameters — no authentication required.

<figure><img src="../.gitbook/assets/Adaptive Content.png" alt=""><figcaption></figcaption></figure>

### Why use URL parameters?

Passing claims through URL parameters is a simple way to personalize the docs experience without requiring users to log in.

It’s perfect for use cases like:

* Showing beginner vs. advanced guides
* Testing new content flows via email or campaigns
* Tailoring landing pages for different user groups

We’ll walk through a setup where we adapt our docs for two personas: beginner developers and advanced developers.

### Enable adaptive content

To get started, head to your **GitBook editor**, and open the **Settings** for your site.

Navigate to the **Audience** tab, and scroll to the bottom. Click **Enable adaptive content** to turn it on for your site.

This unlocks the ability to personalize content using visitor claims — including those passed through the URL.

### Set your visitor schema

A visitor schema defines what claims GitBook should expect when someone visits your site. It’s required to keep your site performant and to enable autocomplete when setting conditions.

Since we’re passing a simple flag to identify advanced users, our schema will look like this:

```json
{
  "type": "object",
  "properties": {
    "unsigned": {
      "type": "object",
      "properties": {
        "isAdvanced": {
          "type": "boolean",
          "description": "Whether the visitor is an advanced user."
        }
      },
      "additionalProperties": false
    }
  },
  "additionalProperties": false
}
```

{% hint style="info" %}
Claims passed via URL parameters must be nested under `unsigned`, since they’re not secured and can be changed by the user. For more secure options, see our guides on [cookies](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content/cookies) or [authenticated access](https://gitbook.com/docs/publishing-documentation/authenticated-access).
{% endhint %}

Paste your schema into the **Visitor schema** section in the Audience settings and click **Save**.

Now your site is ready to receive and respond to claims from URL parameters.

### Personalize a page using conditions

Let’s say you’ve created two pages in your space:

* A **Beginner guide**
* An **Advanced guide**

You only want advanced users to see the advanced guide.

1. Head to the **space** containing your content.
2. Create a new **change request** to make your edits.
3. Click the **three-dot menu** next to your advanced guide.
4. Choose **Set audience → Conditional**.
5. In the condition editor, add the following:

```javascript
visitor.claims.unsigned.isAdvanced == true
```

Click **Save**.

This ensures that only users who visit your site with the claim `isAdvanced=true` in the URL will be able to see the advanced guide.

### Preview and test using segments

You can test this experience before publishing using segments.

1. In your **change request**, go to the **Preview** tab.
2. Click the dropdown at the top that says **Default experience**.
3. Create a new segment and name it “Advanced”.
4. Use the following JSON for claims:

```json
{
  "unsigned": {
    "isAdvanced": true
  }
}
```

Now you can toggle between the **Default** and **Advanced** segments to confirm that your condition is working correctly — the advanced guide should only appear when the claim is present.

### Share your personalized link

Once your change request is merged and your content is live, you can start sharing personalized links.

For example:

```
https://docs.example.com/?visitor.isAdvanced=true
```

Any user who visits this link will see the advanced guide — no login required.

You can use these links in campaigns, onboarding emails, or even add buttons in your site’s header to toggle different views.

### What’s next?

You’ve just set up adaptive content using URL parameters — a quick and flexible way to personalize your docs experience.

You can build on this by:

* Targeting more claims (like region, industry, or use case)
* Creating testing flows for new content
* Offering onboarding paths tailored to user type

[**→ Learn more about adaptive content**](https://gitbook.com/docs/publishing-documentation/adaptive-content)

[**→ Explore other data methods for personalization**](https://gitbook.com/docs/publishing-documentation/adaptive-content/enabling-adaptive-content)
