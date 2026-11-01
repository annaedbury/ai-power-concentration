# ai-power-concentration

An independent R project examining whether global distribution of AI capability is more concentrated than that of economic and military power, and whether that has changed since 2015.

## Data Sources

- **Epoch AI, Notable AI Models** (CC-BY 4.0).Downloaded 31/10/2026; 1091 rows. <https://epoch.ai/data/ai-models>
- **World Bank World Development Indicators** (GDP, military expenditure). Accessed via 'WDI' R package 31/10/2026.

## Scripts

- '00_setup.R': creates project folders
- '01_fetch_data.R': downloads Epoch AI and World Bank data
- '02_inspect.R': inspects raw Epoch file
- '03_clean.R': converts Epoch model list into AI models per year per country

## Data cleaning notes (Epoch AI)

- The raw Epoch file contains 1,091 notable AI models. Of these, 727 have a recorded country of organisation and a publication year between 2013-2024 (window needed to calculate 3-year rolling totals from 2015). Remaining 364 models excluded.
- **Reasons for exclusion** (categories overlap, so they do not sum to 364): 19 models have no countries recorded, 160 were published before 2013, and 203 were published after 2024.
- **Limitation: end date.** The analysis stops at 2024 because World Bank GDP and military expenditure data are not yet complete for later years. The 203 models from 2025-2026 (about 19% of the file) are therefore not captured, so results do not reflect the most recent period of AI development.
- Epoch records the country of each organisation involved in a model in a single text field (e.g. 'China,United Kingdom') so a country can appear more than once for the same model. I split these into 1 row per country and removed repeat entries, so each country appears once per model.
- Models involving several countries are shared equally between them (e.g.a model with 2 countries counts as 0.5 for each).
- **Limitation: multinational entries** 3 of 727 models (\~0.4%) were listed only as "Multinational" so no singular country could be assigned and they are excluded from the country counts. So where "Multinational" appeared alongside a named country, the model is credited to the named country only.
- Final data set contains 724 models.
- Epoch's "notable" models are selected by its researchers, so data set could favor well-documented and English-language work.
