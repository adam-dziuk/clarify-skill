---
name: clarify
description: Rewrites the visitor-facing text of a website into plain language (CEFR B1) directly in its source code, so ordinary, non-technical visitors understand it on first read. Works on main content — headings, paragraphs, service and product descriptions, page sections, FAQ — in HTML, templates, JSX/Vue/Svelte components, Markdown/MDX and i18n translation files, in whatever language the site uses and across all its language versions, keeping names, facts, numbers, SEO key phrases and the form of address intact. Use it whenever someone wants website text simplified, clearer, easier to read, less jargony or understandable for regular people — e.g. "uprość teksty na stronie", "klienci nie rozumieją opisu usług", "make the homepage copy easier to understand", "rewrite this for non-technical visitors" — even if they never say "plain language". Not for writing new sales copy or offers, UI microcopy, meta tags, legal documents, or simplifying code.
---

# Clarify

Rewrite a website's main content into plain language, editing its source files in place, so that a visitor with no technical or industry background understands it on first read.

Picture the reader: a busy adult who is not an expert in this field, is probably reading on a phone, and may not be a native speaker. They are not slow — they just shouldn't have to reread a sentence to learn what the company does, what it costs, or what to do next. Plain is not childish. After your rewrite, the site should still sound like the same company, only easier to follow.

## Scope

**Rewrite:** main content — headings, paragraphs, section intros, service and product descriptions, feature lists, "about us" text, FAQ questions and answers, article bodies on the pages the user picked.

**Leave alone**, even inside files you are editing:

- **UI microcopy** — buttons, navigation and footer links, form labels, placeholders and help text, validation and error messages, notifications, empty states, cookie banners.
- **Metadata and accessibility attributes** — `<title>`, meta description, Open Graph tags, `alt`, `aria-*`, `title` attributes, and SEO-only front matter fields.
- **Legal text** — terms of service, privacy and cookie policies, consent clauses under forms, regulatory disclosures. Rewording a clause can change what it means legally.
- **Quotes and testimonials** — these are words attributed to real people.
- **Code, code comments, admin screens, transactional emails.**

If the user explicitly asks you to include one of these, do it. For legal text, first say that a plain-language version can change the clause's legal effect and should be checked by whoever is responsible for it.

## Workflow

### 1. Find where the text lives

Look at the project structure before touching anything. If the user gave a URL, map its path to the route that serves it — router config, a `pages` or `app` directory, a map of localized slugs. If that isn't obvious, grep the codebase for a distinctive sentence from the page. Don't take the text from the live site: it may differ from what's in the repo.

Copy can sit in:

- markup and templates: `.html`, `.blade.php`, `.twig`, `.erb`, `.liquid`, `.hbs`, `.njk`, `.astro`
- components: `.jsx`, `.tsx`, `.vue`, `.svelte`
- content files: `.md`, `.mdx`, front matter, YAML/JSON data files (content collections, CMS exports)
- translation files: `lang/<locale>/*.php`, `lang/<locale>.json`, `locales/*.json`, `messages/*.json`, `i18n/*.yml`, `*.po`

When a component renders translation keys (`t('home.hero.title')`, `$t(...)`, `{{ 'key'|trans }}`, `__('...')`), the text lives in the translation files — edit those, not the component. Framework files such as Laravel's `validation.php`, `auth.php`, `pagination.php` and `passwords.php` are microcopy; skip them.

**Front matter** mixes content and metadata. Simplify fields that render as visible text — a `title` shown as the H1, an `excerpt`, `lead` or `summary` shown on cards. Leave `slug`, ids, dates, image paths, alt-text fields and SEO-only fields such as `seoTitle` or `metaDescription`. If a field feeds both the page and a meta tag (often `description`), check the template: if it shows on the page, treat it as content and apply the SEO key-phrase rule to it.

Every language version gets simplified. Note which locales exist so you can cover all of them.

**When the source text is the key.** Some setups use the displayed source-language sentence as the key — e.g. Laravel's `__('We offer comprehensive solutions')` with `lang/pl.json` mapping that sentence to Polish. To simplify the source-language text you have to change the key itself:

1. `grep` for the exact string across the whole codebase and find every usage.
2. Replace it in every template and rename the key in every locale file, giving each locale its own simplified value.
3. `grep` again to confirm the old string is gone.

If the key is built dynamically or is used in more places than you can safely check, stop and ask the user instead of guessing.

**When the text isn't in the code.** If the page content comes from a CMS or a database (WordPress, a headless CMS, seeded records), tell the user. Offer the rewrite as a before → after list in the step 6 format, which they can paste into the CMS. Edit seeders or fixtures only if the user confirms that's where the live content comes from.

### 2. Agree on scope

If the user named pages or files, work on those. If they didn't, don't start on the whole site — a sitewide rewrite gives a diff too big to review. Instead, make an inventory of the public pages (route or URL → source files, roughly how much text each has, which locales exist) and ask which ones to do. Use AskUserQuestion with `multiSelect` if it's available; otherwise list the pages in your reply and wait for the user's choice before editing. Recommend starting with the homepage and the pages with the most text.

Check `git status` before editing. If the project isn't under git, or the files you're about to change have uncommitted edits, tell the user: the diff is how they will review and, if needed, revert your work, and mixing your changes with theirs makes that hard. Don't commit unless asked.

### 3. Read the whole page first

Read the page — including the partials and components it pulls in — before changing a single sentence. Work out:

- **What the site offers and who it's for.** You can't simplify what you don't understand.
- **Form of address and register.** Formal ("Państwo", "Sie", "vous"), informal ("ty", "du", "tu") or impersonal; formal, warm or playful. Go with the dominant one.
- **A keep list:**
  - proper names — the company, products, services, plans, places;
  - every fact — prices, dates, opening hours, phone numbers, emails, addresses, quantities, specs, percentages, durations;
  - SEO key phrases — the main phrase in each H1 and H2. A good hint is a phrase that also appears in the `<title>`, the meta description or the URL slug. If you can't tell which part of a heading is the key phrase, leave the heading as it is.
- **Notes left next to the text.** Code comments beside a string often record a decision: a length limit, a word that has to agree grammatically with another, an SEO choice, a call the owner made. Treat these as constraints. If a simpler version would break one, leave that string alone and mention it under "Please check".
- **Text shared with other pages.** Before you edit a translation key, partial or component, grep for where else it's used. If it also appears on pages outside the agreed scope, leave it as it is and list it under "Please check", or ask the user whether to include those pages.

### 4. Rewrite

Read the section of `references/language-notes.md` for the page's language. It lists the patterns that make text hard to read in that language, with fixes. Then apply these principles:

- **One idea per sentence.** Aim for around 15 words on average and split anything over about 25.
- **Everyday words** over formal or bureaucratic ones.
- **Verbs over nouns made from verbs** — "pay", not "make a payment"; "zapłacić", not "dokonać płatności".
- **Active voice.** Say who does what: "we'll send your order", not "your order will be dispatched".
- **Main point first**, details after it.
- **Concrete over vague** — but only with facts already on the page. If the page says somewhere that you reply within 24 hours, "we reply within 24 hours" beats "we ensure fast contact". Never invent a specific detail to replace a vague one.
- **Cut filler, not information.** Filler is anything you could delete without changing what the reader learns: "in today's fast-paced world", "it is worth emphasising that", "we are a company that…", or a sentence that just repeats the one before it. If a phrase tells the reader something — a fact, a condition, a limit, a promise — it stays. When in doubt, keep it.
- **Technical terms:** if an everyday word means the same thing, use it. If the term matters — the reader will see it on an invoice or contract, or it names what they are buying — keep it and explain it in a few words where it first appears on the page. Put the explanation in body text, not in a heading, and don't repeat it every time the term comes back.
- **Keep the form of address and register.** Plain doesn't mean casual: a law firm stays formal and a playful brand stays playful. Don't switch "Państwo" to "ty", or "Sie" to "du". Within the form the site already uses, you may turn impersonal sentences into direct ones ("Istnieje możliwość…" → "Mogą Państwo…"), but only if the site already speaks to the reader somewhere. A site that is impersonal throughout stays impersonal.
- **Don't make headings longer.** They often sit in fixed-size boxes (hero, cards, tiles), so keep them the same length or shorter.

**What must survive exactly.** This is where simplification usually goes wrong, so check each rewrite against your keep list:

- **Proper names**, with the same spelling and capitalisation.
- **Numbers and facts**, with no rounding, no unit conversion and no reformatting ("1 499 zł" stays "1 499 zł").
- **Qualifiers attached to facts**: "from", "up to", "about", "usually", "on working days", "excl. VAT", "od", "do", "nawet", "około", "netto/brutto", and footnote markers like `*`. Dropping "from" in "from €99" turns a starting price into a promise.
- **The strength of each claim.** Don't turn "can help" into "will help", and don't soften a firm guarantee. Hedges carry meaning.
- **SEO key phrases in H1/H2**, word for word and in the same grammatical form. You may rephrase the rest of the heading around them.

Before moving on, check each rewritten passage: does it still say everything the original said — every fact, condition and name? Would a visitor get it on first read? Does it still sound like this company?

### 5. Edit the files without breaking them

Change only the text, never the structure:

- **Keep every tag, attribute, class, link and inline element.** If the sentence has a link or `<strong>`, the new sentence keeps that element around the matching words. Don't merge or split paragraphs or elements. Splitting a long sentence into two inside the same element is fine.
- **Keep template syntax and placeholders exactly as they are**: `{{ $var }}`, `{!! ... !!}`, `{name}`, `:attribute`, `%s`, `{{count}}`, ICU `{count, plural, ...}` and Laravel pluralisation `"one|many"` / `"{0} ...|[1,*] ..."`, including every plural branch.
- **Keep tags inside translation strings**: rich-text tags such as `<0>…</0>` (react-i18next `Trans`), `<b>…</b>` or `<link>…</link>` (next-intl `t.rich`), and raw HTML in strings rendered with `set:html`, `v-html`, `dangerouslySetInnerHTML` or `{!! !!}`. Treat them like inline elements in markup: each tag stays around the matching words.
- **Respect the file's escaping**: quotes inside JSON, PHP and JS strings, apostrophes in JSX text (`&apos;` or `{"'"}`), HTML entities, YAML quoting.
- **Keep the site's typographic conventions.** If it puts `&nbsp;` after single-letter words (common in Polish: `w&nbsp;`, `z&nbsp;`) or uses particular quote and dash styles, use them in your new text too.
- **Make exact, local replacements** with Edit. Don't reformat, re-indent or run formatters on the files.
- **Simplify each language version in its own language**, starting from its own text, not by translating your new version of another locale. Keep the versions in step, though: if you cut a filler sentence in one, cut its counterpart in the others, so every version still tells the reader the same things.

After editing, run cheap checks on the files you touched: parse JSON and YAML, run `php -l` on PHP files, and if you renamed source-string keys, grep for the old strings. If you changed JSX/Vue/Svelte files and the project has a quick lint, typecheck or build script, run it. Fix whatever breaks, and report anything you couldn't fix.

### 6. Report

Write the report in the language the user is speaking to you in. The full list of changes is the point: it's how the user reviews your work without opening every file. Use this structure:

```markdown
## Summary
Pages/files: …, changes: N, language versions: pl, en

## Please check
- <judgement calls the user should confirm: a sentence you cut as filler, a term
  explanation that depends on business details, an ambiguous original>

## Changes

### resources/views/home.blade.php

1. **Before:** <full original sentence or passage>
   **After:** <full rewritten sentence or passage>

2. **Before:** …
   **After:** …

### lang/en.json
…

## Left unchanged on purpose
- <things in the edited files you skipped and why: legal clause, testimonial,
  heading with an unclear SEO phrase, microcopy>
```

Quote whole sentences or passages, not fragments, so each pair makes sense on its own. "Please check" goes before the change list so it doesn't get buried when the list is long. If there's nothing to flag, say so in one line.
