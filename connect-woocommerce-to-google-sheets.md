---
title: Connect WooCommerce to Google Sheets with Coupler.io
slug: connect-woocommerce-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md
source: WooCommerce
destination: Google Sheets
meta_title: Connect WooCommerce to Google Sheets with Coupler.io
meta_description: "Send WooCommerce Orders, Products, and Report: Sales report to Google Sheets for a store dashboard that stays current."
---

![WooCommerce](https://static.coupler.io/importers/woocommerce.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect WooCommerce to Google Sheets with Coupler.io

WooCommerce keeps orders, coupons, reviews, and its built-in reports inside wp-admin, and a manual export does not come back tomorrow with new rows. Coupler.io lands the category you select in Google Sheets on a schedule, ready for a Data Studio dashboard the store team can open without another download.

## How to export WooCommerce data to Google Sheets

Orders, customers, products, coupons, taxes, shipping zones, and the Report totals all start here. Reports use a period; order lists use status and a search.

### Step 1. Basic settings

- **Data entity** — the category for this flow. One entity per flow. The full set, reports included, is listed later on this page.

### Step 2. Advanced settings

- **After date** — keep rows recorded after this date and time. A relative choice (*days ago*, *this month*, *last month*, *this year*, *last year*) saves you from editing the flow next month.
- **Before date** — the latest recorded moment to include. Leave it empty when the tab should run up to the latest orders.
- **Search** — an exact match on a customer name (for example SMYTH) or on a line-item title (for example HOODIE WITH LOGO). Anything short of an exact match is left out.
- **Status** — which orders to pull. Choose Any, Pending, Processing, On-hold, Completed, Cancelled, Refunded, Failed, or Trash.
- **Period** — the window for a report entity. Choose Today, This Week, This Month, Last Month, This Year, or Custom.
- **Start date** — the first day of a report when Period is Custom. For a fixed trailing year, the advanced form is `{{365daysago}}`.
- **End date** — the last day of that custom report window.

### Step 3. Columns

- **Columns** — type the column names you want, one on each line, in the order they should appear. Coupler.io does not ask you to design a separate layout for the spreadsheet.

### Step 4. Blend and transform data

- **Column management** — hide plugin fields nobody reads, give cryptic keys a store-team label, and reorder so order total sits near the left.
- **Join** — Coupler.io’s Join lines WooCommerce orders up with payouts or ad spend on a shared date or order id, and the combined rows land in the sheet together.
- **Append** — stack two sites, or stack this month under a prior extract when you want one long order log.
- **Aggregate** — roll line items to a product or a week inside the flow, which is the grain a Monday meeting actually wants.
- **Custom SQL** — net coupon value out of revenue, or flag orders that are still Processing after a set age.

### Step 5. Google Sheets destination

The store’s fields arrive named. You only say which tab receives them and where the block begins.

- **Sheet** — type a new tab name and Coupler.io places it after the last sheet, or select a tab the file already contains.
- **Cell address / Range** — the start of the import. A cell such as D1 or B5, or a fixed block such as B5:G10. Skip it and writing begins at A1.

### Step 6. Schedule

Processing orders can refresh every 15 minutes if the floor is watching them. Hourly, daily, weekly, and monthly cover everything slower. Overwrite the range already in the sheet, or append new rows under it when the tab is a history.

### Bonus: or just ask the AI Agent to build it for you

It sits in the right sidebar of the Coupler.io app. Say what the sheet is for:

> *"Pull WooCommerce orders with status Processing for this month into Google Sheets, with line items, and refresh the tab every hour."*

Connecting the store is still yours: connect WooCommerce, scope the accounts, and connect Google Sheets. The spreadsheet is selected in the file picker. You name the sheet, and you name a cell if A1 is the wrong corner.

## What data can you export from WooCommerce to Google Sheets with Coupler.io?

There are 23 data entities, and each flow exports one of them. Report entities are in that same list. Coupler.io’s Join can bring a second source onto the sheet before Data Studio charts it.

- **Continents** — the continent list your shipping and tax rules refer to.
- **Countries** — countries the store knows, so a regional report has a stable lookup.
- **Coupons** — every coupon code, which is what you join to orders when a promotion needs a post-mortem.
- **Currencies** — the currencies enabled on the store, useful when more than one price list is live.
- **Customers** — buyer accounts for repeat-rate and support questions.
- **Orders** — the order header: status, totals, and who bought.
- **Orders with line items** — a row per product on the order, which is the grain for SKU sales.
- **Product attributes** — attribute definitions, so size and color filters in a report match the catalog.
- **Product categories** — the category tree merchandising reports against.
- **Product reviews** — review text and ratings, for a quality tab that updates with the store.
- **Product shipping classes** — the classes that drive freight, kept next to the products that use them.
- **Product tags** — tags on products, for campaign groupings that are not formal categories.
- **Products** — the catalog itself, prices and stock included.
- **Report: Coupon totals** — how much each coupon gave away over the Period you set.
- **Report: Customer totals** — customer counts for that same report window.
- **Report: Order totals** — order counts and value, the figure a daily store check starts from.
- **Report: Product totals** — product performance rolled up by the report.
- **Report: Review totals** — review volume over the period, beside the catalog rather than inside each product screen.
- **Report: Sales report** — the store’s sales report for Today, This Week, This Month, Last Month, This Year, or a Custom range.
- **Report: Top sellers report** — the products that sold the most in that period.
- **Shipping zones** — where you ship and how zones are drawn, so freight questions have a map.
- **Tax classes** — the classes products fall into.
- **Tax rates** — the rates behind those classes, which finance needs at filing time.

## Why export WooCommerce to Google Sheets — real life cases

Store leads usually want a Data Studio report of orders, coupons, and reviews, fed by a sheet Coupler.io keeps fresh. Join in Coupler.io can attach gateway payouts to those orders before any chart is drawn.

- **The queue of orders still in Processing**

  Data entity Orders and Status Processing is the list the floor works from. After date set to *this week* drops last month’s completed history. Data Studio counts how many of those rows are still open after noon.

- **This month’s sales without opening wp-admin**

  Choose Report: Sales report and Period This Month, and Coupler.io refreshes the numbers on the schedule. Start date and End date stay unused unless you switch Period to Custom. The Data Studio scorecard reads the sheet, so the Monday meeting is not a screenshot.

- **What the top sellers actually were**

  Report: Top sellers report for Last Month gives merchandising a ranked list that does not change under their feet while they discuss it. Products, in a second flow, supplies price and stock for the same SKUs. Data Studio puts rank and stock on one page.

- **Which coupons paid for themselves**

  Coupons holds the codes; Report: Coupon totals holds what they discounted in the Period. Coupler.io’s Join can put both on one tab before the sheet is saved. Data Studio shows discount given against the orders those codes touched.

- **Reviews that should reach the buyer, not only the product page**

  Product reviews lands ratings and text in a tab the team can filter. Report: Review totals adds the count for the period so one angry week is visible. A Data Studio page sorts low scores beside the products they mention.

- **Tax classes and rates at filing time**

  Tax classes and Tax rates are the lookup; Orders with line items carries the tax charged on each row. A daily or monthly schedule means the sheet is already filled when the return is due. Data Studio breaks tax collected by class.

- **Failed and cancelled checkout, not only completed revenue**

  Status Failed, and a second flow for Cancelled, shows demand that never became Completed. Search can isolate one product title if a single SKU is the suspect, and it has to match exactly. Data Studio charts those statuses next to paid orders.

- **Two sites, one order log**

  Append stacks a second WooCommerce site under the first, and Columns keeps the same header on both. Customers from each site can sit on a neighboring tab. Data Studio filters the site when the group view needs a single brand.

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
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
