# WynTech — An Open Map of the Wynwood Tech District

WynTech is a free, open map and microsite for Wynwood, Miami's tech district. It plots the tech companies, startups, and funds that have set up in the neighborhood, tells the story of how Wynwood went from warehouses to a tech hub, and shows the growth behind it. Anyone can use it, fork it, embed it, or help keep it accurate.

It's built and maintained by [The LAB Miami](https://thelabmiami.com), the coworking space that has anchored Wynwood's tech community since 2012.

**Live site:** https://winstonhos.github.io/  *(update this link to match your repo's GitHub Pages URL)*

---

## Why this exists

Wynwood didn't get handed a tech scene. The people who built one showed up because the neighborhood already had something. WynTech is meant to be a public record of that, kept open on purpose. The map is more useful when the whole community can see it, correct it, and build on it, so the data and the code are free for anyone to use.

## What's in here

| File | What it is |
|------|------------|
| `index.html` | The main site — hero, the map, the growth charts, the numbers, and the case for Wynwood. This is the homepage. |
| `wyntechsidepagev1.html` | "The Start" — the history of Wynwood as an interactive timeline, from the 1920s warehouses to today. |
| `wyntechmapv1.html` | The interactive company map (Mapbox). Embedded inside `index.html` and also works on its own. |
| `wyntechgrowthchartv1.html` | The growth charts (Chart.js) — visitors, businesses, housing, office space, and public funding over time. Embedded inside `index.html`. |
| `companies.json` | **The open dataset.** Every company on the map, verified and unverified, with category, address, coordinates, and basic financials. The map reads this file directly. This is the file to edit if you're adding or correcting a company. |

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

All of this comes from `companies.json`, a single open file separate from the map's code. Anyone can read it, reuse it in their own project, or open a pull request to fix it. See [Contributing](#contributing) below for the exact format.

## Using it

Everything here is static HTML, CSS, and JavaScript. There's no build step and no framework.

**View it live:** just open the GitHub Pages URL above.

**Run it locally:** because the pages embed each other and the map loads its data with `fetch()`, opening `index.html` straight off your computer won't work (browsers block local file embeds and local file fetches for security — this is also what causes a blank map if you skip this step). Run a tiny local server instead:

```bash
# from the folder that holds these files
python3 -m http.server 8000
```

Then open `http://localhost:8000/` in your browser.

**Host it yourself:** drop all the files into any static host — GitHub Pages, Netlify, Cloudflare Pages, Vercel — and it works as-is. Keep all five files (`index.html`, `wyntechsidepagev1.html`, `wyntechmapv1.html`, `wyntechgrowthchartv1.html`, `companies.json`) in the same folder so the links and the data fetch resolve.

## Map setup (Mapbox token)

The map runs on [Mapbox GL JS](https://www.mapbox.com/) and needs an access token to render. The token committed in `wyntechmapv1.html` is restricted on the Mapbox dashboard to WynTech's own domain, so it's safe to be public, the restriction is what protects the account, not secrecy.

**If you're forking this project to deploy on your own domain, that token won't work for you.** You'll need your own:

1. Create a free account at [mapbox.com](https://www.mapbox.com) (the free tier covers far more usage than this project needs).
2. Copy your public token from the Access Tokens page.
3. In `wyntechmapv1.html`, find the line `mapboxgl.accessToken = '...'` near the top of the script and swap in your token.
4. Add a URL restriction on that token scoped to your own domain, so usage stays tied to your deployment.

## Embedding the map elsewhere

The map is a self-contained file, so you can drop it into your own site with an iframe. It needs `companies.json` to sit alongside it (same folder, same host) since that's where it loads its data from:

```html
<iframe
  src="wyntechmapv1.html"
  title="Wynwood Tech Map"
  style="width:100%; height:600px; border:0;"
  loading="lazy">
</iframe>
```

The growth charts work the same way with `wyntechgrowthchartv1.html` and don't need `companies.json`.

## Contributing

The map is only as good as the data behind it, and the community knows the neighborhood better than any single list. Spotted a missing company, a wrong category, or an address that's changed? You don't need permission to fix it, and you don't need to touch any code.

**The fastest way — open an issue.** There's a short form for it, just hit "New issue" on the repo and pick "Add or correct a company." It asks for the name, category, and address, nothing else required.

**The direct way — edit `companies.json` yourself and open a pull request.** It's plain JSON, no build step, no code to run. Each company looks like this:

```json
{
  "name": "Example Co",
  "category": "Tech",
  "address": "123 NW 26th St, Miami FL 33127",
  "lat": 25.801100,
  "lng": -80.204411,
  "domain": "example.com",
  "verified": true,
  "worth": "Private — undisclosed",
  "traded": "Private",
  "movedYear": "2024"
}
```

A few rules that keep the data useful:

- **`verified` should be `true` only if you can point to a real, confirmed Wynwood street address.** If you're reporting a company that's said to be in Wynwood but you can't confirm the address, set `verified: false` and leave `address`, `lat`, and `lng` as `null`. It'll show up in the map's unverified list instead of getting a pin, that's intentional, it keeps unconfirmed info from looking as solid as confirmed info.
- **`category` must be one of:** `Tech`, `VC`, `Finance`, `Media`, `Coworking`, `Legal`. Open an issue first if you think a new category is needed.
- **`lat`/`lng`** should come from an actual geocode of the address, not an eyeballed guess. Google Maps or Mapbox's own geocoder both work, right-click a pin and copy the coordinates.
- Fields you don't know can be `null` (for `worth`, `traded`, `movedYear`) rather than left out entirely, the map expects every field to be present even if empty.

No permission needed for any of this. Open the PR, and it'll get reviewed and merged.

## Built with

- [Mapbox GL JS](https://www.mapbox.com/) `v2.15.0` — the interactive map
- [Chart.js](https://www.chartjs.org/) `v4.4.0` and the annotation plugin `v3.0.1` — the growth charts
- Plain HTML, CSS, and JavaScript — no framework, no build step

Mapbox and Chart.js load from their public CDNs, so the map and charts need an internet connection to render.

## License

Released under the MIT License — free to use, copy, modify, and build on, including commercially. See [`LICENSE`](LICENSE) for the full text.

The company data is shared in the same spirit: open for anyone to use. If you build something with it, a credit back to The LAB Miami / WynTech is appreciated but not required.

## Credits

Made and maintained by [The LAB Miami](https://thelabmiami.com). Data compiled from public sources and on-the-ground verification, with figures drawn from the Wynwood BID, Refresh Miami, Commercial Property Executive, the Miami Herald, and individual firm disclosures.
