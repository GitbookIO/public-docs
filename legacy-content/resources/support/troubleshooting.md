---
description: Quick fixes for common issues in the GitBook app
---

# Troubleshooting basics

### Pages or integrations aren’t loading

If the GitBook app isn’t loading, crashes on certain pages, shows “We couldn’t load the integration”, or analytics dashboards stay empty, the usual cause is an ad blocker or privacy extension blocking parts of the app.

1. Temporarily disable your ad blocker or privacy extension and reload the page.
2. If you don’t want to disable it entirely, add GitBook (and the services it uses) to your extension’s allowlist.
3. Refresh the page to check if it loads correctly.

### Hard refresh your browser

The support team might ask you to _hard_ refresh your browser as part of troubleshooting. This is different from a normal refresh.

{% tabs %}
{% tab title="Chrome" %}
On **Windows**, hold the CTRL key and press F5. On **Mac**, hold the CMD and SHIFT keys and press R.
{% endtab %}

{% tab title="Firefox" %}
On **Windows**, hold the CTRL key and press F5. On **Mac**, hold the CMD and SHIFT keys and press R.
{% endtab %}

{% tab title="Safari" %}
First, empty the cache: hold the OPT and CMD keys and press E. Then refresh the current page: hold the CMD key and press R.
{% endtab %}

{% tab title="Edge" %}
Hold the CTRL key and press F5.
{% endtab %}
{% endtabs %}

### Resolving a “Connection lost” message

“Connection lost” means GitBook can’t establish the network connections it needs — usually because something on your computer or network is blocking them. Common causes include browser extensions, firewalls, security software, proxies, and temporary network issues.

Work through these steps in order:

1. **Clear your cache and restart your browser.** This resolves most temporary connection issues.
2. **Restart your Wi-Fi or ethernet connection**, then try again.
3. **Try a different browser or device.** If GitBook works elsewhere, the issue is specific to your original setup — contact support and mention which browser you were using.
4. **Disable browser extensions** one by one to identify the cause.
5. **Check your firewall or security software** against the allowlist below.

Also check [GitBook’s status page](https://www.gitbookstatus.com/) for any current outages.

#### Safelisting GitBook’s domains

If a firewall or security application is blocking traffic, add the following domains to your allowlist:

**GitBook app**

* `*.gitbook.com` — including `app.gitbook.com`, `api.gitbook.com`, `clearbit-risk.gitbook.com`, `files.gitbook.com`, `segment-cdn.gitbook.com`, and `segment-api.gitbook.com`
* `*.gitbook.io`

**CDNs**

* `cdn.iframe.ly`
* `cdn.polyfill.io`

**Google APIs**

* `*.googleapis.com` — including `firebase.googleapis.com`, `firestore.googleapis.com`, and `www.googleapis.com`
* `*.googleusercontent.com`
* `*.googletagmanager.com`

**Sentry** (error monitoring)

* `*.sentry.io`

If the issue persists after all of these steps, [contact support](README.md) with details about your browser, device, and network setup.
