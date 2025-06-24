---
description: Configure Git Sync with extra functionalities
---

# Content configuration

If you’d like to configure Git Sync further, you can add a `.gitbook.yaml` file at the root of your repository to tell GitBook how to parse your Git repository.

{% code title=".gitbook.yaml" %}
```yaml
root: ./

​structure:
  readme: README.md
  summary: SUMMARY.md​

redirects:
  previous/page: new-folder/page.md
```
{% endcode %}

### Root

The path to lookup for your documentation defaults to the root directory of the repository. Here’s how you can tell GitBook to look into a `./docs` folder:

{% code title=".gitbook.yaml" %}
```yaml
root: ./docs/
```
{% endcode %}

{% hint style="warning" %}
**All other options that specify paths will be relative to this root folder**. So if you define root as `./docs/` and then `structure.summary` as `./product/SUMMARY.md`, GitBook will actually look for a file in `./docs/product/SUMMARY.md`.‌
{% endhint %}

### ​Structure‌ <a href="#structure" id="structure"></a>

The structure accepts two properties:‌

* **`readme`**: Your documentation’s first page. Its default value is `./README.md`
* **`summary`**: Your documentation’s table of contents. Its default value is `./SUMMARY.md`

The value of those properties is a path to the corresponding files. The path is relative to the “root” option. For example, here’s how you can tell GitBook to look into a `./product` folder for the first page and summary:

{% code title=".gitbook.yaml" %}
```yaml
structure:
  readme: ./product/README.md
  summary: ./product/SUMMARY.md
```
{% endcode %}

{% hint style="warning" %}
When Git Sync is enabled, **remember not to create or modify readme files** through GitBook's UI. The readme file should be managed exclusively in your GitHub/GitLab repository to avoid conflicts and duplication issues.
{% endhint %}

### Summary‌ <a href="#summary" id="summary"></a>

The `summary` file is a Markdown file (`.md`) that should have the following structure:

{% code title="./SUMMARY.md" %}
```markdown
‌# Summary​

## Use headings to create page groups like this one​

* [First page’s title](page1/README.md)
    * [Some child page](page1/page1-1.md)
    * [Some other child page](part1/page1-2.md)

* [Second page’s title](page2/README.md)
    * [Some child page](page2/page2-1.md)
    * [Some other child page](part2/page2-2.md)

## A second-page group​

* [Another page](another-page.md)
```
{% endcode %}

Providing a custom summary file is optional. By default, GitBook will look for a file named `SUMMARY.md` in your `root` folder if specified in your config file, or at the root of the repository otherwise.

If you don’t specify a summary, and GitBook does not find a `SUMMARY.md` file at the root of your docs, GitBook will infer the table of contents from the folder structure and the Markdown files below.‌

{% hint style="info" %}
The summary markdown file is **a mirror of the** **table of contents** of your GitBook space. So even when no summary file is provided during an initial import, GitBook will create one and/or update it whenever you update your content using the GitBook editor.

Because of this, it’s not possible to reference the same Markdown file twice in your `SUMMARY.md` file, because this would imply that a single page lives at two different URLs in your GitBook space.
{% endhint %}

### ​Redirects <a href="#redirects" id="redirects"></a>

Redirects allow you to define redirects in your `.gitbook.yaml` configuration file. The path is relative to the “root” option. For example, here’s how you can tell GitBook to redirect users accessing a past url `/help` to a new url `/support`

{% code title=".gitbook.yaml" %}
```yaml
root: ./

redirects:
  help: support.md
```
{% endcode %}

{% hint style="info" %}
Redirects you define in a space’s configuration file are scoped to the corresponding space. We recommend creating [site redirects](../../publishing-documentation/site-redirects.md) for most cases as they apply to the whole site, across spaces.
{% endhint %}

#### Restructuring your content in GitBook

When moving your content within GitBook, most URLs should work as expected depending on complexity of the change. You can use our Broken Links feature to scan your space to find which links are broken, if any.

{% hint style="warning" %}
With Git, when a file is moved many times, the file is removed and a new one is created. This makes it impossible for GitBook to know that a folder has been renamed, for example. Make sure to double-check and add redirects where needed.
{% endhint %}

### Troubleshooting

The YAML file needs to be correctly formatted for the redirects to work. Errors such as incorrect indentation or whitespace can result in your redirects not working. [Validating your YAML file](https://www.yamllint.com/) can ensure that the redirects will work smoothly.

When setting redirects, do not add any leading slashes. For example, trying to redirect to `./misc/support.md` will not work.

It's also important to consider that as long as a page exists for a path, GitBook won’t be looking for a possible redirect. So if you're setting up a redirect for an old page to a new one, you will need to remove the old page in order for the redirect to work.

When Git Sync is enabled, readme files should never be created through GitBook's UI. The README file should be managed exclusively in your GitHub/GitLab repository to avoid conflicts and duplication issues.

