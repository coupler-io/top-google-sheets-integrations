---
title: Connect TikTok Organic to Google Sheets with Coupler.io
slug: connect-tiktok-organic-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md
source: TikTok Organic
destination: Google Sheets
meta_title: Connect TikTok Organic to Google Sheets with Coupler.io
meta_description: Send TikTok Organic profile insights, audience countries, and video lists to Google Sheets for a Data Studio view of the last 60 days.
---

![TikTok Organic](https://static.coupler.io/importers/tiktok.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect TikTok Organic to Google Sheets with Coupler.io

TikTok Organic analytics sit inside the app, stop at 60 days, and assume you will keep checking them there. Coupler.io writes the same profile and video extracts into Google Sheets on a schedule, which gives Data Studio a tab to chart.

## How to export TikTok Organic data to Google Sheets

Six report types cover the profile, its audience, and the video list. There is no account picker on the flow. The connector asks for the profile when you connect TikTok Organic.

### Step 1. Basic settings

- **Report type** — the only choice on this screen. Pick one of the six extracts listed further down. A second question, such as countries plus video results, is a second flow.

### Step 2. Report period

- **Start date** — opening day of the window. TikTok will not return anything older than 60 days, so a relative *days ago* value inside that wall is the useful setting, with *this month* or *last month* when the question is shorter. The date field also accepts the advanced macro `{{365daysago}}`, and the 60-day limit still applies.
- **End date** — closing day. Keep it relative, for example *this month*, and later runs stay inside a moving window without an edit.

### Step 3. Blend and transform data

- **Column management** — keep gender, country, and hour labels readable, and drop empty profile columns the Data Studio page will never show.
- **Join** — attach **Profile audience countries** to **Profile insights** for the same profile, in Coupler.io, so one tab holds both.
- **Append** — stack **Video list insights** from a second TikTok Organic connection under the first, when two profiles should share one column layout and one sheet.
- **Aggregate** — roll **Profile audience hourly activity** up from hours into the dayparts your posting plan uses.
- **Custom SQL** — flag the hours where audience activity peaks, and leave that flag in the sheet Data Studio sorts.

### Step 4. Google Sheets destination

The columns follow the TikTok Organic extract, header included. You name the tab and the starting cell.

- **Sheet** — an existing tab, or a new name. Coupler.io adds a newly named tab after the last tab in the spreadsheet.
- **Cell address / Range** — the start of the write. The default is A1. A lone address such as D1 moves the block to the right. A bounded range such as B5:G10 tells the run where it must stop. B5 alone is enough when you only need to start lower on the tab.

### Step 5. Schedule

The clock can be every 15 minutes, or hourly, or daily, or weekly, or monthly. One mode replaces the cells this flow already filled. The other appends fresh rows under that block. For a 60-day profile window, daily replacement usually matches how the app itself forgets older days.

### Bonus: or just ask the AI Agent to build it for you

Talk to the AI Agent from the sidebar on the right of the Coupler.io app. Tell it which of the six reports the sheet should hold:

> Put Profile insights, Profile audience countries, and Video list insights for our TikTok Organic profile into Google Sheets, covering the last 60 days.

The connector still needs you for the login and the file:

1. Connect TikTok Organic.
2. Pick the profile the connector asks for.
3. Connect Google Sheets via the file picker.
4. Once that file is chosen, name the sheet. Enter a cell only when the block should sit away from the default corner.

## What data can you export from TikTok Organic to Google Sheets with Coupler.io?

Six report types, one per flow. Coupler.io's **Join** can put two of them in the same tab before Data Studio ever opens, which matters because the source itself is a short list.

- **Profile audience genders** — the gender mix of the profile audience, for a Data Studio split that the app otherwise keeps on its own screen.
- **Profile audience countries** — where that audience is, so a map in Data Studio can read a sheet instead of a screenshot.
- **Profile audience hourly activity** — which hours the audience is active, which is the input to a posting clock on the dashboard.
- **Profile insights** — the profile-level series for the window you set, within the 60 days TikTok allows.
- **Video list top countries** — the countries at the top of the video list, beside the profile countries when both questions are in play.
- **Video list insights** — results for the videos in that list, so a Data Studio table can rank them after each refresh.

## Why export TikTok Organic to Google Sheets — real life cases

The last 60 days of a TikTok profile is a small extract, which is why a scheduled sheet beats reopening the app. Join and Aggregate happen in Coupler.io. Data Studio charts the sheet they leave behind.

- **Gender mix on the profile**

  **Profile audience genders** is a short table, and it goes stale the moment someone screenshots it. A scheduled flow keeps the sheet aligned with the latest 60 days. Data Studio draws the split from that sheet at the weekly content meeting.

- **Countries the audience actually occupies**

  **Profile audience countries** answers where viewers are, which changes how you subtitle and when you post. Coupler.io can **Aggregate** tiny country rows if the chart only needs the top of the list. The Data Studio map reads the tab.

- **A posting clock from hourly activity**

  **Profile audience hourly activity** shows the hours the audience shows up. **Aggregate** can fold those hours into morning, afternoon, and evening before the write. Data Studio then highlights the daypart the next video should hit.

- **Profile scorecard for the last 60 days**

  **Profile insights** is the overview the app makes you hunt for. With **End date** relative and the schedule set to replace, the scorecard in Data Studio always describes the current allowed window. Nobody exports a CSV on Monday to get there.

- **Where individual videos traveled**

  **Video list top countries** is the geographic cut of the video list, distinct from the profile-level country mix. Put it in its own tab when the chart should rank videos rather than the account. Data Studio filters that tab to the videos the team is still promoting.

- **Rank the video list**

  **Video list insights** gives the video rows a Data Studio table can sort after every refresh. **Column management** can bring the columns editors recognize to the front. The 60-day ceiling is TikTok's, and the sheet simply stays inside it.

- **Profile and videos in one tab**

  Run **Profile insights** and **Video list insights** as two flows, then let Coupler.io's **Join** attach them for the same profile before the sheet is saved. Data Studio uses that single tab for the page that shows the account and the clips together. A third flow for **Profile audience countries** can join the same way when the page needs a map.

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
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
