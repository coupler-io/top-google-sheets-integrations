---
title: Connect TikTok Ads to Google Sheets with Coupler.io
slug: connect-tiktok-ads-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md
source: TikTok Ads
destination: Google Sheets
meta_title: Connect TikTok Ads to Google Sheets with Coupler.io
meta_description: Load the Basic campaign report and Dynamic Showcase Ads (DSA) report from TikTok Ads into Google Sheets for live Data Studio dashboards.
---

![TikTok Ads](https://static.coupler.io/importers/tiktok.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect TikTok Ads to Google Sheets with Coupler.io

TikTok Ads Manager scatters auction delivery, audience cuts, playable creatives, GMV Max, and Dynamic Showcase Ads across separate reports, and a file saved this morning is old by tomorrow. Coupler.io puts the report you choose into Google Sheets each time the schedule runs, so a Data Studio dashboard can read a sheet that keeps moving.

## How to export TikTok Ads data to Google Sheets

The flow covers auction reporting at campaign, ad group, ad, and advertiser level, audience reports, playable ads, GMV Max, Dynamic Showcase Ads (DSA), and the Campaigns and Ads lists.

### Step 1. Basic settings

- **Report type** — which of the 18 reports this flow pulls. The full names, including every Dynamic Showcase Ads (DSA) report, are in the data section below. One flow holds one report type.
- **Ad accounts** — the advertiser accounts to include. If an account is missing, reconnect TikTok and return to this list.
- **Stores** — the shops whose commerce results belong in the flow. Fill this when the report is about store sales, including a GMV Max campaign report. Standard auction reports stay focused on the ad accounts you already selected.

### Step 2. Report period

- **Start date** — the first day of the pull. Relative options include *days ago*, *this month*, *last month*, *this year*, and *last year*, and they shift on later runs. When a preset is too blunt, write the macro `{{365daysago}}`.
- **End date** — the closing day. A relative end date means the next scheduled run does not need a new close.
- **Split data by period** — how finely time is broken on the rows. The wizard shows the grains this report type allows.

### Step 3. Metrics and dimensions

- **Metrics** — the measures included as columns. Choose the delivery, cost, and result figures the Data Studio chart needs, and leave the rest off the sheet.
- **Audience dimensions** — breakdowns for audience reports: Gender, Age, Country code, Province, DMA region, Behavior, Device brand, Ac, Language, Platform, Interest category, Interest category second level, Interest category third level, Interest category fourth level, Placement, and Contextual tag.
- **DSA dimensions** — catalog breakdowns for Dynamic Showcase Ads: Catalog id, Product set id, Product id, and Sku id.
- **Targeting dimension** — a single targeting cut. The options are Country code and Ad type.
- **Asset dimension** — which creative piece the row describes. Options are Component name, Customer event type, Event source id, Image id, Minis id, Page id, Post id, Room id, and Video material id.
- **Search dimension** — the search cut. The option is Search terms.

### Step 4. Advanced settings

- **Advanced filters** — conditions that drop rows before Google Sheets sees them. Use columns from the report you picked, such as a country or a catalog id, so test activity stays out of the dashboard range.

### Step 5. Blend and transform data

TikTok rows are easier to chart after Coupler.io reshapes them.

- **Column management** — keep Gender, Age, Country code, and the cost metrics, hide the rest, and rename labels the buying team does not recognize.
- **Join** — attach a Dynamic Showcase Ads (DSA) report to store or product data on Catalog id, Product id, or Sku id. The stitch happens before the sheet is written.
- **Append** — place a Basic campaign report under an Audience campaign report when both grains should share a tab.
- **Aggregate** — roll a fine Split data by period up to the month finance already uses.
- **Custom SQL** — isolate Upgraded Smart+ creatives, or keep Search terms that clear a threshold you write in the query.

### Step 6. Google Sheets destination

Columns follow the TikTok report. Coupler.io lays them out from the data.

- **Sheet** — pick a tab that already exists, or type a new tab name. Coupler.io adds a new sheet after the last one.
- **Cell address / Range** — the cell where values start, A1 unless you move it. A single cell such as D1 works, and so does an exact range such as B5:G10 when this block must sit beside another import.

### Step 7. Schedule

Choose every 15 minutes, hourly, daily, weekly, or monthly. Replacing overwrites the cells Coupler.io wrote last time. Appending leaves those cells and adds the new pull underneath, which is how a GMV Max sheet can grow a log without losing last week.

### Bonus: or just ask the AI Agent to build it for you

Skip the field-by-field setup if you would rather say it in a sentence. Open the Coupler.io AI Agent from the right sidebar:

> "Pull a Basic campaign report and an Audience campaign report from TikTok Ads, with Gender and Age, into Google Sheets for last month."

You still:

- Connect TikTok Ads.
- Scope the Ad accounts, and the Stores when the report needs shops.
- Connect Google Sheets and select the spreadsheet in the file picker. That file choice stays manual.
- Name the sheet. Set the cell or range when A1 is the wrong corner.

## What data can you export from TikTok Ads to Google Sheets with Coupler.io?

There are 18 TikTok Ads report types, and each one is a separate flow. Coupler.io's Join can stitch a Dynamic Showcase Ads (DSA) report to another source on Catalog id or Product id before the rows reach Google Sheets. Data Studio then charts the sheet Coupler.io already combined.

- **Basic campaign report** — auction results at campaign level, the grain most pacing sheets start from.
- **Basic ad group report** — the same delivery story one level down, where budget and bidding usually change.
- **Basic ad report (Upgraded Smart+ by ad)** — Upgraded Smart+ results reported on the ad.
- **Basic ad report (Upgraded Smart+ by creative)** — Upgraded Smart+ results reported on the creative, so you can see which asset carried the ad.
- **GMV Max campaign report** — campaign reporting for GMV Max, with Stores selected when the sales belong to a shop.
- **Campaigns** — the campaign list itself, useful as the lookup Coupler.io's Join matches to a performance flow.
- **Ads** — the ad list, the companion lookup for ad-level metrics.
- **Basic advertiser report** — totals at advertiser level when a Data Studio scorecard should not repeat every campaign.
- **Audience campaign report** — campaign metrics split by the Audience dimensions you tick, such as Gender, Age, or Placement.
- **Audience advertiser report** — the same audience cuts rolled to the advertiser.
- **Audience ad report** — audience splits on the ad, which is the grain for creative-and-audience questions.
- **Audience ad group report** — audience splits on the ad group.
- **Playable Ad report** — performance of playable ads.
- **Playable Ad report by country** — playable ads split by country, for a market-by-market sheet.
- **Dynamic Showcase Ads (DSA) campaign report** — DSA results at campaign level.
- **Dynamic Showcase Ads (DSA) report** — the main DSA pull, where Catalog id, Product set id, Product id, and Sku id belong.
- **Dynamic Showcase Ads (DSA) advertiser report** — DSA totals for the advertiser.
- **Dynamic Showcase Ads (DSA) ad group report** — DSA results at ad group level.

## Why export TikTok Ads to Google Sheets — real life cases

Coupler.io Joins Dynamic Showcase rows to product data, Appends audience reports under campaign reports, and Aggregates a fine time split so a Data Studio dashboard can chart one Google Sheet.

- **Morning spend check**

  Basic campaign report for the Ad accounts you ticked, with Start date on *last month*, is the range a Data Studio pacing report refreshes from. Column management can leave cost and delivery columns and hide the rest of the header. The page compares those accounts without a new file from Ads Manager.

- **Smart+ assets versus Smart+ ads**

  Point a Data Studio ranking at Basic ad report (Upgraded Smart+ by creative) when the row should be the asset. Point a second ranking at Basic ad report (Upgraded Smart+ by ad) when the row should stay the ad. Each report keeps its own sheet, and the dashboard links the two pages.

- **GMV Max next to orders**

  Fill Stores and load a GMV Max campaign report. Coupler.io's Join can attach order rows on a shared key before anything is written. The Data Studio commerce page shows shop delivery and those orders together.

- **Gender, age, and country cuts**

  Audience campaign report with Audience dimensions Gender, Age, and Country code feeds a Data Studio demographic page. Province, DMA region, and Interest category are on that same list when the cut has to go further. The dashboard filters Country code and plots Age beside Gender.

- **Catalog ids on showcase ads**

  Dynamic Showcase Ads (DSA) report with DSA dimensions Catalog id, Product id, and Sku id gives every product a stable key in the sheet. Product set id is the other value on that picker. A Data Studio table ranks those ids by the metrics kept on the flow.

- **Playables, then playables by country**

  Playable Ad report is the creative sheet, and Playable Ad report by country is the market sheet. Append both in Coupler.io when the workbook should carry the two grains. Data Studio's market page reads the country tab.

- **Search terms worth keeping**

  Set Search dimension to Search terms, then use Advanced filters so junk queries never reach the cells. The Data Studio report is a filterable list of what remains. Buyers work from the sheet Coupler.io already narrowed.

- **Creative piece and target**

  Asset dimension values Video material id, Image id, and Component name tell a Data Studio creative report which piece served. Targeting dimension contributes either Country code or Ad type. Column management holds the sheet to that short column set so the chart stays readable.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
- [Connect Google Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md)
- [Connect Google Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-analytics-to-google-sheets.md)
- [Connect Google Search Console to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-search-console-to-google-sheets.md)
- [Connect Instagram Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-ads-to-google-sheets.md)
- [Connect Instagram Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-insights-to-google-sheets.md)
- [Connect LinkedIn Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-ads-to-google-sheets.md)
- [Connect LinkedIn Public Data to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-public-data-to-google-sheets.md)
- [Connect Microsoft Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-microsoft-ads-to-google-sheets.md)
- [Connect QuickBooks to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-quickbooks-to-google-sheets.md)
- [Connect Shopify to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
