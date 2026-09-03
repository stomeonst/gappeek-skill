**English** | [简体中文](./README.md)

<p align="center">
  <img src="./assets/gappeek-mark.svg" width="104" alt="GapPeek logo">
</p>

<h1 align="center">GapPeek</h1>

<p align="center">
  <strong>See the market before you choose the product.</strong><br>
  Evidence-led market opportunity research for AI agents.
</p>

GapPeek gives AI agents a repeatable way to examine market demand, supply,
competition, pricing, and recent change. It returns structured market evidence
only when the available data passes its checks. Missing evidence is omitted,
never replaced with invented values.

## Install

Send this command to your AI agent, or run it in a terminal:

```bash
npx skills add stomeonst/gappeek-skill --yes
```

Then ask your agent a market question in natural language.

```text
Use GapPeek to research the US market for compact pet cleaning products.
```

## Questions GapPeek can investigate

| Research goal | Example prompt |
| --- | --- |
| Explore a broad category | `Use GapPeek to examine home storage products in the US and show the strongest related submarkets.` |
| Validate a product direction | `Use GapPeek to compare demand and seller competition for compact pet cleaning products.` |
| Inspect pricing | `Use GapPeek to show the observed price level and competition structure for travel organizers.` |
| Challenge an assumption | `Use GapPeek to check whether demand growth for women's running shoes is accompanied by lower competition.` |
| Compare nearby markets | `Use GapPeek to compare the supply and demand structure of three related bathroom organization markets.` |

## What a report contains

GapPeek keeps the requested direction separate from the market that was
actually analyzed. A report may include the following evidence when available:

| Evidence | What it helps you examine |
| --- | --- |
| Market scope | The platform, country, category, and observation window behind the result |
| Demand | Observed demand level, share, and recent change |
| Supply | Monitored products and sellers in the analyzed scope |
| Competition | Seller structure, product structure, and concentration signals |
| Pricing | Observed price level for the monitored market |
| Related markets | Up to three nearby market directions returned by the service |
| Evidence boundary | Missing fields, dated observations, and the conclusion grade |

## Frozen evidence example

The example below is a dated market observation. It demonstrates the report
structure and does not represent a live market reading.

### US women's running shoes

| Case field | Value |
| --- | --- |
| Observation date | August 27, 2026 |
| Conclusion grade | Observation |

| Metric | Recorded value |
| --- | ---: |
| Monthly sales | 10,513 |
| Monthly sales change | +28.55% |
| Monitored products | 500 |
| Monitored sellers | 251 |
| Leading product concentration | 90.6% |
| Leading seller concentration | 100% |
| Median observed price | $13.12 |

The demand signal is positive, while the observed competition structure is
highly concentrated. GapPeek preserves both facts and keeps the conclusion at
observation grade. It does not turn this evidence into a promise of sales or
profit.

[Read the annotated example](./examples/us-womens-running-shoes.md)

## How it works

1. **Describe the question.** Name a market, category, product direction, and
   country when geography matters.
2. **GapPeek checks the available evidence.** The service resolves the actual
   analysis scope and checks whether the report is suitable to return.
3. **Review the evidence together.** Your agent presents the market size,
   supply, demand, pricing, recent change, and related markets that passed the
   report contract.

If the evidence is insufficient, GapPeek returns a data insufficiency result.
It does not estimate missing counts or silently replace them with zero.

## GapPeek and a one-shot product search

| | One-shot product search | GapPeek |
| --- | --- | --- |
| Starting point | Listings or links matching a query | A defined market question and analysis scope |
| Main output | Individual products | Structured market evidence |
| Supply view | Manual counting and interpretation | Product and seller observations when available |
| Demand view | Signals scattered across results | Demand level, share, and change when available |
| Competition | Inferred manually | Supply structure and concentration shown together |
| Missing data | Easy to overlook | Omitted explicitly and never filled with invented values |
| Decision boundary | Left implicit | Observation date and conclusion grade remain visible |

GapPeek is designed for evidence-led market screening. It complements product
search, sourcing, and human judgment rather than replacing them.

## Report rules

The public [result contract](./references/result-contract.md) defines how an
agent must present GapPeek output:

1. Only reports marked ready by the service can be shown.
2. The requested market and analyzed market remain separate.
3. Missing fields are omitted instead of reported as zero.
4. Related markets are shown only when returned by the service.
5. Price observations never become profit or sales guarantees.

## Privacy and access

GapPeek does not ask users to provide marketplace passwords, cookies, payment
details, store credentials, or personal contact information to the Skill. The
repository contains the installable client and public report contracts. Service
infrastructure and data systems are not distributed in this repository.

GapPeek is an independent research product and is not an official tool of any
marketplace. Users remain responsible for their own business decisions and
compliance obligations.

## Repository guide

| Path | Purpose |
| --- | --- |
| [`SKILL.md`](./SKILL.md) | Agent behavior and research workflow |
| [`scripts/run-hosted-market-screen`](./scripts/run-hosted-market-screen) | Secure client for submitting and reading reports |
| [`references/result-contract.md`](./references/result-contract.md) | Public report fields and presentation rules |
| [`references/intake-contract.md`](./references/intake-contract.md) | Public structured intake contract |
| [`examples/`](./examples) | Dated, annotated report examples |

## License

GapPeek is source-available under the [GapPeek Skill License 1.0](./LICENSE).
You may install and use the unmodified Skill for personal or internal business
research. Modification, redistribution, white-labeling, resale, and
access-control bypass require prior written permission.
