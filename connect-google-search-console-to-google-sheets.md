---
title: Connect Google Search Console to Google Sheets with Coupler.io
slug: connect-google-search-console-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-search-console-to-google-sheets.md
source: Google Search Console
destination: Google Sheets
meta_title: Connect Google Search Console to Google Sheets with Coupler.io
meta_description: Export Google Search Console Search results performance and URLs index performance into Google Sheets for a Data Studio report.
---

![Google Search Console](https://static.coupler.io/importers/google-search-console.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Google Search Console to Google Sheets with Coupler.io

Search Console is built for inspecting one property in the browser, and its download does not repeat itself the next morning. Coupler.io places those reports in Google Sheets on a schedule, so Data Studio can treat the tab as the source of the SEO page.

## How to export Google Search Console data to Google Sheets

Five report types cover search results, search appearance, Discover, Google News, and URL index checks. One flow carries one report type. Sites, dates, dimensions, and the advanced filters shape that extract before it hits the sheet.

### Step 1. Basic settings

- **Sites** — the properties to include. Select every site that should share this report type and this tab.
- **Report type** — one of the five extracts named in the data section. Switching type means a different flow.
- **Inspection URLs** — the addresses to inspect, one per line. This is the list **URLs index performance** checks.

### Step 2. Report period

- **Start date** — the first day Search Console should count. Relative settings such as *last month*, *last year*, or *days ago* keep that boundary moving. The advanced macro `{{365daysago}}` is there when the lookback must be written explicitly.
- **End date** — closing day. *This month* or *this year* leaves the end of the window in step with the calendar.

### Step 3. Dimensions

- **Dimensions** — one or several dimensions that narrow the result. Choose the cuts the Data Studio chart will group by, and skip the ones that would explode the row count.
- **Filters by dimensions** — keep only the dimension values you care about, so the sheet is the slice the report shows.

### Step 4. Advanced settings

- **Search results type** — limit the rows to one search type when the rest of search should stay out of this tab.
- **Aggregate data by** — how rows are rolled up. **Auto** lets Google Search Console choose. **Page** aggregates by canonical URI. **Property** aggregates data for the same property. **News showcase panel** is the other method in the list.
- **Data state** — **All** or **Final**. **All** keeps the newest rows, including data still settling. **Final** keeps rows that are already finalized, which is the safer feed for a Data Studio page you publish.

### Step 5. Blend and transform data

- **Column management** — order the dimension columns to match the SEO dashboard, and hide any field that page does not cite.
- **Join** — match **Search results performance** to **URLs index performance** on the URL, in Coupler.io, before either extract is charted.
- **Append** — stack **Search results performance** from two sites that share the same **Dimensions**, into one tab an agency filter can split.
- **Aggregate** — compress the date grain to the week the Monday report actually prints.
- **Custom SQL** — drop rows that fail a threshold you care about, so Data Studio receives the short list.

### Step 6. Google Sheets destination

Coupler.io takes the column layout from the Search Console response. You choose the tab and the cell where that layout should start.

- **Sheet** — an existing tab, or a name you type. Coupler.io puts a brand-new tab at the end of the tab bar.
- **Cell address / Range** — most flows keep the default A1. Choose B5 when titles occupy the rows above. Choose a closed range such as B5:G10 when the import must stay inside a printed area. D1 is the form when only the starting column should move.

### Step 7. Schedule

Scheduling options cover a 15-minute interval, an hour, a day, a week, and a month. You decide whether the next run clears the existing range or stacks rows below it. A weekly replace fits a Monday SEO review. An append fits a private archive of **Final** rows you do not want overwritten.

### Bonus: or just ask the AI Agent to build it for you

Plain language is enough for the AI Agent. You will find it in the right sidebar of the Coupler.io app:

> Export Search results performance and URLs index performance into Google Sheets, set Data state to Final, and refresh the tab daily.

What remains on you:

1. Connect Google Search Console.
2. Choose the **Sites**, and paste **Inspection URLs** when the flow is an index check.
3. Connect Google Sheets and point the file picker at the workbook.
4. Name the sheet. Change the cell if A1 is occupied.

## What data can you export from Google Search Console to Google Sheets with Coupler.io?

Five report types, one flow each. Coupler.io's **Join** lines up two of them before they land, and the Data Studio report charts that sheet.

- **Search results performance** — the core search extract for the property, shaped by **Dimensions**, **Search results type**, **Aggregate data by**, and **Data state**.
- **Search results performance by appearance** — the same family of search results, cut by appearance, for a Data Studio page that asks how results showed up.
- **Discover performance** — Discover figures for the sites you selected, on their own flow so they are not mixed into web search rows.
- **Google News performance** — News figures for those sites, ready for a Data Studio scorecard that should stay separate from Discover.
- **URLs index performance** — index status for every address you entered under **Inspection URLs**, one URL per line.

## Why export Google Search Console to Google Sheets — real life cases

Search Console is the ranking diary. Data Studio is where that diary becomes the report the SEO team opens on Monday. Coupler.io joins, appends, and aggregates first, and the sheet is what the report reads.

- **The Monday search review**

  **Search results performance**, with **Data state** set to **Final**, is the extract a published page should cite. A weekly schedule that replaces the range means the Data Studio charts move once, on purpose. **Dimensions** hold the cuts that review always uses, and **Filters by dimensions** drop the noise.

- **How the result appeared**

  **Search results performance by appearance** answers a different question from the main performance extract, so it deserves its own flow and its own tab. Data Studio can sit that tab beside the main search page. **Search results type** keeps the appearance cut inside the search type you meant.

- **Discover, apart from web search**

  **Discover performance** does not belong in the same rows as ordinary search results. Its own scheduled sheet lets a Data Studio page track Discover without a filter fighting mixed data. **Aggregate data by** can stay on **Auto**, or move to **Page** when you need canonical URI totals.

- **News as its own scorecard**

  **Google News performance** feeds the scorecard for properties that publish to News. **Property** aggregation rolls data for the same property when the chart should not split every URL. Data Studio reads the sheet after the weekly replace.

- **Index checks for a URL list**

  Paste the URLs into **Inspection URLs**, one per line, and run **URLs index performance**. The sheet becomes the checklist engineering and SEO share. Data Studio can highlight the addresses that failed, and the schedule repeats the inspection without a fresh paste unless the list itself changes.

- **Final numbers versus the latest rows**

  Build one flow with **Data state** **Final** for the report that goes to leadership, and another with **All** for the working tab that should include newer rows. Both can use **Search results performance**. Data Studio points the public page at the Final sheet and the working page at the other.

- **Canonical pages versus the whole property**

  **Aggregate data by** changes the grain of **Search results performance**. **Page** aggregates by canonical URI, which suits a URL-level Data Studio table. **Property** aggregates data for the same property, which suits a single scorecard. Run the two grains as two flows when the report needs both.

- **Search results next to index status**

  Coupler.io's **Join** matches **Search results performance** to **URLs index performance** on the URL before the write. Data Studio then shows performance and index status from one sheet. **Append** remains the better tool when you are stacking the same report type across **Sites** rather than combining two report types.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
- [Connect Google Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md)
- [Connect Google Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-analytics-to-google-sheets.md)
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
