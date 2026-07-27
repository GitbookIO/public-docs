---
description: Write custom GitBook Skills tailored to your team's docs conventions.
---

# Author your own skills

GitBook's own Skills (see [GitBook Skills overview](overview.md)) teach an agent GitBook's syntax and conventions in general. If your team has its own house style on top of that — a preferred voice, specific block usage rules, a review checklist, naming conventions for pages — you can write your own skill and load it alongside GitBook's.

### Basic anatomy

A skill is a `SKILL.md` file with two parts:

* **Frontmatter** — a short `name` and `description`. The description is what your agent (or the harness running it) uses to decide when the skill is relevant, so make it specific about what the skill covers and when to reach for it.
* **Instructions** — the body of the file, written the same way you'd brief a new team member: what to do, what to check, and why, not just a dry list of rules. Keep it focused — a skill that tries to cover everything is harder for an agent to apply well than several narrow ones.

For anything too long to keep in the main body, split it into separate reference files and point to them from the main `SKILL.md`, so the agent only loads the detail it actually needs for the task at hand — see [What SKILL.md contains](whats-inside-a-skill.md) for how GitBook's own skill is structured as an example.

### Where it lives

Like GitBook's own skills, a custom skill can be:

* Installed alongside GitBook's skills in your project, if your assistant supports package-based skills.
* Copied directly into your project as a file, for assistants that read local skill files, or for conventions that are private to your team rather than something you'd publish.

### Keep it current

Treat a house-style skill like any other living document — review and update it as your conventions change, the same way you'd update GitBook's own skill when GitBook adds new features (see [Install GitBook Skills](install-skills.md)). A skill nobody maintains drifts out of date quietly, since an agent has no way to know your conventions changed unless the file says so.
