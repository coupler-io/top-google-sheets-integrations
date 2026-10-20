---
title: Connect YouTube Analytics to Google Sheets with Coupler.io
slug: connect-youtube-analytics-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md
source: YouTube
destination: Google Sheets
meta_title: Connect YouTube Analytics to Google Sheets with Coupler.io
meta_description: Load YouTube Traffic sources, Views, and Watch time (minutes) into Google Sheets for a current Data Studio board.
---

![YouTube Analytics](https://static.coupler.io/importers/youtube.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect YouTube Analytics to Google Sheets with Coupler.io

YouTube Analytics is a strong place to look at one channel and a weak place to feed a shared report, because the download is manual. Coupler.io sends the channel into Google Sheets on a schedule, and Data Studio builds its pages from that sheet.

## How to export YouTube Analytics data to Google Sheets

Seven report types cover the channel, subscribers, videos, traffic sources, and a custom combination of metrics and dimensions. One flow uses one report type. Channels can be combined when they belong in the same tab.

### Step 1. Basic settings

- **Channels** — the channels this report should include. Select each one that belongs in the sheet.
- **Report type** — one of the seven extracts listed below. **Custom** is the type that follows the metrics and dimensions you tick yourself.

### Step 2. Report period

- **Start date** — first day covered. Relative values such as *this year*, *days ago*, and *last year* advance on their own. For an explicit trailing year, use the advanced macro `{{365daysago}}`.
- **End date** — last day covered. *This month* or *last month* keeps the close of the window current.
- **Split data by period** — **Day** or **Month**. **Day** is the grain a trend chart wants. **Month** is the grain a board pack wants.

### Step 3. Metrics and dimensions

- **Metrics** — measures included in the report. The list includes **Views**, **Watch time (minutes)**, **Average view duration**, **Average view percentage**, **Likes**, **Comments**, **Shares**, **Subscribers gained**, and **Subscribers lost**, plus card, annotation, playlist, and YouTube Premium measures such as **YouTube Premium views** and **YouTube Premium watch time (minutes)**.
- **Dimensions** — how those measures break down. Options include **Age**, **Gender**, **Country**, **City**, **Device type**, **Operating system**, **Content type**, **Subscription status**, **Live or on demand**, **Video**, **Playlist**, **Day**, **Month**, and **Insight traffic source type**.
- **Additional dimensions** — further breakdowns on top of **Dimensions**, when one cut is not enough for the Data Studio page.

### Step 4. Sorting options

- **Sorting column** — the column that orders rows in the sheet. Point it at the measure the dashboard should meet first, such as **Watch time (minutes)** or **Views**.

### Step 5. Advanced settings

- **Video ID** — required when you are reading audience retention for one video. Retention-related measures include **Audience watch ratio**, **Relative retention performance**, **Started watching**, and **Stopped watching**, and the dimension **Elapsed video time ratio** belongs with that read.
- **Insight traffic source type** — required if you use the dimension **Insight traffic source detail**. The values are **ADVERTISING**, **EXT_URL**, **RELATED_VIDEO**, **SUBSCRIBER**, **YT_CHANNEL**, **YT_OTHER_PAGE**, and **YT_SEARCH**.

### Step 6. Blend and transform data

- **Column management** — bring **Watch time (minutes)** and **Views** forward, and hide annotation columns this dashboard skips.
- **Join** — connect **Video detailed statistics** to **Traffic sources** on **Video**, inside Coupler.io, so one tab holds both.
- **Append** — stack **Channel detailed statistics** from two channels that were connected separately and share a column layout.
- **Aggregate** — sum **Day** rows into a month even when **Split data by period** was **Day**, if the board pack only prints months.
- **Custom SQL** — subtract **Subscribers lost** from **Subscribers gained** so the sheet carries a net figure Data Studio can score.

### Step 7. Google Sheets destination

The sheet's columns follow the YouTube response. Naming the tab and the starting cell is the destination work. Column types are read from the data.

- **Sheet** — choose a tab that exists, or type a new name. A new tab is added after the last tab.
- **Cell address / Range** — A1 is the default and the right start for a blank tab. D1 leaves a gutter column. B5 starts under a title. B5:G10 fixes both the start cell and the end cell when the import must not spill.

### Step 8. Schedule

Set the timer to 15 minutes, to an hour, to a day, to a week, or to a month. Replace mode refreshes the same cells. Append mode keeps history by writing under the last row. A daily replace suits a channel scorecard. A monthly append suits a long **Watch time (minutes)** series split by **Month**.

### Bonus: or just ask the AI Agent to build it for you

Channel setup can be described to the AI Agent. Find it in the right sidebar while the Coupler.io app is open, then name the report type and the sheet:

> Load Channel detailed statistics and Traffic sources for our channel into Google Sheets, split by Day, including Views and Watch time (minutes).

You still handle the accounts and the file:

1. Connect YouTube and approve the channel access.
2. Choose the **Channels** in scope.
3. Connect Google Sheets and choose which spreadsheet file the picker should write into.
4. Name the sheet, and set the cell when the block should not start at A1.

## What data can you export from YouTube Analytics to Google Sheets with Coupler.io?

Seven report types, one per flow. Coupler.io's **Join** can put channel stats and traffic sources in one tab first, and Data Studio should chart that tab.

- **Channel detailed statistics** — channel-level measures such as **Views**, **Watch time (minutes)**, and **Average view duration**, split by **Day** or **Month**.
- **Channel statistics by content and subscriber type** — the channel cut by **Content type**, **Subscription status**, and **Live or on demand**.
- **Channel subscribers** — the subscriber extract for the channels you selected, for a Data Studio scorecard aimed at the subscriber base.
- **Video detailed statistics** — per-video measures, with **Video** available as a dimension and **Average view percentage** among the metrics.
- **Video statistics by content and subscriber type** — the video-level twin of the channel content and subscriber cut.
- **Traffic sources** — where views came from, using **Insight traffic source type** and, when you filter it, **Insight traffic source detail**.
- **Custom** — your own mix of **Metrics**, **Dimensions**, and **Additional dimensions**, ordered by **Sorting column**.

## Why export YouTube Analytics to Google Sheets — real life cases

Channel managers already live in YouTube Analytics. The sheet is how those figures reach a Data Studio page the rest of the company can open. Do the Join in Coupler.io so the page has one tab to read.

- **A channel scorecard leadership will open**

  **Channel detailed statistics** with **Views**, **Watch time (minutes)**, and **Average view duration**, split by **Day**, is the daily sheet. Replace mode on a morning schedule keeps Data Studio honest. **Sorting column** can put **Watch time (minutes)** first when that is the number the meeting starts with.

- **Subscribers gained against subscribers lost**

  **Channel subscribers** plus **Subscribers gained** and **Subscribers lost** shows whether the channel is growing. **Custom SQL** can subtract lost from gained before the write, and Data Studio scores that net figure. **Split data by period** set to **Month** matches a board pack.

- **What kind of content, and who was subscribed**

  **Channel statistics by content and subscriber type** breaks the channel by **Content type**, **Subscription status**, and **Live or on demand**. A Data Studio page can compare subscribers with everyone else from that sheet. When the page also needs **Video statistics by content and subscriber type**, Coupler.io's **Join** can line the two flows up on a shared key before the write.

- **Which videos earned the watch time**

  **Video detailed statistics** with the **Video** dimension, **Views**, **Average view percentage**, and **Viewer percentage** is the ranking table. **Sorting column** on **Views** or **Watch time (minutes)** sets the order Data Studio inherits. **Additional dimensions** such as **Country**, **Device type**, or **Operating system** can sit on that flow when the chart needs a second cut.

- **Where the view came from**

  **Traffic sources** with **Insight traffic source type** separates **ADVERTISING**, **EXT_URL**, **RELATED_VIDEO**, **SUBSCRIBER**, **YT_CHANNEL**, **YT_OTHER_PAGE**, and **YT_SEARCH**. Add **Insight traffic source detail** only after you set **Insight traffic source type**, because that detail dimension requires the filter. Data Studio can then show which source type actually delivers **Views**.

- **Retention on one video**

  Paste the **Video ID** when the question is audience retention. **Audience watch ratio**, **Relative retention performance**, **Started watching**, **Stopped watching**, and **Elapsed video time ratio** describe where people stay and leave. Data Studio plots that sheet for the video the team is still editing around. A channel-wide report does not need **Video ID**.

- **Playlists, Premium, and the cards on the video**

  **Custom** can pull **Playlist views**, **Playlist watch time (minutes)**, **Playlist starts**, **YouTube Premium views**, and **YouTube Premium watch time (minutes)** into one sheet, with **Playlist** as a dimension. A second custom flow can hold **Card clicks**, **Card impressions**, and **Card click rate** when the creative review is about end screens and cards. Data Studio keeps those as two pages fed by two tabs.

- **Build the odd report yourself**

  **Custom** is the report type for a combination the fixed reports do not offer. Tick **Metrics** such as **Likes**, **Comments**, and **Shares**, **Dimensions** such as **Country** and **Youtube product**, and any **Additional dimensions** the page still needs. **Sorting column** decides the row order. Coupler.io's **Join** can attach that custom sheet to **Channel detailed statistics** before Data Studio draws a single page across both.

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
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
