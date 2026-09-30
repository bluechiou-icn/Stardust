---
name: awesome-design-md
description: Catalog of ~73 DESIGN.md design-system analyses of real product sites (Apple, Stripe, Vercel, Linear, Notion, Nike, Tesla...). Use when the user wants a page or UI "in the style of <brand>", asks for a reference design system, or wants a DESIGN.md to steer UI generation. Fetch on demand; never override the repo's own brand tokens.
---

# awesome-design-md (index wrapper)

Local index for https://github.com/VoltAgent/awesome-design-md (MIT). The 73 files (~2.8 MB) are NOT vendored — fetch only the one you need.

## Use

1. Match the user's request to a slug below. Unsure → show 2–3 candidates and ask.
2. Fetch (read-only, into scratch or inline — do not write into the repo unless the user asks):
   ```bash
   curl -fsSL https://raw.githubusercontent.com/VoltAgent/awesome-design-md/main/design-md/<slug>/DESIGN.md
   ```
3. Read its YAML front-matter (colors / typography / spacing tokens) and prose rules, then apply them to the requested page.
4. If the user wants it kept, save as `DESIGN.md` (project root) or `docs/design-refs/<slug>.md`.

## Slugs

airbnb airtable apple binance bmw bmw-m bugatti cal claude clay clickhouse cohere coinbase composio cursor dell-1996 elevenlabs expo ferrari figma framer hashicorp hp ibm intercom kraken lamborghini linear.app lovable mastercard meta minimax mintlify miro mistral.ai mongodb nike nintendo-2001 notion nvidia ollama opencode.ai pinterest playstation posthog raycast renault replicate resend revolut runwayml sanity sentry shopify slack spacex spotify starbucks stripe supabase superhuman tesla theverge together.ai uber vercel vodafone voltagent warp webflow wired wise x.ai zapier

## Rules

- **Repo brand wins.** If the repo's CLAUDE.md defines brand tokens (palette, fonts, timezone, etc.), borrow only layout / rhythm / typographic ideas from the reference — do not replace the repo's tokens.
- These are style analyses of third-party sites: never copy logos, brand names, trademarks, or marketing copy.
- If a slug 404s, say so; do not substitute a different brand silently.
- Custom request for a brand not in the list: https://getdesign.md/request
