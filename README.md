# UK Sponsor Tool

A browser-based search tool for exploring organisations on the UK Home Office Register of Licensed Sponsors.

**Live tool:** https://zeeshan.cisaan.workers.dev/visa-sponsor

## What it does

- Downloads the current sponsor-register CSV from the GOV.UK publishing page, with a fallback source.
- Reads organisation, town/city, county, visa route and rating fields.
- Groups records by visa route, region and town.
- Calculates totals for routes and regions.
- Publishes the processed data inside a responsive browser interface.
- Uses GitHub Actions to refresh the data automatically.

## Data flow

```
GOV.UK sponsor register
        ↓
Python download and CSV parsing
        ↓
Cleaning, route mapping and regional grouping
        ↓
Totals and town-level aggregation
        ↓
Generated JSON embedded in index.html
        ↓
Automated publication through GitHub Actions
```

## Repository structure

- `update_sponsors.py` — downloads, transforms, groups and writes the sponsor data.
- `index.html` — user interface and generated dataset.
- `.github/workflows/` — automated refresh and deployment workflows.

## Technologies

Python · JavaScript · HTML/CSS · GitHub Actions · GOV.UK open data

## Running the refresh locally

1. Install Python 3.
2. Install the dependency:
   ```bash
   pip install requests
   ```
3. Run:
   ```bash
   python update_sponsors.py
   ```
4. Open `index.html` in a browser.

The script updates the data embedded in `index.html`.

## Data handling and limitations

- The source is the public UK Home Office sponsor register.
- The tool is informational and does not guarantee that an organisation is currently recruiting.
- Regional grouping is based on town/city mappings in the script and may classify unmatched locations as `Other`.
- Source formatting can change, so automated refreshes should be checked for failures.
- No personal user data is collected or stored by the tool.

## Possible next improvements

- Add automated schema and row-count validation.
- Separate generated data from the interface.
- Add tests for route and region mapping.
- Record refresh status and data-quality checks.
