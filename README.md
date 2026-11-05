# Quest Board landing page

This is the one-page website for [Quest Board](https://github.com/guildquests/quest-board), a quest board for teams. It is a static page styled with Tailwind CSS and hosted on GitHub Pages at https://guildquests.github.io.

## Build it

You need Node 22.

```
npm ci
npm run build
```

The build writes `public/style.css`. Open `public/index.html` in a browser to see the page. Use `npm run dev` to rebuild the CSS while you edit.

Every push to `main` deploys the `public/` folder through the GitHub Actions workflow in `.github/workflows/landing.yml`.

## Licenses

The code in this repo is released under the MIT License (see `LICENSE`). The media and fonts keep their own licenses. See `CREDITS.md`.
