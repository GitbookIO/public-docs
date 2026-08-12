---
description: >-
  With documentation personas, you can focus on the challenges your users are
  facing, what they need to achieve, and how your docs can help them get there
---

# Build your docs around your users’ needs with documentation personas

The first step to great product documentation is to know your reader. What do they want to achieve? What context and experience do they bring with them? How do they view the world?

Without that deeper understanding of the people who use your documentation, there’s a risk that you end-up writing for an imagined audience that doesn’t exist. Sure, you can make educated guesses and they might be good enough for much of the time.&#x20;

But documentation and other learning materials are as much a part of the product as the UI, the features, and the support offering. And it’s rare for a successful company to invest in those parts of the product without first understanding who they’re serving. So why should docs be any different?

The good news is that it’s relatively straightforward to [gather the data you need](documentation-personas.md#gathering-qualitative-data) in order to build an accurate picture of the people who turn to your documentation. In particular, there are two techniques that you’ve probably already come across: personas and Jobs to be Done. Together, they can help us make sure that the learning materials we create solve real problems for real people.

### Personas vs Jobs to be Done

Personas describe who a person is, while Jobs to be Done focuses on what they want to achieve. To create effective product documentation, you need to understand both for your users. That starts with data — and we’ll look at how to get that data later on. But first, let’s make sure we’re clear on the different roles that personas and Jobs to be Done play.

#### Personas

Creating personas is like an artist starting with a pencil sketch. The goal isn’t to capture every detail, but just enough to bring the person to life later. To make your personas authentic, you’ll need to observe real people, just as an artist studies their subject.

Personas usually focus on what user researchers call psychographic or behavioral characteristics. These are about what makes the person tick, rather than what they do in their work.

We’ll look more deeply at how to gather data to help you build effective personas later, but here are three broad questions to ask when defining personas:

1. Who are they? Capture the persona’s role, skills, and context. Are they a junior developer learning the ropes or an experienced architect juggling multiple projects? This offers a sense of their background and expertise.
2. What are their goals? This could be very specific to their work, such as integrating an API or troubleshooting an issue. But it could also refer to their career and personal goals.
3. What challenges do they face? Identify the obstacles or frustrations they encounter. Is it a lack of clarity in the documentation, time pressure, or missing examples? Recognizing these pain points allows us to address them directly.

So, what does that look like in practice? Well, here’s an example persona that we can use as a demo. Meet Diane:

* **Name:** Diane
* R**ole:** Senior Backend Developer at a fintech startup
* **Experience:** 8 years of backend development - 5 years with Java monoliths at an enterprise company, 3 years building microservices with Go and Python
* **Goals:**
  * Ship reliable integrations that scale
  * Minimize time spent debugging API issues
  * Keep the team's tech debt manageable
* **Challenges:**
  * Working with multiple API versions across different services
  * Need for precise rate limit and quota documentation
  * Tight deadlines for shipping new integrations
* **Preferred learning style:**
  * Starts with quick reference docs and curl examples
  * Needs detailed error codes and troubleshooting guides
  * Values inline code comments that explain “why” not just “what”
  * Appreciates architecture diagrams for complex flows

Now we know something about Diane’s preferences. That helps us understand the bigger picture of who Diane is and how she works. So, we can structure our docs in a way that allows her to quickly find the exact answers she’s looking for, without unnecessary friction.&#x20;

By catering to her preferred learning style, we help her achieve her goals more efficiently. But it’s not much use knowing how Diane wants to use our documentation if we don’t know what brought her there in the first place.

#### Jobs to be Done

That’s where Jobs to Be Done comes in. It tells us what Diane wants to do. The idea is that Diane “hires” our documentation for a particular job. If the documentation does the job she needs, she’ll hire it again. Otherwise, she’ll “fire” it and find another way to get the job done, whether that’s scouring third-party forums or even turning to another product entirely.

To define our users’ Jobs to Be Done, we can ask three questions:

1. **What specific task are they trying to complete?** This helps us focus on the immediate goal that brought them to the docs.
2. W**hy did they turn to the docs?** Understanding the trigger gives context to the urgency or complexity of their job.
3. **What does success look like for them?** Knowing what outcome the user prioritizes helps us create documentation that leads them directly to their goal.

For Diane, one Job to be Done might look like this:

* **Task:** Debug and fix intermittent 429 errors from the /customers/search endpoint.
* **Trigger:** Production monitoring showed sporadic API failures during peak hours, causing customer search to fail roughly 5% of the time.
* **Success looks like:**
  * Finding the relevant rate limit documentation in under 30 seconds
  * Getting a clear explanation of rate limit calculation and quotas
  * Seeing a code example that demonstrates best practices for handling 429s
  * Quickly locating related troubleshooting guides for common rate limit issues
  * Understanding which metrics to monitor to prevent future rate limit problems

This gives us a snapshot of a specific and realistic scenario. But we shouldn’t get too hung up on that exact error code. What matters is that Diane needs to quickly diagnose and fix a problem.&#x20;

Our documentation needs to support that job by being easily searchable, technically precise, and focused on practical solutions. The specific details help us think concretely about how to structure our docs, but the underlying job –– finding and fixing an error quickly –– is what guides our documentation strategy.

#### Combining personas and Jobs to be Done

Personas tell us who Diane is and how she works. Jobs to Be Done tells us what she’s trying to accomplish in the moment. When we bring these together, we get a fuller picture that helps us create more focused, effective documentation.

In Diane’s case, our Jobs to be Done flavored persona might look like this:

**Persona:**&#x20;

* **Role:** Senior Backend Developer
* **Experience:** 8 years of backend development, currently working on microservices.
* **Goals:** Ship reliable integrations, minimize downtime, and keep technical debt low.
* **Challenges:** Balancing tight deadlines with the need for precise, reliable documentation.
* **Preferred learning style:** Skims through references, focuses on code examples, and prefers concise solutions without unnecessary steps or context.

**Jobs to be Done:**

1. **Diagnose and resolve API issues quickly**
   * **Task:** Identify the root cause of errors, whether it's an unexpected status code or a performance bottleneck.
   * **Trigger:** Production monitoring or user reports indicating failures or degraded performance.
   * **Desired outcome:** Quickly locate relevant documentation, such as error codes, troubleshooting steps, and best practices for handling failures.
2. **Implement new API integrations efficiently**
   * **Task:** Add or update integrations with third-party services
   * **Trigger:** New feature development or client requirements
   * **Desired outcome:** Find comprehensive integration guides with examples, common pitfalls, and configuration options, enabling smooth implementation without extensive trial and error.
3. **Optimize API performance for scalability**
   * **Task:** Ensure APIs can handle increasing traffic and maintain performance under load.
   * **Trigger:** Anticipating future growth or reacting to performance issues during load testing.
   * **Desired outcome:** Access performance tuning tips, rate limit documentation, and architectural recommendations to avoid bottlenecks as the system scales.
4. **Keep technical debt manageable**
   * **Task:** Refactor old code and update documentation to reflect system improvements.
   * **Trigger:** Periodic system reviews or new architectural changes.
   * **Desired outcome:** Find documentation that explains the rationale behind key design choices and up-to-date best practices, making it easier to apply improvements without introducing new issues.

### What this means for your documentation

Creating a documentation strategy based on personas and Jobs to be Done is a huge topic that we can’t cover fully here. So for now, let’s look at some of the more practical ways in which our understanding of Diane might impact what you produce and how you present it.

1. **Provide concise, code-focused examples:** Since Diane prefers to skim and jump straight to code, make sure every guide includes quick, actionable examples upfront, helping her dive right into problem-solving.
2. **Create dedicated troubleshooting materials:** In a moment of crisis, or even just a run-of-the-mill error, Diane wants to get back to being productive as quickly as possible. Make sure that error codes, operational considerations, and troubleshooting guides are easy to find, helping her quickly resolve issues without distractions. Or take it to the next level with an [Ask AI](https://docs.gitbook.com/content-editor/searching-your-content/gitbook-ai) feature, providing a conversational interface to your documentation.
3. **Organize your documentation by product life-stage:** We know that Diane cares about scalability. By providing documentation according to different stages of the product’s life cycle, you’ll make it easier for her to find relevant help when she needs it.

So, let’s look at how to create personas that will help you target your documentation more precisely to the needs of your readers.

### How to create personas for your docs

Creating personas begins with sketching out what you already know. This initial draft is then tested against data, refined based on what you learn, and evolves through an ongoing process of improvement. This first version is often called a proto persona.&#x20;

One of the world’s most respected user experience consultancies, the Nielsen Norman Group, defines proto personas as the first of [three types of persona](https://www.nngroup.com/articles/persona-types/):

* **Proto personas:** Those sketches based on your existing knowledge and assumptions.&#x20;
* **Qualitative-based personas:** Interview your users so that you can find the common threads that lead to specific personas and the jobs they need to do.
* **Statistical personas:** Combine your qualitative research with surveys to a much larger base and then use statistical analysis to find clusters of similar responses.

A proto persona could look something like this:&#x20;

**Name:** Alex the Ambitious Front-End Developer

**Role:** Front-end developer at a mid-sized tech company

**Jobs to be done:**

* **Set up a working environment for a new tool within 30 minutes**
  * Needs a clear "getting started" section with minimal prerequisites and actionable steps to see immediate results.
* **Understand how to implement advanced features to meet specific project requirements**
  * Requires in-depth examples that demonstrate integrating features like API pagination, authentication, or real-time updates into common front-end frameworks (e.g., React).
* **Debug an unexpected issue while integrating the tool**
  * Needs a well-organized troubleshooting guide or error reference that explains common problems (e.g., token misconfigurations) and provides actionable resolutions.
* **Evaluate if the tool meets performance and scalability needs before adoption**
  * Looks for documentation that explains how the tool performs under different conditions (e.g., caching strategies, support for large datasets) with benchmarking examples.
* **Learn how to upgrade the tool or library without breaking their project**
  * Relies on clear versioning notes, migration guides, and examples to confidently update dependencies while minimizing risks to production.

**Pain points:**

* Ambiguous or incomplete setup instructions that delay project timelines.
* Documentation that assumes too much prior knowledge and skips context.
* Lack of migration support or breaking changes introduced without clear guidance.

**Assumptions:**

* Prefers tools with strong community support and an active ecosystem.
* Finds value in tutorials that demonstrate real-world use cases.

#### Using data to refine your personas

All of this seems reasonable and it’s not a bad start. But personas are most valuable when we learn what real people need. For most products, qualitative research will give you an excellent basis for improving how well your docs serve your users.&#x20;

You might be wondering if qualitative data is enough. Remember those statistical personas that the Norman Nielsen Group talks about? They might seem more scientific, but they require significant time, resources, and expertise to do well. Qualitative research, on the other hand, gives you rich insights quickly. A single hour-long conversation with a user can reveal:

* The precise language they use to describe problems
* The context that brings them to your documentation
* Their actual workflow (not just what they say they do)
* The frustrations that make them abandon documentation
* The moments where great docs make their job easier.

#### Gathering qualitative data

So, what techniques can you use to gather qualitative data while leaving room for the rest of your responsibilities?

**1. One-on-one user interviews:**

* Schedule 30-60 minute calls with ten or so people who use your docs. You need to balance their availability with how much you can cover in one call.
* Ask about their work and specific experience with your documentation and of other products.
* Look for patterns in how they describe problems and solutions.&#x20;
* Notice the language they use to talk about their work.
* Ask them to carry out tasks and observe what they do.
* Make sure to transcribe each session. AI transcription services like [Rev.com](https://www.rev.com/) offer an inexpensive and fast way of doing this.

**2. Support ticket analysis:**

* Review tickets where changes to your documentation could have prevented the problem.
* Analyze what led to the support ticket and how documentation could have prevented it.
* Note the actual words people use to describe issues.
* Track which docs pages appear in tickets.

**3. Documentation feedback:**

* Monitor comments and reactions on docs pages.
* Track search terms within your documentation.
* Review visitor statistics to understand the paths that people take through your docs.

#### Analyzing your data                                                                                                                                                                                                                                  &#x20;

Once you’ve gathered your research, you can start piecing together a clear picture of who your documentation personas are and what they want to achieve.&#x20;

Depending on your background, the thought of analyzing all this data might seem a bit overwhelming. But you can get good insights just by reading your transcripts, support tickets, and so on.&#x20;

And what’s more, tools like ChatGPT and Claude can act as an expert assistant that will do the heavy lifting for you while also helping to organize the results in useful ways.

If you do want to get a bit more formal, there are several techniques you can use to unpack your qualitative data, such as:

* **Thematic analysis:** Highlight repeated phrases and concepts, then group them into broader behavioral categories. For example: you might find that a lot of feedback centers on the searchability of your documentation or the availability of code samples in less popular languages.
* **Journey mapping:** Track the steps users take when engaging with your documentation, from entry to exit. For example, you might observe that users frequently bounce between troubleshooting and reference sections, suggesting a need for more integrated content or clearer cross-referencing.
* **Content gap analysis:** Identify topics that your data shows are important but that are not well covered in your documentation. For example, you might find that users often ask about integration with a particular platform or tool but that your documentation covers it only briefly.

These analysis techniques will leave you with a firm idea of what your users want and need. You should also be able to notice correlations between certain types of people and the work they do, their preferences, and the jobs they need your documentation to do for them.&#x20;

And again, this is a great opportunity to use AI tools to save yourself some time and get a helping hand.

#### Using your analysis to create your personas

Once you have your initial analysis done, you can start to create your personas:

1. **Identify demographics:** Start by defining the basic demographic information that impacts how the personas use your documentation. This might include their role, industry, and technical expertise.
2. **Analyze behaviors:** Use the insights from your data analysis to find common behaviors and preferences. For example, do they prefer quick how-to guides or detailed reference docs?
3. **Define their goals and challenges:** From your thematic analysis, identify what each persona is trying to achieve and the obstacles they come across and how both of those relate to your documentation.
4. **Consider learning styles:** People learn in different ways. Identify if your personas prefer visual aids, text-based instructions, hands-on examples, or a combination of these.
5. **Write the Jobs to be Done:** For each persona, list out the specific tasks they are trying to accomplish when they interact with your documentation. This should be directly informed by your journey mapping and content gap analysis.

It might take a few iterations to get your personas feeling truly cohesive and believable. But even from the first draft, you'll find that you're already much more focused on who your documentation is for and how best to serve them.

### Using your personas to improve your docs

Personas aren’t only helpful in creating new documentation. They also give you a new set of information with which to make your existing documentation more useful.&#x20;

Here are some quick wins you can get with your existing docs:

* **Reorganize content:** Now you have a better understanding of how and when your users come to your documentation, you can shape your information architecture and navigation accordingly.
* **Add quick access points:** Create landing pages tailored to specific roles and problems, providing a jumping off point to the resources they need most.
* **Fill the gaps:** It’s likely that your research will help you identify gaps in your documentation that you weren’t aware of before. It might even help you uncover show-stopping problems that harm new user conversion or even cause people to churn.

And, of course, the process doesn’t stop there. You can use the relationships you’ve built with your interview participants to help review the changes you make.

### Use a documentation platform that supports your research

Personas and Jobs to be Done are part of a bigger story about making your product experience as friction-free as possible. And while the actual material you produce and how you organize it are the biggest impact you can have, how you get your documentation to your readers is equally as important.

With GitBook, you can create product documentation that your users love _and_ that support your persona and Jobs to be Done research. Here’s how:

* **Feedback:** GitBook’s [page ratings](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/analytics/insights#pages-and-feedback) and feedback gives your readers a quick and easy way to provide feedback and allows you to see how well individual pages serve your users.
* **Traffic insights:** Use [built-in insights](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/analytics/insights) to get data about your docs site’s traffic and visitor behavior, helping you to create journey maps and understand the jobs your readers want to achieve.
* **Search analytics:** Understand what [search terms](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/analytics/insights#search) people are using to navigate your docs.

And there’s more to GitBook, including a git-based workflow, real-time and async branch-based collaboration, Ask AI to help your users find info in your docs faster, and more. [Try it out for yourself](https://gitbook.com/join).

[**→ Get started with GitBook for free**](https://app.gitbook.com/join)

[**→ Combine multiple sites into one using site sections**](../content-organization-and-localization/combine-multiple-docs-sites-using-sections.md)

[**→ How to use SEO techniques to improve your documentation**](../seo-and-llm-optimization/how-to-use-seo-techniques-to-improve-your-documentation.md)
