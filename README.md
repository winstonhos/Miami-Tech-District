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

The map and the charts are standalone HTML files. The main site pulls them in as embeds, but each one opens and works on its own too.

## The map

The map plots verified Wynwood companies and lets you filter them by category:

- **Tech** — startups and tech companies
- **VC** — venture firms and funds
- **Finance** — fintech and financial services
- **Media** — media and creative companies
- **Coworking** — shared workspaces, including The LAB
- **Legal** — law firms serving the district

Each pin is a real, address-verified location. The count shown at the top reflects only companies we've been able to confirm.

## Using it

Everything here is static HTML, CSS, and JavaScript. There's no build step and no framework.

**View it live:** just open the GitHub Pages URL above.

**Run it locally:** because the pages embed each other, opening `index.html` straight off your computer won't load the map or charts (browsers block local file embeds for security). Run a tiny local server instead:

```bash
# from the folder that holds these files
python3 -m http.server 8000
```

Then open `http://localhost:8000/` in your browser.

**Host it yourself:** drop all the files into any static host — GitHub Pages, Netlify, Cloudflare Pages, Vercel — and it works as-is. Keep all four HTML files in the same folder so the links between them resolve.

## Embedding the map elsewhere

The map is a self-contained file, so you can drop it into your own site with an iframe:

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

The map is only as good as the data behind it, and the community knows the neighborhood better than any single list. If a company is missing, has moved, or is in the wrong category:

- **Open an issue** describing what's wrong or what's missing. Include the company name and, if you have it, the street address.
- **Open a pull request** if you're comfortable editing the files directly.

Corrections and additions are welcome from anyone. You don't need permission.

When adding a company, please include enough to verify it: the name, a Wynwood street address, and a category. Entries we can't confirm get held as unverified rather than mapped.

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
