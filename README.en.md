[简体中文](./README.md) | **English**

<p align="center"><img src="./assets/gappeek-mark.svg" width="104" alt="GapPeek logo"></p>
<h1 align="center">GapPeek</h1>
<p align="center"><strong>Find opportunities through market evidence.</strong></p>

Research product demand, competition and prices on Temu, TikTok Shop, Amazon, Shopee or Walmart. Each research task focuses on one selected platform.

[Start web research](https://gappeek.com/en/research) · [Sample report](https://gappeek.com/en/sample-report) · [Version history](./CHANGELOG.md)

## Install

Send this command to your AI agent or run it in a terminal:

```bash
npx skills add stomeonst/gappeek-skill --yes
```

After installation, register on GapPeek and verify your email. Ask your agent to connect GapPeek, then enter its binding code on the [Devices page](https://gappeek.com/en/account/devices). Research requires account credits. Restart your agent if it has not discovered the new Skill.

## Ask a market question

```text
Find market opportunities for men's wallets on Temu.
```

```text
Research men's wallets on Temu in the United States.
```

```text
Research pet cleaning products on Shopee.
```

Choose one platform for each research task. Name a country to restrict the scope, or examine the supported countries and regions for that platform. If the platform is unclear, your agent will ask you to choose before submitting research.

## What you can examine

| Question | Evidence |
| --- | --- |
| Is there demand? | Observed sales, demand structure and available changes |
| How competitive is it? | Products, sellers and concentration |
| What are the prices? | Observed prices in each market's currency |
| Are the products relevant? | Matched, adjacent and unverified samples |
| What should be researched next? | Markets for further investigation and supporting evidence |

Reports retain the actual platform, country and observation date. Missing values are not filled with zero, samples are not presented as whole markets, and results do not guarantee sales or profit.

## Versions and rollback

Each release keeps its own tag, change record and installation package. Previous versions are retained. Download `gappeek.skill` from the desired [release](https://github.com/stomeonst/gappeek-skill/releases) and ask your agent to install it.

Alternatively, check out a tag and install from the local directory:

```bash
git clone https://github.com/stomeonst/gappeek-skill.git
cd gappeek-skill
git checkout v0.1.1-20260910.3
npx skills add . --yes
```

Client releases and service capabilities evolve separately. Reverting the client does not roll back service accounts or data.

## Repository

- [SKILL.md](./SKILL.md): the agent research workflow.
- [Input contract](./references/intake-contract.md) and [result contract](./references/result-contract.md).
- [Client script](./scripts/run-hosted-market-screen): submit queries and retrieve reports.
- [Dated example](./examples/us-womens-running-shoes.md): a frozen observation from August 27, 2026.

This repository distributes the Skill client and public contracts. Backend code, account secrets and raw data are kept outside this repository.

## License

[GapPeek Skill License 1.0](./LICENSE) permits installing the unmodified Skill for personal or internal business research. Modification, redistribution, white labeling, resale and access-control bypass require prior written permission.
