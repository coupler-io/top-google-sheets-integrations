---
title: Connect Instagram Ads to Google Sheets with Coupler.io
slug: connect-instagram-ads-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-ads-to-google-sheets.md
source: Instagram Ads
destination: Google Sheets
meta_title: Connect Instagram Ads to Google Sheets with Coupler.io
meta_description: Export Reports and Insights, List of Campaigns, List of Ad sets, and List of Ads from Instagram Ads into Google Sheets for a live Data Studio report.
---

![Instagram Ads](https://static.coupler.io/importers/instagram-ads.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Instagram Ads to Google Sheets with Coupler.io

Instagram ads are bought inside Meta's ads tools, which were built to edit delivery, not to hold a shared history. Coupler.io refreshes Instagram Ads into Google Sheets for you, which gives a Data Studio dashboard a workbook to sit on.

## How to export Instagram Ads data to Google Sheets

Four categories: Reports and Insights, List of Ad sets, List of Campaigns, and List of Ads.

### Step 1. Basic settings

- **Ad accounts** — which accounts this flow reads. Select every account that should land in the same import.
- **Report type** — Reports and Insights, or one of the three lists. The rest of the setup follows that pick.

### Step 2. Report period

- **Start date** — opening day of the analytics window. The relative picker (*days ago*, *this month*, *last month*, *this year*, *last year*) covers the usual cases. Use `{{365daysago}}` only when you need a trailing year the presets do not name.
- **End date** — closing day of that window, kept relative so the sheet does not stall on the afternoon you configured it.
- **Split data by period** — Daily, Weekly, Monthly, or Totals only. The untouched setting is a daily breakdown.

### Step 3. Metrics and dimensions

- **Metrics and dimensions** — columns on Reports and Insights. Pick the handful a chart can actually show, and leave the rest out of the sheet.
- **Breakdowns** — further cuts on that insight extract, stored as their own columns in the sheet.

### Step 4. Advanced settings

- **Attribution settings** — whose window the sheet copies. Take Use ad account settings to mirror the account, take Use ad group settings to mirror the ad set, or take Specify manually when one rule has to cover every account.
- **Action attribution windows** — the lookback that still counts a result. Options include 1 day click, 7 days click, 28 days click, 1 day view, 1 day engaged view, DDA, Incrementality, and Skan click.
- **Filters** — Graph API syntax that removes rows before import, so a draft campaign never reaches the client tab.

### Step 5. Blend and transform data

Finish the Instagram rows prior to the write.

- **Column management** — retain the Metrics and dimensions you picked, hide the rest, and rename headers a client will not decode.
- **Join** — line Reports and Insights up with List of Campaigns, List of Ad sets, and List of Ads so a name sits on every insight row.
- **Append** — place a second account's extract under the first when two clients share a workbook.
- **Aggregate** — if Split data by period is Daily, roll to the week the status meeting uses.
- **Custom SQL** — a condition Filters could not spell, applied before the cells are filled.

### Step 6. Google Sheets destination

Insight columns and list columns show up already headed. You only say where the block sits. There is no hand-built column map.

- **Sheet** — the tab to fill, or a fresh name. Coupler.io adds a new sheet after the last tab.
- **Cell address / Range** — A1 writes from the top-left. D1 or B5 shifts that corner. B5:G10 limits the import to the rectangle.

### Step 7. Schedule

Choose a refresh from every 15 minutes up through once a month. A replace run keeps a single current block for the Data Studio chart. An append run stacks each new extract under the rows already there.

### Bonus: or just ask the AI Agent to build it for you

Inside the Coupler.io app, the right sidebar is the AI Agent. Ask it for the sheet directly:

> Load Instagram Ads Reports and Insights into Google Sheets, split Weekly, on a sheet named IG ads.

It chooses Report type, the date fields, Metrics and dimensions, and Breakdowns, and it checks with you when Ad accounts could go more than one way.

You still:

1. Connect Instagram Ads yourself.
2. Scope the Ad accounts.
3. Connect Google Sheets and pick the spreadsheet in the file picker.
4. Name the sheet, and the cell if it should not begin at A1.

## What data can you export from Instagram Ads to Google Sheets with Coupler.io?

Four categories. One flow, one Report type. Coupler.io's Join can set List of Campaigns and List of Ad sets beside Reports and Insights in the sheet a Data Studio report reads, so names are already on the insight rows.

- **Reports and Insights** — delivery for the Ad accounts and dates you set, with columns from Metrics and dimensions, slices from Breakdowns, and credit rules from Action attribution windows.
- **List of Ad sets** — the ad set inventory, so setup detail has a list of its own to join onto insights.
- **List of Campaigns** — campaign names and records, the labels a Data Studio filter should use instead of raw ids.
- **List of Ads** — the ad inventory, which you can join to insights when the question is which ad ran.

## Why export Instagram Ads to Google Sheets — real life cases

A Data Studio report on a Coupler.io sheet is the practical way to review Instagram paid media with people who should not be handed an ads login.

- **Scorecard for the accounts on the slide**

  Reports and Insights is the Report type, Ad accounts is limited to the accounts on the slide, and Split data by period is Daily or Totals only. Metrics and dimensions is the column list. The Data Studio scorecard tiles read those columns from the sheet.

- **A campaign name the filter can use**

  List of Campaigns holds the names. Coupler.io's Join places that catalog onto the Reports and Insights rows before the import, so the sheet is not stuck on an id. The Data Studio filter is a campaign name.

- **Ad set setup beside the result**

  List of Ad sets is how the ad set was built. Reports and Insights is what that ad set did. Coupler.io's Join matches the two on the way into the sheet, and the Data Studio page shows setup and result together.

- **Ads present in the catalog that never spent**

  List of Ads includes ads that exist even when they did not deliver. Coupler.io's Join pairs that inventory with Reports and Insights. The Data Studio report flags rows that are on the list and missing from delivery.

- **Weekly rows, then one month figure**

  Reports and Insights with Split data by period on Weekly, and Start date on *this month* or *last month*, matches the client email. Coupler.io's Aggregate collapses those weeks when the deck wants a single month figure. The Data Studio report you send uses the collapsed sheet.

- **One click window on every account**

  Attribution settings left on Use ad account settings keeps each account's own rule. Specify manually, with an Action attribution windows value such as 7 days click, makes the accounts comparable. The Data Studio report lines Ad accounts up under that shared window.

- **Two clients in one workbook**

  Filters keeps each extract to the campaigns that client should see. Coupler.io's Append stacks the two Reports and Insights results into one sheet. The Data Studio report switches clients from that sheet.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
- [Connect Google Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md)
- [Connect Google Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-analytics-to-google-sheets.md)
- [Connect Google Search Console to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-search-console-to-google-sheets.md)
- [Connect Instagram Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-insights-to-google-sheets.md)
- [Connect LinkedIn Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-ads-to-google-sheets.md)
- [Connect LinkedIn Public Data to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-public-data-to-google-sheets.md)
- [Connect Microsoft Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-microsoft-ads-to-google-sheets.md)
- [Connect QuickBooks to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-quickbooks-to-google-sheets.md)
- [Connect Shopify to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md)
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
