---
title: Connect LinkedIn Public Data to Google Sheets with Coupler.io
slug: connect-linkedin-public-data-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-linkedin-public-data-to-google-sheets.md
source: LinkedIn Company Pages
destination: Google Sheets
meta_title: Connect LinkedIn Public Data to Google Sheets with Coupler.io
meta_description: Load LinkedIn Company Pages overviews, follower trends, and post video views into Google Sheets for a Data Studio dashboard.
---

![LinkedIn Public Data](https://static.coupler.io/importers/linkedin.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect LinkedIn Public Data to Google Sheets with Coupler.io

LinkedIn keeps company-page results in separate analytics panels, and the built-in exit is a file you download by hand. Coupler.io brings that LinkedIn Public Data into Google Sheets on a repeating schedule, so a Data Studio dashboard can open on current page, post, and video figures.

## How to export LinkedIn Public Data data to Google Sheets

One flow covers a single report type. The fifteen types span page overviews, follower and audience demographics, post lifetime results, video measures, reaction counts, and six older extracts that still carry the word deprecated in the name.

### Step 1. Basic settings

- **Pages** — tick the company pages this flow should read. Several pages can travel together, each row still marked by the page it came from.
- **Report type** — the extract you want in the tab. Fifteen choices are listed in the data section below, including the ones whose names say deprecated.

### Step 2. Report period

- **Start date** — the first day of the window. Relative choices such as *last year*, *this month*, or *days ago* move forward on later runs. When you need a fixed lookback written out, the advanced form is the macro `{{365daysago}}`.
- **End date** — the last day. A relative end such as *this month* or *last month* saves you from editing the flow every Monday.
- **Split data by period** — the grain used to divide that window, when the report type can be split. Leave the decision aligned with the chart you expect in Data Studio.

### Step 3. Dimensions

- **Breakdown dimension** — an extra cut on top of the report type, for the types that offer one. Use it when a single total would hide the slice the dashboard needs.
- **Dimension** — the main dimension for this report. Pick the one the Data Studio chart will group by.

### Step 4. Metrics

- **Metrics** — the measures that belong to the report type you chose. On **Post: video performance**, examples include **Views**, **Viewers**, **Time viewed (ms)**, and **Time viewed for views (ms)**. Those four illustrate the video set. Other report types carry their own measures.

### Step 5. Blend and transform data

- **Column management** — rename page and post columns into the words your dashboard already uses, hide deprecated leftovers, and put the page name in the first column.
- **Join** — line up **Page: follower gains trend** with **Page: performance insights** on the shared page, inside Coupler.io, before either series is written.
- **Append** — stack the same report type from company pages that live under a second LinkedIn login, so one tab holds the agency roll-up.
- **Aggregate** — collapse a fine follower series to the week or month a scorecard actually shows.
- **Custom SQL** — derive a ratio from **Views** and **Viewers** when the metric picker stops at the raw measures.

### Step 6. Google Sheets destination

Coupler.io lays the columns out from the LinkedIn extract itself, including the header row and the column types.

- **Sheet** — pick a tab that already exists, or type a new name. A new tab is created after the last one in the file.
- **Cell address / Range** — where the block begins. A cell such as B5 starts below a title row. D1 shifts the block one column in. A closed range such as B5:G10 keeps the write inside a fixed patch. The default is A1.

### Step 7. Schedule

Intervals on offer run from every 15 minutes through hourly, daily, weekly, and monthly. Each run can overwrite the range already sitting in the sheet, or add new rows beneath it. Daily replacement suits a page scorecard. Weekly append suits a history of follower gains you do not want collapsed.

### Bonus: or just ask the AI Agent to build it for you

Company-page setup can go to the AI Agent. It lives in the right sidebar of the Coupler.io app. Spell out the company-page tab and let it fill the report type, dates, and metrics:

> Load Page: performance insights and Post: video performance for our company pages into Google Sheets, include Views and Viewers on the video report, and refresh the tab every morning.

You still do four things yourself:

1. Connect LinkedIn Company Pages and sign in.
2. Choose the **Pages** that belong in the flow.
3. Hook Google Sheets up and choose the workbook with the file picker.
4. Type the tab name. If the write should start off the top-left, put that address in the cell field.

## What data can you export from LinkedIn Public Data to Google Sheets with Coupler.io?

Fifteen report types are available, and one flow handles one of them. Coupler.io's **Join** can match two of those flows on the page before a single tab is written, so Data Studio charts the sheet instead of blending the extracts itself.

- **Page: lifetime overview** — a standing snapshot of the company page for the scorecard that only needs the long view.
- **Page: performance insights** — the page series a weekly Data Studio trend is built from, once the schedule keeps the tab current.
- **Page: cumulative posts performance** — publishing volume over time, so a content lead can see output without opening each post.
- **Page: follower gains trend** — the slope of new followers, ready for a line chart that marketing reviews with the rest of the page numbers.
- **Page: follower demographics insights** — who actually follows the page, in a shape Data Studio can filter.
- **Page: audience demographics insights** — who the page can reach, set beside follower demographics when both questions matter.
- **Post: individual posts lifetime performance** — one row per post with its lifetime result, which is the table an editor sorts in Data Studio.
- **Post: video performance** — video measures for each post, including examples such as **Views**, **Viewers**, **Time viewed (ms)**, and **Time viewed for views (ms)**.
- **Post: social reactions & comments count** — reaction and comment totals beside the post, so community effort is visible next to reach.
- **Posts: shares insights (deprecated)** — the older shares extract, kept for a Data Studio page that was built against that layout.
- **Posts: UGC posts insights (deprecated)** — the older UGC post extract, for a board that still expects those columns.
- **Page: shares lifetime overview (deprecated)** — a lifetime shares snapshot in the previous shape, useful while an old report is being retired.
- **Time-based (deprecated)** — the previous time-split extract, when a historical chart still points at it.
- **Lifetime total statistic (deprecated)** — the previous lifetime total, for a scorecard that has not been repointed yet.
- **Post: individual posts performance (deprecated)** — the earlier per-post extract, distinct from the lifetime post report, for dashboards that still read it.

## Why export LinkedIn Public Data to Google Sheets — real life cases

Company-page figures become a management habit once they live in a sheet a Data Studio page can reopen. Coupler.io's Join, Append, and Aggregate finish before that sheet is written.

- **Monday page review**

  **Page: lifetime overview** and **Page: performance insights** arrive on the schedule you set, so the Data Studio page shows the company page without a fresh download. Coupler.io's **Aggregate** can roll the performance rows to a week before they hit the tab. The chart reads that sheet.

- **Follower growth with a face on it**

  **Page: follower gains trend** is the series a growth chart needs. Coupler.io's **Join** attaches **Page: follower demographics insights** on the page, and Data Studio shows both the slope and who joined. Comms and marketing share one tab.

- **Audience the page can reach**

  **Page: audience demographics insights** answers who is available to see the page, which is a different cut from who already follows it. A Data Studio bar or map reads the sheet after each refresh. **Split data by period** keeps that cut on the dates the report uses.

- **A post ledger for editors**

  **Post: individual posts lifetime performance** and **Post: social reactions & comments count** give each post a row the content team can sort. **Column management** can place reactions beside the post before the write. Editors stop copying figures out of the post list.

- **Video attention, not only starts**

  **Post: video performance** can carry **Views**, **Viewers**, **Time viewed (ms)**, and **Time viewed for views (ms)**, among the measures that report offers. Data Studio can plot **Views** against **Time viewed (ms)** from the sheet. Clips that start well and clips that hold attention separate cleanly.

- **How much the page published**

  **Page: cumulative posts performance** tracks output over the window you set. A Data Studio scorecard on that sheet is enough for a weekly content standup. Replacement mode on the schedule keeps the scorecard from stacking a duplicate block every Monday.

- **Several company pages on one board**

  **Pages** lets one flow cover every company page you select. Coupler.io's **Append** stacks a second flow when another client sits under a different LinkedIn login. Data Studio filters the finished sheet by page.

- **Boards that still expect an older extract**

  **Posts: shares insights (deprecated)**, **Posts: UGC posts insights (deprecated)**, **Page: shares lifetime overview (deprecated)**, **Time-based (deprecated)**, **Lifetime total statistic (deprecated)**, and **Post: individual posts performance (deprecated)** are still selectable. Point a flow at one of them when an existing Data Studio page depends on that layout. New boards should use the current page and post report types.

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
- [Connect Microsoft Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-microsoft-ads-to-google-sheets.md)
- [Connect QuickBooks to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-quickbooks-to-google-sheets.md)
- [Connect Shopify to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md)
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
