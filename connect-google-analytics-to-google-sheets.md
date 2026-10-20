---
title: Connect Google Analytics to Google Sheets with Coupler.io
slug: connect-google-analytics-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-analytics-to-google-sheets.md
source: Google Analytics 4 (GA4)
destination: Google Sheets
meta_title: Connect Google Analytics to Google Sheets with Coupler.io
meta_description: Combine Google Analytics 4 metrics such as Sessions and Purchase revenue in Google Sheets so a Data Studio report stays current.
---

![Google Analytics](https://static.coupler.io/importers/google-analytics.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Google Analytics to Google Sheets with Coupler.io

GA4 keeps sessions, revenue, and channel detail inside its own reports, and a download from that screen is a one-time file. Coupler.io writes the property into Google Sheets on a schedule you set, ready for a Data Studio dashboard that rereads the same tab.

## How to export Google Analytics data to Google Sheets

There is no report-type parameter. Each flow is one combination of up to 9 dimensions plus the metrics you pick. The groupings further down are ways to choose those labels. They are not separate exports hiding in a menu.

### Step 1. Basic settings

- **Properties** — the GA4 properties this flow should read. Choose every property that belongs in the tab.

### Step 2. Report period

- **Start date** — first day of the window. The default is 60 days ago. Relative options such as *this year*, *last year*, and *days ago* roll forward on later runs. A specific lookback can be written with the advanced macro `{{365daysago}}`.
- **End date** — last day of the window. The default is today. *This month* or *last month* keeps the close of the window moving.

### Step 3. Metrics and dimensions

- **Metrics** — the measures for this flow, up to 10. A second flow is how you carry measures past that set. Labels you might combine are listed in the groupings below, including **Sessions**, **Engaged sessions**, and **Purchase revenue**.
- **Dimensions** — up to 9 dimensions in the same flow. **Date** is the default, so a time series is already present unless you remove it. Add labels such as **Session source / medium** or **Country** when the Data Studio chart needs a breakdown.

### Step 4. Blend and transform data

- **Column management** — shorten long dimension headers, and place **Purchase revenue** next to **Sessions** in the order the dashboard reads.
- **Join** — align a sessions flow with an ecommerce flow on **Date** inside Coupler.io, before both land in one tab.
- **Append** — stack two GA4 properties that were pulled as separate flows and share the same metrics and dimensions.
- **Aggregate** — roll **Date** rows up to a month when the Data Studio page never shows a day.
- **Custom SQL** — divide **Ecommerce purchases** by **Sessions** in the flow so the sheet already holds that ratio.

### Step 5. Google Sheets destination

Headers and column types come from the GA4 response. Your job is the tab name and the cell where writing starts.

- **Sheet** — select a tab already in the file, or type a name. Coupler.io creates that new sheet after the last existing one.
- **Cell address / Range** — default start is A1. Shift the start to D1 when notes already occupy the left columns. Lock the write with a range like B5:G10 when this import shares the tab with cells people type into. B5 by itself only moves the starting corner.

### Step 6. Schedule

Choose a cadence: every 15 minutes, an hourly slot, a daily slot, a weekly slot, or a monthly slot. Replacement rewrites the current range. Appending keeps prior rows and writes the new ones underneath. A daily replace matches a dashboard that should mirror GA4 as of this morning. A monthly append is how a year of **Date** rows stays on the tab.

### Bonus: or just ask the AI Agent to build it for you

From the right sidebar of the Coupler.io app, ask the AI Agent for the metrics, the dimensions, and the sheet:

> Build a Google Sheets flow for our GA4 property with Sessions, Engagement rate, and Session source / medium, keep Date, and start at the beginning of this month.

A few choices stay with you:

1. Connect Google Analytics and approve access.
2. Select the **Properties** in scope.
3. Connect Google Sheets and choose the spreadsheet through the file picker.
4. Call the tab whatever the dashboard expects. Override the starting cell when A1 would land on a title block.

## What data can you export from Google Analytics to Google Sheets with Coupler.io?

There is no catalogue of report types on this connector. The eight bullets below are an editorial grouping of real **Metrics** and **Dimensions** labels, not separate report types. One flow is one combination of up to 9 dimensions plus the metrics you pick. You choose these groupings inside **Metrics** and **Dimensions**. They are not a dropdown of report types. Coupler.io's **Join** can still unite two such flows on **Date** before Data Studio charts the sheet.

- Traffic and acquisition. In **Dimensions**, select **Session source / medium**, **Session campaign**, **Session default channel group**, **First user source**, and **Primary channel group** so a Data Studio acquisition page can split the property by how visits arrived.
- Engagement. In **Metrics**, select **Sessions**, **Engaged sessions**, **Engagement rate**, **Average session duration**, **Bounce rate**, **Views**, and **Event count**, and add the dimension **Event name** when the sheet should name the events behind **Event count**.
- Users. Pick **Active users**, **New users**, and **Total users**, and add the dimension **New / returning**, so Data Studio can separate first-time people from people who came back.
- Ecommerce. Pick **Purchase revenue**, **Transactions**, **Ecommerce purchases**, **Add-to-carts**, and **Checkouts**, plus dimensions **Item name** and **Item brand**, for a merchandising page fed by the sheet.
- Ads cost. Pick **Ads cost**, **Ads clicks**, **Ads impressions**, and **Return on ad spend** when the Data Studio page should show paid cost next to the sessions those ads produced.
- Organic search. Pick **Organic google search clicks**, **Organic google search impressions**, **Organic google search click through rate**, and **Organic google search average position** for a search block that lives beside the rest of the property.
- Geography and tech. In **Dimensions**, select **Country**, **City**, **Device category**, **Browser**, and **Operating system** so the same metrics can be cut by place and by the tool used to visit.
- Pages. In **Dimensions**, select **Page path**, **Page title**, **Landing page**, and **Hostname** when the sheet should answer which URLs collected the metrics you chose.

## Why export Google Analytics to Google Sheets — real life cases

Each Data Studio page asks the GA4 property a different question, and the sheet is what keeps that page from going stale. Coupler.io handles Join, Append, Aggregate, and the other transformations first. Data Studio visualizes the tab.

- **Acquisition by channel and campaign**

  A flow with **Session source / medium**, **Session campaign**, **Session default channel group**, **First user source**, and **Primary channel group** is the acquisition table most marketing pages need. **Date** stays in the flow unless you remove the default. Data Studio breaks the sheet down by those labels after each scheduled replace.

- **Engagement the content team recognizes**

  **Sessions**, **Engaged sessions**, **Engagement rate**, **Average session duration**, **Bounce rate**, **Views**, **Event count**, and **Event name** describe whether visits did anything. Ten metrics is the ceiling on one flow, so leave a less urgent measure for a second run. Coupler.io's **Aggregate** can roll **Date** to a week before Data Studio draws the trend.

- **New people versus people who returned**

  **Active users**, **New users**, **Total users**, and **New / returning** answer who showed up. Put them in one flow with **Date** and the Data Studio scorecard can show the mix without a GA4 exploration. **Properties** can include a second property when the same definitions apply to both.

- **Store activity from view to purchase**

  **Purchase revenue**, **Transactions**, **Ecommerce purchases**, **Add-to-carts**, **Checkouts**, **Item name**, and **Item brand** belong on the merchandising page. **Join** that flow to the sessions flow on **Date** inside Coupler.io when revenue and traffic must share a tab. Data Studio reads the joined sheet.

- **What the ads cost inside GA4**

  **Ads cost**, **Ads clicks**, **Ads impressions**, and **Return on ad spend** are the cost labels on this connector. A Data Studio page can place them next to **Sessions** once both sets are in the sheet. Run the cost labels as their own flow if the ten-metric cap is already full.

- **Organic Google search beside the rest of the site**

  **Organic google search clicks**, **Organic google search impressions**, **Organic google search click through rate**, and **Organic google search average position** are a search block, chosen in **Metrics** like any other measure. Data Studio can show that block on the same report as engagement once Coupler.io's **Join** has aligned the flows on **Date**. The sheet is the shared source.

- **Country, city, and the device in their hand**

  **Country**, **City**, **Device category**, **Browser**, and **Operating system** are five of the nine dimensions a flow may hold, with room left for **Date**. That is enough for a Data Studio map and a device split on one tab. Add a metric such as **Sessions** or **Views** in the same flow.

- **Which pages collected the visit**

  **Page path**, **Page title**, **Landing page**, and **Hostname** turn the same metrics into a page report. **Column management** can put **Landing page** first when the dashboard leads with entry URLs. Data Studio sorts the sheet after the daily run.

## Other Google Sheets integrations

Every other source you can land in Google Sheets with the same no-code setup:

- [Connect Facebook Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-ads-to-google-sheets.md)
- [Connect Facebook Page Insights to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-facebook-page-insights-to-google-sheets.md)
- [Connect Google Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-google-ads-to-google-sheets.md)
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
