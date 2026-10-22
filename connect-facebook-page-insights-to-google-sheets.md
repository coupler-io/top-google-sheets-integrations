---
title: Connect Facebook Page Insights to Google Sheets with Coupler.io
slug: connect-facebook-page-insights-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md
source: Facebook Page Insights
destination: Google Sheets
meta_title: Connect Facebook Page Insights to Google Sheets with Coupler.io
meta_description: "Export Page: performance insights and Post: posts lifetime performance from Facebook Page Insights to Google Sheets for fresh Data Studio reports."
---

![Facebook Page Insights](https://static.coupler.io/importers/facebook.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Facebook Page Insights to Google Sheets with Coupler.io

The insights view on a Facebook Page is a screen for browsing, not a workbook your team can version, share, or open every Monday. Coupler.io sends the page, post, reel, or video report into Google Sheets on a schedule, and a Data Studio dashboard is built on that sheet.

## How to export Facebook Page Insights data to Google Sheets

You can export a page overview, page performance, a daily follower snapshot, lifetime posts, lifetime reels, and daily video performance.

### Step 1. Basic settings

- **Pages** — the Facebook Pages this flow should read. Select every Page that belongs in the same sheet.
- **Report type** — one of the six reports. Their names are listed in full further down. Each flow uses a single report type.

### Step 2. Report period

- **Start date** — when the reporting window opens. Relative values — *days ago*, *this month*, *last month*, *this year*, *last year* — roll forward on the next run. The macro `{{365daysago}}` covers a trailing year when the presets are not enough.
- **End date** — when the window closes. Pair a relative end with the start so nobody edits the flow next month.
- **Created after** — only include items created after this date. It narrows the period alongside the start and end.
- **Created before** — only include items created before this date.
- **Split data by period** — Daily or Monthly. Daily is the grain for a follower line. Monthly suits a page scorecard.

### Step 3. Metrics

- **Metrics** — the measures this page or post report should include. Pick the ones the Data Studio chart will show, and leave unused measures out of the header row.

### Step 4. Metrics and dimensions

- **Metrics and dimensions** — the combined picker for reports that need both measures and breakdowns in one step. The wizard can show this field twice; it is the same field title both times, so you set the metrics and dimensions the report is asking for and move on.

### Step 5. Advanced filters

- **Created after** — the created-after bound again, this time for post-level reports. Post: posts lifetime performance, Post: reels lifetime performance, and Post: video daily performance use this repeat of the date so the post set is limited even when the report period was already set.
- **Created before** — the matching created-before bound for those same post-level reports.

### Step 6. Advanced settings

- **Post columns** — which post attributes travel with the metrics. The list includes Message, Call to action, Multi-share end card, Multi-share optimized, Message tags, Event, Attachments, Created time, Scheduled publish time, Posted to, Posted by, Permalink URL, Timeline visibility, Is subscribed, Status type, Is published, Is hidden, Is expired, Is popular, Is spherical, Promotable Id, Promotion status, Is eligible for promotion, Video buying eligibility, Instagram eligibility, Is Instagram eligible, Application, and Can reply privately. Leave the selection empty to bring every column. Post Id and the post updated time are included either way.
- **Data behavior** — how values are stored. Latest data keeps only current values, and it is what you get if you leave the field empty. Track changes over time saves daily snapshots so a later chart can see the path, not only the latest point.

### Step 7. Blend and transform data

Page rows and post rows answer different questions, and Coupler.io can combine them first.

- **Column management** — keep Message, Permalink URL, and Created time visible, hide flags nobody charts, and set the date types.
- **Join** — place Page: performance insights beside Post: posts lifetime performance so a page total and its posts share a sheet.
- **Append** — stack Post: reels lifetime performance under Post: posts lifetime performance when the content calendar should be one list.
- **Aggregate** — turn a Daily split into a month for a scorecard that only shows Monthly.
- **Custom SQL** — keep rows whose Promotion status or Is eligible for promotion matches the queue you are building.

### Step 8. Google Sheets destination

The header row comes from the page and post fields you selected. Coupler.io lays those columns out from the data.

- **Sheet** — a tab that is already in the file, or a new name. Coupler.io creates a new sheet after the last tab.
- **Cell address / Range** — the starting cell, or a box the import must stay inside. Examples are B5, D1, and B5:G10. A1 is the default.

### Step 9. Schedule

Fifteen minutes is the shortest refresh. You can also choose hourly, daily, weekly, or monthly. Overwrite mode clears the previous page block and writes the new one in its place. Stacking mode leaves the old block and puts the new rows below it, which keeps earlier page snapshots in the tab. Data behavior is a different control: Track changes over time stores daily snapshots inside the import, and Latest data keeps the current values.

### Bonus: or just ask the AI Agent to build it for you

Typing every date and column is optional. The Coupler.io AI Agent lives in the right sidebar of the app:

> "Export Page: performance insights and Post: posts lifetime performance for my Facebook Pages into Google Sheets, split monthly, with Message and Permalink URL on the posts."

You still:

- Connect the Facebook account that owns the Pages.
- Choose which Pages this flow may read.
- Connect Google Sheets and pick the spreadsheet in the file picker. Choosing the file is a manual step.
- Name the sheet, and name the starting cell when it is not A1.

## What data can you export from Facebook Page Insights to Google Sheets with Coupler.io?

Six report types are available, and each one is its own flow. Coupler.io's Join can put a page report next to a post report before the write, which is the range a Data Studio dashboard should read.

- **Page: general overview** — a top-level read of the Page for the window you set, enough for an executive scorecard.
- **Page: performance insights** — the performance view of the Page, split Daily or Monthly.
- **Page: followers daily snapshot** — follower figures as a daily snapshot, the series behind a growth line.
- **Post: posts lifetime performance** — lifetime results for posts, with Message, Permalink URL, and Created time when you ask for those Post columns.
- **Post: reels lifetime performance** — lifetime results for reels, so short video is not buried in the general post list.
- **Post: video daily performance** — video results by day, using Created after and Created before on the post-level filters when the archive should be bounded.

## Why export Facebook Page Insights to Google Sheets — real life cases

Coupler.io's Join sets page insights beside posts, Append stacks reels under the post list, and Aggregate rolls a Daily split into a month before a Data Studio report opens the Google Sheet.

- **This month's page scorecard**

  Page: general overview and Page: performance insights, Split data by period set to Monthly, are the two ranges a Data Studio scorecard can switch between. Start date and End date stay relative so the month moves on by itself. Data behavior Latest data keeps that scorecard on the current figures.

- **Follower snapshots by day**

  Page: followers daily snapshot with Split data by period set to Daily is the series a Data Studio line chart plots. Track changes over time on Data behavior stores a snapshot on each run. The chart reads that trail from the sheet.

- **Posts still worth opening**

  Post: posts lifetime performance, with Post columns Message, Permalink URL, and Created time, is the content table in a Data Studio report. Created after and Created before on the post-level filters decide which posts qualify. Permalink URL is the link the report exposes for each row.

- **Reels in the same content list**

  Post: reels lifetime performance stays its own flow until Append places it under Post: posts lifetime performance. A Data Studio content page can then treat posts and reels as one list. The chart splits that stacked range by format.

- **Video, one day at a time**

  Post: video daily performance, limited with Created after and Created before, is the sheet a Data Studio time series follows. The daily rows are what this report stores. The chart steps through that video tab.

- **Posts that can be promoted**

  Post columns Promotion status, Is eligible for promotion, Promotable Id, and Is published mark the boost queue inside a Data Studio filter. The report keeps rows where Is eligible for promotion is set. Promotable Id is the value the media team copies off that page.

- **A current figure or a daily trail**

  Data behavior Latest data leaves the current page number in the sheet a Data Studio scorecard shows. Track changes over time keeps daily snapshots when the chart has to show the path of a metric. One flow uses one of those two behaviors.

- **Organic page rows beside paid**

  Coupler.io's Join attaches Page: performance insights to a paid-social extract on a shared page key. The Data Studio report charts organic page results next to those paid rows. The match is already stored in Google Sheets.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
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
