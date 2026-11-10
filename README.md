# LJH Haiti Readiness Monitor

## Dashboard and CSV publishing

This directory owns the frontend (`index.html`) and its deployed CSV files under `data/`.

All SQL source files and the hourly extraction job now live in the separate private repository:
[cap-git-01/tapin-haiti-data-pipeline](https://github.com/cap-git-01/tapin-haiti-data-pipeline).

The pipeline executes the three canonical SQL files and writes:
- `data/readiness.csv` — team readiness snapshot (contact identifiers removed before publishing)
- `data/readiness_trend.csv` — historical trend extract
- `data/contacts.csv` — NOT automatically refreshed: contains contact details, pending access policy

The pipeline commits the first two CSV files to this repository; the existing Cloudflare Pages Git integration, if enabled, should then deploy them. The workflow must be configured with SSH/database secrets and a scoped Git token before this works. No successful production pipeline run is asserted here.

## Local preview

From this directory run `python -m http.server 8000` and open http://localhost:8000.

## Data caveats

- Historical membership is reconstructed from timestamps and may omit status changes.
- The current day is partial until it ends.
- Trend cohorts follow current team assignments and may not represent historical team/division membership.
- The contacts dataset contains personally identifiable information and must not be published without an approved access model.
- The source queries are maintained only in the pipeline repository.
