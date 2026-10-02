# US Provider Industry Payments — the NPI registry joined to CMS Open Payments

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23098004.svg)](https://doi.org/10.5281/zenodo.23098004)

One row per US healthcare provider who received a payment from a drug or device company between
2019 and 2025: the provider's NPI, registered specialty and location from the national NPI registry
(NPPES), next to the total CMS Open Payments reports for them, the number of payments, the largest
paying company and the kind of payment that carried the most money. Plus totals by state and by
specialty.

CMS publishes the registry and Open Payments as separate files — the payment files are 62 million
individual transfers. This is the two joined on the NPI, the key both carry, and reduced to one
row per provider. No name matching is involved anywhere.

**Browse it online:** every provider is a page on **[npiwho.com](https://npiwho.com/)** — with
Medicare prescribing and billing, education and hospital affiliations — for example the
[payment rankings](https://npiwho.com/payments) by state and specialty.

Also on **[Kaggle](https://www.kaggle.com/datasets/npiwho/us-provider-payments)** and **[Hugging Face](https://huggingface.co/datasets/npiwho/us-provider-payments)**, and archived with a DOI on **[Zenodo](https://doi.org/10.5281/zenodo.23098004)**.

Current data: see [`data/VERSION.json`](data/VERSION.json).

## Files

| File | Rows | What it is |
|---|---|---|
| [`data/provider_industry_payments.csv.gz`](data/provider_industry_payments.csv.gz) | 1,649,041 | One row per provider with at least one reported payment, largest total first. Gzipped CSV (GitHub's 100 MB limit); `pandas.read_csv` reads it as is |
| [`data/payments_by_state.csv`](data/payments_by_state.csv) | 56 | Providers, providers with payments and total paid, per state and territory |
| [`data/payments_by_specialty.csv`](data/payments_by_specialty.csv) | 698 | The same per registered specialty (NUCC taxonomy) |
| [`datapackage.json`](datapackage.json) | | [Frictionless](https://frictionlessdata.io/) descriptor |

```python
import pandas as pd
df = pd.read_csv("https://github.com/npiwho/us-provider-payments/raw/main/data/provider_industry_payments.csv.gz")
```

## Columns of `provider_industry_payments`

| Column | Example | Notes |
|---|---|---|
| `npi` | `1366487498` | National Provider Identifier |
| `entity_type` | `individual` | `individual` (NPI type 1) or `organization` (type 2) |
| `name` | `STEPHEN S BURKHART` | As registered in NPPES |
| `credential` | `M.D.` | As registered, unnormalised |
| `specialty` | `Orthopaedic Surgery Physician` | Primary taxonomy's name |
| `taxonomy_code` | `207X00000X` | NUCC code of the primary taxonomy |
| `city`, `state`, `postal_code` | `SAN ANTONIO`, `TX`, `78258` | Primary practice location in NPPES |
| `payments_total_usd` | `185316401.27` | Sum of the general payments reported for 2019–2025 (research payments and ownership interests are not included) |
| `payments_count` | `95` | Number of payment records |
| `program_years` | `2019-2024` | First and last year with a payment |
| `largest_payer` | `Arthrex, Inc.` | The company with the largest total to this provider |
| `largest_payment_nature` | `Royalty or License` | The kind of payment with the largest total |

## What the figures are not

**A payment total is not income and not an allegation.** The largest totals are mostly royalties
on devices a physician helped design and payments for companies a manufacturer acquired; at the
other end, 429,482 of these providers received under $100 in seven years —
typically meals at sponsored events. The records say a financial relationship was reported, which
is what the Physician Payments Sunshine Act requires; they say nothing about whether it influenced
care.

Payment records are submitted by the paying companies. Providers can dispute them with CMS; a
correction there reaches this dataset at the next refresh.

## Sources and licence

- [NPPES](https://download.cms.gov/nppes/NPI_Files.html), the monthly full NPI file, CMS
- [Open Payments](https://openpaymentsdata.cms.gov/) general payments, program years 2019–2025, CMS
- [NUCC Health Care Provider Taxonomy](https://www.nucc.org/), for specialty names

All are works of the US government (17 U.S.C. § 105) except the NUCC code set, used here for
names only. This compilation is released under [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/).

## Citation

If you use this data, please link to [npiwho.com](https://npiwho.com/), where it is maintained and
browsable:

```
NPI Who (2026). US Provider Industry Payments: the NPI registry joined to CMS Open Payments. Zenodo. https://doi.org/10.5281/zenodo.23098004
```

## Updates

Regenerated from the pipeline that builds npiwho.com when CMS publishes a new Open Payments
program year (each June) and with the NPPES registry. Issues and corrections are welcome.
