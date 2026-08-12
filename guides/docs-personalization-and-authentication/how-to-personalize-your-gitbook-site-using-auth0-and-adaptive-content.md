# How to personalize your GitBook site using Auth0 and adaptive content

{% hint style="info" %}
You’ll need an [Ultimate site](https://www.gitbook.com/pricing) using [Authenticated Access](https://gitbook.com/docs/publishing-documentation/authenticated-access) with Auth0 to follow this guide.
{% endhint %}

Adaptive content lets you go beyond static documentation — tailoring what users see based on who they are. Whether it’s enterprise teams, pro users, or new customers, you can personalize docs based on each user’s plan, region, or role.

This guide walks you through how to configure GitBook to work with Auth0, pass user claims into your documentation, and show different content to different users — all using adaptive content.

{% embed url="https://www.youtube.com/embed/uhWeQkgyg8Y?si=Vt5aKgHmnGU98nRE" %}

### Protect your site with Auth0

Before you can personalize your docs, you’ll need to protect them behind Auth0 login.

Start by heading to your **site settings** in GitBook, opening the **Integrations** tab, and installing the **Auth0** integration.

Next, log into your [Auth0 dashboard](https://auth0.com/), and create a new application. Set it up for Node.js and Express (or whichever framework you’re using).

In your Auth0 app settings, copy the following values into GitBook:

* **Domain**
* **Client ID**
* **Client Secret**

Then, copy the **Callback URL** from GitBook and paste it into the “Allowed callback URLs” field in your Auth0 app settings. Click **Save**.

Back in GitBook, enable the toggle labeled **Include claims in JWT token**, then click **Save**.

Finally, head to the **Audience** tab in your site settings. Under **Access**, choose **Authenticated Access**, and select **Auth0** from the dropdown.

Publish your site and test it — visiting your docs should now prompt a login via Auth0.

### Attach claims with Auth0 Actions

Now that your site requires login, you can pass user-specific data (called _claims_) into GitBook to personalize the docs.

In Auth0, go to the **Actions** section in the sidebar and click **Library**.

Create a new Action:

* Name it something like “Add Enterprise Claim”
* Set the trigger to **Login / Post Login**

Use this basic code to attach a claim named `isEnterprise` to every logged-in user:

```javascript
exports.onExecutePostLogin = async (event, api) => {
  api.idToken.setCustomClaim('isEnterprise', true);
};
```

> You can add more complex logic here to assign claims only to specific users based on your own rules.

Save and **Deploy** your Action.

Then, go to **Triggers → Post Login**, and drag your Action into the workflow. Click **Apply** to finish.

At this point, any user who logs into your site will have the `isEnterprise` claim attached.

### Enable adaptive content in GitBook

Back in GitBook, open your site settings and go to the **Audience** tab.

Scroll down and enable **Adaptive content**. This unlocks the ability to personalize your content using visitor claims.

GitBook will generate a **visitor signing key** — you won’t need it for Auth0, but it’s good to keep track of.

### Set your visitor schema

Visitor schemas tell GitBook what claims to expect, and are required to use adaptive content.

Since we’re passing the `isEnterprise` claim, we’ll set up the following schema:

```json
{
  "type": "object",
  "properties": {
    "isEnterprise": {
      "type": "boolean",
      "description": "Whether the visitor is an Enterprise user."
    }
  },
  "additionalProperties": false
}
```

Paste this into the **Visitor schema** section and click **Save**.

#### Step 5: Adapt your docs content

Now that claims are being passed to GitBook, you can use them to show or hide content based on user type.

Let’s say you’ve created a special **Enterprise** section in your docs. To make it only visible to users with the `isEnterprise` claim:

1. Go to **Site settings → Structure**
2. Click the **three-dot menu** next to your Enterprise section
3. Choose **Set audience → Conditional**
4. In the condition editor, paste:

```javascript
visitor.claims.isEnterprise == true
```

Click **Save**.

That’s it — only enterprise users will now see this section when they visit your docs.

### Test your setup with segments

You can simulate different types of users using segments in the editor preview.

Go to the **Preview** tab in your site settings.

From the dropdown in the top bar, choose **Create new segment**. Name it “Enterprise user” and use this JSON:

```json
{
  "isEnterprise": true
}
```

Switch between the **Default experience** and **Enterprise user** segment to confirm your conditions work as expected.

#### Optional: Personalize your header links

You can also adapt your site’s header links — for example, showing a dedicated support link only to enterprise users.

1. Go to **Settings → Customization → Layout**
2. Add a header link to your support page
3. Open the three-dot menu for the link and set the audience to **Conditional**
4. Use the same condition as before:

```javascript
visitor.claims.isEnterprise == true
```

Save and test in the preview.

### What’s next?

You’ve now set up adaptive content with Auth0 and GitBook — giving every user a personalized docs experience.

You can continue expanding this setup by:

* Passing different claims for different user types
* Using claims to show specific onboarding flows
* Hiding or showing content based on features, regions, or roles

[**→ Learn more about adaptive content**](https://gitbook.com/docs/publishing-documentation/adaptive-content)

[**→ Explore GitBook’s authenticated access**](https://gitbook.com/docs/publishing-documentation/authenticated-access)
