# jimsander.net

Personal site for Jim Sander. Plain static HTML and CSS. No build step, no CMS, no tracking.

Replaces an old WordPress install.

## Layout

| Path | What |
|---|---|
| `index.html` | Home page |
| `why-not-linkedin.html` | Article: "FU LinkedIn." |
| `style.css` | Shared theme for every page |
| `img/` | Screenshots used in the article. Personal details blurred before commit. |
| `media/` | Popcorn clips. Short silent loop for the home page; full clip with sound for the article. |

## Preview locally

Open `index.html` in a browser. All links are relative, so it works straight from disk.

## Deploy

Hosted on Cloudflare Pages, project `jimsander-net`. Deployed by direct upload of the site files:

```bash
D=$(mktemp -d)
cp -R index.html why-not-linkedin.html style.css img media "$D"/
source ~/.cloudflare/pages-ci-token.env
CLOUDFLARE_ACCOUNT_ID=<account-id> npx wrangler@3 pages deploy "$D" --project-name jimsander-net --branch main
```

- Use `wrangler@3`. Newer wrangler routes Pages through Workers and fails with a Pages-only token.
- Preview URL: [jimsander-net.pages.dev](https://jimsander-net.pages.dev/)

## Adding a page

- Copy an existing page so it picks up the header, the privacy scroller, and the footer.
- Give each `h2` an `id` and list it in the page's contents block.
- Add the new file to the `cp` line above.
