---
icon: server
---

# MCP servers for published docs

Every published GitBook site automatically includes a Model Context Protocol (MCP) server.&#x20;

This allows AI assistants to access your documentation content directly, making it easy for tools like Claude Desktop, Cursor, and VS Code extensions to answer questions using your docs.

The MCP server is available at your site’s URL with `/~gitbook/mcp` appended. For example, GitBook’s docs are located at `https://gitbook.com/docs`, so the MCP server is at `https://gitbook.com/docs/~gitbook/mcp`.

{% hint style="info" %}
Visiting this URL in your browser will result in an error. Instead, you can share this with tools that can make HTTP requests, like LLMs or IDEs.
{% endhint %}

### Connecting an AI assistant

{% stepper %}
{% step %}
#### Find your MCP server URL

Take your published GitBook site URL and add `/~gitbook/mcp` to the end.
{% endstep %}

{% step %}
#### Configure your AI tool

Add the MCP server URL to your AI assistant’s settings. Each tool has a slightly different setup process, so you should check out the docs for your tool of choice to see how to configure an MCP server for it.
{% endstep %}

{% step %}
#### Start using your docs

Once connected, your AI assistant can search through your documentation, retrieve specific pages, and answer questions using your content. The assistant will have real-time access to your published documentation.
{% endstep %}
{% endstepper %}

### Requirements

Your GitBook site must be published for the MCP server to work. The server only provides access to published content, never drafts or unpublished changes.

Your AI tool needs to support the Model Context Protocol and be able to make HTTP requests to your site. Most modern AI assistants that support MCP will work with GitBook’s servers.

The MCP server respects your site’s visibility settings. If your site is public, the MCP server is publicly accessible. If your site requires authentication, the MCP server will too.

### Enable or disable easy MCP linking

In the **Page actions** section of your [Customization](customization/) settings, you can enable the **Connect with MCP server** option. This enables visitors to your docs site to quickly copy a link to your site's MCP server right from [the Page actions menu](customization/extra-configuration.md#page-actions).

### Privacy and access

The MCP server only provides read-only access to your published documentation. It doesn’t expose any user data, analytics, or internal GitBook information.

Only the latest published version of your content is available through the MCP server. Draft content and unpublished changes remain private until you publish them.

### Common issues

If your AI assistant can’t connect to your MCP server, first check that your GitBook site is published and accessible. The URL should respond when you visit it in a browser.

Make sure you’re using the correct URL format with `/~gitbook/mcp` at the end. The URL should match exactly what you see when you visit your published site.

Some AI tools require specific transport methods or have particular MCP configuration requirements. Check your AI tool’s documentation for MCP setup instructions.

