---
description: How to reach GitBook support and what to include.
---

# Get support

There are two ways to reach us:

* In the app, click the **question mark icon** in the [sidebar](the-gitbook-interface.md), then **Contact us** → **Send us a message**.
* Email [support@gitbook.com](mailto:support@gitbook.com) directly.

### What information should I share?

To help us help you as efficiently as possible:

* If your request relates to a specific space, include a link to it.
* Describe the steps you took, what happened, and what you expected instead.
* If you saw an error message, include it in full.
* A screenshot or short screen recording is extremely helpful.

### When will I get a response?

We aim to respond within 1 business day. Our support team works Monday to Friday, 9am–5pm GMT (±3 hours) — at busy times a response may take a little longer, but we'll always get back to you.

{% hint style="info" %}
We don't currently offer real-time support through the in-app widget — we respond as soon as we can, and you'll get an inbox notification when we do.
{% endhint %}

### Reporting a bug

Report bugs the same way — through the messaging widget or by [emailing support](mailto:support@gitbook.com) — with as much context as possible about how you encountered it.

<details>

<summary>Generate a network capture (HAR) for troubleshooting</summary>

A HAR capture records the requests and responses your browser makes with the GitBook app. Generate one, plus a console log, and send both as shared links in your support case.

**Chrome**

1. Go to the page in GitBook where you're seeing the issue.
2. Open the Chrome menu (⋮) → **More tools** → **Developer tools**.
3. Click the **Network** tab and enable **Preserve log**.
4. Make sure recording is on (a red circle at the top left of the Network tab — click the black circle if it isn't).
5. Refresh the page and reproduce the problem while it records.
6. Right-click any row in the activity pane and choose **Save as HAR with content**.
7. Open the **Console** tab, right-click, and **Save as...** — name it `Chrome-console.log`.

**Firefox**

1. Go to the page in GitBook where you're seeing the issue.
2. Open the Firefox menu → **Web Developer** → **Network**.
3. Enable **Persist logs**.
4. Refresh the page and reproduce the problem while it records.
5. Right-click any row and choose **Save all as HAR**.
6. Open the **Console** tab, select all, and paste into a text file named `console-log.txt`.

**Safari**

1. Go to the page in GitBook where you're seeing the issue.
2. **Develop** → **Show Web Inspector**.
3. Open the **Console** tab and enable **Preserve log**.
4. Switch to the **Network** tab, refresh, and reproduce the problem while it records.
5. Right-click any row and choose **Export HAR**.
6. Open the **Console** tab, select all, and paste into a text file named `console-log.txt`.

**Edge**

1. Go to the page in GitBook where you're seeing the issue.
2. Open the Edge menu (⋮) → **Developer tools**.
3. Open the **Network** tab and clear **Clear entries on navigate** (the blue-arrow-with-red-X icon).
4. Confirm recording is on (green play button).
5. Refresh the page and reproduce the problem while it records.
6. Click the **Export as HAR** icon (floppy disk).
7. Open the **Console** tab, select all, and paste into a text file named `console-log.txt`.

</details>

### Connectivity issues

<details>

<summary>Services GitBook depends on</summary>

If a firewall or security tool blocks traffic to any of these, add an exception so GitBook can work on your network:

* **App:** `*.gitbook.com` (including `app.`, `api.`, `clearbit-risk.`, `files.`, `segment-cdn.`, `segment-api.`) and `*.gitbook.io`
* **CDNs:** `cdn.iframe.ly`, `cdn.polyfill.io`
* **Google APIs:** `*.googleapis.com` (including `firebase.`, `firestore.`, `www.`), `*.googleusercontent.com`, `*.googletagmanager.com`
* **Sentry:** `*.sentry.io`

Common causes of connectivity issues: temporary local/regional network problems, browser security settings or plugins, antivirus software, firewalls, proxies, local network settings, or your provider/region.

{% hint style="info" %}
Check [our status page](https://www.gitbookstatus.com/) for any outages to GitBook or the third-party services it relies on.
{% endhint %}

If nothing resolves it, share the details with [GitBook Support](mailto:support@gitbook.com).

</details>

### Hard-refreshing your browser

<details>

<summary>How to hard refresh, by browser</summary>

Our support team may ask you to hard refresh as part of troubleshooting — this differs from a normal refresh.

* **Chrome** — Windows: Ctrl + F5. Mac: Cmd + Shift + R.
* **Firefox** — Windows: Ctrl + F5. Mac: Cmd + Shift + R.
* **Safari (Mac)** — first empty the cache (Opt + Cmd + E), then refresh (Cmd + R).
* **Edge (Windows)** — Ctrl + F5.

</details>

### Security FAQs

<details>

<summary>Where and how is my data stored?</summary>

All user data and content is stored in the US on [Google Cloud](https://cloud.google.com), backed by the same infrastructure and security Google uses for its own services.

Customer data lives in U.S. data centers. Some data (HTML pages and assets) may be cached in other geographies by our CDN — access to private content through the CDN is always validated through our application servers using a full permissions system.

Google follows, and often leads, most of the industry's best practices, and is compliant with major security [standards and certifications](https://cloud.google.com/security/compliance/).

</details>

<details>

<summary>Is GitBook SOC 2 certified?</summary>

Yes — see [our security page](https://policies.gitbook.com/privacy-and-security/security/security-as-a-company-value#soc-2-type-2) for details. Customers and prospects can request the audit report by contacting our sales team at `sales@gitbook.io`.

For more on how GitBook approaches security, see our [Security FAQ](https://policies.gitbook.com/privacy-and-security/security/security-faq).

</details>
