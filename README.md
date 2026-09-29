# ikaizen.github.io

Static site for iKaizen games (GitHub Pages user site).

- `/c/<level>` — Color Connect challenge landing page. There are no files under `/c/`: GitHub Pages serves `404.html` for every unknown path, and its script reads the level/time from the URL. Buttons: **Open in game** (Android `intent://`, falls back to the store) and **Google Play** with an install referrer carrying the link, so a new player lands in the challenge after installing.
- `/.well-known/assetlinks.json` — Android App Links verification for `com.colorconnect.flow` (`.nojekyll` keeps Pages from dropping the dot-folder). Add the **Play app signing** SHA-256 (Play Console → Test and release → App integrity) before relying on verified links in the store build.
- Link format, signature and game side: `SOCIAL_DESIGN.md` §1 in the game repo.
