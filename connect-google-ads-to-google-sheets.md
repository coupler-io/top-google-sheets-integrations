---
title: Connect Google Ads to Google Sheets with Coupler.io
slug: connect-google-ads-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md
source: Google Ads
destination: Google Sheets
meta_title: Connect Google Ads to Google Sheets with Coupler.io
meta_description: Send Campaign performance, Keywords performance, and Custom GAQL from Google Ads into Google Sheets so Data Studio dashboards stay current.
---

![Google Ads](https://static.coupler.io/importers/googleadv.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Google Ads to Google Sheets with Coupler.io

The Google Ads UI opens one report at a time, and a cross-account workbook still starts as a pile of downloads. Coupler.io writes the Report type you pick to Google Sheets on a schedule, so a Data Studio dashboard can stay pointed at one tab.

## How to export Google Ads data to Google Sheets

Report type covers performance reports, the resource lists behind them (accounts, campaigns, ads, budgets, constants, and the rest), and Custom GAQL when no preset matches.

### Step 1. Basic settings

- **Ad accounts** — active accounts you can access. Every account you tick is part of this flow.
- **Report type** — the performance report, the resource list, or Custom GAQL. One flow carries one choice.
- **Custom GAQL** — the query itself, filled in when Report type is Custom GAQL. That query decides which rows and columns the sheet receives.

### Step 2. Report period

- **Start date** — the first day in the report. Left alone, it sits 60 days back. *days ago*, *this month*, *last month*, *this year*, and *last year* keep moving. When none of those presets is a trailing year, use the advanced macro `{{365daysago}}`.
- **End date** — the last day. The unset value is today, so a relative end stays with the calendar.
- **Split data by periods** — how the range is cut into periods. The sheet repeats the report once per period instead of once for the whole Start date to End date span.

### Step 3. Blend and transform data

Do this while the Google Ads rows are still inside Coupler.io.

- **Column management** — hide id fields that exist only as join keys, and rename GAQL headers into labels a buyer will recognize on the tab.
- **Join** — attach Campaigns, Campaign budgets, Labels, or Bidding strategies onto Campaign performance so the catalog and the numbers share a sheet.
- **Append** — put Keywords performance under Search query performance, or stack a second account beneath the first.
- **Aggregate** — roll a fine Split data by periods grain, or a detail report such as Click performance, up to the level the chart should plot.
- **Custom SQL** — trim a Custom GAQL result, or combine two report shapes that Append would only stack blindly.

### Step 4. Google Sheets destination

Column order follows the preset report or the Custom GAQL result. Aim the import at a tab and a cell. Coupler.io lays the columns out from the data.

- **Sheet** — a tab that already exists, or a new name. The new tab is added after the last sheet in the file.
- **Cell address / Range** — A1 if you leave it. D1 or B5 moves the top-left corner. B5:G10 stops the import at that rectangle.

### Step 5. Schedule

Every 15 minutes suits a live bidding check. Hourly, daily, weekly, and monthly suit a review cadence. Replace the range when the tab should mirror the latest report. Append new rows under it when you want each extract kept.

### Bonus: or just ask the AI Agent to build it for you

Open the Coupler.io app and use the AI Agent in the right sidebar. Tell it which report belongs in the sheet:

> Load Campaign performance and Keywords performance from my Google Ads accounts into Google Sheets, from 60 days ago through today.

It sets Ad accounts, Report type, Custom GAQL when you asked for a query, Start date, End date, and Split data by periods. It stops to ask when the account list is ambiguous.

You still:

1. Connect Google Ads with your own login.
2. Decide which Ad accounts are in scope.
3. Connect Google Sheets and pick the spreadsheet in the file picker.
4. Name the sheet, plus the cell when A1 is the wrong corner.

## What data can you export from Google Ads to Google Sheets with Coupler.io?

Fifty-seven Report type options. Each flow carries one of them. Coupler.io's Join can fasten resource lists such as Campaigns, Campaign budgets, and Labels onto a performance report before the spreadsheet is touched, so Data Studio reads one prepared tab.

- **Campaign performance** — campaign delivery over Start date and End date, the sheet most weekly reviews open first.
- **Keywords performance** — a row per keyword you actually bought.
- **Ad group performance** — results at ad group grain, between the campaign total and the individual ad.
- **Ad performance** — a row per ad, so a tired asset shows up without a UI export.
- **Asset group performance** — asset groups, kept apart from classic ad groups.
- **Custom GAQL** — any resource the presets skip, with columns defined by the Custom GAQL field.
- **Account performance** — one grain across the Ad account when the dashboard only needs account totals.
- **Ad group audience performance** — how each audience on an ad group responded.
- **Ad group performance by country** — that ad group grain cut by country.
- **Ad group performance by state** — the same idea at state level.
- **Ad group performance by region** — regional rows for the ad group.
- **Ad group performance with install conversion** — ad groups plus install conversions on the row.
- **Age range performance** — delivery split by age range.
- **Campaign audience performance** — audiences evaluated at campaign level.
- **Campaign performance by ad network type** — each ad network type kept on its own rows.
- **Campaign performance by country** — campaigns split by country.
- **Campaign performance by state** — campaigns split by state.
- **Campaign performance by region** — campaigns split by region.
- **Campaign performance with conversion actions name** — the conversion action name sitting on the campaign result.
- **Campaign performance with unique user stats** — unique-user figures beside the campaign totals.
- **Click performance** — click-level rows rather than an aggregated delivery total.
- **Display keyword performance** — keywords as they behaved on Display.
- **Display topics performance** — topics targeted on Display.
- **Expanded landing page** — the expanded landing page rows behind the ads.
- **Gender performance** — delivery split by gender.
- **Keywordless query** — searches that matched without a keyword you added.
- **Landing page** — the landing pages ads sent people to.
- **Placeholder feed item** — feed items that act as placeholders.
- **Placeholder** — placeholder records in the account.
- **Placement performance** — where the ads actually served.
- **Responsive search ad performance** — responsive search ads and how they delivered.
- **Search query performance** — the searches that triggered the ads.
- **Shopping performance** — shopping results for the products you advertise.
- **User location performance** — where the user was, distinct from the targeted geography.
- **Video campaign performance with conversions** — video campaigns with conversions included on the row.
- **Accounts** — the account list, so other reports can be joined back to a stable account record.
- **Ad groups** — the ad group catalog, parent campaign included, without the performance measures.
- **Ads** — the ad catalog itself.
- **Campaigns** — the campaign catalog, names and status separate from Campaign performance.
- **Campaign budgets** — budget objects you can join onto the campaigns that spend them.
- **Campaign criterion** — criteria attached to campaigns.
- **Campaign labels** — which labels sit on which campaigns.
- **Accessible bidding strategies** — bidding strategies the account is allowed to use.
- **Bidding strategies** — strategies already present in the account.
- **Carrier constant** — the carrier reference list those reports point at.
- **Language constant** — the language reference list.
- **Mobile app category constant** — app-category reference values.
- **Mobile device constant** — device reference values.
- **Operating system version constant** — operating-system version reference values.
- **Topic constant** — topic reference values used by topic targeting.
- **Ad group criterion** — criteria hanging off ad groups.
- **Call details** — call reporting rows for ads that collect calls.
- **Feed** — feeds stored on the account.
- **Feed item** — the items inside those feeds.
- **Labels** — label definitions, ready to join onto Campaign labels.
- **User interest** — interest audiences available to the account.
- **User list** — remarketing and customer lists in the account.

## Why export Google Ads to Google Sheets — real life cases

Buyers keep a Data Studio report on the Google Ads sheet when clicking through one UI report per question burns the weekly review.

- **This month's campaigns**

  Campaign performance is the Report type. Start date and End date are *this month* or *last month*, and Split data by periods decides how many rows the chart receives. Data Studio scorecards on the review deck point at that tab.

- **Bought keyword, actual search**

  Keywords performance and Search query performance are different Report type choices. Coupler.io's Join builds one sheet from both before anything is written to the destination. The Data Studio report shows the keyword you pay for and the search that triggered the ad together.

- **A GAQL grain with no preset**

  Report type Custom GAQL means the text in Custom GAQL defines the columns, including a resource the preset list never names. Campaign criterion or User list can be in that result when the query asks for them. The Data Studio report charts whatever came back.

- **Three geography reports, one map**

  Campaign performance by country, Campaign performance by state, and User location performance each need their own flow. Coupler.io's Aggregate reduces a fine Split data by periods extract to one row per place. The Data Studio map is drawn from the sheet you kept.

- **Shopping and video on one slide**

  Shopping performance and Video campaign performance with conversions cannot share a Report type. Coupler.io's Append puts both extracts in the same tab. The Data Studio slide compares those two blocks.

- **Asset groups carrying a campaign name**

  Asset group performance and Ad group performance stay on separate flows. Coupler.io's Join adds the Campaigns list so both grains show the campaign name. The Data Studio report gives each grain its own chart.

- **Budget and bid strategy on the row**

  Campaign budgets and Bidding strategies are resource lists, not delivery numbers. Coupler.io's Join fastens them to Campaign performance. The Data Studio report uses that sheet to show a campaign whose budget object explains a flat result.

- **Call and click detail, rolled up**

  Click performance and Call details are too fine for a leadership visual. Coupler.io's Aggregate rolls them to a coarser grain, and a second flow can still land the unrolled rows on another tab. Data Studio uses the rolled sheet for the total and the raw sheet for the drill.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
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
