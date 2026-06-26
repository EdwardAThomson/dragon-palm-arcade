# Dragon Palm Arcade

A small browser arcade for the [Dragon Palm](https://github.com/0xe25f/dragon-palm) fantasy
8-bit console — pick a cartridge from the menu and play. Hosted at a subdomain of
**octonion.io** via Cloudflare Pages.

It's a fully static site: a single `index.html` (the console emulator + a cart picker), a
`carts/` folder of `.dgc` cartridges, and a `carts.json` manifest that drives the dropdown.
No build step.

## Run locally

Any static server works (the launcher `fetch()`es `carts.json`, so `file://` won't do):

```sh
python3 -m http.server   # then open http://localhost:8000
```

## Cartridge menu

The dropdown is populated from [`carts.json`](carts.json). To add a cart: drop `name.dgc`
into `carts/` and add `{ "file": "name.dgc", "name": "Display Name" }` to the manifest.

| File | Title |
| --- | --- |
| `adder.dgc` | Adder |
| `hoard.dgc` | Dragon Hoard |
| `magic-screen.dgc` | Magic Screen |
| `tennis.dgc` | Dragon Tennis |
| `dungeon.dgc` | Dungeon Crawl |

## Deploy (Cloudflare Pages)

1. Push this repo to GitHub.
2. Cloudflare Pages → **Create project** → connect the repo.
3. Framework preset **None**, build command **(empty)**, output directory **`/`** (it's already static).
4. **Custom domains** → add the subdomain (e.g. `dragon.octonion.io`). With octonion.io's DNS on
   Cloudflare, the CNAME is created automatically.

Every push to the production branch redeploys, so adding a cart = commit + push.

## Credits & licence

The console emulator and the launcher page are based on the MIT-licensed
[Dragon Palm](https://github.com/0xe25f/dragon-palm) and
[Dragon Carts](https://github.com/0xe25f/dragon-carts) projects by 0xe25f. The bundled
`adder`, `magic-screen`, and `tennis` carts are from those projects (MIT). `hoard.dgc`
(Dragon Hoard) and `dungeon.dgc` (Dungeon Crawl, a tile RPG) are original carts by Edward
Thomson.

This repository is MIT licensed — see [LICENSE](LICENSE).
