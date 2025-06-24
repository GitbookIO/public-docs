---
description: Pass visitor data into your docs through a feature flag provider.
---

# Feature flags

GitBook provides helper functions and integrations for popular feature flag service providers like **LaunchDarkly** and **Bucket**.

### LaunchDarkly

{% stepper %}
{% step %}
### Install the LaunchDarkly integration

To get started, you’ll first need to [install the LaunchDarkly integration](https://app.gitbook.com/integrations/launchdarkly) into your GitBook site.
{% endstep %}

{% step %}
### Set up your project and access keys

Add your project key and your service access token from your [LaunchDarkly settings](https://app.launchdarkly.com/settings).
{% endstep %}

{% step %}
### Install the GitBook helper

After setting up the LaunchDarkly integration, you’ll need to install the GitBook adaptive content helper in your project.

```bash
npm install @gitbook/adaptive
```
{% endstep %}

{% step %}
### Configure your client

Finally, you’ll need to use the `withLaunchDarkly` helper with the LaunchDarkly React SDK to pass context into GitBook.

```javascript
import { render } from 'react-dom';
import { withLaunchDarkly } from '@gitbook/adaptive';
import { asyncWithLDProvider, useLDClient } from 'launchdarkly-react-client-sdk';
import MyApplication from './MyApplication';

function PassFeatureFlagsToGitBookSite() {
    const ldClient = useLDClient();
    React.useEffect(() => {
        if (!ldClient) {
            return;
        }
        return withLaunchDarkly(ldClient);
    }, [ldClient]);
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
        <LDProvider>
            <PassFeatureFlagsToGitBookSite />
            <MyApplication />
        </LDProvider>,
        document.getElementById('reactDiv'),
    );
})();
```
{% endstep %}
{% endstepper %}

Once connected, any feature flag value available in LaunchDarkly will be exposed as part of the visitor schema under the `unsigned.launchdarkly.flags` object.

### Bucket

{% stepper %}
{% step %}
### Install the Bucket Integration

To get started, you’ll first need to [install the Bucket integration](https://app.gitbook.com/integrations/bucket) into your GitBook site.
{% endstep %}

{% step %}
### Set up your secret key

Add your secret key from your [Bucket settings](https://app.bucket.co/envs/current/settings/app-environments).
{% endstep %}

{% step %}
### Install the GitBook helper

After setting up the Bucket integration, you’ll need to install the GitBook adaptive content helper in your project.

```bash
npm install @gitbook/adaptive
```
{% endstep %}

{% step %}
### Configure your client

Finally, you’ll need to use the `withBucket` helper with the LaunchDarkly React SDK to pass context into GitBook.

```javascript
import { withBucket } from '@gitbook/adaptive';
import { BucketProvider, useClient } from '@bucketco/react-sdk';
import MyApplication from './MyApplication';

function PassFeatureFlagsToGitBookSite() {
    const client = useClient();
    React.useEffect(() => {
        if (!client) {
            return;
        }
        return withBucket(client);
    }, [client]);
    return null;
}
export function Application() {
    const currentUser = useLoggedInUser();
    const appConfig = useAppConfig();
    return (
        <BucketProvider
            publishableKey={appConfig.bucketCo.publishableKey}
            user={{
                id: currentUser.uid,
                email: currentUser.email ?? undefined,
                name: currentUser.displayName ?? '',
            }}
            company={{
                id: currentUser.company.id,
            }}
        >
            <PassFeatureFlagsToGitBookSite />
            <MyApplication />
        </BucketProvider>
    );
}
```
{% endstep %}
{% endstepper %}

Once connected, any feature flag value available in Bucket will be exposed as part of the visitor schema under the `unsigned.bucket.flags` object.

{% hint style="info" %}
Feature flag values are evaluated on the client side, so avoid using this method to pass sensitive or security-critical data.
{% endhint %}
