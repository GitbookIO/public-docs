# How to make a great-looking docs site

## How to build a great-looking GitBook docs site

Good documentation isn’t just well-written — it’s well-designed. A docs site that reflects your brand, organizes content clearly, and uses the right visual components builds trust with readers before they’ve read a single word.

This guide walks through the process of building a polished GitBook docs site from scratch, in the order that works best: structure first, then visual customization, then content layout. Each step builds on the last.

***

### Step 1: Start with information architecture

Before you touch fonts or colors, figure out how your content is organized. This is the most important decision you’ll make, and it’s worth spending real time on it.

Ask yourself:

* Is your product a single tool, or does it have distinct areas (e.g., a main product, an API, an admin panel)?
* Do different types of users need fundamentally different content — say, developers vs. end users?
* Are there natural groupings by use case or by feature area?

The answers determine whether you need one space or multiple spaces, and how your top-level navigation should be structured. A common mistake is to jump straight to theming and then realize the navigation doesn’t make sense — which means rebuilding.

**Practical tip:** If you’re migrating from an existing site, map out how the current content is organized before importing anything. Sometimes existing docs have accumulated structure that made sense historically but doesn’t serve readers well. A migration is a good moment to rethink it.

***

### Step 2: Set up your site skeleton

Once you know your information architecture, build the skeleton of your site before filling in any content.

* Create your spaces and set up top-level navigation
* Add placeholder pages for major sections so the structure is visible
* Don’t worry about getting the page hierarchy perfectly organized yet — you’ll adjust that as content is added

One thing to defer until later: your landing page. It’s tempting to build the home page first, but it works best as a reflection of what the site contains. Build it once the structure and content are in place.

If you have an existing docs repo or content source, this is the right moment to [sync](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/docs-as-code/git-sync) or import it. If your content is scattered across multiple places, assemble it into the right spaces before moving on.

***

### Step 3: Choose your theme

With the structure in place, it’s time to make visual decisions. The most important of these is your **theme**, because it affects the entire site — not just the header.

GitBook’s themes (such as Clean, Muted, Bold, Gradient) each set a distinct visual direction. Rather than trying to tweak individual components to get the look you want, choose the theme that’s closest to your brand’s feel, then adjust from there.

**How to pick:**

* **Clean** — minimal, no strong backgrounds; good for brands that want content front and center
* **Muted** — adds subtle tonal backgrounds; works well for brands with softer palettes
* **Bold** — stronger contrast between header and content; suits confident, high-contrast brands
* **Gradient** — adds gradient elements; works for modern SaaS brands with expressive visual identities

If you’re unsure, check your marketing site and your product interface. Look at whether headers use strong color or stay neutral, whether there’s depth and shadow in UI components, and whether the overall feel is minimal or expressive. Your docs should feel like they belong to the same family.

***

### Step 4: Set your colors and fonts

#### Colors

GitBook’s color system has two main axes: **primary** (used for CTAs and interactive elements) and **tint** (which influences backgrounds, borders, and depth).

Start by setting your primary color — this is typically your main brand color. GitBook will generate a perceptually consistent palette from it, so you don’t need to set every shade manually. For most brands, this is all you need.

If you want a two-tone look, or if you need to push dark mode backgrounds toward true black, explore the tint color setting. The tint color influences how backgrounds and borders feel across the entire site.

**Finding the right color values:** If you don’t have a brand guide handy, open your marketing site in your browser and use the inspector (right-click → Inspect, then use the color picker or look at CSS variables) to identify the exact hex values your brand uses. This is the most reliable way to get a precise match.

#### Fonts

GitBook supports custom fonts in WOFF2 format. To find out which fonts your brand uses, ask your marketing team or inspect your company’s site — the font names are typically visible in the CSS.

* **Google Fonts** are the easiest option: find the font name, and you can load it directly.
* **Licensed/custom fonts** used by your brand can often be identified via the inspector and sourced through your design team. Make sure you have the appropriate license to use them in your docs.

**Note:** GitBook requires WOFF2 format for [custom font uploads](https://app.gitbook.com/s/NkEGS7hzeqa35sMXQZ4X/manage-your-site/customization/icons-colors-and-themes#custom-fonts-ultimate-only). If you only have TTF or OTF files, free conversion tools are widely available online.

***

### Step 5: Configure component styles

With theme and colors set, work through the component-level styling options. These act as modifiers on top of your theme:

* **Sidebar style** — default (no background) or filled (adds a background). The filled style inverts appropriately on darker themes, so it works across all four.
* **Link style** — default underline, or accent color. Match what your brand uses elsewhere.
* **Icon style** — duotone icons tend to work well for most brands; match to what your brand uses in its product UI if you have a preference.
* **Corner radius** — straight or rounded. Look at buttons and cards on your marketing site to calibrate this.
* **Header buttons** — use a primary button for your main CTA, an optional secondary button for another key action, and links for anything tertiary. Avoid turning everything into a button.

Dark mode is worth considering here too. It can be a differentiating feature, but it requires more work: you need to make sure your colors, logos, and assets all hold up in dark mode before enabling it.

***

### Step 6: Build your content pages

With the structure and styling in place, fill in your content. Most pages in a GitBook site use the standard docs layout — a page with a sidebar and table of contents. This is the right choice for most reference and how-to content.

For spaces or sections that need a more visual, navigational feel, consider **landing pages**. Landing pages use a full-width layout without a sidebar, and are designed to orient readers and point them toward the right content.

A typical landing page pattern:

* A **search bar** with suggested queries to help readers find common topics quickly
* **Cards** with a header, description, and optional CTA — these are the primary building block for navigation on landing pages
* **Buttons** or links for secondary actions

Keep landing pages focused on orientation rather than content. The goal is to help readers find what they need, not to put everything on one page.

***

### Final tips

**Build landing pages last.** They work best once the rest of the site is built, because they reflect and link to the content that exists.

**Reuse a small set of components.** Cards, search bars, columns, and hint blocks cover the vast majority of what most docs sites need. Resist the urge to use every component available — consistency is more valuable than variety.

**Think about your readers’ first question.** Whatever it is — “how do I get started?”, “what does this product do?”, “where’s the API reference?” — make sure the answer is visible within one click of landing on your site.

**When in doubt, look at your marketing site, existing docs, and product UI.** And use whichever one most recently reflects your current brand. Visual identities evolve, and different surfaces update at different times.
