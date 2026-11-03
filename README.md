# A rival that grew the market: twenty years of KTX in open data

**Live page:** https://likrentai.github.io/koreanrail/
**Case study:** https://likrentai.github.io/koreanrail/case-study.html
**Case study (PDF):** https://likrentai.github.io/koreanrail/case-study.pdf

Korean high-speed rail carried 20 million passengers in 2004, its opening year, and 117 million in 2024. On the way it gained a rival operator (SR's SRT, from December 2016), new lines and a pandemic. This project follows Korea Railroad Corporation (KORAIL) open data from 2004 to 2025 to ask three questions: did the rival split the market or grow it, did new lines create travel or move it, and has everything recovered from COVID?

## What it shows

- **SRT took riders from KTX, but the market grew.** At the 14 stations SRT served in 2019, KTX riders fell 3% from 2016 to 2019, but KTX and SRT together rose 36%, against 12% at KTX stations SRT does not serve.
- **New lines created rail travel rather than moving it.** The Gangneung line carried 2.6 million riders in 2019 while the old lines to the east coast lost 0.2 million; KTX riders at the Honam stations rose 47% in the first year of the Honam high-speed line, against 3% at all other KTX stations.
- **High-speed rail is above 2019; metro rail is not.** High-speed riders were 24% above 2019 in 2024; KORAIL metro rail was still 4% below 2019 in 2025, with the old commuter lines lagging most.
- **Service disruptions per train km fell by about two thirds** between 2016 to 2019 and 2022 to 2024.

The interactive page has three views: a station explorer for all 88 KTX and SRT stations, a timeline of twenty years of high-speed rail with the events that shaped it, and the hourly shape of the metro rail day, line by line. Station and line names are given in Hangul with English in brackets.

## A note on estimates

Most numbers are counts published by KORAIL. Two are not:

- The **pre-COVID path** for high-speed rail is a Holt-Winters model fitted to January 2017 to December 2019. With only three years to learn from, it is shown as a range between a straight and a levelling-off trend, not as one line.
- The **train km** table does not state its unit; it behaves like train km per day, and yearly train km are that figure times 365. The fall in disruptions is the same in the raw counts.

The case study lists every other problem found in the data and how it was handled (renamed stations, two station series that overlap, a mistitled sheet, small differences between tables).

## Files

| Path | What it is |
|---|---|
| `00load.ipynb` | Loads and checks the station tables (KTX monthly 2004 to 2022; KTX and SRT yearly 2016 to 2024) |
| `01totals.ipynb` | Loads and checks the national tables: riders by train type and by line, train runs, revenue, accidents and service disruptions |
| `02metro.ipynb` | Loads and checks KORAIL's metro rail workbooks: boardings by station (2019, 2024, 2025) and gate taps by hour (2024, 2025) |
| `03explore.ipynb` | Five candidate findings side by side, with draft charts |
| `04charts.ipynb` | The case study charts (`docs/images/cs_f*.png`) |
| `05pagedata.ipynb` | The small JSON files the interactive page reads (`docs/data/`) |
| `data/clean/` | The tidy tables made by notebooks 00 to 02 (CSV, UTF-8) |
| `data/names_en.csv` | English names for stations and lines |
| `docs/index.html` | The interactive page (Plotly) |
| `docs/case-study.html`, `docs/case-study.pdf` | The case study |
| `docs/data/`, `docs/images/`, `docs/fonts/` | Data, pictures and fonts for the two pages |
| `requirements.txt` | The Python packages used |

## How to run it

1. Download the raw files listed below into `data/raw/` (subfolders `datagokr`, `railstat` and `korail_metro`). They are not included here; each is free to download.
2. Create an environment with Python 3.12 and install the packages, for example with uv: `uv venv --python 3.12`, then `uv pip install -r requirements.txt`.
3. Run the notebooks in order, 00 to 05. Notebooks 03 to 05 can also be run straight away from the tables in `data/clean/`.
4. To view the page, run `python -m http.server 8000` in the `docs` folder and open http://localhost:8000. The page cannot load its data when opened as a file.

Raw files used:

- Public Data Portal (data.go.kr): 한국철도공사_KTX 월별 역별 승하차 (KTX boardings and alightings by station and month) and 한국철도공사_KTX 구간별 통계 데이터 (KTX statistics by section).
- Korean Railway Statistics (railstat.korail.com), 주제별통계 > 지역간철도, downloaded as CSV with codes: 역별 여객 승하차 실적(KTX,SRT), 역별 여객승하차 실적(총계), 역별 여객 승하차 실적(KTX) 2004 to 2015, 연도별 여객수송(인원), 선별 여객 수송실적(인원) 2004 to 2015 and 2016 to 2024, 열차종별 운행횟수, 철도사고·운행장애 발생현황, 연도별 운수수입실적.
- KORAIL metro rail statistics (info.korail.com, 광역철도 수송통계): the 2024 and 2025 transport and hourly workbooks, and the 2019 monthly station workbook.

## Credits

- Data: Korea Railroad Corporation (KORAIL), through the Public Data Portal (https://www.data.go.kr), the Korean Railway Statistics portal (https://railstat.korail.com) and KORAIL's metro rail statistics (https://info.korail.com). SRT figures as published in the Korean Railway Statistics. The Public Data Portal lists these datasets as free to use with no restriction on the scope of use.
- Fonts: Archivo (Omnibus-Type), Source Serif 4 (Adobe) and Noto Sans KR (Google), all under the SIL Open Font License 1.1.
- Charts: Plotly.js 2.35.2 (MIT licence), served from jsDelivr; matplotlib.

This is an independent project, not affiliated with or endorsed by KORAIL, SR or any of the sources.

## Licence

The code (notebooks, HTML and JavaScript) is under the MIT licence; see `LICENSE`. The tables I made in `data/clean/` and `docs/data/` are under CC BY 4.0: please credit "Lik Ren Tai, from KORAIL open data". The original KORAIL data stays under its own terms, and the fonts under the SIL Open Font License.

Lik Ren Tai, November 2026
