---
description: >-
  How GitBook Agent reads your style guide and applies its rules when it reviews
  and edits content.
---

# How GitBook Agent enforces your style guide

When GitBook Agent works with your style guide, its job is to make content follow your rules, not to improve writing in general. It's designed to be precise and conservative, and it aims to surface the same issues each time it checks the same content.

## What the Agent reads

* **The first page, on every task.** The Agent loads your style guide's first page in full whenever it writes, edits, or reviews content.
* **Other pages, when relevant.** Before the Agent writes or reviews content that another page covers, such as a word list or a content type, it reads that page from the table of contents.
* **Nothing else.** Your style guide is the Agent's only source of rules. It doesn't apply rules from an upstream guide, from general knowledge of good style, or from any other style guide. If your style guide names Google's or Microsoft's guide as its base, the Agent treats that as background for people, not as rules.

Your edits always win: change a rule and the Agent follows your version; delete a rule and the Agent stops enforcing it.

## Which rules the Agent enforces

How you write a rule decides what the Agent does with it:

| What you write                           | Example                              | What the Agent does                                                                                                                                                   |
| ---------------------------------------- | ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A rule with a numbered ID                | `G-11`: Use the serial comma         | Flags violations and cites the ID. Fixes them when editing.                                                                                                           |
| A definite, checkable rule without an ID | "Never use semicolons."              | Flags violations and cites the rule with a short quote. Fixes them when editing.                                                                                      |
| Guidance                                 | A description of your voice and tone | Applies it when writing new text. For existing text, offers it only as a suggestion, never as a flag.                                                                 |
| A rule that's still a placeholder        | `[Add a rule]`                       | Ignores it until you replace the placeholder. If most of your style guide is placeholders, the Agent tells you that its check covers only the rules you've completed. |

The Agent also respects each rule's exceptions. Text that falls under a listed exception, such as "passive is fine when the actor is unknown", isn't a violation.

To write rules the Agent can enforce, see [Build your style guide](build-your-style-guide.md#write-rules-the-agent-can-enforce).

## When the Agent reviews

During a review, the Agent flags issues and changes nothing. Each flag names the rule, where the issue is, what's wrong, and the fix. For example:

| Part     | Example                                                                  |
| -------- | ------------------------------------------------------------------------ |
| Rule     | `G-10`: Use active voice                                                 |
| Location | "Rotate your API key": "The key is rotated by the system every 90 days." |
| Issue    | Passive voice where the actor is known.                                  |
| Fix      | "The system rotates the key every 90 days."                              |

The Agent aims for around five flags per pass, so the most important issues come first. If more issues exist, it says so and gives a count. Flags are ranked by category, in this order: word choice and terminology, formatting and punctuation, grammar, and procedures. Within a category, they follow page order.

Guidance never appears as a flag. Instead, the Agent adds at most one short "worth a human look" note per pass.

## When the Agent edits

When you ask the Agent to fix content or align it with your style guide, it applies a rule wherever the fix is unambiguous. When a rule allows two reasonable outcomes, the Agent leaves the text unchanged and lists it as a suggestion.

After editing, the Agent summarizes its changes by rule, with counts. For example: "G-7: replaced 'click on' with 'click', 6 instances." Suggestions based on guidance appear in a short list at the end.

## What the Agent never changes

In both reviews and edits, the Agent never flags or changes:

* Content inside code blocks, inline code, command output, or API and product identifiers
* Direct quotations and cited material
* Text exempted by a rule's exception
* The meaning or facts of your content

The Agent applies rules as written. It doesn't soften, strengthen, or reinterpret a rule to fit the content. If a rule is ambiguous, the Agent applies its literal reading and mentions the ambiguity in its "worth a human look" note.

## Without a style guide

If your site has no style guide, the Agent doesn't review for style. On change requests, it comments only on clear, objective issues, such as typos, contradictions, incorrect instructions, or unfinished sections.

## Style guides and custom instructions

Custom instructions are short, site-specific directions for GitBook Agent. A style guide is a full, shared set of writing rules. The Agent uses both, and if they conflict, the style guide wins.

Put the writing rules you want enforced in your style guide. Use custom instructions for other directions, such as how to add links or which block types to avoid.
