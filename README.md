# starsplit

The public site for **Starsplit**, a cosmic match-3 for iPhone and iPad. Three static pages,
served by GitHub Pages:

| page | why it exists |
|---|---|
| `index.html` | the game |
| `privacy.html` | the **Privacy Policy URL** App Store Connect requires |
| `support.html` | the **Support URL** App Store Connect requires |

No build step, no dependencies. Edit the HTML and push; Pages serves it.

## Status: not live yet — GitHub Pages is deliberately OFF

The repo is public so that Pages *can* serve it, but Pages has not been switched on, because
the contact address is still a placeholder and a privacy policy published with a placeholder
contact is worse than no page at all.

**Step 1 — replace `[SUPPORT-EMAIL]`.** It is the only placeholder in the repo, and it appears
three times (once in `privacy.html`, twice in `support.html`):

```bash
grep -rn "\[SUPPORT-EMAIL\]" .
```

**Step 2 — turn Pages on.** Settings → Pages → Source: deploy from branch, `main`, `/` (root).
The pages then land at:

```
https://isaacfrett.github.io/starsplit/            → App Store "Marketing URL" (optional)
https://isaacfrett.github.io/starsplit/privacy.html → App Store "Privacy Policy URL" (required)
https://isaacfrett.github.io/starsplit/support.html → App Store "Support URL" (required)
```

Do them in that order. Pages is served from a CDN and gets indexed, so a placeholder that goes
up is a placeholder that stays in caches after it is fixed.

## Keeping the privacy policy true

`privacy.html` says Starsplit collects nothing, sends nothing, and contains no network code.
That is currently a checkable fact about the app, not a promise — the game has no HTTP client,
no analytics, no advertising SDK, and writes its save to the app's own sandbox.

The game does have **`Ads` and `Iap` interfaces wired up behind debug-only stubs**, and a
release build constructs neither a live ad network nor a live store. The day either becomes
real, this page stops being true. Update it — and the date at the top — *before* that build
ships, not after.

## Design

The palette is the game's own (`scripts/view/pal.gd`: `SPACE`, `PANEL`, `PANEL_EDGE`, `TEXT`,
`MUTED`, `GOLD`), so the site and the app read as one place. The four grids on the front page
are the star split's footprints, drawn the way `SplitPopup` draws them in game — as the shape
each option *clears*, rather than as a picture of its two ingredients.
