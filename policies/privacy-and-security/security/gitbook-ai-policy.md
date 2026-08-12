---
description: How GitBook processes data for AI features.
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# GitBook AI Policy

## Overview

GitBook uses AI across the product. Features include AI Search, GitBook Assistant, editor writing tools, and AI Insights.

This policy explains data handling, providers, and available controls.

Our core commitments are:

* GitBook never uses customer content to train its models or third-party models.
* Organization admins can disable AI features at the site level.
* GitBook applies the same security and privacy standards to AI processing.

## AI providers and data processing

### Providers

GitBook uses OpenAI’s enterprise API for AI features. OpenAI does not train, improve, or fine-tune models with customer data sent through this API.

OpenAI is a [subprocessor](subprocessors.md).

### Zero data retention

Zero data retention coverage varies by endpoint:

* GitBook runs the content-scrubbing pipeline with `store=false`. It removes sensitive data before further AI processing.
* GitBook Agent and Channels use `store=true`. These endpoints do not have zero data retention coverage.

GitBook enables zero data retention per endpoint. It does not use one formal OpenAI agreement.

## How data flows through AI features

### GitBook Assistant on published sites

When a visitor asks GitBook Assistant a question:

1. The browser sends the question to GitBook’s backend.
2. GitBook retrieves relevant indexed site content for context.
3. GitBook sends the question and context to OpenAI.
4. GitBook streams the response to the visitor’s browser.

GitBook stores the question, response, sources, and metadata for AI Insights. Metadata includes the model ID, session identifiers, and timestamp.

GitBook does not include visitor personal data beyond the submitted question.

### AI Search

GitBook uses OpenAI and Turbopuffer for AI Search. When GitBook indexes content, it sends documentation pages to OpenAI in large chunks. A chunk can contain a full page.

OpenAI creates vector embeddings. GitBook stores the embeddings in Turbopuffer, a third-party vector database.

When someone searches, GitBook sends their query to OpenAI for embedding. GitBook sends the resulting vector to Turbopuffer for similarity matching.

OpenAI creates embeddings only. Turbopuffer performs all similarity matching.

### AI writing features and GitBook Agent

Editor writing features send selected content and surrounding page context to OpenAI. These features include rewriting, summarization, and translation.

GitBook Agent receives tools for searching, reading, and editing pages. It independently selects the tools needed to fulfill a request.

During a session, GitBook Agent can access content within the current site or space. Existing permissions control access beyond the current site or space. GitBook Agent cannot access content unavailable to the requester.

### Content indexing

GitBook indexes published documentation for AI Search and GitBook Assistant. GitBook sends page content chunks to OpenAI’s embeddings API.

OpenAI converts the content into vector embeddings. GitBook stores the embeddings in Turbopuffer.

GitBook routes embedding requests through Cloudflare AI Gateway. Cloudflare caches embedding results for performance and cost efficiency. This caching can retain page content chunks.

OpenAI handles input retention as described in [Zero data retention](gitbook-ai-policy.md#zero-data-retention). Cloudflare does not link cached data to an organization.

### Open in ChatGPT or Claude

The “Open in ChatGPT / Claude” action sends the current page directly to ChatGPT or Claude. The visitor’s account settings govern this transfer.

This action does not use GitBook’s OpenAI enterprise agreement. GitBook’s zero-retention, retention, and no-training terms do not apply.

## Data retention and logging

### Data GitBook stores

| Data type                                                             | Purpose                         | Retention                                              |
| --------------------------------------------------------------------- | ------------------------------- | ------------------------------------------------------ |
| Question text and AI-generated response                               | AI Insights analytics           | Indefinite                                             |
| Response ID, model ID, and sources                                    | AI Insights analytics           | Indefinite                                             |
| Session and visitor identifiers                                       | AI Insights analytics           | Indefinite                                             |
| Operational metadata, including token usage, service tier, and errors | Operational monitoring          | Indefinite                                             |
| Vector embeddings of published content                                | AI Search and GitBook Assistant | Updated on publish and deleted when content is removed |

GitBook does not store visitor IP addresses with AI interaction records.

## AI security protections

### Input handling

GitBook sends user inputs to the AI provider as entered. GitBook does not filter or redact queries before they reach the LLM.

External connector content, such as Intercom content, is an exception. GitBook runs that content through the content-scrubbing pipeline before it reaches the LLM.

Published-site AI features include site content in LLM context. Organizations that publish sensitive or access-restricted content can consider this before enabling AI features.

### Infrastructure

GitBook encrypts all communication with OpenAI using TLS. GitBook securely stores AI provider API keys and rotates them regularly.

GitBook’s SOC 2 Type II certification and GDPR compliance cover AI processing.

## Customer controls

### Disabling AI features

GitBook offers two control levels:

* **Organization level:** Organization admins can turn off **Enable GitBook AI** in organization settings. This disables AI writing and editing tools and **Ask AI** for every organization member.
* **Site level:** Site owners can separately enable or disable AI Search and GitBook Assistant in site settings.

When you disable AI features, GitBook does not send that site’s content to AI providers.

### Open in ChatGPT or Claude

Site owners can disable the “Open in ChatGPT / Claude” action. To configure it, select **Site customization** → **Page actions** → **Open in AI providers**.

Turning off **Page actions** removes this action. It also disables the MCP server at `~gitbook/mcp`.

To keep MCP available, leave **Page actions** enabled. Then disable only **Open in AI providers**.

See [Open in ChatGPT or Claude](gitbook-ai-policy.md#open-in-chatgpt-or-claude) for data handling details.

## Compliance and legal

### GDPR

GitBook’s [Data Processing Agreement](../statement/#dpa) covers AI data processing. OpenAI processes visitor queries as a subprocessor.

GitBook’s DPA and standard contractual clauses cover this transfer.

### No training commitment

GitBook does not use customer data to train AI or machine learning models. GitBook will not do so without prior written consent.

This commitment covers all GitBook content. It includes documentation, API specifications, and internal knowledge bases. It applies whether AI features are enabled or disabled.

### Related policies

* [Subprocessors](subprocessors.md)
* [Terms of Service](../../terms.md)
* [Privacy Statement](../statement/)
* [Data Processing Agreement](../statement/#dpa)
* [Security FAQ](security-faq.md)
