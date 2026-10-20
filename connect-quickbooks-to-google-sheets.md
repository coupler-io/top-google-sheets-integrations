---
title: Connect QuickBooks to Google Sheets with Coupler.io
slug: connect-quickbooks-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-quickbooks-to-google-sheets.md
source: QuickBooks, QuickBooks Reports
destination: Google Sheets
meta_title: Connect QuickBooks to Google Sheets with Coupler.io
meta_description: Load QuickBooks Invoice, Bill, and Profit and Loss Detail into Google Sheets on a schedule for a live finance dashboard.
---

![QuickBooks](https://static.coupler.io/importers/quickbooks.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect QuickBooks to Google Sheets with Coupler.io

QuickBooks Online shows customers, bills, and financial statements on screen, and the spreadsheet you export by hand is out of date the next time someone records a payment. Coupler.io keeps two sources: QuickBooks for records, and QuickBooks Reports for statements. Either one lands in Google Sheets on a schedule, ready for a Data Studio finance dashboard.

## How to export QuickBooks data to Google Sheets

Lists — customers, invoices, bills, items, and the rest of the records — use the QuickBooks source. Profit and loss, aging, cash, and the other statements use QuickBooks Reports. Set the records flow up first.

### Step 1. Basic settings

- **Data entity** — the record type this flow exports. One entity per flow. Every name is listed in the next section, with nothing grouped above that list.

### Step 2. Advanced settings

- **Where** — a condition for rows that have no dedicated filter. On Account, for example, you can keep AccountType equal to Accounts Receivable and leave the other account types out.
- **Order** — sort the export. Name the field and add DESC for descending; the field alone is ascending. An email sort such as EmailAddress DESC is the usual pattern.
- **Split by** — when one record holds several lines, name the nested list so each line becomes its own row. For an invoice’s lines, type Line.

Statements are a second source. When you create the flow, pick QuickBooks Reports instead of QuickBooks, then choose the statement and the period below. Records and reports can later share one sheet through Join.

### Step 3. Basic settings

- **Report name** — the statement this flow pulls. Profit and Loss Detail, AR Aging Summary, Cash Flow, and the rest of the catalog are listed after the records.
- **Display columns by** — how the statement is sliced across the top. Choices include Total, Month, Week, Days, Quarter, Year, Customers, Vendors, Classes, Departments, Employees, ProductsAndServices, Name, Account, Transaction Type, Customer, Vendor, Employee, Location, Payment Method, and Day.

### Step 4. Report period

- **Report period** — the named window. Choose Today, Yesterday, This Week, Last Week, This Week-to-date, Last Week-to-date, Next Week, Next 4 Weeks, This Month, Last Month, This Month-to-date, Last Month-to-date, Next Month, This Fiscal Quarter, Last Fiscal Quarter, This Fiscal Quarter-to-date, Last Fiscal Quarter-to-date, Next Fiscal Quarter, This Fiscal Year, Last Fiscal Year, This Fiscal Year-to-date, Last Fiscal Year-to-date, Next Fiscal Year, or Custom.
- **Start date** — used when Report period is Custom. Relative options such as *days ago*, *this month*, *last month*, *this year*, and *last year* keep the window moving. A full trailing year is the advanced macro `{{365daysago}}`.
- **End date** — the closing day of a custom window.
- **Report date** — the as-of day for a statement that is a snapshot rather than a range.

### Step 5. Columns

- **Columns** — which report columns to keep. Leave this empty and QuickBooks sends its default set. Some columns appear only when Multicurrency or Location Tracking is turned on in the company file.

### Step 6. Advanced settings

- **Report structure** — the layout of the statement once it is in the sheet. Pick the structure you want to read; you do not rebuild the statement by hand.

### Step 7. Blend and transform data

- **Column management** — hide fields the close does not use, rename API-style headers, and put the amount column where the controller expects it.
- **Join** — Coupler.io’s Join matches Invoice rows to a sales export on document number or date, so the books and the store share a tab before anyone builds a chart.
- **Append** — stack a second company under the first, or stack this period’s Transaction List under last period’s.
- **Aggregate** — sum bill lines to a vendor or a month inside the flow, which is the grain an AP meeting wants.
- **Custom SQL** — age a balance yourself, or flag JournalEntry rows that do not net to zero.

### Step 8. Google Sheets destination

Transaction fields and statement columns are taken from what QuickBooks returned. Point the flow at a tab and a starting cell.

- **Sheet** — an existing tab works, and so does a name you type. A new name is created after the last sheet in the file.
- **Cell address / Range** — a starting cell such as D1 or B5 opens the block there. An exact range such as B5:G10 keeps the write inside that box. A1 is the default.

### Step 9. Schedule

A cash tab often wants hourly, or every 15 minutes if collections is watching it. The board pack can wait for daily, weekly, or monthly. Replace the cells already filled, or append fresh rows underneath when the tab is a journal of each run.

### Bonus: or just ask the AI Agent to build it for you

Open it from the right sidebar inside the Coupler.io app. A records prompt and a statement prompt both work. For example:

> *"Load QuickBooks Profit and Loss Detail for this fiscal year into Google Sheets, with columns by month, and refresh it every morning."*

You connect QuickBooks yourself and scope the accounts, including whether the flow is the QuickBooks source or QuickBooks Reports. Google Sheets is connected separately; the file picker is where you choose the spreadsheet, then you name the sheet and any starting cell other than A1.

## What data can you export from QuickBooks to Google Sheets with Coupler.io?

The QuickBooks source has 33 record types, one Data entity per flow. Coupler.io’s Join can stitch a report or a sales file onto those rows before they reach the sheet. QuickBooks Reports adds 28 statements, each as its own flow.

- **Account** — the chart of accounts those statements roll into.
- **Attachable** — files hanging off a transaction, so a backup of what was uploaded sits with the books.
- **Bill** — vendor bills, the starting point for what you owe.
- **BillPayment** — payments against those bills, which is how AP clears.
- **Budget** — budget figures to set beside actuals.
- **Class** — class tracking labels used when sales or costs are split that way.
- **CompanyInfo** — the company file identity, useful when several companies share a workbook.
- **CreditMemo** — credits issued to customers.
- **Customer** — the customer list collections and sales both need.
- **Department** — department labels for a split of the books.
- **Deposit** — bank deposits, for matching cash that actually arrived.
- **Employee** — employees referenced by time and by some reports.
- **Estimate** — quotes that have not become invoices yet.
- **ExchangeRate** — rates when more than one currency is in play.
- **Invoice** — customer invoices, the open items behind receivables.
- **Item** — products and services you sell or buy.
- **JournalEntry** — manual journals that never appear on an invoice or a bill.
- **JournalCode** — journal codes that classify those entries.
- **Payment** — customer payments applied to invoices.
- **PaymentMethod** — the methods those payments used.
- **Preferences** — company preferences that explain why a column is present or missing.
- **Purchase** — purchases recorded outside a formal bill.
- **PurchaseOrder** — commitments to vendors before the bill exists.
- **RefundReceipt** — refunds given at the time of sale.
- **SalesReceipt** — sales taken without a separate invoice.
- **TaxAgency** — the agencies you remit tax to.
- **TaxCode** — codes on transactions.
- **TaxRate** — the rates behind those codes.
- **Term** — payment terms on invoices and bills.
- **TimeActivity** — time logged, for billing or for payroll cross-checks.
- **Transfer** — movements between accounts, which a cash tab has to see.
- **Vendor** — who you pay.
- **VendorCredit** — credits from vendors that reduce what you owe.

> **Note:** The reports below are available in the **QuickBooks Reports** source in Coupler.io, separate from the QuickBooks source above. Pick QuickBooks Reports when you create the flow, then choose the report in **Report name**.

- **Account List Detail** — the chart of accounts with the detail columns a reconciliation expects.
- **AP Aging Detail** — each unpaid bill with its age, for the payment run.
- **AP Aging Summary** — what you owe by vendor, without every bill line.
- **AR Aging Detail** — open invoices with their age, which is the collections worklist.
- **AR Aging Summary** — receivables by customer, the figure a cash meeting starts from.
- **Balance Sheet** — assets, liabilities, and equity at the report date you set.
- **Cash Flow** — cash coming in and going out over the Report period.
- **Customer Balance** — what each customer still owes.
- **Customer Balance Detail** — the transactions that make up that balance.
- **Customer Income** — income attributed to customers.
- **Expenses by Vendor** — spend by vendor for a cost review.
- **General Ledger Detail** — ledger lines under the close, not only the totals.
- **Inventory Valuation Summary** — the stock value QuickBooks is carrying.
- **Journal Report** — journal activity in the period.
- **Profit and Loss Summary** — the profit and loss rolled up, which is the version a board pack quotes.
- **Profit and Loss Detail** — profit and loss with the transactions under each line, which is the version finance drills into.
- **Sales by Class Summary** — sales split by Class.
- **Sales by Customer** — sales by customer, beside the Invoice list when you need both.
- **Sales by Department** — sales split by Department.
- **Sales by Product** — sales by item.
- **Tax Summary** — tax collected and the amount to remit.
- **Transaction List** — transactions in the period, across types.
- **Transaction List by Customer** — that list grouped by customer.
- **Transaction List by Vendor** — the same idea grouped by vendor.
- **Transaction List with Splits** — transactions with their split lines kept, so a class or account split is not collapsed.
- **Trial Balance** — debits and credits before you sign off the period.
- **Vendor Balance** — the remaining balance per vendor.
- **Vendor Balance Detail** — bills and payments behind each vendor balance.

## Why export QuickBooks to Google Sheets — real life cases

Controllers build a finance dashboard in Data Studio from a sheet Coupler.io refreshes: profit and loss, cash, and who owes whom. Coupler.io’s Join can place a store’s sales beside Invoice rows before that dashboard is drawn.

- **A profit and loss the board can open**

  On QuickBooks Reports, set Report name to Profit and Loss Detail, Display columns by to Month, and Report period to This Fiscal Year. Coupler.io writes the statement into the sheet each morning. Data Studio charts the months without anyone re-exporting from QuickBooks.

- **Cash, not only accrual profit**

  Cash Flow for This Month, with Report date or the period bounds set the way the treasurer reads cash, lands next to Deposit and Transfer from the records source. Replace mode keeps a single current block. Data Studio shows the month’s movement beside the bank total.

- **Who still owes you**

  AR Aging Summary is the headline; AR Aging Detail is the invoice list collections calls from. Invoice and Customer, in their own flows, supply terms and contact fields the aging report does not. Data Studio filters past-due buckets.

- **Bills due this week**

  AP Aging Detail plus Bill and Vendor gives AP a sheet of what is unpaid and who to pay. Where can limit Account rows to Accounts Receivable on a different flow, while this one stays on bills. Data Studio totals the amount due before Friday.

- **Store sales against the books**

  Coupler.io’s Join matches SalesReceipt or Invoice to an order export on date or document number, and the combined rows hit one tab. The Data Studio page then compares recognized sales with what the store recorded, instead of asking someone to line up two downloads.

- **Class and department profitability**

  Sales by Class Summary and Sales by Department use the Class and Department lists you can also export as records. Display columns by can follow Class or Department when the statement itself should be sliced that way. Data Studio keeps a page per class for the operators who own them.

- **Vendor spend before the budget meeting**

  Expenses by Vendor beside Budget shows where actuals left the plan. PurchaseOrder adds commitments that are not bills yet. A weekly schedule is enough for that meeting. Data Studio highlights vendors over the budget line.

- **Trial balance at close**

  Trial Balance for Last Month, plus Journal Report and JournalEntry, is the pack the reviewer ticks through. Columns left empty keeps QuickBooks’ default statement columns. Data Studio is optional here; many teams just freeze the sheet once the period locks.

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
- [Connect Shopify to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-shopify-to-google-sheets.md)
- [Connect TikTok Ads to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-ads-to-google-sheets.md)
- [Connect TikTok Organic to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-tiktok-organic-to-google-sheets.md)
- [Connect WooCommerce to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-woocommerce-to-google-sheets.md)
- [Connect Xero to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md)
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
