# xinzuo.com.au Liquid theme — TYICDI hiring task snapshot

This is the sanitized Shopify theme powering [xinzuo.com.au](https://xinzuo.com.au), shared for the **TYICDI developer hiring task**.

## What's here

Standard Shopify theme structure:

- `sections/` — Liquid section files (header, hero, collection-list, footer, etc.)
- `snippets/` — reusable Liquid partials
- `blocks/` — block-level Liquid components
- `templates/` — JSON page templates (which sections appear on which page)
- `layout/` — `theme.liquid` wrapper
- `assets/` — CSS, JS, fonts, SVGs the theme ships
- `config/` — `settings_schema.json` (theme customizer schema) + `settings_data.json` (current settings)
- `locales/` — translation strings

## What's NOT here (and why)

- No `.env` — never been in the theme
- No admin scripts or internal tooling — those live outside the theme and aren't part of what a dev would edit
- No backups, audit folders, blog drafts, screenshots — repo cleanliness only
- No app credentials, webhook URLs, API tokens — verified via grep before push

In short: this is what you'd see if you ran `shopify theme pull` against a fresh Shopify store on the same theme code, minus things that don't belong in a theme repo.

## How to use this for the hiring task

1. Clone this repo.
2. Optional but useful: install [Shopify CLI](https://shopify.dev/docs/themes/tools/cli) and run `shopify theme dev` against a free Shopify Partner dev store you create. That'll boot a local preview server so you can see your fix render against real Shopify data.
3. Edit any Liquid / CSS / JS / JSON file to demonstrate your proposed fix.
4. Commit your fix to your OWN public GitHub repo (NOT this one) per the brief.

If you don't want to set up Shopify CLI: edit the files anyway, take screenshots from the live xinzuo.com.au site as the "before", and we'll read your diff. The eye-test for engineering judgment doesn't require a running dev store.

## License

This code is shared **solely for the TYICDI developer hiring task**. Brand, product imagery, and store content are © Xinzuo Australia / Told You I Could Do It. Do not redistribute, fork for commercial use, or use as the basis for any other project.
