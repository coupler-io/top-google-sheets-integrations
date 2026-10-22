---
title: Connect Instagram Insights to Google Sheets with Coupler.io
slug: connect-instagram-insights-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-insights-to-google-sheets.md
source: Instagram Insights
destination: Google Sheets
meta_title: Connect Instagram Insights to Google Sheets with Coupler.io
meta_description: "Send Profile: daily reach and Story: performance totals (last 24 hours) from Instagram Insights to Google Sheets for current Data Studio dashboards."
---

![Instagram Insights](https://static.coupler.io/importers/instagram-ads.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Instagram Insights to Google Sheets with Coupler.io

Instagram's insights screen is meant for a quick look, and several story reports only cover the last 24 hours. Coupler.io copies the profile, post, or story report into Google Sheets whenever the schedule fires, so a Data Studio dashboard can keep the rows after that in-app window has moved on.

## How to export Instagram Insights data to Google Sheets

The export includes profile totals, follower and audience breakdowns, post performance and comments, story reports limited to the last 24 hours, and the deprecated carousel report.

### Step 1. Basic settings

- **Profiles** — the Instagram profiles to include. A flow can cover more than one profile and still land in a single sheet.
- **Report type** — one of the 17 reports, named in full in the data section below, including Post insights: carousel (deprecated) and the three last-24-hours story reports. Each flow uses one report type.

### Step 2. Report period

- **Start date** — the opening day for reports that take a range. The relative picker includes *days ago*, *this month*, *last month*, *this year*, and *last year*. For a year back with no preset, use the macro `{{365daysago}}`.
- **End date** — the closing day of that range.
- **Timeframe** — a short preset some reports use instead of typing both dates. The options are This month and This week.
- **Published after** — include posts published after this date.
- **Published before** — include posts published before this date.
- **Split by** — the time grain. Options are Totals only, Daily, and Monthly (31st day not included). The monthly option leaves the 31st out, so a month-end chart should account for that.

### Step 3. Metrics and dimensions

Demographic reports are the ones that use this step. Other report types bring the columns implied by the report you selected.

- **Metrics** — Engaged audience demographics or Reached audience demographics.
- **Dimension** — how that audience metric is split. The choices are Age; Gender; Age, Gender; City; and Country.

### Step 4. Advanced settings

- **Show promoted posts ad ids in separate rows** — turn this on when a promoted post should expand so each ad id occupies its own row, which makes a paid-versus-organic filter possible later.
- **Data behavior** — storage mode. Latest data keeps current values, and it applies when the field is left empty. Track changes over time saves daily snapshots for a trend.

### Step 5. Blend and transform data

Do the reshaping in Coupler.io, then let the sheet hold the result.

- **Column management** — surface the demographic metric you chose, hide empty story columns on a profile flow, and place City or Country where the chart expects them.
- **Join** — connect Profile: account overview to a sales or ads source on a shared key, so follower context arrives with outcomes.
- **Append** — add each day's Story: performance totals (last 24 hours) under the previous pull, and the 24-hour window is no longer the only history you keep.
- **Aggregate** — sum Profile: daily reach into a week when Daily is finer than the report you present.
- **Custom SQL** — separate organic rows from promoted ones after ad ids have been split onto their own rows.

### Step 6. Google Sheets destination

Instagram columns follow the report type. Coupler.io lays the header out from that data.

- **Sheet** — an existing tab, or a name you type. A new name is created after the last sheet in the file.
- **Cell address / Range** — a single cell such as B5 or D1, or a range such as B5:G10. It defaults to A1.

### Step 7. Schedule

Because story reports cover only the last 24 hours, schedule them daily, or every 15 minutes if that window needs to be caught before it rolls. Hourly, weekly, and monthly still suit profile summaries. One mode writes the new pull over the prior cells. The other mode places fresh story rows below what is already stored, so yesterday remains after Instagram drops it from the live report.

### Bonus: or just ask the AI Agent to build it for you

You can hand the description to the Coupler.io AI Agent in the right sidebar instead of setting each control:

> "Send Profile: daily reach and Story: performance totals (last 24 hours) from my Instagram profiles into Google Sheets, with a daily split."

You still:

- Connect Instagram Insights.
- Choose the Profiles in scope.
- Connect Google Sheets and pick the spreadsheet in the file picker. The spreadsheet file is a manual step.
- Name the sheet. Change the cell if the import should not begin at A1.

## What data can you export from Instagram Insights to Google Sheets with Coupler.io?

Seventeen report types are available. Each report type is one flow. Coupler.io's Append can stack a last-24-hours story pull under the prior day's rows, and Join can attach a profile report to another source, before Data Studio charts the sheet.

- **Post: performance totals** — post totals, bounded with Published after and Published before when the sheet should cover one publishing window.
- **Profile: account overview** — the profile headline numbers for the profiles you selected.
- **Profile: performance insights** — a deeper performance view of the profile than the overview alone.
- **Profile: followers daily breakdown (last 30 days)** — follower movement across the last 30 days.
- **Profile: followers demography insights** — who follows the profile, using Engaged audience demographics or Reached audience demographics and a Dimension such as Age, City, or Country.
- **Post: comment details review** — comment-level detail for posts, the sheet a community team reviews.
- **Post: profile interactions breakdown** — how people interacted with the profile from posts.
- **Story: performance totals (last 24 hours)** — story totals available only for the last day, which is why a repeating schedule plus Append is worth setting.
- **Story: navigation by action type (last 24 hours)** — story navigation split by action type, also limited to the last 24 hours.
- **Story: profile interactions breakdown (last 24 hours)** — profile interactions coming from stories in that same one-day window.
- **Profile: daily reach** — reach by day. Split by can be Daily, Totals only, or Monthly (31st day not included).
- **Profile: performance by media type** — profile performance split by media type.
- **Profile: performance by follow type** — results split by whether the person follows the profile.
- **Profile: links taps by contact button type** — which contact buttons collected taps.
- **Profile: reach by media product type and follow type** — reach crossed by media product type and follow type.
- **Profile: new audience demography insights** — demography for newer audience, with the same Metrics and Dimension choices as the follower demography report.
- **Post insights: carousel (deprecated)** — the older carousel export, still available when an existing sheet depends on that report.

## Why export Instagram Insights to Google Sheets — real life cases

Coupler.io Appends each story import under the prior day, Aggregates Profile: daily reach into a week, and Joins a profile report to another source before a Data Studio dashboard reads the Google Sheet.

- **Headline profile and the fuller view**

  Profile: account overview is the headline range, and Profile: performance insights is the deeper profile range, each from its own flow. A Data Studio page lays the two sheets on one screen. Editors glance at the overview, then open the performance block for the same profiles.

- **Reach by day, or by month without the 31st**

  Profile: daily reach with Split by set to Daily is the trend a Data Studio line follows. Monthly (31st day not included) is the month grain, and that option leaves the 31st out of the rollup. Aggregate can still fold the daily sheet into a week when the page needs both grains.

- **Who was engaged, and who was reached**

  Profile: followers demography insights and Profile: new audience demography insights take Metrics of Engaged audience demographics or Reached audience demographics. Dimension is Age, Gender, the combined Age, Gender value, City, or Country. A Data Studio map uses City and Country, and a bar chart uses Age, off that sheet.

- **Posts published inside a window**

  Post: performance totals bounded by Published after and Published before is the post table a Data Studio content report dates. Post: profile interactions breakdown adds the interaction mix for those same profiles. The report compares only the posts that fall in the window.

- **A queue of comments**

  Post: comment details review writes one row per comment into Google Sheets. Column management can keep the comment fields a community Data Studio report actually lists. The report counts those rows by post.

- **Story rows after the day closes**

  Story: performance totals (last 24 hours), Story: navigation by action type (last 24 hours), and Story: profile interactions breakdown (last 24 hours) cover only the latest day. Append every daily run in Coupler.io so the Data Studio story page still has yesterday. The page reads the sheet that kept those pulls.

- **Followers, other viewers, and media type**

  Profile: performance by follow type and Profile: reach by media product type and follow type split followers from everyone else. Profile: performance by media type is a third sheet for the media-type cut. Data Studio compares the three ranges on one audience page.

- **Button taps and one row per ad id**

  Profile: links taps by contact button type is the Data Studio view of which contact buttons were tapped. Show promoted posts ad ids in separate rows gives every ad id its own line in the sheet. The dashboard filters that expanded range down to paid rows.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
- [Connect Google Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md)
- [Connect Google Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-analytics-to-google-sheets.md)
- [Connect Google Search Console to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-search-console-to-google-sheets.md)
- [Connect Instagram Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-instagram-ads-to-google-sheets.md)
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
