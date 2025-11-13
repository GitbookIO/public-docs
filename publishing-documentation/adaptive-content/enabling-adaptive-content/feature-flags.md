---
description: Pass visitor data into your docs through a feature flag provider.
---

# Feature flags

{% hint style="warning" %}
Using adaptive content with feature flags requires adding code to your application.

Currently, the GitBook helper only supports React based setups.
{% endhint %}

GitBook provides helper functions and integrations for popular feature flag service providers like [**LaunchDarkly**](feature-flags.md#launchdarkly) and [**Reflag**](feature-flags.md#reflag).

This allows you to read the feature flags users have access to in your product, as they read your docs. This is useful if you need to show documentation for features that are only available to a specific group of people.

### LaunchDarkly

LaunchDarkly allows you to send feature flag access as claims through the [`launchdarkly-react-client-sdk`](https://launchdarkly.com/docs/sdk/client-side/react/react-web) and GitBook’s [`@gitbook/adaptive`](https://app.gitbook.com/o/d8f63b60-89ae-11e7-8574-5927d48c4877/s/zq8ynchcecIscc4uulgN/) package.

If you’re using LaunchDarkly feature flags in your product already, chances are you already have this package configured.

To pass you these feature flags as claims to GitBook, follow these steps:

{% stepper %}
{% step %}
**Install the LaunchDarkly integration**

To get started, you’ll first need to [install the LaunchDarkly integration](https://app.gitbook.com/integrations/launchdarkly) into your GitBook site.
{% endstep %}

{% step %}
**Set up your project and access keys**

Add your project key and your service access token from your [LaunchDarkly settings](https://app.launchdarkly.com/settings) to the integration’s configuration.
{% endstep %}

{% step %}
**Install and add the GitBook helper to your application**

After setting up the LaunchDarkly integration, you’ll need to install the GitBook adaptive content helper in your application.

```bash
npm install @gitbook/adaptive
```
{% endstep %}

{% step %}
**Configure your application**

You’ll need to use the `withLaunchDarkly` helper with the LaunchDarkly React SDK to pass context into GitBook.

<pre class="language-javascript"><code class="lang-javascript">import { render } from 'react-dom';
<strong>import { withLaunchDarkly } from '@gitbook/adaptive';
</strong><strong>import { asyncWithLDProvider, useLDClient } from 'launchdarkly-react-client-sdk';
</strong>import MyApplication from './MyApplication';

function PassFeatureFlagsToGitBookSite() {
<strong>    const ldClient = useLDClient();
</strong>    React.useEffect(() => {
        if (!ldClient) {
            return;
        }
<strong>        return withLaunchDarkly(ldClient);
</strong>    }, [ldClient]);
    return null;
}
(async () => {
    const LDProvider = await asyncWithLDProvider({
        clientSideID: 'client-side-id-123abc',
        context: {
            kind: 'user',
            key: 'user-key-123abc',
            name: 'Sandy Smith',
            email: 'sandy@example.com'
        },
        options: { /* ... */ }
    });
    render(
        &#x3C;LDProvider>
            &#x3C;PassFeatureFlagsToGitBookSite />
            &#x3C;MyApplication />
        &#x3C;/LDProvider>,
        document.getElementById('reactDiv'),
    );
})();
</code></pre>
{% endstep %}

{% step %}
**Check your visitor schema**

A [visitor schema](./#set-your-visitor-schema) is required in order for your claims to be able to be read in your published site. Installing and configuring the LaunchDarkly integration should automatically set your visitor schema for you.
{% endstep %}

{% step %}
**Personalize your content**

After setting your visitor schema, you’re ready to tailor your docs experience for the users visiting your site, using the feature flags the user has access to.

Any feature flag value available in LaunchDarkly will be exposed as part of the visitor schema under the `visitor.claims.unsigned.launchdarkly` object. Read more about unsigned claims [here](./#set-an-unsigned-claim).

Head to [adapting your content](../adapting-your-content.md) to learn more about personalizing your docs for your users.
{% endstep %}
{% endstepper %}

### Reflag

Reflag allows you to send feature flag access as claims through the [`@reflag/react-sdk`](https://www.npmjs.com/package/@reflag/react-sdk) and GitBook’s [`@gitbook/adaptive`](https://github.com/GitbookIO/integrations/tree/main/packages/adaptive) package.

If you’re using Reflag feature flags in your product already, chances are you already have this package configured.

To pass you these feature flags as claims to GitBook, follow these steps:

{% stepper %}
{% step %}
**Install the Reflag Integration**

To get started, you’ll first need to [install the Reflag integration](https://app.gitbook.com/integrations/bucket) into your GitBook site.
{% endstep %}

{% step %}
**Set up your secret key**

Add your secret key from your [Reflag settings](https://app.reflag.com/envs/current/settings/app-environments) to the integration’s configuration.
{% endstep %}

{% step %}
**Install the GitBook helper to your application**

After setting up the Reflag integration, you’ll need to install the GitBook adaptive content helper in your application.

```bash
npm install @gitbook/adaptive
```
{% endstep %}

{% step %}
**Configure your application**

You’ll need to use the `withReflag` helper with the Reflag React SDK to pass context into GitBook.

<pre class="language-javascript"><code class="lang-javascript"><strong>import { withReflag } from '@gitbook/adaptive';
</strong><strong>import { ReflagProvider, useClient } from '@reflag/react-sdk';
</strong>import MyApplication from './MyApplication';

function PassFeatureFlagsToGitBookSite() {
<strong>    const client = useClient();
</strong>    React.useEffect(() => {
        if (!client) {
            return;
        }
<strong>        return withReflag(client);
</strong>    }, [client]);
    return null;
}
export function Application() {
    const currentUser = useLoggedInUser();
    const appConfig = useAppConfig();
    return (
        &#x3C;ReflagProvider
            publishableKey={appConfig.reflagCom.publishableKey}
            user={{
                id: currentUser.uid,
                email: currentUser.email ?? undefined,
                name: currentUser.displayName ?? '',
            }}
            company={{
                id: currentUser.company.id,
            }}
        >
            &#x3C;PassFeatureFlagsToGitBookSite />
            &#x3C;MyApplication />
        &#x3C;/ReflagProvider>
    );
}
</code></pre>
{% endstep %}

{% step %}
**Check your visitor schema**

A [visitor schema](./#set-your-visitor-schema) is required in order for your claims to be able to be read in your published site. Installing and configuring the Reflag integration should automatically set your visitor schema for you.
{% endstep %}

{% step %}
**Personalize your content**

After setting your visitor schema, you’re ready to tailor your docs experience for the users visiting your site, using the feature flags the user has access to.

Any feature flag value available in Reflag will be exposed as part of the visitor schema under the `visitor.claims.unsigned.reflag` object. Read more about unsigned claims [here](./#set-an-unsigned-claim).

Head to [adapting your content](../adapting-your-content.md) to learn more about personalizing your docs for your users.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Feature flag values are evaluated on the client side, so avoid using this method to pass sensitive or security-critical data.
{% endhint %}
