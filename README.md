# tses89214.github.io

Personal site of Jia Xuan (Po) Jian (簡嘉炫), a senior data engineer: <https://tses89214.github.io>

Built with [Hugo](https://gohugo.io/) (extended) and the [Blowfish](https://blowfish.page/) theme, deployed to GitHub Pages by `.github/workflows/hugo.yml` on every push to `main`.

## Layout

- `content/`: pages in Traditional Chinese (`*.zh-tw.md`, default) and English (`*.en.md`): About, Projects, Blogs.
- `content/projects/`: one file per project; each card links straight to its Medium article or GitHub repo through `externalUrl`.
- `config/_default/`: site settings; profile, headline and links are in `languages.*.toml`, menus in `menus.*.toml`.
- `assets/css/custom.css`: small layout overrides (centering, content width).
- `static/`: favicon set and the English resume (`Po-Jian-Resume-EN.pdf`).

## Run locally

```
git clone --recurse-submodules https://github.com/tses89214/tses89214.github.io
cd tses89214.github.io
hugo server
```

The theme is a git submodule (`themes/blowfish`), so clone with `--recurse-submodules`.
