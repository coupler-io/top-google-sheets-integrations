---
title: Connect Microsoft Ads to Google Sheets with Coupler.io
slug: connect-microsoft-ads-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-microsoft-ads-to-google-sheets.md
source: Microsoft Ads (Bing Ads)
destination: Google Sheets
meta_title: Connect Microsoft Ads to Google Sheets with Coupler.io
meta_description: Schedule the Campaign performance report and Keyword performance report from Microsoft Ads into Google Sheets for current Data Studio dashboards.
---

![Microsoft Ads](https://static.coupler.io/importers/microsoft.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Microsoft Ads to Google Sheets with Coupler.io

Microsoft Ads (Bing Ads) keeps campaign, keyword, hotel, and shopping numbers in a reporting screen that still expects a fresh download whenever the dates move. Coupler.io writes the report you select into Google Sheets on a schedule you set, which gives a Data Studio dashboard a sheet that is already up to date.

## How to export Microsoft Ads data to Google Sheets

One flow can cover search and audience performance, hotel and product reports, ad extensions, calls, goals and funnels, share statistics, or a Custom report when a preset shape is wrong.

### Step 1. Basic settings

- **Ad accounts** — tick every Microsoft Ads account this flow should read. Several accounts can share one sheet, with each row still traceable to its account.
- **Report type** — the report that defines the rows. All 44 types are listed in the data section below. A flow carries one report type; Coupler.io's Join can line two flows up later.

### Step 2. Report period

- **Report period** — a preset window, or Custom when you would rather type the bounds yourself. Custom is what opens Start date and End date.
- **Start date** — the first day included. The relative picker offers *days ago*, *this month*, *last month*, *this year*, and *last year*, so later runs move the window without an edit. A year-long offset can be written as the macro `{{365daysago}}`.
- **End date** — the last day included. Keep this relative as well when the sheet should close on the newest completed day.
- **Split data by period** — the time grain of each row. Choices are Summary, Hourly, Daily, Weekly from Sunday, Weekly from Monday, Monthly, and Yearly.

### Step 3. Metrics and dimensions

- **Metrics** — the measures that become columns. The list includes Impressions, Clicks, Spend, CTR, Average CPC, Average CPM, Conversions, Conversion rate, Revenue, Return on ad spend, Impression share percent, Impression lost to budget percent, Impression lost to rank agg percent, Click share percent, All conversions, All revenue, Assists, Phone calls, Low quality clicks, Video views, and Video completion rate, among others. Take the ones the Data Studio chart will actually read.
- **Dimensions** — the breakdowns that sit beside those metrics. The picker offers the dimensions this report type supports.

### Step 4. Dimensions

- **Dimensions** — a second dimension picker that some report types open after the metrics screen. It is an extra breakdown, used when that report asks for a cut the first dimension list does not cover. Skip it on reports that never show the step.

### Step 5. Advanced settings

- **Advanced filters** — row limits applied before the write, so zero-delivery keywords or paused campaigns never reach the sheet. Build the condition from columns the chosen report actually returns.

### Step 6. Blend and transform data

Shape the Microsoft Ads rows before they occupy cells.

- **Column management** — rename labels such as Impression share percent, drop metrics nobody charts, reorder so Spend sits beside Revenue, and set types on date and number columns.
- **Join** — match a Campaign performance report to a Geographic performance report, or to another channel, on a shared key. The joined rows are what land in Google Sheets.
- **Append** — stack an Account performance report from several accounts, or place Microsoft Ads under another source's rows, as one continuous range.
- **Aggregate** — roll an Hourly or Daily split up to the week a scorecard expects, including Weekly from Monday when that is the grain you want stored.
- **Custom SQL** — keep campaigns above a spend floor, or compute a ratio the preset metric list does not offer, and load the query result.

### Step 7. Google Sheets destination

Coupler.io lays the columns out from the Microsoft Ads fields you kept.

- **Sheet** — an existing tab, or a new name. A name that is not there yet is created after the last sheet in the file.
- **Cell address / Range** — where the first value goes. A single cell such as B5 or D1, or an exact range such as B5:G10. The default is A1.

### Step 8. Schedule

Pick a cadence of every 15 minutes, hourly, daily, weekly, or monthly. A run that overwrites puts the new Microsoft Ads block on top of the cells from the previous import. A run that adds beneath keeps those cells and places the new rows under them. Overwrite fits a scorecard that should show only the latest window. Adding beneath fits a log of Weekly from Monday snapshots you want to keep.

### Bonus: or just ask the AI Agent to build it for you

You can describe the report instead of clicking through every field. The Coupler.io AI Agent is in the app, on the right sidebar:

> "Load a daily Campaign performance report for my Microsoft Ads accounts — Impressions, Clicks, Spend, CTR, Conversions, and Return on ad spend — into Google Sheets for the last 90 days."

You still:

- Connect Microsoft Ads.
- Choose which Ad accounts the flow may read.
- Connect Google Sheets and pick the spreadsheet in the file picker. The file itself stays a manual choice.
- Name the sheet, and set the cell when the import should not start at A1.

## What data can you export from Microsoft Ads to Google Sheets with Coupler.io?

Coupler.io can export 44 Microsoft Ads report types. Each report type is its own flow. Coupler.io's Join stitches two of those flows — a campaign report and a geography report, for example — before either one lands in the sheet, so Data Studio charts a range that is already combined.

- **Campaign performance report** — campaign delivery and cost for the accounts you ticked, the usual source for a weekly scorecard.
- **Keyword performance report** — how each bidded keyword is spending against the clicks and conversions it returns.
- **Ad group performance report** — ad group results inside a campaign, before budget moves between them.
- **Ad performance report** — which individual ads are carrying clicks and conversions.
- **Ad extension by ad report** — extensions shown beside a specific ad.
- **Ad extension by keyword report** — extensions in the context of the keyword that triggered the ad.
- **Ad extension detail report** — extension-level detail when the by-ad and by-keyword views are too coarse.
- **Call detail report** — call activity from ads, read next to the Phone calls metric.
- **Budget summary report** — what each budget did across the report period you set.
- **Search campaign change history report** — edits on search campaigns, so a swing in Spend has a paper trail.
- **DSA auto target performance report** — results for dynamic search auto targets.
- **DSA category performance report** — dynamic search performance grouped by category.
- **DSA search query performance report** — queries that dynamic search ads actually matched.
- **Hotel dimension performance report** — hotel-ad results split by hotel attributes.
- **Hotel dimension performance report with share performance statistics** — those hotel attributes plus share statistics.
- **Hotel group performance report** — hotel ads rolled up to hotel groups.
- **Hotel group performance report with share performance statistics** — hotel groups with share statistics included.
- **Account performance report** — one performance view per ad account, which is the agency roll-up grain.
- **Account performance report with share performance statistics** — account totals with share statistics on the same rows.
- **Ad dynamic text performance report** — how dynamic text variants inside ads performed.
- **Ad group performance report with share performance statistics** — ad group results with share statistics attached.
- **Asset performance report** — delivery earned by individual assets.
- **Asset group performance report** — results at asset-group level.
- **Audience performance report** — which audiences the selected metrics moved for.
- **Campaign performance report with share performance statistics** — campaign results plus share statistics such as Impression share percent.
- **Conversion performance report** — conversion outcomes rather than traffic alone.
- **Destination URL performance report** — landing URLs that collected the clicks.
- **Goals and funnels report** — goal and funnel progress over the period.
- **Publisher usage performance report** — how results differ by publisher on the Microsoft network.
- **Search query performance report** — queries people typed, set beside the keywords you bid.
- **Share of voice report** — how much of the available impression pool the account captured.
- **Product dimension performance report** — shopping results by product attribute.
- **Product dimension performance report with share performance statistics** — product attributes plus share statistics.
- **Product match count report** — how many products matched, a check on catalog coverage.
- **Product partition performance report** — product groups and the results of each partition.
- **Product partition performance report with share performance statistics** — partitions with share statistics included.
- **Product partition unit performance report** — the unit level underneath a product partition.
- **Product search query performance report** — queries that triggered product ads.
- **Age gender audience report** — age and gender slices of the audience.
- **Geographic performance report** — results by the geography you targeted.
- **Negative keyword conflict report** — negatives that may be blocking queries you still want.
- **Professional demographics audience report** — professional-audience slices of delivery.
- **User location performance report** — where the person was, which can differ from the targeted geography.
- **Custom report** — a column set you assemble when none of the named reports match the sheet.

## Why export Microsoft Ads to Google Sheets — real life cases

Coupler.io's Join matches Microsoft Ads reports on a shared key, Append stacks accounts, and Aggregate turns an Hourly grain into a week before a Data Studio dashboard charts the Google Sheet.

- **Monday search review**

  Campaign performance report columns Impressions, Clicks, Spend, CTR, Average CPC, and Conversions, with Split data by period set to Weekly from Monday, fill the tab behind a Monday Data Studio page. Aggregate can lift a Daily split to a month when a second chart on that page wants a coarser bar. Nobody downloads a fresh Microsoft Ads file for the meeting.

- **Keywords with weak clicks**

  A Data Studio table reads Keyword performance report fields Low quality clicks, Low quality clicks percent, and Spend. Advanced filters can hold zero-delivery keywords out of the range. The report sorts on Low quality clicks percent so the noisiest bids surface first.

- **Share lost to budget or rank**

  Campaign performance report with share performance statistics supplies Impression share percent, Impression lost to budget percent, and Impression lost to rank agg percent for a budget Data Studio chart. Spend sits on the same sheet so the lost-share series has a cost scale beside it. Account leads open that page before they add money.

- **Calls against revenue**

  Join Call detail report to Conversion performance report in Coupler.io and keep Phone calls, Conversions, Revenue, and Return on ad spend. The Data Studio page checks whether call volume moves with Revenue. Both reports are already one range when the chart loads.

- **Hotel groups and hotel attributes**

  Append Hotel group performance report under Hotel dimension performance report so property ads share a tab a Data Studio filter can slice. Hotel group performance report with share performance statistics can stand in when share figures belong on that same page. The dashboard reads the stacked hotel range.

- **Shopping partitions and the queries behind them**

  Join Product partition performance report to Product search query performance report, and park Product match count report on a neighboring tab for catalog coverage. A Data Studio list shows which partitions spent and which queries triggered them. The match-count tab is the coverage check next to that list.

- **Age, gender, and professional audiences**

  Append Age gender audience report and Professional demographics audience report onto one audience tab. Column management can line up the metric names the two reports share. Data Studio draws the audience page from that single range.

- **Targeted geography and user location**

  Join Geographic performance report to User location performance report in Coupler.io, then let a Data Studio map compare the place you targeted with the place the person was. The two reports stay distinguishable on the sheet. Gaps between them show up as two series on one chart.

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
- [Connect QuickBooks to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-quickbooks-to-google-sheets.md)
- [Connect Shopify to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md)
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
