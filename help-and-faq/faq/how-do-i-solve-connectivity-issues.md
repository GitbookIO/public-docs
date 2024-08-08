---
description: Avoiding network related access issues.
---

# How do I solve connectivity issues?

Here is a list of services GitBook relies on to run its app. If you have any kind of firewall or application that blocks all traffic or some of the sites listed below, you should add an exception to allow GitBook to work in your network.

### App

* `*.gitbook.com`
  * `app.gitbook.com`
  * `api.gitbook.com`
  * `content.gitbook.com`
  * `clearbit-risk.gitbook.com`
  * `files.gitbook.com`
  * `segment-cdn.gitbook.com`
  * `segment-api.gitbook.com`
* `*.gitbook.io`

### CDNs

* `cdn.iframe.ly`
* `cdn.polyfill.io`

### Google APIs

* `*.googleapis.com`
  * `firebase.googleapis.com`
  * `firestore.googleapis.com`
  * `www.googleapis.com`
* `*.googleusercontent.com`
* `*.googletagmanager.com`

### Sentry

* `*.sentry.io`

### Troubleshooting

Here are a few possible causes for your connectivity issues:

* Temporary local or regional network issues
* Browser security settings
* Browser plugins
* Security/antivirus
* Firewalls
* Plugins/extensions
* Proxies
* Local network settings
* Your provider
* Your area/region

{% hint style="info" %}
Please always check [our status page](https://www.gitbookstatus.com/) to see if there are any outages to our app or the third-party services we rely on.
{% endhint %}

If everything fails, please share the details with <img src="../../.gitbook/assets/gitbook-support.png" alt="" data-size="line"> [GitBook Support](mailto:support@gitbook.com).
