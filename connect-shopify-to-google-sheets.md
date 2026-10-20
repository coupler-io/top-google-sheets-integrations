---
title: Connect Shopify to Google Sheets with Coupler.io
slug: connect-shopify-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md
source: Shopify
destination: Google Sheets
meta_title: Connect Shopify to Google Sheets with Coupler.io
meta_description: Pull Shopify Orders, Customers, Products, and Inventory into Google Sheets on a schedule for a current sales dashboard.
---

![Shopify](https://static.coupler.io/importers/shopify.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Shopify to Google Sheets with Coupler.io

Shopify’s admin keeps orders, customers, products, and stock on separate screens, and a CSV you download is already stale by the afternoon. Coupler.io writes the category you pick into Google Sheets on a schedule, so a Data Studio dashboard can read a tab that still matches the store.

## How to export Shopify data to Google Sheets

Orders, customers, products, inventory, fulfillments, refunds, shipping lines, and the older legacy shapes all come from this source. One flow carries one category.

### Step 1. Basic settings

- **Data entity** — the category this flow keeps in the sheet. Pick one. Every option, including each legacy shape, is listed further down.

### Step 2. Columns

- **Columns** — the fields to keep, and the order they should take. Store name, Entity ID (an Order ID, for example), and Updated At always come back with the export.

### Step 3. Date filters

- **Created after date** — include records created after this moment. The relative picker (*days ago*, *this month*, *last month*, *this year*, *last year*) moves the window forward on later runs. Times follow your browser’s time zone. A trailing year is an advanced case: write `{{365daysago}}`.
- **Created before date** — the closing bound on creation time. Leave it open if the sheet should stay current through today.
- **Changed after date** — only records updated after this moment, which keeps a frequent refresh from re-reading the whole history.
- **Changed before date** — drop anything changed later than this moment when you are rebuilding a week that already closed.

### Step 4. Advanced filters

- **Filter after ID** — skip records at or below this id so the next run can continue from where the last one stopped. Pair it with an append into the sheet when you want a growing log.
- **Status** — which orders to include. Choose Any, Open, Closed, or Cancelled. This is the order-state field.
- **Financial status** — the payment state of those orders. Choose Any, Authorized, Pending, Paid, Partially paid, Refunded, Voided, Partially refunded, or Unpaid.
- **Fulfillment status** — how far shipping has got. Choose Any, Shipped, Partial, or Unshipped.
- **Status** — a second field with the same title, used for product state when the entity is a product. Choose Any, Active, Archived, or Draft.

### Step 5. Blend and transform data

- **Column management** — drop variant attributes merchandising never opens, rename Entity ID so the sheet says Order ID, and put money columns first.
- **Join** — Coupler.io’s Join matches orders to ad clicks or to a ledger on a shared date or id, and writes one combined tab before any chart is built.
- **Append** — stack a second shop under the first. Store name shows which store each row came from.
- **Aggregate** — sum line revenue up to a product or a day inside the flow, so the sheet already holds the grain the meeting uses.
- **Custom SQL** — add a returning-buyer flag, freight-adjusted margin, or any figure the chosen entity does not already contain.

### Step 6. Google Sheets destination

Coupler.io lays columns out from the Shopify payload itself. You choose where that block sits.

- **Sheet** — select a tab the file already has, or type a new name. Coupler.io creates that sheet after the last one.
- **Cell address / Range** — where the import starts. One cell, such as B5 or D1, or an exact range such as B5:G10. The default is A1.

### Step 7. Schedule

A warehouse watching unshipped orders can refresh every 15 minutes. A catalog review is fine on hourly, daily, weekly, or monthly. Each run can overwrite the block already in the tab, or add new rows beneath it.

### Bonus: or just ask the AI Agent to build it for you

The AI Agent is in the Coupler.io app, in the right sidebar. Describe the tab you want instead of clicking every field:

> *"Load Shopify orders created in the last 90 days with financial status Paid into Google Sheets, and refresh that tab every day."*

What stays with you: connect Shopify, scope the accounts, then connect Google Sheets. Choose the spreadsheet in the file picker, name the sheet, and set a cell when the block should not open at A1.

## What data can you export from Shopify to Google Sheets with Coupler.io?

Twenty-two data entities are available, and each flow uses one of them. Coupler.io’s Join can attach a second source to that export before the sheet is written. The legacy entities are here too: they keep an older column layout alive for sheets that already depend on it.

- **Orders** — one row per order, which is the grain a daily revenue tab needs.
- **Customers** — buyer records for repeat purchase and location questions.
- **Inventory** — quantities on hand, so a buyer can see what is about to run out.
- **Products** — the catalog, which you then narrow with Active, Archived, or Draft.
- **Products with variants** — a row per variant, so size and color stay visible.
- **Orders with line items** — revenue at the SKU that was actually sold.
- **Orders with activities** — the edit history on an order, when you need to know what changed.
- **Orders transactions** — payments taken against the order, separate from the order header.
- **Orders refunds transactions** — money sent back, without opening each order in the admin.
- **Orders with refunded items** — which units were returned, not only the refund total.
- **Orders with shipping lines** — freight charged on the order, ready to set beside a carrier bill.
- **Order fulfillments with line items** — what left the building, line by line.
- **Orders (legacy)** — the earlier orders layout, so a sheet built on it keeps receiving rows.
- **Products (legacy)** — the earlier product columns for a catalog tab you would rather not rebuild.
- **Inventory (legacy)** — the earlier stock columns when a reorder file already points at them.
- **Customers (legacy)** — the earlier customer columns for a shared buyer list.
- **Products with variants (legacy)** — variant rows in the older layout an option-level sheet already expects.
- **Orders with line items (legacy)** — SKU-level sales in the older layout a margin file was built on.
- **Orders with activities (legacy)** — the older activity columns if an audit tab depends on them.
- **Order fulfillments with line items (legacy)** — the older fulfillment layout for a pick list that should not change shape.
- **Orders with shipping lines (legacy)** — the older shipping-line columns when freight reporting is already wired up.
- **Orders refunds transactions (legacy)** — the older refund-transaction columns so a finance archive does not break.

### Dataset templates

Coupler.io also ships dataset templates: named tables that already combine Shopify fields. Each name below is its own flow, with a one-line sense of what you get. Three of them also read Google Analytics.

- **Shopify Returning customer rate** — the share of orders from people who had already bought, which is the retention number most store reviews ask for.
- **Shopify inventory monthly stockout forecast** — which variants are likely to hit zero over the coming months, so purchase orders go out before a season ends.
- **Shopify inventory weekly stockout forecast** — stock-out risk on a weekly grain for the replenishment meeting.
- **Shopify inventory daily stockout forecast** — a day-level warning list for whoever watches fast movers.
- **Shopify Sales by product variant** — units and revenue at variant grain, so a single colorway can be judged on its own.
- **Shopify Sales by sources** — sales split by the source on the order, for a channel-mix view.
- **Shopify top customers** — buyers ranked by what they spend, for account follow-up.
- **Shopify sales by order fulfillment status** — sales grouped by whether the order has shipped, partly shipped, or not shipped.
- **Shopify sales by order financial status** — sales grouped by the payment state, from paid through refunded.
- **Shopify Sales by billing location** — sales by the billing geography, for regional targets.
- **Shopify Total customers & Avg order value** — how many customers you have beside what a typical order is worth.
- **Shopify Top selling products** — products ranked by sales, which is the list merchandising opens each week.
- **Shopify Sales by new vs returning customers** — order value from people buying for the first time, set beside order value from people who already had an order.
- **Shopify Line Items with Shipping and Taxes** — each line with freight and tax on the same row, so margin does not need a second download.
- **Shopify Total sales by line item** — sales totaled at line-item grain.
- **Shopify Total sales by order** — sales totaled on the order, which is how many finance teams recognize a sale.
- **Shopify Orders with COGS** — orders carrying cost of goods, so gross margin is already on the sheet.
- **Shopify Line items with COGS** — cost at line grain, which matters when variants do not share a cost.
- **Shopify and GA4 monthly performance** — Shopify sales next to site traffic for the month; this template also uses Google Analytics.
- **Shopify and GA4 weekly performance** — Shopify results beside Google Analytics, totaled by week for an operating review.
- **Shopify and GA4 daily performance** — a daily pairing of Shopify sales and Google Analytics, so a launch can be checked the next morning.

## Why export Shopify to Google Sheets — real life cases

Merchandising, finance, and the warehouse can share one Google Sheet, and Data Studio is where that sheet becomes the store dashboard. Coupler.io’s Join puts a second source on the tab first — ad cost, or a ledger — and the Data Studio report then charts that sheet.

- **Paid orders on the morning scorecard**

  Set Data entity to Orders and Financial status to Paid, and set Created after date with the relative picker so the window rolls. Coupler.io refreshes the tab on the schedule you chose. Data Studio reads that tab for revenue, order count, and what a typical paid order is worth.

- **A pick list of orders that have not shipped**

  Status Open plus Fulfillment status Unshipped turns the sheet into work still on the floor, and Changed after date keeps the pull to orders touched recently. The warehouse sorts the tab. Data Studio can chart how many of those rows are aging past a day.

- **Refunds beside the orders they came from**

  Orders refunds transactions shows money going back, and Financial status Refunded or Partially refunded narrows the order list to the same story. Filter after ID lets a later run add only newer refunds under the existing rows. Finance checks the sheet against payouts.

- **Variants about to stock out**

  Inventory plus a daily schedule keeps on-hand counts from sitting still, and the Shopify inventory daily stockout forecast template turns those counts into a warning list. Buyers sort the sheet by days of cover. Data Studio highlights variants already at zero.

- **Drafts and archived products that should not be live**

  On Products, the product-state Status field set to Draft or Archived shows catalog rows that are not for sale. Products with variants adds the option-level detail when a parent product is still Active. A Data Studio table flags drafts that have sat untouched since last season.

- **Freight and tax on the same line as revenue**

  Orders with shipping lines keeps the freight you charged next to the order. The Shopify Line Items with Shipping and Taxes template puts tax on that row as well. Data Studio compares shipping collected with what you expected to keep.

- **First-time buyers versus people who returned**

  Customers gives you the people; Shopify Sales by new vs returning customers splits the money. Created after date limits the cohort to a season or a year. The Data Studio report shows whether growth is new demand or repeat demand.

- **Every store in one tab**

  Append stacks a second shop under the first, and Store name tells them apart. Columns can keep the same fields in both, so the sheet does not grow a different header per brand. Data Studio uses that column as a filter on a group sales view.

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
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
