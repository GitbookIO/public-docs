---
description: "The Code block: what it does and how to use it."
---

# Code block

Add code to a page with a code block — useful for sharing configurations, code snippets, code files, command-line usage examples, API call examples, and more.

### Add a code block

1. Place your cursor on an empty line and type `/`.
2. Select **Code block** from the insert menu.
3. GitBook inserts the block, cursor ready, so you can paste or type code.

Combine a code block with a [tabs block](tabs.md) to show the same example in multiple languages.

### Code block options

Open the block's Options menu (or its Actions menu) to configure:

* **Set syntax…** — highlight in any supported language. GitBook uses [Prism](https://github.com/PrismJS/prism) for highlighting — check [Test Drive Prism](https://prismjs.com/test.html#language=markup) for supported languages; if GitBook and Prism differ, GitBook might be a version or two behind.
* **With line numbers** — useful when the code represents a whole file, or is long; hide them for short snippets or CLI usage.
* **With caption** — a caption above the code, often a filename, but usable as a title or description.
* **Wrap code** — wraps long lines so they're all visible without horizontal scrolling; pair with line numbers to keep new lines easy to spot.
* **Expandable** — collapses the block to 10 lines with an expand button, if it has more than 10 lines.

### Code block actions

**Copy the code** — hover the block and click the middle icon that appears to copy its contents to your clipboard.

### Representation in Markdown

````markdown
{% code title="index.js" overflow="wrap" lineNumbers="true" %}
```javascript
import * as React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, window.document.getElementById('root'));
```
{% endcode %}
````
