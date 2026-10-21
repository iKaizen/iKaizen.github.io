# ikaizen.github.io

Static site for iKaizen games (GitHub Pages user site).

- `/c/<level>/?l=<level>&t=<time_cs>&s=<sig>` — Color Connect challenge page for levels 1–2000 (`c/<level>/index.html`), whose link preview is that level's unsolved board (`og/<level>.png`, 600×315). **Generated — don't edit by hand:** edit the template `c/index.html`, then in the game repo run `python3 tools/build_og_pages.py <this repo> --to 2000` (cards from `tools/render_og_levels.gd`).
- `/c/?l=<level>&t=<time_cs>&s=<sig>` — the same page for levels beyond that range (`c/index.html`, preview `og.png`). A real file so Pages answers HTTP 200 and chat apps build a link preview. Buttons by OS:
  - Android: **Open in game** (`intent://`, falls back to Play) + **Google Play** with an install referrer carrying the link, so a new player lands in the challenge after installing.
  - iOS: **Open in game** = `izecolorconnect://c/?l=…` (a Universal Link tapped on its own domain never opens the app) — if the page is still visible after a moment, go to the App Store · **App Store** button · note "install, then tap your friend's link again" (no deferred link on iOS). The App Store button stays hidden until `APP_STORE_ID` (and `APP_STORE_PT`, the provider token for campaign links) are filled in at the top of the script.
  - Desktop: the store buttons.
- `/c/<level>?…` — the older link form: for levels 1–2000 Pages redirects it to `/c/<level>/`, and the page copies the level from the path into `?l=`; beyond that there is no file, so Pages serves `404.html`, which redirects it to `/c/?l=<level>&…`.
- `og.png` (1200×630) — generic link-preview image for levels without their own card (an unsolved board with a "?": the game shares text + link only, so this card is the picture friends see). Rendered by the game repo: `Godot --path . --script tools/render_og.gd` → `store/og.png`, copied here.
- `/.well-known/assetlinks.json` — Android App Links verification for `com.colorconnect.flow` (`.nojekyll` keeps Pages from dropping the dot-folder). SHA-256s: Play app signing key (store installs), upload key, debug key (dev builds) — Play Console → Protected by Google Play → App signing.
- `/.well-known/apple-app-site-association` — iOS Universal Links: `VN246TCC33.com.colorconnect.flow`, paths `/c/*`.
- `/app-ads.txt` — AdMob seller line for publisher `pub-8841516934558170`. The store listings' developer website must be `https://ikaizen.github.io` for AdMob to find it.
- Link format, signature and game side: `SOCIAL_DESIGN.md` §1 in the game repo.
