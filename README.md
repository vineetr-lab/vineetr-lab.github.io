# kb-sync test site

> Published as a **user site** (`vineetr-lab.github.io`) rather than a project site, and that is
> not cosmetic. Sitemap discovery is ORIGIN-scoped: `robots.txt` lives at the origin root by spec,
> and the well-known sitemap paths are origin-relative. A GitHub *project* site lives at
> `vineetr-lab.github.io/<repo>/`, so its `robots.txt` and `sitemap.xml` sit at a subpath where no
> discovery will look — `https://vineetr-lab.github.io/robots.txt` simply 404s. The first attempt
> at this site was a project site and could not be discovered at all.

A deliberately boring static site for exercising knowledge-base **website import and sync**.

Published with GitHub Pages. Four pages and a **generated** `sitemap.xml`.

The sitemap is built by `.github/workflows/pages.yml`, which takes each page's
`<lastmod>` from that file's own last commit. That detail is the whole point: a
hand-written sitemap has a frozen `lastmod`, so a sync takes its cheap path and
never notices an edit; a sitemap stamped with build time marks every page as
touched on every deploy, so nothing is ever skipped. Per-file git dates are what a
real generator produces, and they make **"edit one page, re-fetch exactly one
page"** actually true.

## Using it

1. Discover `vineetr-lab.github.io/kb-sync-test-site` and import the four pages.
2. Sync once — everything reports `unchanged`, baselines are stamped, nothing uploads.
3. **Edit `pricing.html`** in the GitHub UI, commit, wait ~30s for the deploy.
4. Sync again — that one page reports `updatedContent`; the others stay `unchanged`,
   and the crawl log shows **one** request rather than four.
5. **Delete `changelog.html`** and sync — it reports `removed` (the page 404s).

`security.html` is the control: it should never change.
