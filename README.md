# TRENDS-THAI

A decade-long, province-level weekly multi-disease surveillance dataset
of dengue, chikungunya, and hand, foot, and mouth disease (HFMD) in
Thailand, 2016 to 2025.

This repository holds the analysis-ready dataset and the reproduction
script. The dataset itself will be archived on Zenodo; the accompanying
data descriptor, tables, and figures are published separately.

The repository name is TRENDS-THAI. The dataset will be archived on
Zenodo and assigned DOI: <Zenodo DOI placeholder>.

## Contents

```
trends-thai/
    README.md                     this file
    LICENSE                       CC BY 4.0 (data) + MIT (code)
    requirements.txt              Python package dependencies
    analysis_pipeline.py          full pipeline in one file
    data/                         optional local download location for the Zenodo dataset
```

## Dataset

The analysis-ready dataset will be distributed via Zenodo as
`TRENDS-THAI dataset.xlsx`. Both data sheets share `P-code` and
`Province` as join keys.

| Sheet | Rows | Cols | Description |
|---|---|---|---|
| weekly data       | 40,579 | 17 | weekly counts and pre-computed rates per province |
| province data     | 77     | 15 | province attributes plus year-specific populations 2016 to 2025 |
| data dictionary   | 21     |  5 | variable definitions for both data sheets |

Each row in `weekly data` is one (province, epidemiological week)
observation. The population denominator lives in `province data` as ten
yearly columns (`Population 2016` through `Population 2025`); to recover
the population for any (P-code, Year) row in `weekly data`, join the two
sheets on `P-code` and select the matching year column. The boundary
version of the province polygons (valid from 22 January 2022, version
v01) is recorded in the `province data` sheet's intro line.

## Data sources

- **Disease counts:** Ministry of Public Health 506 notifiable disease
  surveillance system, Thailand. https://ddc.moph.go.th/
- **Population denominators:** Bureau of Registration Administration,
  Department of Provincial Administration, Thailand.
  https://stat.bora.dopa.go.th/
- **Province polygons:** Royal Thai Survey Department, distributed as
  the United Nations Office for the Coordination of Humanitarian
  Affairs (OCHA) Common Operational Dataset.
  https://data.humdata.org/dataset/cod-ab-tha

## Quick start

```bash
git clone https://github.com/<your-org>/TRENDS-THAI.git
cd TRENDS-THAI
pip install -r requirements.txt
python analysis_pipeline.py --xlsx "data/TRENDS-THAI dataset.xlsx" --outdir output
```

After downloading the dataset from Zenodo, place it in `data/` or pass
the downloaded file path directly to `--xlsx`.

The pipeline writes four CSV summaries into `output/`:

- `validation_summary.csv` - row counts, province count, total cases.
- `annual_summary.csv` - yearly totals per disease.
- `phase_summary.csv` - mean weekly rates by pandemic phase
  (Pre-COVID 2016 to 2019, Pandemic 2020 to 2022, Post-acute 2023 to 2025).
- `top_provinces.csv` - top 10 provinces per disease by mean annual rate.

## Citation

A formal data descriptor accompanies this release; please cite it when
reusing the dataset. The full citation will be added here once the
descriptor is published. Zenodo DOI: <Zenodo DOI placeholder>.

## Licence

- **Dataset:** Creative Commons Attribution 4.0 International (CC BY 4.0).
- **Code:** MIT License.

See `LICENSE` for the full text.
