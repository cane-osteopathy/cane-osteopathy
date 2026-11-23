# Cane Osteopathy — static site

This directory is a self-contained static export of the legacy PHP site. It can
be served by any static file host, including GitHub Pages.

## Preview locally

Run an HTTP server from this directory so that the pretty URLs
(`about/`, `treatments/`, etc.) resolve to their `index.html` files:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

Do not open `index.html` directly with `file://`; the directory URLs will not
work without an HTTP server.

## Minify the CSS

The readable stylesheet source is `css/app.unminified.css`. The stylesheet used
by the site is the minified `css/app.css`.

Edit `css/app.unminified.css`, then rebuild `css/app.css` with
[clean-css-cli](https://github.com/clean-css/clean-css-cli):

```sh
npx --yes clean-css-cli@5 -o css/app.css css/app.unminified.css
```

Or install it globally:

```sh
npm install -g clean-css-cli
cleancss -o css/app.css css/app.unminified.css
```

If you do not have Node.js locally, you can run the minifier with Docker:

```sh
docker run --rm -v "$PWD/css":/css node:20-bookworm-slim \
  sh -c 'npx --yes clean-css-cli@5 -o /css/app.css /css/app.unminified.css'
```

After minifying, reload the local preview to check your changes.

## Deployment

The directory already includes `.nojekyll` for GitHub Pages. Publish the
contents of this directory as the site root (or copy them into the root of a
dedicated GitHub Pages repository).
