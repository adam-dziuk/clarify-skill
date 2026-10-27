# clarify-skill

A Claude Code plugin that rewrites the main content of a website into plain language (CEFR B1), so ordinary, non-technical visitors understand it on first read.

The `clarify` skill edits the site's source files in place: HTML, templates (Blade, Twig, Liquid…), JSX/Vue/Svelte components, Markdown/MDX and i18n translation files. It works in whatever language the site is written in and simplifies every language version. It keeps intact:

- proper names (company, products, services, plans),
- facts and numbers, together with their qualifiers ("from €99", "on working days"),
- SEO key phrases in H1/H2,
- the site's form of address and tone,
- markup, template syntax and translation placeholders.

Technical terms that matter are kept and explained in a few words where they first appear. UI microcopy, meta tags, `alt` text, legal documents and testimonials are left alone.

When you don't name specific pages, the skill lists the site's pages and asks where to start. When it's done, it reports every change as a before → after pair, flags its judgement calls for you to check, and lists what it skipped on purpose.

## Install

```
/plugin marketplace add adam-dziuk/clarify-skill
/plugin install clarify-skill@clarify-skill
```

For development, load it for a single session with `claude --plugin-dir /path/to/clarify-skill`.

## Usage

Ask in your own words, for example "uprość teksty na stronie głównej" or "make the services page easier to understand for regular people". You can also call the skill directly as `clarify-skill:clarify`.

## License

[MIT](LICENSE)
