# starsplit

The public site for **Starsplit**, a cosmic match-3 for iPhone and iPad. Three static pages,
served by GitHub Pages:

| page | why it exists |
|---|---|
| `index.html` | the game |
| `privacy.html` | the **Privacy Policy URL** App Store Connect requires |
| `support.html` | the **Support URL** App Store Connect requires |

No build step, no dependencies. Edit the HTML and push; Pages serves it.

## Before this goes live

**Replace `[SUPPORT-EMAIL]`.** It appears on the privacy and support pages and is the only
placeholder in the repo:

```bash
grep -rn "\[SUPPORT-EMAIL\]" .        # find them
```

Then, in the repo's **Settings → Pages**, set the source to the `main` branch root. The pages
land at `https://<user>.github.io/starsplit/`.

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
