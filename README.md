# starsplit

The public site for **Starsplit**, a cosmic match-3 for iPhone and iPad. Static files,
served by GitHub Pages at **starsplit.app**:

| file | why it exists |
|---|---|
| `index.html` | the game |
| `privacy.html` | the **Privacy Policy URL** App Store Connect requires |
| `support.html` | the **Support URL** App Store Connect requires |
| `app-ads.txt` | **AdMob's verification file.** Only works at the domain ROOT — see below |
| `CNAME` | what points Pages at the custom domain. **Deleting it breaks ad serving** |

No build step, no dependencies. Edit and push; Pages serves it.

## Status: live

Pages is on, serving from `main` at the repository root, and the contact address is real.

```
https://starsplit.app/             → App Store "Marketing URL"
https://starsplit.app/privacy.html → App Store "Privacy Policy URL" (required)
https://starsplit.app/support.html → App Store "Support URL" (required)
https://starsplit.app/app-ads.txt  → AdMob authorised-sellers verification
```

## The domain is load-bearing, in two ways at once

**`app-ads.txt` only counts at the root of the host.** Google crawls
`https://<hostname>/app-ads.txt` and strips the path — *"paths like example.com/myapp/app-ads.txt
will not work"*. This was a GitHub **project**-pages site at `isaacfrett.github.io/starsplit/`,
and a project repo can only ever serve under `/<repo>/`, so the file was unservable where the
crawler looks. The custom domain makes this repo's root the domain root, which fixes it without
renaming the repo or moving any page.

So two separate App Store obligations now ride on one domain — the privacy policy and ad
verification. **If `starsplit.app` lapses, ads stop filling and a required listing field 404s.**
Keep auto-renew on. Same for the `CNAME` file: remove it and everything silently reverts to
`isaacfrett.github.io/starsplit/`, where `app-ads.txt` is unreachable again — a failure that would
surface months later as ads mysteriously dying.

The old `isaacfrett.github.io/starsplit/*` URLs 301-redirect here, so links already in the wild
keep working.

**Apple checks that these resolve**, and a Support URL that 404s is a rejection rather than a
note. Load all three after any change to this repo, not just the one that was edited.

Pages is served from a CDN and gets indexed, so anything published here outlives being fixed —
which is why the contact address was put in before Pages went on rather than after.

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
