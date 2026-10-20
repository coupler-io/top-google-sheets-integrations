---
title: Connect Facebook Ads to Google Sheets with Coupler.io
slug: connect-facebook-ads-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md
source: Facebook Ads (Meta Ads)
destination: Google Sheets
meta_title: Connect Facebook Ads to Google Sheets with Coupler.io
meta_description: Export Reports and Insights, List of Sponsored Leads, and List of Business invoices from Facebook Ads into Google Sheets for live Data Studio dashboards.
---

![Facebook Ads](https://static.coupler.io/importers/facebook.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Facebook Ads to Google Sheets with Coupler.io

Ads Manager is a buying screen. Pulling a durable extract for someone who does not have a Meta seat means another CSV, another date range, and another argument about which export was current. Coupler.io puts Facebook Ads into Google Sheets on the cadence you choose, and that sheet is what a Data Studio dashboard should read.

## How to export Facebook Ads data to Google Sheets

Nine categories sit under Report type: performance insights, sponsored leads, creatives, ad sets, campaigns, ads, ads with creatives, the activity log, and business invoices.

### Step 1. Basic settings

- **Report type** — one category per flow. The later screens follow that choice, so pick the list or the insight extract before you touch dates.
- **Ad accounts** — the accounts this flow is allowed to read. Tick every account that should share the sheet.
- **Pages** — the Pages to read when the category is tied to a Page rather than only to an ad account.
- **Businesses** — the Business Manager accounts whose invoices you want, used when Report type is List of Business invoices.

### Step 2. Report period

- **Start date** — a moving window. *days ago*, *this month*, *last month*, *this year*, and *last year* all roll forward after you save. A full trailing year that the presets cannot express is the advanced macro `{{365daysago}}`.
- **End date** — where the window stops. A relative end keeps the next run from freezing on the day you built the flow.
- **Split data by period** — Daily, Weekly, Monthly, or Totals only. Daily is the grain you get if you leave the control alone.

### Step 3. Date filters

These four fields bound List of Business invoices. They do not replace Start date on an insights flow.

- **Billing start date** — first billed month to include. Leave it empty and the extract starts six months back.
- **Billing end date** — last billed month. Empty runs through today.
- **Issue start date** — use this when you care about the day Meta issued the invoice. Setting it turns the billing-period filter off.
- **Issue end date** — newest issue date still allowed in the sheet.

### Step 4. Metrics and dimensions

- **Metrics and dimensions** — the columns on Reports and Insights. Start from the defaults and add only the measures the Data Studio chart will plot.
- **Breakdowns** — extra slices on that same insight extract, so one flow can carry more than a single total.

### Step 5. Advanced settings

- **Attribution settings** — where the credit rule comes from. Use ad account settings follows the account. Use ad group settings follows the ad set. Specify manually is the override when every account in the flow must share one rule.
- **Action attribution windows** — how long a click or view still counts. Real choices include 1 day view, 1 day click, 7 days click, 28 days click, DDA, Incrementality, Skan view, and Skan click.
- **Filters** — a Graph API filter that drops rows before they reach the sheet, so a paused test campaign never becomes a Data Studio point.
- **Lead generation forms** — on List of Sponsored Leads, limit the extract to named forms. Leave the field blank and every form on the selected Pages comes through.
- **Ad creative columns** — for creative extracts, tick attributes such as Creative name, Body, Title, Call to action type, Image URL, Link URL, or Instagram permalink URL. Blank means all of them. Core ad properties still arrive either way.
- **Updated since** — on ad lists, ignore ads that have not changed since the date you set.

### Step 6. Blend and transform data

Shape the Meta extract before Google Sheets sees it.

- **Column management** — hide delivery fields no chart uses, rename API-style headers, and put Creative name next to the measures you kept.
- **Join** — match Reports and Insights to List of Campaigns, List of Ad sets, or List of Ads with ad creatives on the shared id, so names and numbers occupy one tab.
- **Append** — stack a second ad account, or a second paid source, under the Meta rows when one workbook has to hold the portfolio.
- **Aggregate** — collapse a Daily split into the weekly or monthly block the dashboard actually shows.
- **Custom SQL** — a query over those rows when you need a condition Filters cannot express, such as campaigns that also appear in List of Activities.

### Step 7. Google Sheets destination

Facebook columns arrive in the order the extract produced them. You choose the tab and the starting cell. You do not draw a column map.

- **Sheet** — an existing tab, or a name that does not exist yet. A new sheet is created after the last tab in the file.
- **Cell address / Range** — the default start is A1. A lone cell such as B5, or D1 if the block should begin in column D, moves that corner. An exact range such as B5:G10 keeps the write inside those cells.

### Step 8. Schedule

Choose every 15 minutes when a media buyer is watching the day, or hourly, daily, weekly, or monthly for a calmer tab. Each run can replace the range already in the sheet or append new rows under it. Insight jobs and retries stay with Coupler.io.

### Bonus: or just ask the AI Agent to build it for you

You can skip the screens. The AI Agent sits in the right sidebar of the Coupler.io app. Describe the sheet in ordinary language:

> Load Reports and Insights for my Facebook Ad accounts into Google Sheets, split Daily, on a sheet named Meta insights starting at A1.

It selects Report type, Metrics and dimensions, Breakdowns, and the date window, and it asks when a choice is really yours.

You still:

1. Connect Facebook Ads by signing in to Meta.
2. Scope Ad accounts, Pages, and Businesses.
3. Connect Google Sheets and pick the spreadsheet in the file picker.
4. Name the sheet, and set the cell if the import should not start at A1.

## What data can you export from Facebook Ads to Google Sheets with Coupler.io?

Nine categories. One flow exports one Report type. Coupler.io's Join can attach List of Campaigns, List of Ad sets, and List of Ads with ad creatives to Reports and Insights before any tab is written, so the Data Studio dashboard charts structure and delivery from a single sheet.

- **Reports and Insights** — the performance extract. Columns come from Metrics and dimensions, time grain from Split data by period, and credit rules from Attribution settings.
- **List of Sponsored Leads** — people who submitted a lead form, scoped with Lead generation forms and Pages, ready for a handoff sheet sales can open.
- **List of Ad creatives** — the creative library, including Creative name, Body, Title, Call to action type, Image URL, and Link URL, whether or not an ad is spending.
- **List of Ad sets** — ad set records for the Ad accounts you ticked, so targeting and budget setup have a home next to delivery.
- **List of Campaigns** — campaign records for those same accounts, the names a Data Studio filter should use.
- **List of Ads** — one row per ad. Updated since keeps scheduled runs focused on ads that actually changed.
- **List of Ads with ad creatives** — the ad and its creative columns in one extract, which saves a Join when the question is which Title ran.
- **List of Activities** — the account change feed, so a budget edit or a paused ad has a timestamp beside the trend.
- **List of Business invoices** — what Meta billed the Businesses you selected, cut by Billing start date and Billing end date, or by Issue start date and Issue end date.

## Why export Facebook Ads to Google Sheets — real life cases

Media, finance, and client leads read Meta through a Data Studio dashboard on this sheet, because Ads Manager is a poor shared scorecard.

- **Daily insight wall**

  Reports and Insights is the Report type, Split data by period stays on Daily, and Metrics and dimensions is cut to the measures the wall chart plots. When Monday wants a week instead of a day, Coupler.io's Aggregate rolls those rows before they are written. The Data Studio dashboard is pointed at the grain you saved.

- **Which Title spent**

  List of Ads with ad creatives brings Creative name, Body, Title, Call to action type, and Image URL. Coupler.io's Join binds that list to Reports and Insights on the ad, so creative columns and delivery columns share a row. The Data Studio report ranks Title from that sheet.

- **Form fills sales can open**

  List of Sponsored Leads uses Pages for the Pages that own the forms, and Lead generation forms either names the forms or stays blank. Coupler.io's Join adds List of Ads so each submission keeps the ad that collected it. A Data Studio report on the joined sheet counts fills by form.

- **What finance was billed**

  List of Business invoices is limited with Businesses, then Billing start date and Billing end date, or Issue start date and Issue end date when the issue day is the cut. Coupler.io's Join matches those bills to Reports and Insights on the same Ad accounts. The Data Studio page is the tie-out of invoice against delivery.

- **Edits sitting on the trend**

  List of Activities is who changed the account and when. Coupler.io's Join lines that feed up with a Daily Reports and Insights extract by date. The Data Studio trend marks those dates, so a paused ad is not read as a drop in demand.

- **What is actually in the account**

  List of Campaigns, List of Ad sets, and List of Ads are three flows, and Updated since drops ads that have not changed. Coupler.io's Join nests the three lists into one sheet. The Data Studio report is how the team looks up what is live.

- **7 days click beside 1 day view**

  One flow leaves Attribution settings on Use ad account settings. The other uses Specify manually and an Action attribution windows value of 7 days click or 1 day view. Coupler.io's Append stacks both extracts and keeps the window on the row, which is what the Data Studio page compares.

- **Every client on one portfolio page**

  Filters removes test campaigns inside each client's own flow. Coupler.io's Append places those Reports and Insights extracts under one another, with Ad accounts still on the row. The Data Studio dashboard treats that sheet as the agency book.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

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
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
