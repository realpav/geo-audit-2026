# GEO readiness audit — 26 sites (SEO & web-dev niche), October 2026

Open dataset: how ready real websites are for AI search (GEO / AEO), measured with 23-checks rule set.

**Live tool:** https://realpav.ru/en/geo-check/ (free, no signup)
**Russian version:** https://realpav.ru/geo-instrument/
**Methodology notes below.** No proprietary data — every row is reproducible by running the tool on the same domain.

## What was measured

23 checks in five groups:

| Group | Checks |
|---|---|
| AI crawler access | robots.txt rules for GPTBot, OAI-SearchBot, ChatGPT-User, PerplexityBot, ClaudeBot, Claude-SearchBot, Google-Extended, Applebot-Extended |
| llms.txt | file present, size reported |
| Structured data | Organization / LocalBusiness / LegalService (string **or array** `@type`), FAQPage |
| Content structure | question-style headings, H2 hierarchy, lists, tables, text volume |
| Trust signals | author and dates, outbound sources, term definitions, page title, meta description |

Result: `score = sum of weights of passed checks`, shown as percent.

## Sample

26 sites: 10 owned by the studio, 16 in the SEO / web-development niche (SaaS tools, media, agencies). Four additional sites failed on SSL/timeout and were excluded.

## Headline numbers

| Metric | Value |
|---|---|
| Median score | 61% |
| Sites ≥ 80% | 8 of 26 |
| Sites < 50% | 3 of 26 |
| No FAQPage schema | 20 of 26 (77%) |
| No Q&A block on page | 19 of 26 (73%) |
| No author/date markup | 19 of 26 (73%) |
| No question-style headings | 19 of 26 (73%) |
| No llms.txt | 12 of 26 (46%) |
| No Organization schema | 10 of 26 (38%) |

## Notable observations

- Large media properties scored 48–57% despite strong authority: content quality and machine readability are not the same thing.
- Established SEO SaaS tools scored 70% — they build tools for SEO but had not prepared their own pages for AI search.
- Agencies selling “modern SEO” scored lowest (35% and 43%).
- Some “failures” are checker bugs, not site problems — e.g. `"@type": ["LegalService","Organization"]` was not recognised until the regex was fixed. Always verify a failing check by hand.

## Limitations

- Technical readiness only. A high score does not mean a model will cite the site.
- The 23 checks are this project's rule set, not an industry standard.
- Single niche, single date. Re-run before drawing conclusions about trends.
- Results are cached for 30 minutes; use `?fresh=1` on the API to re-check.

## Data

[`geo-audit-2026-10.csv`](geo-audit-2026-10.csv) — one row per site:

```
domain,group,score_percent,points,failed_checks
```

`group` is `own` (studio properties) or `niche` (third parties). `failed_checks` is a semicolon-separated list of failed check names (English labels).

## Reproduce

1. Open https://realpav.ru/en/geo-check/
2. Paste a domain, read the score
3. Or query the API directly:

```bash
curl "https://realpav.ru/wp-json/realpav/v1/geo-ai-check?url=example.com&fresh=1"
```

Returns JSON: `percent`, `score`, `max`, `checks[]` with `label`, `ok`, `comment`, `hint`, plus `recommendations[]`.

## License

Data: CC0 1.0. Text: CC BY 4.0 — attribution appreciated: “Realpav GEO audit, October 2026”.

## Author

Andrey Ponomarev, Realpav web studio (Balashikha, Russia) — https://realpav.ru/
