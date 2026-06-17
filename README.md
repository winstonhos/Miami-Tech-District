# WynTech — An Open Map of the Wynwood Tech District

WynTech is a free, open map and microsite for Wynwood, Miami's tech district. It plots the tech companies, startups, and funds that have set up in the neighborhood, tells the story of how Wynwood went from warehouses to a tech hub, and shows the growth behind it. Anyone can use it, fork it, embed it, or help keep it accurate.

It's built and maintained by [The LAB Miami](https://thelabmiami.com), the coworking space that has anchored Wynwood's tech community since 2012.

**Live site:** https://winstonhos.github.io/  *(update this link to match your repo's GitHub Pages URL)*

---

## Why this exists

Wynwood didn't get handed a tech scene. The people who built one showed up because the neighborhood already had something. WynTech is meant to be a public record of that, kept open on purpose. The map is more useful when the whole community can see it, correct it, and build on it, so the code is free for anyone to use.

## What's in here

| File | What it is |
|------|------------|
| `index.html` | The main site — hero, the map, the growth charts, the numbers, and the case for Wynwood. This is the homepage. |
| `wyntechsidepagev1.html` | "The Start" — the history of Wynwood as an interactive timeline, from the 1920s warehouses to today. |
| `wyntechmapv1.html` | The interactive company map (Mapbox). Self-contained, with its own data built in. Embedded inside `index.html` and also works on its own. |
| `wyntechgrowthchartv1.html` | The growth charts (Chart.js) — visitors, businesses, housing, office space, and public funding over time. Embedded inside `index.html`. |

The map and the charts are standalone HTML files. The main site pulls them in as embeds, but each one opens and works on its own too.

## The map

The map plots verified Wynwood companies and lets you filter them by category:

- **Tech** — startups and tech companies
- **VC** — venture firms and funds
- **Finance** — fintech and financial services
- **Media** — media and creative companies
- **Coworking** — shared workspaces, including The LAB
- **Legal** — law firms serving the district

Each pin is a real, address-verified location. Companies we haven't been able to verify an address for still show up in a separate unverified list inside the map, rather than being plotted.

## Using it

Everything here is static HTML, CSS, and JavaScript. There's no build step and no framework.

**View it live:** just open the GitHub Pages URL above.

**Run it locally:** the map's own data is built directly into the file, so it works the moment you open it, no server needed for that part. The map tiles themselves (Mapbox) and the growth charts (Chart.js) still need a real internet connection either way, since those load from external CDNs regardless of how you're viewing the page.

If you want the most reliable local setup (matching exactly how it'll behave once hosted):

```bash
# from the folder that holds these files
python3 -m http.server 8000
```

Then open `http://localhost:8000/` in your browser.

**Host it yourself:** drop all the files into any static host — GitHub Pages, Netlify, Cloudflare Pages, Vercel — and it works as-is. Keep all four HTML files (`index.html`, `wyntechsidepagev1.html`, `wyntechmapv1.html`, `wyntechgrowthchartv1.html`) in the same folder so the links between them resolve.

## Map setup (Mapbox token)

The map runs on [Mapbox GL JS](https://www.mapbox.com/) and needs an access token to render. The token committed in `wyntechmapv1.html` is restricted on the Mapbox dashboard to WynTech's own domain, so it's safe to be public, the restriction is what protects the account, not secrecy.

**If you're forking this project to deploy on your own domain, that token won't work for you.** You'll need your own:

1. Create a free account at [mapbox.com](https://www.mapbox.com) (the free tier covers far more usage than this project needs).
2. Copy your public token from the Access Tokens page.
3. In `wyntechmapv1.html`, find the line `mapboxgl.accessToken = '...'` near the top of the script and swap in your token.
4. Add a URL restriction on that token scoped to your own domain, so usage stays tied to your deployment.

## Embedding the map elsewhere

The map is a self-contained file with its data built in, so you can drop it into your own site with just an iframe, no other files needed alongside it:

```html
<iframe
  src="wyntechmapv1.html"
  title="Wynwood Tech Map"
  style="width:100%; height:600px; border:0;"
  loading="lazy">
</iframe>
```

The growth charts work the same way with `wyntechgrowthchartv1.html`.

## Contributing

The map is only as good as the data behind it, and the community knows the neighborhood better than any single list. Spotted a missing company, a wrong category, or an address that's changed? You don't need permission to flag it.

**Open an issue** describing what's wrong or what's missing, the company name, category, and address if you have one. It'll get reviewed and the map updated.

**Or open a pull request** if you're comfortable editing `wyntechmapv1.html` directly, the company data sits near the top of its script, in a `companies` array.

## Built with

- [Mapbox GL JS](https://www.mapbox.com/) `v2.15.0` — the interactive map
- [Chart.js](https://www.chartjs.org/) `v4.4.0` and the annotation plugin `v3.0.1` — the growth charts
- Plain HTML, CSS, and JavaScript — no framework, no build step

Mapbox and Chart.js load from their public CDNs, so the map and charts need an internet connection to render.

## License

Released under the MIT License — free to use, copy, modify, and build on, including commercially. See [`LICENSE`](LICENSE) for the full text.

## Credits

Made and maintained by [The LAB Miami](https://thelabmiami.com). Data compiled from public sources and on-the-ground verification, with figures drawn from the Wynwood BID, Refresh Miami, Commercial Property Executive, the Miami Herald, and individual firm disclosures.
