---
description: >-
  Define your team's writing rules in a dedicated styleguide space, and keep
  every contributor, human or GitBook Agent, consistent.
icon: pen-ruler
tags:
  - early-access
---

# Styleguide

A styleguide is a dedicated space that holds your team's writing rules and conventions. It's the single source of truth for how content on your site should be written — voice and tone, terminology, formatting, and structure.

A styleguide serves two audiences:

* **Your team:** writers and reviewers have one shared reference for how to write, so documentation stays consistent no matter who edits it.
* **GitBook Agent:** the Agent reads your styleguide and treats it as the source of truth it must follow whenever it writes, edits, or reviews content. It overrides the Agent's own defaults and general writing conventions.

{% hint style="info" %}
**Styleguides are in early access.** The styleguide feature is rolling out gradually. If you don't see it yet, it isn't enabled for your organization.
{% endhint %}

### How GitBook Agent uses your styleguide

GitBook Agent loads your styleguide's first page in full into its context on every task, so that page always drives its work. It reads other pages only on demand, using the table of contents.

**Put your main rules on the first page.** Keep every rule you want enforced there, and use additional pages for detail the Agent can pull in when relevant. Your edits always win: change a rule and the Agent follows your version; delete a rule and the Agent stops enforcing it.

The styleguide is the Agent's only source of rules. If your styleguide mentions an upstream guide — like Google's or Microsoft's — as its base, that mention is background for human readers, not an instruction to the Agent. If a convention matters to you, write it down.

#### Enforceable rules and guidance

Styleguides distinguish between two tiers of content, and the difference is whether a rule carries a numbered ID:

* **Numbered rules** (like `G-10` or `MS-9`) are the enforceable tier. The Agent flags violations of them directly and cites the ID, so you can trace any flag back to the exact rule that produced it.
* **Unnumbered guidance** — like a voice description — is judgment territory. The Agent applies it when writing and offers it as suggestions for human review, but never flags it as a violation.

To add an enforceable rule, give it the next number after the current highest, wherever the rule lives. Never renumber or reuse an ID — past flags and your decision log refer to them. Over time, numbers won't match page order; that's normal. An ID's only job is to stay stable.

{% hint style="info" %}
In the starter template, the `SG-` prefix is yours to change — but keep it stable once you start using the guide.&#x20;
{% endhint %}

### Create a styleguide

You can start styleguide setup from several places:

* From your site's dashboard, go to **Tools**, click **Styleguide**, then click **Set up**.
* Open **Site settings → Styleguide** and set it up from there.

Then choose a starting point (detailed below):

* Reuse an existing styleguide from your organization.
* Pick a template — Starter, Google, or Microsoft.
* Upload a file or import from a URL, if you already have a styleguide.

The first time you open your styleguide, GitBook shows a short intro explaining that you edit it like any other space.

#### Use an existing styleguide

If your organization already has styleguides in use elsewhere, they appear at the top of the setup screen, along with the sites that use them. When you choose one, you can:

* **Use it as-is** — attach it shared with the other sites that use it. Edits apply everywhere it's used.
* **Fork it** — create a dedicated copy for this site (named `Styleguide - {site name}`) that you can evolve independently.

#### Pick a template

GitBook offers three templates to start from:

<table><thead><tr><th width="204.75390625">Template</th><th>Best for</th></tr></thead><tbody><tr><td><strong>Starter template</strong></td><td>Defining your own voice and rules from scratch. Each section explains what belongs there and why, with scaffolding you fill in yourself.</td></tr><tr><td><strong>Google styleguide</strong></td><td>Clear, precise, and professional writing for a developer audience. Generated from the Google developer documentation style guide.</td></tr><tr><td><strong>Microsoft styleguide</strong></td><td>Warm, simple, and human writing for a broad audience — including readers who aren't technology experts. Generated from the Microsoft Writing Style Guide.</td></tr></tbody></table>

The Google and Microsoft templates come pre-filled with enforceable rules from their source guides — covering voice, word lists, grammar, formatting, procedures, accessible writing, and inclusive language — and are ready to use as-is. Everything is yours to edit: a template is a starting point, not a contract.

{% hint style="info" %}
GitBook reviews and updates base templates when the source guides change, so templates stay current with the guides they're generated from.
{% endhint %}

**Customize the "Needs your input" sections**

Every template marks the parts you must customize with a **Needs your input** hint. Before your styleguide is ready to use, work through these — they typically include:

* The snapshot date of the base guide version the template reflects (Google and Microsoft templates)
* Your product name and documentation mission
* Who reads and writes your documentation, and what the guide covers
* Your product names, feature names, and any terms your team debates, added to the word list
* An owner, a review cadence, and how to propose changes
* A first entry in the decision log

Everything without a hint is pre-filled and ready to use as-is. Placeholder rules that you haven't filled in yet are inactive — the Agent won't enforce them until you replace the placeholders with real content.

#### Upload a file

If you already keep a styleguide in another tool, you can import it instead of starting from a template:

1. In the setup screen, click **Upload a file**.
2. Drop your Markdown, HTML, DOCX, or ZIP files — or browse to select them.
3. Optionally, enable **Enhance import with AI** to automatically refine and clean up the imported content.
4. Click **Start import**.

#### Import from a URL

If your styleguide is published online, GitBook can import it directly:

1. In the setup screen, click **Import from an URL**.
2. Enter the docs link you want to import.
3. Optionally, enable **Enhance import with AI** to automatically refine and clean up the imported content.

GitBook imports all public pages under the URL you enter, up to 200 pages. For example, if you import `website.com/docs/`, it will include `website.com/docs/article`, but not `website.com/other-parent/page`. For larger sites, import smaller sub-paths separately.

### What to put in your styleguide

A styleguide is most useful when it captures the decisions that are easy to get wrong or inconsistent across a team. The templates share a common structure, and each section settles a different class of style debate:

* **Introduction:** what the guide is for and what your documentation is for. A guide with a stated purpose gets maintained; one without gets abandoned.
* **Audience and scope:** who reads your docs, who writes them, and what the guide covers. Half of all style debates are really audience debates in disguise; settle them once here.
* **Voice and tone:** how you address the reader and how formal or friendly you are, plus enforceable rules for anything mechanically checkable, like punctuation and contractions.
* **Word list:** your product names, exact casing, preferred terms, and settled terminology debates. Record only the terms your team has debated; keep entries terse.
* **Grammar and mechanics:** sentence-level defaults for person, tense, and voice. The exception column matters as much as the rule: it keeps the Agent from flagging legitimate text.
* **Formatting:** heading case, UI elements, links, code, and when to use lists, steppers, hints, and other blocks.
* **Writing procedures:** step format, imperative verbs, one action per step.
* **Error messages and failure states:** tone rules for the moments readers are most stressed. Optional; delete it if your docs don't include error text.
* **Accessible writing** and **Inclusive language:** near-universal, checkable rules most teams adopt as written.
* **Content types and templates:** your page types, so writers and the Agent know which structure a page should follow. Many teams use a framework like [Diátaxis](https://diataxis.fr/).
* **Ownership and updates:** the owner, review cadence, and how to propose a change. A guide nobody owns drifts into fiction.
* **Decision log:** your institutional memory. Changing a rule changes what the Agent enforces; the log remembers why, so settled debates stay settled. Record every deliberate departure from a base guide here.

### Edit your styleguide

A styleguide is a space, so you edit it the same way you edit the rest of your documentation:

* **In GitBook:** make your changes in a change request, then merge them when you're ready.
* **With Git Sync:** if the styleguide space is synced to GitHub or GitLab, edit it as markdown in your repository.

To open your styleguide, use the **Styleguide** entry in your site's sidebar, or the **Edit** action in **Site settings → Styleguide**.

### Share a styleguide across sites

A styleguide belongs to your organization, so several sites can rely on the same one — the editing agent applies the same writing rules everywhere, and all your documentation follows one voice.

After you create a styleguide, GitBook offers to link it to any other sites in your organization that don't have one yet. You can also attach an existing styleguide — shared or forked — when setting up a site, as described earlier.

To see every styleguide in your organization and which sites use each one, open the **Styleguides** entry in your organization sidebar.

#### Detach a styleguide

To stop a site from using its styleguide, open **Site settings → Styleguide** and choose **Detach**. Detaching keeps the styleguide space — it may still be used by other sites. If no other site references it, GitBook offers to delete it permanently.

### Put your styleguide to work

With your styleguide in place, ask GitBook Agent to do a pass on your existing documentation to align it with the styleguide. From then on, the Agent checks that your styleguide is respected every time it writes, edits, or reviews content — flagging violations of numbered rules with their IDs, and offering unnumbered guidance as suggestions for human review.

There are two main ways to run a styleguide review on your changes:

#### Review a page before requesting a review

While you're working on a page, you can ask the Agent to check the page against your styleguide — use **Check consistency against styleguide** in the Improve menu, or ask in chat. The Agent reviews the page and leaves comments summarizing what it found

#### Request a styleguide review on a change request

When your site has a styleguide, GitBook Agent appears as a suggested reviewer on your change requests, tagged **Styleguide review**:

1. In your change request, click **Request review**.
2. Add a title and description for your changes — or click **Generate** to let the Agent write them from your changes.
3. Under **Reviewers**, click **Request** next to **GitBook Agent** to have it run a styleguide review of the change request. You can add human reviewers alongside it, or leave the list empty to notify all reviewers in your organization.

The Agent reviews your changes against the styleguide and requests changes on the change request if it finds violations, citing the rules that produced each flag.

### How the Agent enforces your styleguide

When GitBook Agent works with your styleguide, its job is conformance to your rules — not general writing improvement. It's designed to be precise, conservative, and consistent: the same content checked against the same styleguide always produces the same findings.

#### Your styleguide is the only source of rules

The Agent never applies a rule from an upstream guide, from general knowledge of good style, or from any style guide it knows, unless the rule is written in your styleguide.&#x20;

The Agent also respects a few things about how your rules are written:

* **Placeholder rules are inactive.** Template pages contain bracketed placeholder text like `[Product name]` or `[Add a rule]`. A rule whose substance is still placeholder text isn't yet a rule — the Agent won't enforce it. If your styleguide is mostly placeholders, the Agent tells you it's largely unfilled and that enforcement is limited to the rules you've completed, rather than presenting a partial pass as comprehensive.
* **Exceptions are respected.** Many rules carry exceptions ("passive is fine when the actor is unknown"). Text that falls under a listed exception is not a violation.
* **Definite rules count even without an ID.** If you write a rule without a numbered ID but it reads as a definite, checkable instruction ("never use semicolons"), the Agent enforces it and cites it by a short quote instead of an ID.

#### When the Agent reviews

During a styleguide review — on a page, or on a change request — the Agent flags issues but changes nothing. Each flag includes:

* **Rule:** the rule ID from your styleguide (for example `G-10`), or a short quote of your rule if it has no ID.
* **Location:** the heading or line where the issue occurs, plus the offending text.
* **Issue:** one sentence stating the violation.
* **Fix:** the corrected text, ready to paste.

Reviews are capped at **5 flags per pass**. If more issues exist, the Agent reports the 5 highest-priority ones and ends with a one-line note that further issues exist, with a count. Flags are ranked by category — word choice and terminology first, then formatting and punctuation, then grammar, then procedures — and within a category, in page order.

Unnumbered guidance — voice, tone, and structural advice — never appears as a flag. At most, the Agent adds one combined "worth a human look" note per pass covering anything from the judgment tier.

#### When the Agent edits

When you ask the Agent to fix content or align it with your styleguide, it applies numbered rules directly wherever the fix is unambiguous. When a rule has two defensible outcomes, the Agent leaves the text unchanged and lists it as a suggestion instead of guessing.

After editing, the Agent outputs a change summary grouped by rule ID, with counts — for example, "G-7: replaced 'click on' with 'click', 6 instances." Judgment-tier suggestions appear in a separate short list at the end.

#### What the Agent never touches

In both reviews and edits, the Agent never flags or changes:

* Content inside code blocks, inline code, command output, or API and product identifiers
* Direct quotations and cited material
* Text exempted by a rule's own exception
* The meaning or facts of your content
* Anything covered only by a rule that isn't in your styleguide

#### Consistency

The Agent enforces rules as written, even where it might "disagree" — it never softens, strengthens, or reinterprets a rule to fit the content. If a rule is ambiguous as written, the Agent applies its literal reading and notes the ambiguity in its human-review note, rather than inventing intent. And if your site has no styleguide configured, the Agent doesn't fall back to general judgment — it offers to help you start one instead.

### Styleguides and custom instructions

A styleguide complements the site-level custom instructions you can give GitBook Agent. Custom instructions are short, site-specific directions; a styleguide is a full, shared document of your writing rules.
