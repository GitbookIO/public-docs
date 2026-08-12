---
description: Learn how to build beautiful, interactive API documentation in GitBook.
---

# Document your API in GitBook in 5 simple steps

This comprehensive guide will walk you through the process of documenting your API in GitBook, from initial setup to advanced customization. By the end, you’ll have a professional API reference that your users will love.

<figure><img src="../.gitbook/assets/Empty state.png" alt=""><figcaption></figcaption></figure>

### What is API documentation or an API reference?

GitBook’s API features allows you to create beautiful, interactive API documentation using your OpenAPI (formerly Swagger) specification. It supports:

* OpenAPI 3.0 and 3.1 specifications
* Multiple API versions
* Custom code samples
* Enums and complex data types
* CI/CD integration
* \+ more

#### Prerequisites

Before you begin, you’ll need:

* A [GitBook account](https://app.gitbook.com/join) and a space in an organization
* Your API specification in OpenAPI format (JSON or YAML)
* A basic understanding of your API structure

### Step 1: Upload your OpenAPI specification

1. Navigate to your GitBook organization
2. Click the **OpenAPI** section in the sidebar
3. Click **Add specification**
4. Choose one of these upload methods:
   * **Direct upload**: Upload your OpenAPI specification file
   * **URL import**: Provide a public URL to your specification
   * **CLI**: Use the CLI to publish your OpenAPI spec to GitBook

### Step 2: Insert your API reference into your docs

{% hint style="info" %}
The rest of this guide assumes you already have a docs site in GitBook to add content to. Head to our [guide on creating documentation](../editing-and-publishing-documentation/complete-guide-to-publishing-docs-gitbook.md) in GitBook to get started.
{% endhint %}

#### **Once your specification is uploaded, you can add it to your documentation:**

1. Go to the space where you want to insert your API reference
2. Click the **+ Add new...** button at the bottom of the table of contents
3. Select **Open API reference** from the list
4. Choose your API specification

#### To insert specific endpoints to an existing page:

1. Insert an API block by pressing <kbd>/</kbd> or clicking the + button on an empty block and choosing **OpenAPI**
2. Select your API specification
3. Choose **Select endpoints**
4. Pick the specific operations you want to include

After adding your specification, GitBook will automatically generate a full API reference for your endpoints described in your OpenAPI spec.

Make sure to publish your site or merge the change request you’re working in to see your changes live on your GitBook site.

### Step 3: Structure your API reference

{% hint style="warning" %}
With GitBook, you can customize your API reference through different options in your OpenAPI spec. You can learn more about the OpenAPI specification [here](https://swagger.io/specification/).
{% endhint %}

GitBook does more than just render your OpenAPI spec. It lets you customize your API reference for better clarity, navigation, and branding.

You can customize many things in your API reference, from the page titles, descriptions and icons, to the organization and grouping of your endpoints, to the code samples you display.

{% stepper %}
{% step %}
#### Add tags to your OpenAPI spec

You can organize your endpoints by adding a set of tags at the top level of your OpenAPI spec.

```yaml
tags:
  - name: pet
  - name: store
  - name: user
```

Adding a list of tags will allow you to describe the pages and order of your API. The example above creates three pages you can add endpoints to, called “Pet”, “Store”, and “User”.

The order of pages in GitBook matches the order of tags in your OpenAPI tags array.
{% endstep %}

{% step %}
#### Add page titles, icons, and descriptions

After defining your tags, you can customize them further by adding titles, icons, and descriptions

```yaml
tags:
  - name: pet
    x-page-title: Pet
    x-page-icon: paw
    x-page-description: A collection of API endpoints for pets
    description: Description at the top of the Pet page.
  - name: store
    x-page-title: store
    x-page-icon: store
    x-page-description: A collection of API endpoints for the store
    description: Description at the top of the Store page.
  - name: user
    x-page-title: Users
    x-page-icon: user
    x-page-description: A collection of API endpoints for users
    description: Description at the top of the Users page.
```

The `x-page-title`, `x-page-icon`, and `x-page-description` describe the title, icon, and description used in the GitBook page respectively.

`description` allows you to add content to the top of the page, before the API endpoints show.
{% endstep %}

{% step %}
#### Add your endpoints to your pages

After creating your pages through the tags you set, you can start adding your tags to your endpoints.

```yaml
paths:
  /pet:
    put:
      tags:
        - pet
      summary: Update an existing pet.
      description: Update an existing pet by Id.
```

The operation above will be added to the page we defined earlier in step 1. You can repeat this step to start organizing your endpoints however you like.
{% endstep %}

{% step %}
#### Group your pages together

If you’d like to group multiple pages together, you can use `x-parent` in tags to define hierarchy:

```yaml
tags:
  - name: business
  - name: pet
    x-parent: business
  - name: store
    x-parent: business
```

The above example will create a table of contents that looks like this:

```
Business
├── Pet
└── Store
```

If a top level page has no description or content, GitBook will automatically show a card-based layout for the sub-pages within.
{% endstep %}
{% endstepper %}

### Step 4: Enhance your API endpoints

After setting up the structure of your API documentation, you can continue to add extra functionality and information to your endpoints to make them easier to understand or use.

#### Build richer descriptions with GitBook blocks

Tag description fields support GitBook [Markdown](https://gitbook.com/docs/creating-content/formatting/markdown), including advanced [blocks](https://gitbook.com/docs/creating-content/blocks) like tabs:

```yaml
tags:
  - name: pet
    description: |
      Here is the detail of pets.

      
{% tabs %}
      {% tab title="Dog" %}
      Here are the dogs
      {% endtab %}

      {% tab title="Cat" %}
      Here are the cats
      {% endtab %}

      {% tab title="Rabbit" %}
      Here are the rabbits
      {% endtab %}
      {% endtabs %}
```

Adding this Markdown to your operation’s description will add a tab block to the description in your endpoint in GitBook.

#### Add custom code samples

You can also add custom code samples directly in your OpenAPI specification. You can use `x-code-samples` to add language specific code samples that render in your API methods.

```yaml
paths:
  /users:
    get:
      summary: List Users
      operationId: listUsers
      x-code-samples:
        - lang: JavaScript
          source: |
            fetch('https://api.example.com/users')
              .then(response => response.json())
              .then(data => console.log(data));
        - lang: Python
          source: |
            import requests
            response = requests.get('https://api.example.com/users')
            data = response.json()
            print(data)
```

### Step 5: Test your endpoints

After your endpoints are configured and structured, you and your users are ready to test your endpoints — right from your own docs!

Any endpoints added to GitBook through your OpenAPI reference are automatically added with a “Test it” button, which lets you and your users send test requests right from your docs.

You can customize parameters, add authentication tokens, and much more. Make sure you publish your docs and test out your API to make sure everything looks and is working correctly!

Want to see an example? Head to our own developer docs to see [GitBook’s own API](https://gitbook.com/docs/developers/gitbook-api/api-reference) in action. You can also take a look at how we’ve structured [our own OpenAPI spec](https://api.gitbook.com/openapi.json) to learn more about structuring an OpenAPI spec at scale.

### Wrapping up

Now that you’ve got your API documentation up and running, it’s important to keep things consistent — consistency is key!

Check our guide on [the seven principles of great API documentation](api-documentation-principles.md) — it’s a great reference as your API continues to grow. And if you’re curious to learn more about OpenAPI and how to build better docs in GitBook, make sure you head to our own [documentation](https://gitbook.com/docs/api-references/openapi) to learn more about OpenAPI and GitBook.
