# Collection publishing

## Publishing your collection

![](<../.gitbook/assets/Publish Collection (1).png>)

Publishing a collection allows you to publish all – or a subset – of the collections' spaces. Collection publishing works almost exactly the same as space publishing.

### Public collection

A public collection is available to **anyone** on the internet. It will be indexed by search engines so that everyone can read it.

### Unlisted collection

Unlisted collections are publicly available, but they won't be indexed by search engines such as Google. They will still be accessible to anyone who has links to your documentation.\
It lets you easily share your content without it being searchable.

### 'Share link only' collection

Publish to a unique link. It will be accessible only by people who have access to the link. This link can be revoked and regenerated at any time.

**Learn more about shareable links** 🔗 :

{% content-ref url="../features/shareable-links.md" %}
[shareable-links.md](../features/shareable-links.md)
{% endcontent-ref %}

### Visitor authentication

Authenticate visitors accessing your collection with your custom backend. If your docs should be accessible to certain users only, and you have a mechanism to authenticate those users with your login system, you can use GitBook's visitor Authentication feature to make sure only the right people see your docs.

**Learn more about visitor authentication:**

{% content-ref url="../features/visitor-authentication.md" %}
[visitor-authentication.md](../features/visitor-authentication.md)
{% endcontent-ref %}

### Unpublished collection <a href="what-is-a-private-space" id="what-is-a-private-space"></a>

A private collection is a collection that only you and the team members you invited to collaborate can access. That means it can only be read and edited by members of your organization. This is a more secure way to keep your content private to a specific group of people.

{% hint style="info" %}
<mark style="color:blue;">**Good to know:**</mark> Unpublished collections are only accessible in the GitBook app, by a logged-in, authorized user. Visiting an unpublished collection will require you to be logged in and have the relevant permissions to access it.
{% endhint %}

### Changing your collection visibility <a href="setting-up-visibility" id="setting-up-visibility"></a>

If you would like to change the visibility of your collection simply navigate back to the publish button and select the visibility settings you want for your collection.

### Accessing share links and custom domains

After publishing content, hit the 'Link settings' button to access your share links (if you've published as 'Share link only') and your custom domain settings.

Here, you can generate or revoke any share links, or link a custom domain to your published content.

## Spaces inside a published collection

When you publish a collection, you still need to decide which spaces should be published in that collection or not. This might be a little confusing at first, but it lets you maintain private spaces inside a published collection. Maybe you've got a collection full of useful spaces, but you're working on a completely new space to live alongside them. Rather than creating and editing that space somewhere compeltely different, you can keep it where it's supposed to live, and only publish it as part of the collection when you're ready.

To include spaces in a published collection, set the [space visibility](../spaces/space-visibility.md) to 'In Collection' – this will include the space as part of the published collection.

## Collections as variants

Currently, the only publish mode for collections is as a container for 'variants'. Users of the previous version of GitBook will be familiar with this concept, but the gist is that publishing a collection of variants allows you to 'wrap' a number of spaces in a single published interface.

When you publish a collection of variants, any child space that's published along with the collection will be quickly accessible through a dropdown in the sidebar of the published content, allowing readers to switch between variants at any time.

Variants are useful if you need to offer a grouped experience for spaces, such as documenting multiple versions of an API (v1, v2, v3, etc.) or having multiple translations of your content easily accessible.

{% hint style="info" %}
<mark style="color:blue;">**Good to know:**</mark> Currently, variants are the only supported publish mode for a collection, so by default, any published collection will act as a variant container.
{% endhint %}
