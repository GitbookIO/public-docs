---
description: Add a column to create different layouts in your documentation.
---

# Columns

Columns are a great way to create different layouts for your documentation. You can add many different types of blocks inside a column, and adjust the width of each side to customize it to the design you need.

{% columns %}
{% column width="50%" %}
### Create a seamless experience between your docs and product

Integrate your documentation right into your product experience, or give users a personalized experience that gives them what they need faster.

<a href="https://www.gitbook.com/#alpha-waitlist" class="button primary">Learn more</a>
{% endcolumn %}

{% column %}
<figure><img src="../../.gitbook/assets/columns.png" alt="An image of GitBook icons demonstrating side by side column functionality"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## Representation in Markdown

<pre class="language-markdown" data-overflow="wrap"><code class="lang-markdown"><strong>## Example
</strong><strong>
</strong>{% columns %}
{% column width="50%" %}
### Create a seamless experience between your docs and product

Integrate your documentation right into your product experience, or give users a personalized experience that gives them what they need faster.

&#x3C;a href="https://www.gitbook.com/#alpha-waitlist" class="button primary">Learn more&#x3C;/a>
{% endcolumn %}

{% column %}
&#x3C;figure>&#x3C;img src="../../.gitbook/assets/GitBook vision post.png" alt="An image of GitBook icons demonstrating side by side column functionality">&#x3C;figcaption>&#x3C;/figcaption>&#x3C;/figure>
{% endcolumn %}
{% endcolumns %}
</code></pre>
