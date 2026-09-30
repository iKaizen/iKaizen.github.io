# ikaizen.github.io

Static site for iKaizen games (GitHub Pages user site).

- `/c/?l=<level>&t=<time_cs>&s=<sig>` — Color Connect challenge landing page (`c/index.html`, a real file so Pages answers HTTP 200 and chat apps build a link preview from `og.png`). Buttons by OS:
  - Android: **Open in game** (`intent://`, falls back to Play) + **Google Play** with an install referrer carrying the link, so a new player lands in the challenge after installing.
  - iOS: **Open in game** = `colorconnect://c/?l=…` (a Universal Link tapped on its own domain never opens the app) — if the page is still visible after a moment, go to the App Store · **App Store** button · note "install, then tap your friend's link again" (no deferred link on iOS). The App Store button stays hidden until `APP_STORE_ID` (and `APP_STORE_PT`, the provider token for campaign links) are filled in at the top of the script.
  - Desktop: the store buttons.
- `/c/<level>?…` — the older link form: no file, so Pages serves `404.html`, which redirects it to `/c/?l=<level>&…`.
- `og.png` (1200×630) — rendered from `og/og.html`: `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars --window-size=1200,630 --virtual-time-budget=5000 --screenshot=og.png "file://$PWD/og/og.html"`
- `/.well-known/assetlinks.json` — Android App Links verification for `com.colorconnect.flow` (`.nojekyll` keeps Pages from dropping the dot-folder). Add the **Play app signing** SHA-256 (Play Console → Test and release → App integrity) before relying on verified links in the store build.
- Link format, signature and game side: `SOCIAL_DESIGN.md` §1 in the game repo.
