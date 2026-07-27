---
description: "Everyday things to do with GitBook from your agent: create sites, draft content, restructure docs."
---

# Common workflows

Once your client is connected, here are a few concrete prompts to get you started.

{% prompt description="Create and configure a new docs site." %}
```markdown
Using the GitBook MCP tools, create a new docs site for me.

1. List my organizations and confirm which one to use before creating anything.
2. Ask what the site is for and what content I have (folder, repo, or just a description). If I point you at a source, echo back what you find there so I can confirm it's right.
3. Show me a short plan — site name, spaces, page structure — and wait for my yes.
4. Create the site, add the content, and publish. Then fetch the live URL to confirm it works and share it with me.
```
{% endprompt %}

{% prompt description="Open a change request and draft content." %}
```markdown
Using the GitBook MCP tools, draft new content for my docs in a change request — don't edit anything live.

1. List my organizations and sites, and confirm which space to work in.
2. Ask me what the content should cover, then open a change request and draft the pages inside it.
3. Match the tone and structure of my existing pages — read a few first.
4. When done, share the change request preview link so I can review and merge it in GitBook.
```
{% endprompt %}

{% prompt description="Move, rename, or restructure pages across a site." %}
```markdown
Using the GitBook MCP tools, help me restructure my docs site.

1. List my organizations and sites, confirm which one, then fetch its current structure and show it to me.
2. Ask what I want changed, then propose the new structure as a simple before/after tree — don't move anything until I approve.
3. Apply the changes, keeping URLs and internal links intact where possible; flag anything that will break.
4. Show me the final structure and the change request or live result to verify.
```
{% endprompt %}

Looking for the exact tool names and parameters behind these prompts? See [MCP tools reference](mcp-tools-reference.md).
