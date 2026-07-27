---
description: Publish your integration privately or publicly, and submit it to the marketplace.
---

# Publishing and submitting integrations

## Publishing your integration

Publishing pushes your integration to GitBook using the options defined in its `gitbook-manifest.yaml`. To publish, your manifest needs a `name`, `title`, `description`, `visibility`, `script`, `scopes`, and `organization` — see the [manifest reference](manifest-reference.md).

```bash
gitbook publish
```

After publishing, you'll get a link in your console to find and install your integration. Run `gitbook publish` again any time to update it.

### Visibility

To share or test your integration with others, change its `visibility`:

| Visibility | Description |
|---|---|
| `private` | Default for new integrations. Only members of the organization set in the manifest can install it. |
| `unlisted` | Members of any organization can install it, but only via its shared install link. |
| `public` | Members of any organization can install it. Required before submitting to the marketplace. |

## Submitting your integration for review

Once your integration is published and working via its install link, you can go further and list it on GitBook's public, verified integrations page.

### 1. Publish publicly

Set `visibility: public` in `gitbook-manifest.yaml` — this lets GitBook test and review your integration from outside your organization.

### 2. Test with others

Before submitting, test the integration with people outside your organization to catch bugs and gather feedback. Worth checking:

* How good is the end-user experience?
* Is the integration fully functional?
* Are there edge cases you haven't considered?
* Does it expose any private or insecure data?

### 3. Prepare assets

All of this metadata comes from your `gitbook-manifest.yaml` and is shown on your integration's listing page once published:

| Field | Notes |
|---|---|
| **Name** | Must be unique across all GitBook integrations. Avoid suffixes like `-gitbook` or `-integration`. |
| **Icon** | High-resolution, 1:1 aspect ratio. Recommended: 512×512px. |
| **Preview images** | High-resolution. Recommended: 1600×800px, 2:1 aspect ratio. |
| **Summary** | Displayed under the preview images. Supports Markdown. |
| **Description** | Displayed to the right of the name on the listing page. |
| **Categories** | Used to sort and filter integrations on GitBook's integrations page. |
| **External links** | Displayed on the left side of the listing page. |

{% hint style="info" %}
GitBook has a [preview image and icon generator](https://integrate-vs.lovable.app/) that meets the design requirements above.
{% endhint %}

### 4. Submit

Once you've tested your integration and prepared its assets, submit it via [this form](https://forms.gle/SXBdguvquFsCUtDX8). You'll need to provide:

* Your name and contact email address.
* The published integration's name.
* A link to its code repository (public, or accessible to GitBook staff if private).
* Its installation link.
