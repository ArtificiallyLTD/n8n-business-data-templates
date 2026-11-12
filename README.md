# n8n templates for business data

Ready-to-import [n8n](https://n8n.io) workflows that pull fresh business data on a schedule and drop it where your team already works: Google Sheets and Slack. Each one calls an [Apify](https://apify.com/artificially) Actor through the Apify API, so there is nothing to host and no scraper to maintain.

| Template | What it does | Schedule | Data source |
| --- | --- | --- | --- |
| [Daily LinkedIn jobs to Google Sheets](linkedin-jobs-to-google-sheets.json) | Adds new LinkedIn jobs for your keywords and location to a sheet, without duplicates | Daily, 8:00 | [LinkedIn Jobs Scraper](https://apify.com/artificially/linkedin-jobs-scraper) |
| [New SAM.gov opportunities to Slack](samgov-opportunities-to-slack.json) | Posts one Slack digest of new federal contract opportunities matching your NAICS codes | Weekdays, 8:00 | [SAM.gov Contract Opportunities Scraper](https://apify.com/artificially/samgov-opportunities-scraper) |
| [Competitor hiring tracker](competitor-hiring-tracker.json) | Logs new roles from competitors' career sites (Greenhouse, Lever, Ashby, Workable and more) | Mondays, 8:00 | [Career Site Jobs Scraper](https://apify.com/artificially/career-site-jobs-scraper) |
| [Tech stack enrichment](website-tech-stack-enrichment.json) | Fills a sheet of domains with each site's CMS, ecommerce, analytics, CRM, email provider and payments | On demand | [Website Tech Stack Detector](https://apify.com/artificially/website-tech-stack-detector) |
| [New YC companies to Google Sheets](yc-new-companies-to-google-sheets.json) | Adds companies that newly appear in the Y Combinator directory, optionally by industry or hiring status | Mondays, 7:00 | [Y Combinator Scraper](https://apify.com/artificially/ycombinator-scraper) |

## Setup

1. **Import:** in n8n, open *Workflows → Import from file* (or paste the JSON into a new workflow).
2. **Apify token:** create a free [Apify account](https://console.apify.com/sign-up) and copy your API token from *Settings → API & Integrations*.
3. **Credential:** in n8n, add a **Header Auth** credential named `Apify API token` with header name `Authorization` and value `Bearer YOUR_TOKEN`.
4. **Connect and edit:** connect Google Sheets or Slack, then edit the **Settings** node (keywords, NAICS codes, companies). The sticky note in each workflow lists the exact steps.

## How it works

Each workflow calls the Apify endpoint `run-sync-get-dataset-items`, which runs the Actor and returns its results in one request (up to 5 minutes). The monitoring templates use the Actors' `onlyNewSinceLastRun` option, so every run returns only items you have not seen before. That state is kept in your own Apify account, per filter set.

## Cost

You pay each Actor's price on your Apify account (a small fee per run plus a fee per result); there is no subscription. Apify's free plan includes monthly credit for trying them out. For example, the daily LinkedIn jobs workflow saving 50 jobs a day costs about $10 a month. Each Actor's Store page lists its current price.

## Tested with

n8n 2.44, HTTP Request node 4.2, Google Sheets node 4.5, Slack node 2.2. Every template was run against the live Actors before publishing.

## License

MIT. Built by [Artificially](https://apify.com/artificially).
