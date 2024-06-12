# Content configuration

If you’d like to configure GitSync further, you can add a `.gitbook.yaml` file at the root of your repository to tell GitBook how to parse your Git repository.

Here’s an example:

{% tabs %}
{% tab title=".gitbook.yaml" %}
```yaml
root: ./

​structure:
  readme: README.md
  summary: SUMMARY.md​

redirects:
  previous/page: new-folder/page.md
```
{% endtab %}
{% endtabs %}

## Root

The path to lookup for your documentation defaults to the root directory of the repository. Here’s how you can tell GitBook to look into a `./docs` folder:

{% tabs %}
{% tab title=".gitbook.yaml" %}
```yaml
root: ./docs/
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**All other options that specify paths will be relative to this root folder**. So if you define root as `./docs/` and then `structure.summary` as `./product/SUMMARY.md`, GitBook will actually look for a file in `./docs/product/SUMMARY.md`.‌
{% endhint %}

## ​Structure‌ <a href="#structure" id="structure"></a>

The structure accepts two properties:‌

* **`readme`**: Your documentation’s first page. Its default value is `./README.md`
* **`summary`**: Your documentation’s table of content. Its default value is `./SUMMARY.md`

The value of those properties is a path to the corresponding files. The path is relative to the “root” option. For example, here’s how you can tell GitBook to look into a `./product` folder for the first page and summary:

{% tabs %}
{% tab title=".gitbook.yaml" %}
```yaml
structure:
  readme: ./product/README.md
  summary: ./product/SUMMARY.md
```
{% endtab %}
{% endtabs %}

#### ​Summary‌ <a href="#summary" id="summary"></a>

The `summary` file is a Markdown file (`.md`) that should have the following structure:

```
‌# Summary​

## Use headings to create page groups like this one​

* [First page’s title](page1/README.md)
    * [Some child page](page1/page1-1.md)
    * [Some other child page](part1/page1-2.md)

* [Second page’s title](page2/README.md)
    * [Some child page](page2/page2-1.md)
    * [Some other child page](part2/page2-2.md)

## A second-page group​

* [Yet another page](another-page.md)
```

Providing a custom summary file is optional. By default, GitBook will look for a file named `SUMMARY.md` in your `root` folder if specified in your config file, or at the root of the repository otherwise.

If you don’t specify a summary, and GitBook does not find a `SUMMARY.md` file at the root of your docs, GitBook will infer the table of contents from the folder structure and the Markdown files below.‌

{% hint style="info" %}
The summary markdown file is **a mirror of the** [**table of contents**](https://docs.gitbook.com/getting-started/overview#table-of-contents) of your GitBook space. So even when no summary file is provided during an initial import, GitBook will create one and/or update it whenever you update your content using the GitBook editor.

Because of this, it’s not possible to reference the same Markdown file twice in your `SUMMARY.md` file, because this would imply that a single page lives at two different URLs in your GitBook space.
{% endhint %}

## ​Redirects <a href="#redirects" id="redirects"></a>

Redirects are commonly used when you are migrating your documentation from one provider to another — like when you just moved your docs to GitBook. Broken links can impact your SEO so we recommend setting up redirects where needed.

#### Restructuring your content in GitBook

When moving your content within GitBook, most URLs should work as expected depending on complexity of the change. There are a number of tools that will allow you to verify which links were broken, if any.

{% hint style="warning" %}
With Git, when a file is moved many times, the file is removed and a new one is created. This makes it impossible for GitBook to know that a folder has been renamed, for example. Make sure to double-check and add redirects where needed.
{% endhint %}

### How to create a redirect

You can create custom redirects of a URL to a page by specifying the path to the corresponding file. The path is relative to the “root” option. For example, here’s how you can tell GitBook to redirect users accessing a past url `/help` to a new url `/support`

{% code title=".gitbook.yaml" %}
```yaml
root: ./

redirects:
  help: support.md
```
{% endcode %}

#### How to redirect on a more complex path:

Original URL: `https://docs.company.com/help` which has now moved to `https://docs.company.com/misc/support` on GitBook.

{% code title=".gitbook.yaml" %}
```yaml
root: ./

redirects:
  help: misc/support.md
```
{% endcode %}

{% hint style="danger" %}
The path `misc/support.md` needs to be a real existing path within the repository. It needs to be relative to the current `root` setting in`.gitbook.yaml`.\
Please don’t add any leading slashes. For example, `./misc/support.md` will not work.
{% endhint %}

### Troubleshooting

The YAML file needs to be correctly formatted for the redirects to work. Errors such as incorrect indentation or whitespace can result in your redirects not working. [Validating your YAML file](https://www.yamllint.com/) can ensure that the redirects will work smoothly.

It's also important to consider that as long as a page exists for a path, GitBook won’t be looking for a possible redirect. So if you're setting up a redirect for an old page to a new one, you will need to remove the old page in order for the redirect to work.
