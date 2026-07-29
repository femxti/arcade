# The Arcade — on GitHub Pages

Everything here is static: plain HTML files, no build step, no dependencies.
That is exactly what GitHub Pages serves, so publishing takes a couple of minutes.

```
index.html          the landing page linking every game
games/*.html        the games, one self-contained file each
```

## Publish it (browser only, no git needed)

1. On github.com click **+ → New repository**. Name it e.g. `arcade`.
   Make it **Public** — free GitHub Pages only serves public repos.
2. On the empty repo page click **uploading an existing file**.
3. Drag in `index.html` AND the whole `games` folder. Commit.
4. **Settings → Pages**. Under *Build and deployment* set
   Source = **Deploy from a branch**, Branch = **main**, folder = **/ (root)**. Save.
5. Wait about a minute. The site appears at
   `https://<your-username>.github.io/arcade/`

To update a game later, open the file on GitHub, click the pencil, paste the
new version, commit. Pages redeploys on its own.

## If you prefer git

```bash
git init
git add .
git commit -m "The arcade"
git branch -M main
git remote add origin https://github.com/<your-username>/arcade.git
git push -u origin main
```
Then do step 4 above.

## About the high score table

GitHub Pages serves files and nothing else — it cannot run server code.
So the shared leaderboard cannot live here. In this copy of Ghost Hunter
`SCORE_API` is set to `''`, which means the Hall of Hunters is saved
**per device**: your phone keeps your table, another phone keeps its own.
For a family arcade that is usually what you want anyway.

### If you do want one shared table
Keep the games on GitHub Pages and put only the tiny scores function
somewhere that runs code. The function already sends open CORS headers,
so it works from another domain:

1. Deploy the `ghost-hunter-netlify` package (free tier is plenty).
2. In `games/ghost-hunter.html` find the `SCORE_API` line near the top of
   the script and set it to the full URL:
   `const SCORE_API = 'https://your-site.netlify.app/api/scores';`
3. Commit. GitHub Pages hosts the arcade, Netlify answers for the board.

Cloudflare Pages is the other option worth knowing: unlike GitHub Pages it
serves static files *and* runs functions, so it could host both halves alone.

## Phones
Open the site in the browser and use **Add to Home Screen**. The games run
fullscreen and work offline once loaded.
