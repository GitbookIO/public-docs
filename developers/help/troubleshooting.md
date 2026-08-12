---
description: Resolve loading, connection, and caching issues in the GitBook app
---

# Troubleshooting

#### Pages or integrations aren't loading

If the GitBook app isn't loading, crashes on certain pages, shows "We couldn't load the integration", or analytics dashboards stay empty, the usual cause is an ad blocker or privacy extension blocking parts of the app.

1. Temporarily disable your ad blocker or privacy extension and reload the page.
2. If you don't want to disable it entirely, add the domains under [Allowed domains](troubleshooting.md#allowed-domains) to your extension's allowlist.
3. Refresh the page to check if it loads correctly.

#### "Connection lost"

"Connection lost" means GitBook can't establish the network connections it needs — usually because something on your computer or network is blocking them. Common causes include browser extensions, firewalls, security software, proxies, and temporary network issues.

Work through these steps in order:

1. **Clear your cache and restart your browser.** This resolves most temporary connection issues.
2. **Restart your Wi-Fi or ethernet connection**, then try again.
3. **Try a different browser or device.** If GitBook works elsewhere, the issue is specific to your original setup — mention which browser you were using when you contact support.
4. **Disable browser extensions** one by one to identify the cause.
5. **Check your firewall or security software** against [Allowed domains](troubleshooting.md#allowed-domains).

Also check [GitBook's status page](https://www.gitbookstatus.com/) for any current outages.

#### Hard refresh your browser

The support team might ask you to _hard_ refresh your browser. This is different from a normal refresh — it clears cached files the page is still using.

{% tabs %}
{% tab title="Chrome, Firefox, and Edge" %}
On **Windows**, hold the CTRL key and press F5. On **Mac**, hold the CMD and SHIFT keys and press R.
{% endtab %}

{% tab title="Safari" %}
First, empty the cache: hold the OPT and CMD keys and press E. Then refresh the current page: hold the CMD key and press R.
{% endtab %}
{% endtabs %}

#### Allowed domains

If a firewall, proxy, or security application is blocking traffic, add these domains to your allowlist.

**Required.** GitBook doesn't work without these:

* `*.gitbook.com` — including `app.gitbook.com`, `api.gitbook.com`, and `files.gitbook.com`
* `*.gitbook.io`
* `*.googleapis.com` — including `firebase.googleapis.com`, `firestore.googleapis.com`, and `www.googleapis.com`
* `*.googleusercontent.com`
* `cdn.iframe.ly` — needed for embedded content

**Optional.** These cover analytics and error monitoring. Blocking them doesn't affect how GitBook works:

* `segment-cdn.gitbook.com` and `segment-api.gitbook.com`
* `clearbit-risk.gitbook.com`
* `*.googletagmanager.com`
* `*.sentry.io`

If the issue persists after all of these steps, contact support with details about your browser, device, and network setup.
