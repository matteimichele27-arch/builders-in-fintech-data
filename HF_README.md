---
license: cc-by-4.0
pretty_name: Builders in Fintech — Fintech Funding Rounds, Companies and Investors
language:
  - en
tags:
  - finance
  - fintech
  - venture-capital
  - funding-rounds
  - startups
  - investors
size_categories:
  - 1K<n<10K
configs:
  - config_name: funding_rounds
    data_files: data/funding-rounds.csv
    default: true
  - config_name: companies
    data_files: data/companies.csv
  - config_name: investors
    data_files: data/investors.csv
  - config_name: funding_index
    data_files: data/funding-index.csv
  - config_name: investor_scorecards
    data_files: data/investor-scorecards.csv
---

# Builders in Fintech — Fintech Funding Rounds, Companies and Investors

An editorially curated, sourced dataset of fintech funding rounds worldwide, with the companies that raised and the investors that took part. It is the public export of the database behind [Builders in Fintech](https://buildersinfintech.ai), a fintech news publication, weekly newsletter and podcast run by Michele Mattei.

As of 29 September 2026 it holds 2,164 approved equity rounds across 16 currencies and 56 countries, plus debt facilities, fund closes, grants and IPOs recorded as separate categories. Coverage is continuous from November 2023 and refreshed weekly from the live site.

## Files

| Config | File | One row per |
|---|---|---|
| `funding_rounds` (default) | `data/funding-rounds.csv` | funding round: announcement date, company, round type, category (equity, debt, fund, grant, ipo), amount and currency as announced, investors with lead flag, company country when known, source link |
| `companies` | `data/companies.csv` | company that appears in at least one published record |
| `investors` | `data/investors.csv` | investor organisation |
| `funding_index` | `data/funding-index.csv` | week of the Builders Fintech Funding Index (round-count index, median USD round size index, coverage flag) |
| `investor_scorecards` | `data/investor-scorecards.csv` | investor with a 24-month follow-on rate on recorded rounds |

The exact column names are the first row of each file. A JSON copy of the rounds is at https://buildersinfintech.ai/data/funding-rounds.json.

```python
from datasets import load_dataset
rounds = load_dataset("<hf-user>/builders-in-fintech", "funding_rounds", split="train")
```

## How the data is made

- **Sources.** Every round comes from a published Builders in Fintech item: the weekly newsletter (November 2023 onwards) or the daily news pipeline (September 2026 onwards), which draws on company announcements, press releases and trade press. Each row links back to its source where one exists.
- **Editorial review.** Only records approved by the editor are exported. Automatically extracted candidates stay out until reviewed.
- **Amounts are never converted.** An amount is stored in the currency it was announced in. Totals and rankings must be computed per currency. Undisclosed amounts are left empty.
- **Dates** are announcement dates, not closing dates.
- **Corrections** are logged on the affected news article and flow into the next weekly refresh.

Full methodology: https://buildersinfintech.ai/methodology

## Known limitations

- Coverage reflects what the publication reported. It is broad but not exhaustive, and the capture rate rose when the daily pipeline started in September 2026. Treat counts over time as coverage-dependent.
- Company country is missing for many older records.
- Some very large AI rounds are included where they were reported in fintech coverage.
- A company's first round in this dataset may not be its first round ever.
- Funding Index weeks flagged `coverage_affected` overstate activity: round capture increased in September 2026, and the flag clears once the 12-week baseline reflects the new coverage (mid-December 2026).
- Follow-on rates count only rounds we recorded, so true rates are likely higher.

## Other ways to access it

- Live MCP server for AI agents (no key): `https://buildersinfintech.ai/mcp`
- Browse: https://buildersinfintech.ai/funding
- Weekly Funding Index: https://buildersinfintech.ai/funding/index

## Licence and citation

CC BY 4.0. Attribute "Builders in Fintech" and link to https://buildersinfintech.ai.

```bibtex
@misc{mattei_buildersinfintech_2026,
  author    = {Mattei, Michele},
  title     = {Builders in Fintech: Fintech Funding Rounds, Companies and Investors},
  year      = {2026},
  publisher = {Builders in Fintech},
  url       = {https://buildersinfintech.ai/data},
  doi       = {<Zenodo DOI once minted>}
}
```

Contact: info@buildersinfintech.ai
