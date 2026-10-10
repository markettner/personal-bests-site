# Site redesign — handoff notes

New home page and a new features page, ported from the Design canvas ("C · Home page" / "C · Features page").
`index.html` has been replaced by the redesigned home page (the previous version is in git history, last committed in `2f73954`).

## Files

| File | Status | Purpose |
|---|---|---|
| `index.html` | replaced | Redesigned home page. |
| `features.html` | new | Full features page, linked from home ("See all features", nav "Features"). |
| `styles.css` | new | Shared stylesheet for all four pages. |
| `privacy_policy.html`, `support.html` | rewritten | Moved onto `styles.css` (new nav, kicker + headline, `.prose-card` sections). Privacy policy rewritten for iCloud sync, Apple Intelligence and the website (10 October 2026). |

No build step, no framework. The only JS is the iPhone / iPad / Mac switcher at the bottom of `features.html`.

## Brand (fixed — don't change)

- Font: **Lexend** (Google Fonts), weights 400–800. 800 is new, used for big headlines.
- Background: `linear-gradient(165deg, #1a1a2e 0%, #16213e 40%, #0f3460 100%)`.
- Brand gradient (headline accents, step numbers, CTA card): `linear-gradient(135deg, #ffd700 0%, #ff6b6b 50%, #ee5a24 100%)` → `.gradient-text` / `--brand-gradient`.
- Gold `#ffd700` for section headings, tile titles, check icons, "New" badges.
- Text white at 100 / 82 / 70 / 50 % opacity. Glass surfaces `rgba(255,255,255,.06–.1)` with `rgba(255,255,255,.1–.15)` borders.
- Pills and buttons: `border-radius: 50px`. Cards: 16 px (small), 28–32 px (large).
- All tokens live in `:root` in `styles.css`.

## Still to do

### Screenshots
Every `.shot` element is a placeholder. Replace its text with an `<img>` (CSS already handles `.shot img` → cover):

- `index.html`: hero iPhone (`.phone`), plus one per highlight (Discover, Rank, Private & everywhere).
- `features.html`: one per spotlight (6: Discover, Rank, Map, Clean up, Recap, Stay on top), plus the iPhone / iPad / Mac frames in the device switcher (`.device-frame.iphone|ipad|mac`; aspect ratios ≈ 220×450, 440×320, 520×330). Each placeholder's text says what it should show.

### Copy
All copy is written (source: `Personal Bests/docs/feature-list.md` in the app repo). Remaining: `[RELEASE DATE]` for 1.2 in the features changelog. "New" badges (spotlights 03–05 and the tiles) and the "New in 1.2" header pill will need removing or updating with the next release; the home page is deliberately release-agnostic.

### Layout details worth keeping
- Headline gradient phrases use `.nowrap` so they never split across lines; both headlines were swept at 320–1600 px with no overflow. Below 600 px the headline sizes scale with the viewport (`styles.css`, the 600 px media query) so no single word ends up alone on a line.
- `features.html` forces the break after "Every feature," with a `<br>`.
- The CTA card is optically centred (`--cta-optical`): content shifts down up to 11 px on wide screens, where the wide headline makes it top-heavy, and stays geometrically centred on phones. The reasoning is in the comment above `.cta-card`.

Adding or removing a spotlight: copy a `<section class="wrap spot">` block; add `reverse` to alternate the image side; update the numbers and the jump-nav pills in the page header.

### Before going live
- Lexend is self-hosted (`fonts/`, licence in `fonts/Lexend-OFL.txt`); no page requests anything from Google.
- If any third-party resource is ever added (fonts, analytics, embeds), update the privacy policy's "This website" section.
- Optional: give `features.html` its own OG image.

## Checked
Both pages render without horizontal scroll at 1440 px and 390 px, and the device switcher toggles correctly.
