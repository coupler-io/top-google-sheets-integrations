---
title: Connect LinkedIn Ads to Google Sheets with Coupler.io
slug: connect-linkedin-ads-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-ads-to-google-sheets.md
source: LinkedIn Ads
destination: Google Sheets
meta_title: Connect LinkedIn Ads to Google Sheets with Coupler.io
meta_description: Export Ad analytics by single dimension, Sponsored leads, and Conversions from LinkedIn Ads into Google Sheets for live Data Studio dashboards.
---

![LinkedIn Ads](https://static.coupler.io/importers/linkedin.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect LinkedIn Ads to Google Sheets with Coupler.io

Campaign Manager is where media gets bought. It is an awkward place to keep a sheet that sales, finance, and an agency all refresh from. Coupler.io delivers LinkedIn Ads into Google Sheets at the interval you set, leaving a Data Studio dashboard a current sheet to chart.

## How to export LinkedIn Ads data to Google Sheets

Eleven report types, from single-dimension and multi-dimension analytics through member-dimension performance, sponsored leads, users, campaign groups, campaigns, creatives, video ads, sponsored shares, and conversions.

### Step 1. Basic settings

- **Ad accounts** — the accounts included in this flow. Select each one that should share the import.
- **Report type** — one of the eleven categories. Analytics, lead, and catalog extracts do not share a single shape, so they stay in separate flows.

### Step 2. Report period

- **Start date** — first day of the window. Prefer *days ago*, *this month*, *last month*, *this year*, or *last year* over a fixed date you will have to edit. The advanced macro `{{365daysago}}` holds a trailing year when the picker cannot.
- **End date** — last day. A relative end means the next scheduled run is still about the present.
- **Split data by period** — Totals only, Daily, Monthly, or Yearly. Pick the grain the Data Studio chart will use, or a finer one you plan to roll up later.

### Step 3. Metrics and dimensions

- **Metrics** — up to 18 metrics on the analytics report. A second flow covers anything that does not fit in that set.
- **Dimension** — the single cut on a report that takes one dimension. Campaign is the usual choice when the page is a campaign trend.
- **Dimensions** — one or more of Account, Campaign, Campaign group, Card index, Company, Campaign objective type, Conversion, Creative, Impression device type, Placement name, Serving location, and Shares (creative sponsored content).

### Step 4. Advanced settings

- **Advanced filters** — extra limits on the extract so a status, group, or other condition you can express here never lands in the sheet.
- **Lead generation forms** — on Sponsored leads, name the forms to fetch. Blank brings leads from every form.

### Step 5. Blend and transform data

Reshape LinkedIn rows before they occupy cells.

- **Column management** — order Metrics beside Dimension, drop empty catalog fields, and give the remaining headers names the sheet's readers already use.
- **Join** — match Ad analytics by single dimension to Campaign groups, Creatives, or Conversions so catalog attributes sit on the analytic row.
- **Append** — stack Sponsored leads from two Ad accounts into one lead tab.
- **Aggregate** — roll a Daily split up to Monthly or Yearly when the dashboard's grain is coarser than the extract.
- **Custom SQL** — keep only rows for a Dimensions value such as Company when Advanced filters was the wrong place for that cut.

### Step 6. Google Sheets destination

Whichever Dimensions you selected arrive as columns, in the order the extract built them. You name the tab and the cell. Coupler.io does the column layout from the data.

- **Sheet** — the tab for this report. A name that is not already there becomes a new sheet after the last tab.
- **Cell address / Range** — unset, the first cell is A1. B5 or D1 anchors the block elsewhere, which matters when row 1 already has notes. B5:G10 bounds the write to that range.

### Step 7. Schedule

Every 15 minutes, hourly, daily, weekly, or monthly. Replace the range when the tab should show only the latest LinkedIn window. Append new rows under it when each extract has to remain underneath the last one.

### Bonus: or just ask the AI Agent to build it for you

The right sidebar of the Coupler.io app holds the AI Agent. Hand it the report in a sentence:

> Load Ad analytics by single dimension for my LinkedIn Ads accounts into Google Sheets, split Monthly, with Campaign as the Dimension.

It fills Report type, dates, Split data by period, Metrics, and Dimension or Dimensions. It asks before it guesses an account list.

You still:

1. Connect LinkedIn Ads with your own access.
2. Scope Ad accounts.
3. Connect Google Sheets and pick the spreadsheet in the file picker.
4. Name the sheet, and set a cell other than A1 when the block should not start there.

## What data can you export from LinkedIn Ads to Google Sheets with Coupler.io?

Eleven report types. One flow each. Coupler.io's Join can put Campaign groups, Creatives, and Conversions next to Ad analytics by single dimension before the sheet is saved, so Data Studio does not have to blend those tabs itself.

- **Ad analytics by single dimension** — performance cut by one Dimension, on a Split data by period of Totals only, Daily, Monthly, or Yearly, with up to 18 Metrics.
- **Ad analytics by multiple dimensions** — the same style of analytics with Dimensions, so Campaign can share the row with Placement name, Impression device type, or Company.
- **Campaign performance by member dimension** — campaign results broken by the member dimension that report exposes, for questions about who saw the media.
- **Sponsored leads** — form fills, narrowed with Lead generation forms or left open to every form on the account.
- **Ad account users** — who has access to the Ad accounts, a reference list for an access review.
- **Campaign groups** — the group records that sit above campaigns, useful once Join attaches them to analytics.
- **Campaigns** — the campaign catalog, separate from the analytic grain, so names and settings have their own extract.
- **Creatives** — creative records you can join when Dimension or Dimensions includes Creative.
- **Video ads** — the video-ad inventory, distinct from the broader Creatives list.
- **Shares (creative sponsored content)** — sponsored share records, also available as a Dimensions value on multi-dimension analytics.
- **Conversions** — conversion records, which Join can align to analytics that use Conversion as a dimension.

## Why export LinkedIn Ads to Google Sheets — real life cases

Pipeline reviews go faster when LinkedIn Ads lives in a Data Studio report that reads a sheet, rather than in a Campaign Manager tab only one person can open.

- **Campaign line over days or months**

  Ad analytics by single dimension is the Report type, Dimension is Campaign, and Split data by period is Daily or Monthly. Metrics stays inside the 18-metric cap. The Data Studio trend chart reads this sheet.

- **Placement and device together**

  Ad analytics by multiple dimensions lets Dimensions hold Campaign, Placement name, and Impression device type on one row. A Daily extract is finer than a monthly page, so Coupler.io's Aggregate rolls it before the write. The Data Studio report uses that rolled sheet.

- **Member cut for the sales meeting**

  Campaign performance by member dimension is its own Report type. It is not a value you can tick under Dimensions, so it needs a separate flow and its own tab. The Data Studio sales report places that tab next to the campaign trend.

- **Sponsored leads from two accounts**

  Sponsored leads uses Lead generation forms when only some forms matter, and leaves it blank when every form should come through. Coupler.io's Append stacks two Ad accounts into one lead sheet, then Coupler.io's Join adds Campaigns so the campaign name travels with the lead. The Data Studio report counts that sheet by campaign.

- **Who can change the account**

  Ad account users is the roster of people with access. Metrics does not apply to this Report type. The Data Studio report is a table on that sheet for the access review.

- **Planning at campaign-group level**

  Campaign groups is the catalog, and Campaign group is the Dimension on Ad analytics by single dimension. Coupler.io's Join adds catalog fields from Campaign groups onto the analytic rows. The Data Studio planning report breaks the page by Campaign group.

- **Creatives beside the video inventory**

  Set Dimension to Creative on Ad analytics by single dimension for the performance side. Coupler.io's Join brings in the Creatives report, while Video ads and Shares (creative sponsored content) stay on neighboring tabs. The Data Studio report compares creative performance with the video inventory.

- **Company, objective, and conversions**

  On Ad analytics by multiple dimensions, Dimensions can be Company and Campaign objective type, with Split data by period on Yearly or Totals only. Coupler.io's Join aligns the Conversions report where Conversion is already a dimension on the row. The Data Studio planning report reads that prepared sheet.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
- [Connect Google Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md)
- [Connect Google Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-analytics-to-google-sheets.md)
- [Connect Google Search Console to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-search-console-to-google-sheets.md)
- [Connect Instagram Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-ads-to-google-sheets.md)
- [Connect Instagram Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-insights-to-google-sheets.md)
- [Connect LinkedIn Public Data to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-public-data-to-google-sheets.md)
- [Connect Microsoft Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-microsoft-ads-to-google-sheets.md)
- [Connect QuickBooks to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-quickbooks-to-google-sheets.md)
- [Connect Shopify to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md)
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
