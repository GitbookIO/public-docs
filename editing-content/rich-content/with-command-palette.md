# Block-level content

## Headings <a href="headings" id="headings"></a>

GitBook offers 3 levels of headings, [which should be enough to properly structure your content](https://practicaltypography.com/headings.html). Headings structure your documents. Heading levels 1 and 2 will appear in the outline on the right.

All headings have anchor links, which are links that you can use to point to a particular section of your documentation.

You can see the anchors of a title when your content is in a reading mode. If you want to add an anchor to some text, just add a [relative link](../rich-text.md#relative-links).

{% hint style="info" %}
**Good to know:** Reading on a screen is less comfortable than reading on paper. Make sure your content is not too long with too many titles. Sometimes splitting your content into different pages creates a better overview! 🤓
{% endhint %}

## Lists <a href="lists" id="lists"></a>

You can add bullet lists, numbered lists and task lists to your content:‌

* This is a bullet list.
  * You can use `Tab` to indent…
* …and `Shift+Tab` to outdent.

1. A number list comes in handy when trying to prioritize.
   1. You can use `Tab` to indent…
2. and `Shift+Tab` to outdent.

* [ ] Here's a task that hasn't been done
  * [x] And here's a subtask that has been done, indented using `Tab`.
  * [ ] Aaaaand, here's a subtask that hasn't been done.

## Code blocks <a href="code-blocks" id="code-blocks"></a>

You can insert some code on GitBook by using **code blocks**. Each code block can have a language set, and syntax highlighting will be applied automatically based on this language.

{% code title="index.js" %}
```javascript
‌import * as React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, window.document.getElementById('root'));
```
{% endcode %}

## Quote <a href="quote" id="quote"></a>

> Hello world!

## Image block <a href="quote" id="quote"></a>

The most common type of images is an "image block". They are full-width images containing a caption. You can center or align them to the left. You can insert them like this:

Image blocks can display a gallery of images.

![Each image](https://images.unsplash.com/photo-1544716278-ca5e3f4abd8c?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw1fHxib29rfGVufDB8fHx8MTYyODc1MTk5MA\&ixlib=rb-1.2.1\&q=85) ![can have its](https://images.unsplash.com/photo-1589998059171-988d887df646?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw5fHxib29rfGVufDB8fHx8MTYyODc1MTk5MA\&ixlib=rb-1.2.1\&q=85) ![own caption](https://images.unsplash.com/photo-1524995997946-a1c2e315a42f?crop=entropy\&cs=srgb\&fm=jpg\&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw2fHxib29rc3xlbnwwfHx8fDE2Mjg3NTIwNzY\&ixlib=rb-1.2.1\&q=85)

## Tables <a href="tables" id="tables"></a>

You can add tables to better organize your information.

<table><thead><tr><th>Company</th><th data-type="select">Status</th><th>Contact</th><th>MRR</th></tr></thead><tbody><tr><td><strong>Ace AI</strong> – Design</td><td></td><td><a href="mailto:noreply@gitbook.com">rena@ace.ai</a></td><td>$420</td></tr><tr><td><strong>Discrete Data</strong> – API</td><td></td><td><a href="mailto:noreply@gitbook.com">dave@dd.inc</a></td><td>$69</td></tr></tbody></table>

Table columns can have the following data types, which apply restrictions or embellishments to every cell in the column:

* **Text**: standard text. Can be formatted.
* **Number:** a number, with or without floating digits.
* **Checkbox:** a checkbox that can be checked or unchecked.
* **Select:** data can be selected from a pre-defined list of options. Can be single-choice or multiple-choice.
* **Users:** data can be selected from a list of the organization's members. Can be single-choice or multiple-choice.
* **Files:** data is a reference to a file in the space. New files can be uploaded when populating cells in the column.
* **Rating:** A star rating, with a configurable maximum.

### Changing a column type

You can use the column dropdown menu to change a column's type. Select the new type and hit save. You'll be prompted to confirm this change, as column data could be deleted or malformed by this action.

### Resizing columns

You can drag from a column's edge to resize it. Column resizing is stored as a percentage of the overall width, which allows for relative sizing based on the overall width of the table.

### Scrolling tables

Tables that are wider than the editor container will be horizontally scrollable.

{% hint style="info" %}
**Good to know:** You can drag and drop columns and rows to reorder them, and delete columns or rows using their respective context menus.
{% endhint %}

## Hints & Callouts <a href="hints-and-callouts" id="hints-and-callouts"></a>

Hints are a great way to bring the reader's attention to specific elements in your documentation. Hints can be inserted in the UI, or [when running the GitHub sync in the markdown file](../markdown.md#hints-and-callouts).‌

There are 4 different types of hints, you have already seen some of them in this documentation.

{% hint style="info" %}
**Info hints** are great for showing general information, or providing tips and tricks.
{% endhint %}

{% hint style="success" %}
**Success hints** are good for showing positive actions or achievements.
{% endhint %}

{% hint style="warning" %}
**Warning hints** are good for showing important information or non-critical warnings.
{% endhint %}

{% hint style="danger" %}
**Danger hints** are good for highlighting destructive actions or raising attention to critical information.
{% endhint %}

## Page link <a href="page-link" id="page-link"></a>

A page link is the best way to create relations between different pages.

{% content-ref url="../markdown.md" %}
[markdown.md](../markdown.md)
{% endcontent-ref %}

## API Methods & OpenAPI Integration <a href="api-methods" id="api-methods"></a>

An API Method block is used to manually document an HTTP API endpoint.

{% swagger method="get" path="/user" baseUrl="https://api.example.com/v1" summary="Get a user" %}
{% swagger-description %}
Use this method to get information about a user
{% endswagger-description %}
{% endswagger %}

You can also sync with an OpenAPI or Swagger file or URL to include auto-generated methods in your documentation.

{% swagger src="https://petstore.swagger.io/v2/swagger.json" path="undefined" method="undefined" %}
[https://petstore.swagger.io/v2/swagger.json](https://petstore.swagger.io/v2/swagger.json)
{% endswagger %}

## Tabs

Tabs are also a good way to structure your content. Here is an example that lists instructions relevant to specific platforms:

{% tabs %}
{% tab title="Windows" %}
Here are the instructions concerning Windows
{% endtab %}

{% tab title="OSX" %}
Here are the instructions concerning OSX
{% endtab %}

{% tab title="Linux" %}
Here are the instructions concerning Linux
{% endtab %}
{% endtabs %}

## Equations and formulae

Math & Tex blocks support displaying mathematical formulae in the [MathTex format](https://katex.org)

$$
s = \sqrt{\frac{1}{N-1} \sum_{i=1}^N (x_i - \overline{x})^2}
$$

## Files

{% file src="../../.gitbook/assets/hello-world.pdf" %}
Hello world
{% endfile %}
