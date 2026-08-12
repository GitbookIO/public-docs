---
description: "Discover how you can use AI tools to improve your docs workflow —\_including its limitations and how to overcome them"
---

# Introducing AI into your product documentation workflow

Product documentation may seem like the ideal job for AI tools such as large language models (LLMs). But if you’ve already tried to write docs using ChatGPT, Claude, or one of the other LLMs then you’ll know that results can be mixed, at best.

But even if AI-based tools can’t write your technical documentation or user manual from scratch, there are several ways you can create an AI product docs workflow today. In this article, we’re going to look at where LLM-based AI tools can help you to create and improve your product documentation, suggest ways to introduce AI into your git documentation process, and flag up some areas where you’ll need to be extra cautious.

### AI tools and documentation today <a href="#ai-tools-and-documentation-today" id="ai-tools-and-documentation-today"></a>

So, while this isn’t a complete guide on how to write user manuals with AI, let’s explore what large language models (LLMs) can currently offer us as documentation writers:

* **Outline and provide a first draft** – Facing a blank page or an empty Markdown file can be daunting. It’s not unusual for editing to feel easier than drafting. With the right prompts, an LLM-based tool can help you jump past that tricky first step by giving you a basic outline for your user manual or technical documentation. Then you can use your skills as a writer and editor to create a real first draft.
* **Create templates** – Similarly, LLMs are great at creating reusable templates. For example, you can ask an AI tool to review examples from your existing product documentation and then create a template based on that analysis. Or create an entirely new template with a rough description of what you need, then refine until it’s right.
* **Extract useful information from internal docs** – In most teams, you’ll have access to commit messages, process documentation, release notes, technical specs, and similar materials that can act as inputs to your product documentation. Although LLM-based tools will struggle to turn those into a coherent learning pathway, they can help you find common themes and create fleshed-out drafts based on internal notes.
* **Simplify and summarize** – Writing long, rambling sentences is easy. One of the hardest jobs in technical documentation is communicating concepts clearly and succinctly. AI-based tools can help cut through the noise to find the signal in what you’re writing.
* **Convert code samples** – If you have code samples for one language, an LLM can convert them into the other languages that you support. But make sure to get a specialist in each language to check they’re idiomatically correct.
* **Check for factual and language errors** – Think of generalist LLMs as proofreaders with a limited attention span. If you make your prompts specific and limit the scope of each task, you can use an AI tool to identify inconsistencies, confusing language, and technical errors that a standard spell checker might miss. However, keep in mind their limited context windows and lack of product knowledge mean you need to closely monitor the process to minimize the chances of errors slipping through.
* **Enforce style guides** – While a non-AI prose linter like [Vale](https://vale.sh/) might be a better option for enforcing style guides as part of your git documentation workflow, LLM-based tools can help you find deviations from your style guide. But beware that you can fit only so much of your style guide into a prompt, so you might need to do several passes.
* **Translate and localize** – Generalist LLMs are helpful for basic translations, but they often struggle with technical language. For more accurate, idiomatic translations, consider specialized tools that focus on technical documentation. And always ask a native speaker to review before you publish.
* **Chat-like interface to look-up answers** – Even the best index or table of contents can’t beat truly great search. Once your product documentation is live on your site, integrating an LLM means that your users can ask questions about your docs and receive summarized, plain text answers. This isn’t so much about improving your git documentation workflow but about making your product documentation more accessible to the people who need it.

Like most software tools, LLMs are at their best when it comes to predictable tasks — especially when you can provide very specific instructions. If you work within their limitations, they can boost your productivity and help you deliver higher quality work. So, let’s look at what those limitations are.

### The limitations of AI tools for documentation <a href="#the-limitations-of-ai-tools-for-documentation" id="the-limitations-of-ai-tools-for-documentation"></a>

It’s hard to get an honest picture of both the good and the bad of LLMs. It’s not unusual for hype to obscure the real value of a new technology. But advanced tools like ChatGPT go a step further by appearing almost magical.

When you can have a conversation with what appears to be an infinitely knowledgeable and articulate partner, the tool behind the conversation can seem capable of almost anything.

But for us as people who write technical documentation and product manuals, not understanding the limitations could lead to delivering embarrassing or even career-limiting errors in our work.

So, let’s take a look at the weaknesses of AI tools when it comes to documentation:

* **The LLM doesn’t know your product** – LLMs rely on existing, publicly available data. Usually that’s from a snapshot months or even years in the past. It’s rare that your role is to rehash publicly available information. Instead, you are often the first person to write the product manual for new or updated functionality. This means the best that generalist LLMs can do is make educated guesses based on old information. The result is that LLMs typically can’t write product documentation from scratch, no matter how detailed your prompts are.
* **LLMs can’t think for you** – It’s not just that LLMs lack detailed knowledge of your product — they also can’t empathize with the user. They don’t understand the goals of the person reading your documentation or how to bridge the gap between your product and their needs. Even if you use bullet points or outlines instead of drafting detailed sections, you still need to do the foundational thinking and use it as the input for the LLM to improve.
* **LLMs are forgetful** – Earlier, we touched on the limited context window of LLMs. [Claude’s paid version can take in around 500 pages of text](https://support.anthropic.com/en/articles/8606394-how-large-is-claude-pro-s-context-window) in one session. [OpenAI’s GPT-4o model has a context window](https://openai.com/api/) of roughly 300 pages of text. Although this might seem like a lot, important details from earlier in the conversation can still be missed, especially in long or complex documentation tasks. For something as lengthy as a product manual, an LLM might lose consistency, leading to potential errors.
* **LLMs are fuzzy** – Large language models work by predicting what word is most likely to come next. There are ways to finetune that but the result can be text that seems plausible rather than being accurate. Unless you stay on top of the details, you might end up with documentation that seems right at first but that doesn’t match up with the product in practice.
* **They’re over confident** – An LLM won’t tell you when it isn’t sure about an answer because it has no way to tell. Instead, it will churn out text that sounds about right but could be entirely wrong.
* **And they hallucinate** – Going beyond just being confidently incorrect, LLMs can sometimes produce the computer equivalent of hallucinations. Since they generate text based on what’s most likely to come next, rather than what is true, they can sometimes provide answers that are entirely fabricated.

Now that we understand the strengths and limitations of AI tools for product documentation, let’s look at how you can put them to work.

### Introducing an AI product docs workflow <a href="#introducing-an-ai-product-docs-workflow" id="introducing-an-ai-product-docs-workflow"></a>

Each team, product, and workflow has its own peculiarities. What works for one team might not work for yours. That’s why the first step to implementing AI in your documentation workflow is to find one or two places where you can experiment without much risk.

Once you’ve knocked-off the rough edges, you can integrate AI tools more deeply into your product documentation workflow. You’ll find what works well for your team but here’s one approach you could take to introducing an AI product docs workflow.

#### 1: Ad-hoc experiments <a href="#id-1-a-d-hoc-experiments" id="id-1-a-d-hoc-experiments"></a>

For most people, this is where their integration of AI tools into the documentation workflow stops. It’s easy and accessible — after all, nearly anyone can create a ChatGPT or Gemini account. Plus, it’s relatively low risk since you maintain full control over what gets included in your final documentation.

Using the chat interfaces from public LLM providers, you can get help at any stage of your writing or editing process. This brings us back to all the ways LLMs can be useful right now, including:

* Outlining, structuring, and drafting
* Checking for errors that a spellchecker or Grammarly might miss
* Simplifying and summarizing
* Translating from one language to another
* Converting code samples.Document and comment code with AI assistance.

However, if you’re only using AI instinctively or when you’re stuck, it becomes harder to turn that into a repeatable process that consistently enhances your product documentation workflow.

#### 2: Manual but with process <a href="#id-2-manual-but-with-process" id="id-2-manual-but-with-process"></a>

To take the next step with your AI product docs workflow, start by analyzing what works, identify areas for improvement, and pause anything that takes more time than it saves. The key is to create lightweight, repeatable processes and share them with everyone involved in creating and maintaining your documentation.

Here are some of the steps you might take:

* Create and maintain a library of shared prompts, organized by task type and stage of the product documentation process.
* Develop formal processes that reflect the most effective ways your team has found to use AI for specific tasks in technical documentation.
* Incorporate AI-related steps into your documentation review process, including checks for consistent terminology and automated summarization.
* Keep a log of AI-driven experiments and share the results with your team, allowing you to refine and improve your prompt library and overall AI product docs workflow.

#### 3: Integrating AI into your Git documentation workflow <a href="#id-3-integrating-ai-into-your-git-documentation-workflow" id="id-3-integrating-ai-into-your-git-documentation-workflow"></a>

This is where you start to put more faith in AI products by building them directly into your CI/CD process. At this point, you’re moving beyond chat interfaces and, instead, integrating LLMs directly into your git workflow through the APIs provided by LLM companies. Alternatively, you might use open-source models or take advantage of the AI functionality available in tools like [GitBook](https://www.gitbook.com/).

With this workflow, you’re still using these tools for many of the same tasks as before. However, your prompts are now optimized to the point where you can predict their outcomes, and you’ve used them enough to understand their limitations.

Most importantly, working with LLMs in this way gives you two ways to shape them to your specific needs:

* **Fine-tuning** – Fine-tuning means taking an existing LLM and training it on your specific data, such as internal documentation or product manuals, so it understands the unique context of your product. While effective, it’s resource-intensive and typically done infrequently.
* **Retrieval-augmented generation (RAG)** – RAG allows an LLM to access and incorporate up-to-date information in real-time by pulling data from a vector database. This makes it particularly useful for handling rapidly-changing content, such as technical documentation or product updates.

For many teams, the effort required for fine-tuning or using RAG may outweigh the benefits, especially if your documentation doesn’t change frequently. In such cases, tools like GitBook, which manage context automatically, can be more efficient.

[GitBook’s API](https://app.gitbook.com/s/2SyQSbIa1iYS7z6Dx5di/gitbook-api) also allows you to integrate this data with other platforms. For example, you could build a documentation chatbot in Intercom that enables users to get answers directly from your docs.

### Using GitBook AI in your docs workflow <a href="#using-gitbook-ai-in-your-docs-workflow" id="using-gitbook-ai-in-your-docs-workflow"></a>

If you’re ready to start using AI for creating and maintaining your documentation, [GitBook AI](https://www.gitbook.com/solutions/ai) allows you to bypass the ChatGPT experimentation stage. It ingests your existing documentation and gives you tools directly in the GitBook app to:

* Write new content based on your prompts
* Continue, explain, and summarize your existing content
* Create and iterate on code samples to accompany your documentation
* Improve your writing through spelling, grammar, and tone checks
* Translate from one language to another.

GitBook AI can make your published documentation easier to access, too. When you [enable it for your product docs](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/create-content/searching-your-content/gitbook-ai#for-published-content), your readers can ask questions in their own words and get tailored answers in seconds — with references back to the relevant page in your docs.

All of these tools — and everything we’ve talked about in this article — make this an incredibly exciting time to be involved in the documentation process. AI technologies are constantly evolving and improving, so while everything we’ve talked about here is relevant today, we’ll check back in and regularly update it to make sure it stays relevant into the future. Right now, for example, GitBook AI uses GPT-4o to provide the best and most accurate results — but who knows what the next model will be capable of.

We can’t wait to see how the next generation of AI tools will improve documentation for everyone. For now, though, we’d love to hear how you’re approaching AI in your docs workflow. Let us know on X (formerly Twitter).

[**→ Get started with GitBook for free**](https://app.gitbook.com/join)

[**→ Get an overview of GitBook AI**](https://www.gitbook.com/solutions/ai)

[**→ Read about writing docs with GitBook AI**](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/gitbook-agent/write-and-edit-with-ai)
