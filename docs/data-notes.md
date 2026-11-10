# Data notes

## LMIA files (ESDC, open.canada.ca)
Dataset: Temporary Foreign Worker Program (TFWP): Positive LMIA employers list
Licence: Open Government Licence – Canada

| File | Period | NOC | Header row | Data rows | Downloaded | Sources |
|---|---|---|---|---|---|---|
| tfwp_2022q2_positive_en.xlsx | Apr–Jun 2022 | 2011 | 1 | 15,167 | 2026-11-09 | https://open.canada.ca/data/en/dataset/90fed587-1364-4f33-a9ee-208181dc0b97/resource/d93b17b3-4c84-45d0-8d4a-b44a54f733e6
| tfwp_2025q2_pos_en.xlsx | Apr–Jun 2025 | 2021 | 1 | 15,273 | 2026-11-09 | https://open.canada.ca/data/en/dataset/90fed587-1364-4f33-a9ee-208181dc0b97/resource/fbfda891-5327-4e01-927e-0e0dd580d304
| tfwp_2026q2_pos_en.xlsx | Apr–Jun 2026 | 2021 | 1 | 7,344 | 2026-11-09 | https://open.canada.ca/data/en/dataset/90fed587-1364-4f33-a9ee-208181dc0b97/resource/2b94f80d-fa27-4d2e-9b90-6f67fe69bf50

## Structure
- Row 0: title (contains the period, e.g. "April to June 2026")
- Row 1: column headers
- Last 7-8 rows: notes, identified by an empty `Program Stream`
- One row per employer + occupation + stream

## Columns
| Column | Example | Notes |
|---|---|---|
| Province/Territory | Ontario | Padded with trailing spaces; includes "Employers carrying on business in Canada with Head Office outside of Canada" |
| Program Stream | Global Talent Stream | High Wage, Low Wage, Primary Agriculture, Global Talent Stream, Permanent Resident Only |
| Employer | Stripe | Manually entered, inconsistent spelling/case |
| Address | Paradise, NL A1L 3B3 | "City, PROV POSTAL"; foreign addresses for head-office-outside-Canada rows |
| Occupation | 21231-Software engineers and designers | "code-title"; NOC 2011 (4-digit) before Sept 2024 releases |
| Incorporate Status | Unknown | ~79% Unknown, so low value |
| Approved LMIAs / Positions | 1 / 2 | Called "Requested …" in the 2022 file; loads as float because of the notes rows |

## Differences between files
- 2022: column names have trailing spaces
- 2022: "Requested LMIAs/Positions" instead of "Approved …"
- 2022: NOC 2011 codes; 2025+: NOC 2021
- File naming: `_positive_en` vs `_pos_en`

## Cleaning plan for Phase 3
- [ ] Read with `header=1`; strip column names
- [ ] Rename Requested → Approved
- [ ] Drop notes rows (empty Program Stream)
- [ ] Strip whitespace in all text columns
- [ ] Cast counts to int
- [ ] Extract year/quarter from the title row
- [ ] Split Occupation into `noc_code` + `noc_title`
- [ ] Map NOC 2011 → 2021 (StatCan concordance)
- [ ] Parse Address into city / province code / postal code; handle foreign addresses
- [ ] Normalize employer names for matching

## Caveats (for the app disclaimer)
- Excludes employers whose names are personal names, so the list is incomplete
- Approved positions ≠ work permits issued
- Numbers may be revised in later releases

## Early insights (2026Q2)
- 508 tech rows; 276 Global Talent Stream, 231 High Wage
- Tech is concentrated in QC, ON, BC, AB
- Very few tech LMIAs in Atlantic Canada, so AIP lists are needed as a separate source

## AIP designated employer lists
| Province | URL | Format | ~Employers | Notes |
|---|---|---|---|---|
| NS | | | | |
| NB | | | | |
| PEI | | | | |
| NL | | | | |