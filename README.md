# Surgical Preparedness Index (SPI) self-assessment tool

An interactive version of the Surgical Preparedness Index, which lets a hospital rate its capacity to keep planned (elective) surgery running during a system shock. The hospital rates 23 indicators across four domains and gets a total score out of 115, domain scores, benchmarks and a PDF report.

Live site: https://drjmartins.github.io/spi-tool/

Reference: NIHR Global Health Unit on Global Surgery & COVIDSurg Collaborative. Surgical Preparedness Index. *The Lancet* 2022; 400:1607–17. https://doi.org/10.1016/S0140-6736(22)01846-3

## How it works

- `index.html` is the whole tool: one static page with no build step. It loads Chart.js from a CDN.
- `assets/` holds the Surgical Data and Policy Lab look shared with the NHS Waiting Times dashboards: `sdpl.css` (IBM Plex Sans, lab header bar, lab footer band, magenta heading accent), the lab seal and the Plex font files (SIL Open Font Licence, see `assets/fonts/LICENSE-IBM-Plex-Sans.txt`). Page colours are set at the top of the `<style>` block in `index.html`: navy UI, navy-shade domains and toned-down red-to-green ratings, all at least 4.5:1 contrast with white text.
- It is hosted on GitHub Pages from the `main` branch (repo root). Pushing to `main` updates the live site within a minute or two.
- Everything is calculated in the browser. Nothing is sent anywhere unless the user ticks the research consent box.

## Research data (REDCap)

- If the user consents, the tool opens the University of Birmingham REDCap public survey in a new tab with their answers filled in from the link. They press Submit in REDCap. No REDCap API token is held in the page.
- Hospital name and city are optional. They appear on the user's own PDF only and are never sent to REDCap.
- If the user does not consent, nothing is sent. The results page offers a "Contribute my results" button, which opens the survey without consent filled in.
- `redcap/spi_redcap_data_dictionary.csv` is a record of the REDCap form fields. Make changes to the live form in REDCap's Online Designer, not by re-uploading this file, because an upload can remove the survey's Stop Action on consent.
- `redcap/country_choices.txt` lists the country choices (ISO 3166-1 alpha-3 code, name), one per line, in the format REDCap's choice box expects.
- When analysing the data, only use records where `consent = 1`.

## Country and income group

- Countries use ISO 3166-1 alpha-3 codes, plus `XKX` for Kosovo and `OTH` for "Other / not listed". The same list is held in `index.html` (`COUNTRIES`) and in `redcap/country_choices.txt`, and the two must match.
- Choosing a country fills in its World Bank income group automatically. The user can change it.
- The income groups come from the World Bank classification for FY2027 (July 2026 release), stored in `data/wb_income_fy2027.json` and inline in `index.html` (`WB_INCOME`, `WB_INCOME_YEAR`). The World Bank updates the list every July: https://datahelpdesk.worldbank.org/knowledgebase/articles/906519

## Updating the site

1. Edit `index.html`.
2. Preview it locally with `python3 -m http.server 8099` and open http://localhost:8099
3. Commit and push to `main`.

## Licence

The SPI is licensed under CC BY 4.0.
