---
icon: cloud-bolt
description: Deliver a tailored documentation experience based on who's reading.
hidden: true
noIndex: true
---

# Adaptive content

{% hint style="warning" %}
This feature is currently is still currently under development, and is subject to change. More information on using this feature in production will be updated soon.
{% endhint %}

When a user visits your site, you may already know things about them - who they are, which plan they're subscribed to, which features they have access to.

Adaptive content helps to build a tailor documentation experience based on who is reading.

<figure><img src="../.gitbook/assets/10_01_25_adaptive_content.svg" alt=""><figcaption><p>Define user access to a page through it's visibility.</p></figcaption></figure>

When a user visits your sites, we call the data they bring with them their "claims". These claims are controllable by you - the site author - and can be used through the GitBook product to change your site's behaviour.

Out of the box, we are intending to provide the following features built around user claims:

* Show and hide pages based on the claims.
* Show and hide entire sections or variants based on the claims.  For example, you may want to show a "Beta features" section if they user has the BETA\_USER flag.
* Conditionally change the header of your site based on the claims. For example, you may choose to show a "Sign in" button for users who have no claims. This can redirect to your authentication server and back to your docs, bringing the claims along the way.

We also have future plans to support:

* Changing the written content of your docs based on the claims. Some examples may be:
  * Showing upgrade callouts if the user is not on the required plan for a feature.
  * Inlining user API keys alongside API blocks.
* ... and more! We're keen to hear what you'd like to do with these claims!

## User claims

We intend to support a few different ways for you to bring user claims into the GitBook docs, but we are also keen to hear more from you on this!

#### Generating claims

You generate claims on your side - somewhere in your software stack. Generating claims means turning user properties into an encoded string, signed with a private key associated with your site. This means others can't fake claims on behalf of your users.

```
const token = createGitBookClaims({ isEnterpriseUser: true }, GITBOOK_PRIVATE_KEY);
// token = eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Once you have this token, you then put it somewhere GitBook can read it.

### Passing the claims token through the URL

One of simplest ways is to pass the token in the URL:

https://docs.gitbook.com?jwt\_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

This isn't always practical - it relies on your users specifically clicking on this URL. However, you might build this functionality into your auth server and put it in a Login button in the header:

1. Add a "Sign in" button to your docs header, only shown if user has no claims.
2. Sign in takes the user to your auth server, where the user can log in.
3. Once logged in, your auth server builds the claims token and redirects the user back to your docs site with the URL.
4. GitBook reads the token from the URL and strips it - to the user they don't see anything but now they have claims.

### Setting the claims token in a cookie

Similarly, if you control the root domain of your docs, you can set this token in a cookie that GitBook will read. For example:

1. Whenever a user visits app.mysite.com, calculate their claims tokens and set it in a cookie called `gitbook-visitor` on the mysite.com domain.
2. The next time the user visits docs.mysite.com, GitBook will read the cookie and apply the claim within.
