# Kakkerlak

A clickable web prototype of the Kakkerlak app. It is a static site with no build step: `index.html` plus `assets/`.

All asset paths are relative, so the site works from any subpath, e.g. `https://<user>.github.io/kakkerlak/`.

## Run locally

```sh
python3 -m http.server
```

Then open http://localhost:8000/.

## Host on GitHub Pages

1. Push this folder to a repo (e.g. `kakkerlak`).
2. Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The site will be at `https://<user>.github.io/<repo>/`.

`.nojekyll` stops GitHub Pages from running Jekyll over the files.
