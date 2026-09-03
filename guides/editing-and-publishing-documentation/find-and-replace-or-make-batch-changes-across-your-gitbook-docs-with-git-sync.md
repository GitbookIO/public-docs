---
description: Find, replace, and update content across your GitBook docs with GitBook Agent
---

# Updating docs in bulk with GitBook Agent

{% hint style="warning" %}
#### GitBook now supports find & replace through GitBook Agent

Head to [GitBook Agent](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/gitbook-agent) to learn more about using GitBook Agent to edit pages in bulk.
{% endhint %}

GitBook Agent can find and replace content across your documentation. It can also make broader, targeted updates in a change request.

Use GitBook Agent for routine bulk edits. It keeps changes together for review before you merge them.

### Start a bulk update

To make a bulk update:

1. In your space, click the GitBook Agent icon next to **Edit**.
2. Describe the change, the pages it affects, and any exclusions.
3. Click **Start change request**.
4. In **Changes**, review every proposed edit.
5. Merge the change request when the updates are correct.

### Write a focused prompt

If you want to make targeted changes to your documentation — such as a ‘find and replace’ process for an outdated or incorrect term — you can use a focused prompt.&#x20;

Be sure to include these details in your prompt:

* The text or content you want to change.
* The replacement or intended outcome.
* Any pages to include and content to exclude.

Here’s an simple example prompt you could copy and customize:

{% prompt description="Find an replace content" %}
```markdown
Find all instances of “Gitbook” and replace them with “GitBook.” Ignore code blocks and URLs. Tell me how many replacements you make.
```
{% endprompt %}

For larger changes, it’s a good idea to also state the goal and constraints. If there are pages pages that define the correct wording or structure, reference them in the prompt to point the Agent in the right direction.

### Review bulk edits

GitBook Agent will make the updates in a change request. Be sure to review the change request and the diff before merging.

Pay particular attention to the following:

* Each replacement has the intended meaning.
* Links, formatting, and page structure remain correct.
* The change request excludes content outside the requested scope.

### FAQ

<details>

<summary>Can I still use Git Sync for bulk updates?</summary>

Yes. Git Sync creates a bidirectional connection with a GitHub or GitLab repository. Use it when your documentation follows a docs-as-code or CI/CD workflow, or you want to use a different AI agent (e.g. ChatGPT, Codex, Claude etc) to make changes to your documentation.

Create a branch, commit the changes, open a pull or merge request, and merge after review.

</details>

<details>

<summary>Can GitBook Agent exclude some matches?</summary>

Yes. Name the pages to include and content to exclude. For example, tell GitBook Agent to ignore code blocks, URLs, or a specific page.

</details>
