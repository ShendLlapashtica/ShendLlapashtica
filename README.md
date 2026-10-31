# Shend Llapashtica

I build data integrations that cost almost nothing to run.

Most integration work is paid for twice: once for the upstream data, and again
for the servers, bandwidth and cache that carry it to whoever asked. A lot of
that second bill is optional. My work is mostly finding where it is optional —
moving egress to the client, making a cache key honest, deleting a round trip —
and then proving the result still holds under real traffic.

### What I work on

- **Zero-marginal-cost architecture.** Moving third-party fetches to the
  visitor's browser, so a page of live data costs the operator nothing per view.
  The hard part is never the fetch — it is doing it without exposing the
  upstream, and without the visitor's address getting cut off.
- **Third-party API resilience.** Pacing, circuit breaking, and block detection
  for services that do not announce a block with a status code.
- **Data enrichment and matching.** Turning a catalogue nobody normalised —
  names in three languages, typos in the index itself — into something a filter
  can actually query.
- **Keeping secrets out of what ships.** Bundles, commits, and now the output of
  coding agents.

### Open source

| | |
|---|---|
| **[leak-guard](https://github.com/ShendLlapashtica/leak-guard)** | A Claude Code plugin that stops your coding agent writing an API key into a file git would commit — and allows it into `.env`, because that is where it belongs. 42 tests, zero dependencies, fails open. |
| **[bundle-leak-check](https://github.com/ShendLlapashtica/bundle-leak-check)** | Fail the build when your JavaScript bundle ships what it must not: a key, an internal hostname, or a global you believed was tree-shaken away. 17 tests, zero dependencies. |
| **[polite-fetch](https://github.com/ShendLlapashtica/polite-fetch)** | Stop your visitors getting IP-banned by a third-party API. Request pacing, a circuit breaker, and block detection that works when the upstream redirects instead of returning 403. 12 tests, zero dependencies. |
| **[cbs-zero-cost-inventory-widget](https://github.com/ShendLlapashtica/cbs-zero-cost-inventory-widget)** | How a live inventory widget serves a catalogue of six figures with no server, no database and no per-view cost — and the four problems you hit on the way. |

### How I work

Every one of those repositories exists because something broke in production
first, and the README says what broke. A per-minute rate limit that let all
thirty requests leave in three milliseconds. A block detector that ignored `404`
and therefore classified every single block as "nothing to see here". A cache
header that read `s-maxage=NaN`, which every CDN silently ignores. A guard that
threw on every invocation, failed open exactly as designed, and so allowed
everything — found by a test, not by reading the code.

I would rather publish the bug than the claim. If a thing has 42 tests, the
README says what the 42 cover.

---

`cjap.dev@gmail.com` · open to integration and platform work
