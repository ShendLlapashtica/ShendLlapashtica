# Shend Llapashtica

**I turn markets that publish no API into data products people pay for.**

I design, build and run the whole thing: the ingestion, the normalisation, the
API, the keys and billing, and the infrastructure underneath, built so that it
costs close to nothing per request. Two of those products are live today, and
one of them is licensed by car dealers and importers across Europe.

[shend.dev](https://shend.dev) · [encar-api.com](https://encar-api.com) · [auto-vg.com](https://auto-vg.com) · **[info@shend.dev](mailto:info@shend.dev)**

---

### What I run

**[Encar API](https://encar-api.com)**: the Korean used-car market as clean JSON.
Korea's largest car marketplace has no public API, names its cars in Korean with
no English on the generation record, files prices in units of 10,000 KRW and
writes model years as `YYYYMM`. Encar API turns that into data a European
importer can filter, price and buy from. Nearly three in ten listings in that
market are the same car advertised twice. The duplicate carries its own ad id
but the original's photos, so the image path names the other advertisement, and
that is how they are caught. Licensed by dealers and importers to source cars
from Korea without building the pipeline themselves.
[Documentation](https://encar-api.com/docs)

**[auto-vg.com](https://auto-vg.com)**: one search across **20 national
used-car markets**, from Canada and Switzerland to Poland, Ukraine, Morocco and
China. Every market has its own language, currency, units and traps (Chinese
prices in 万, Swedish mileage in *mil*, filters that silently return the whole
catalogue). Every source is verified live before it ships, and a query a market
cannot answer exactly is refused rather than answered wrong. It runs on a
cache-first relay at the edge, so a page of live data costs almost nothing to serve.
The same data is available as an API at [apiforcar.com](https://www.apiforcar.com).

### What I can build for you

- **A data product from a market with no API.** Ingestion, normalisation,
  de-duplication, an API with keys and plans, and documentation. The full stack,
  delivered and running.
- **Infrastructure that stops costing per request.** Edge caches with honest
  keys, egress moved off your servers, round trips deleted, and proof that it
  still holds under real traffic.
- **Integrations that survive the upstream.** Pacing, circuit breaking, and
  block detection for services that never announce a block with a status code.
- **Data nobody normalised, made queryable.** Names in three languages, typos
  in the index itself, units that differ by a factor of ten thousand.
- **AI-agent development that does not leak.** Keeping keys out of commits,
  bundles and the output of coding agents.

### Open source

Each of these exists because something broke in production first, and its README
says what broke.

| | |
|---|---|
| **[leak-guard](https://github.com/ShendLlapashtica/leak-guard)** | A Claude Code plugin that stops your coding agent writing an API key into a file git would commit, and allows it into `.env`, because that is where it belongs. 44 tests, zero dependencies, fails open. |
| **[bundle-leak-check](https://github.com/ShendLlapashtica/bundle-leak-check)** | Fails the build when your JavaScript bundle ships what it must not: a key, an internal hostname, or a global you believed was tree-shaken away. 17 tests, zero dependencies. |
| **[polite-fetch](https://github.com/ShendLlapashtica/polite-fetch)** | Stops your visitors getting IP-banned by a third-party API. Request pacing, a circuit breaker, and block detection that works when the upstream redirects instead of returning 403. 12 tests, zero dependencies. |
| **[cbs-zero-cost-inventory-widget](https://github.com/ShendLlapashtica/cbs-zero-cost-inventory-widget)** | How a live inventory widget serves a catalogue of six figures with no server, no database and no per-view cost, and the four problems you hit on the way. |

### How I work

I would rather publish the bug than the claim. A per-minute rate limit that let
all thirty requests leave in three milliseconds. A block detector that ignored
`404` and so classified every block as "nothing to see here". A cache header
that read `s-maxage=NaN`, which every CDN silently ignores. A guard that threw on
every call, failed open exactly as designed, and so allowed everything. Each was
found by a test, not by reading the code. If a project says it has 44 tests,
the README says what the 44 cover.

---

**Work with me:** integration, data-product and platform work.
Write to **[info@shend.dev](mailto:info@shend.dev)** with what you need to build.
