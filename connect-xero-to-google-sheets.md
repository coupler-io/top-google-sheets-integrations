---
title: Connect Xero to Google Sheets with Coupler.io
slug: connect-xero-to-google-sheets
canonical: https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-xero-to-google-sheets.md
source: Xero, Xero Reports
destination: Google Sheets
meta_title: Connect Xero to Google Sheets with Coupler.io
meta_description: Export Xero Invoices, Payments, and Profit And Loss to Google Sheets on a schedule for a current finance dashboard.
---

![Xero](https://static.coupler.io/importers/xero.svg) → ![Google Sheets](https://static.coupler.io/importers/google_spreadsheet.svg)

# Connect Xero to Google Sheets with Coupler.io

Xero keeps invoices, bank lines, payroll, and financial statements in different parts of the organisation, and a spreadsheet saved from the screen does not pick up the next receipt. Coupler.io has two sources: Xero for those records, and Xero Reports for the statements. Both can refresh a Google Sheets tab on a schedule for a Data Studio dashboard.

## How to export Xero data to Google Sheets

Accounting lists, payroll for the regions Xero supports here, and projects all use the Xero source. Profit and loss, the balance sheet, aged receivables, and the other statements use Xero Reports. Start with the records wizard.

### Step 1. Basic settings

- **Xero tenant** — the organisation this flow reads. If it is missing from the list, reconnect the account under Connections.
- **Data entity** — the list or payroll or project category to export. One category per flow. The groups are written out in the next section.
- **Report type** — Detailed or Simple. Simple includes the default fields and is available for every data entity. Detailed adds further fields and is available for Invoices, Contacts, Bank transactions, and Manual journals.
- **Projects** — which projects to read when the entity is project work, so tasks and time are not pulled for the whole organisation.

### Step 2. Date filters

- **Changed after** — records modified after this moment. Anchor it on *days ago*, or choose *this month*, *last month*, *this year*, or *last year*, so the next run shifts without an edit.
- **Start date** — the opening day of a range the entity uses.
- **End date** — the closing day of that range.
- **Created after** — only records created after this moment.
- **Created before** — drop records created later than this moment.
- **Expiring after** — the start of an expiry window. Quotes are the entity this usually matters for.
- **Expiring before** — the end of that expiry window.

### Step 3. Advanced settings

- **Statuses** — for invoices, one or more of Draft, Submitted, Authorised, Paid, Voided, and Deleted. Projects use a field titled Statuses by default for the same kind of filter.
- **Journal number more than** — journals whose journal number is greater than this value.
- **Journal number less than** — journals whose journal number is lower than this value.
- **Split by** — when a document has several lines, name the nested list so each line is its own row. For invoice lines, type LineItems.
- **Status** — time entries title this filter Status rather than Statuses. Pick the status those time rows must have.
- **Include archived** — also bring records that Xero has archived, so a closed project or a retired contact is not left out.

Lists, payroll, and projects stay on the Xero source. Financial statements are a second source, Xero Reports. Pick Xero Reports when you create the flow, then set the statement with the steps below.

### Step 4. Basic settings

- **Xero tenant** — the same kind of organisation choice as on the records source. Reconnect under Connections if the organisation is not listed.
- **Report type** — the statement. Aged Payables By Contact, Profit And Loss, Trial Balance, and the other names are listed after the records.
- **Report structure** — Xero-style format keeps the statement looking like Xero. Date-by-row format puts each period on its own row, which is easier to chart.

### Step 5. Contact

- **Contact ID** — the contact a single-contact statement needs. Aged Receivables By Contact and Aged Payables By Contact are the usual cases.

### Step 6. Bank account

- **Bank Account ID** — the bank account when the statement is about one account, such as Bank Statement.

### Step 7. Report period

- **Date** — the as-of day for a snapshot such as the balance sheet.
- **Start date** — the first day of a ranged statement. Relative dates work, and a trailing year can be written as the advanced macro `{{365daysago}}`.
- **End date** — the last day of that range.

### Step 8. Parameters

- **Number of periods to compare** — how many earlier periods to place beside the current one.
- **Period** — the length of each of those periods. Choose Month, Quarter, or Year.
- **Tracking category ID** — break the statement down by one tracking category. Comparison across periods is not available once a tracking category is set; you get a single period.
- **Tracking category ID-2** — a second tracking category, with the same single-period limit.
- **Tracking option ID** — narrow a tracking category to one option. The wizard uses this title for the option filter. You filter with the option, not with the category id alone.
- **Tracking option ID-2** — the option under the second tracking category.
- **Include cash transactions only** — restrict the statement to cash transactions when you want cash movements rather than unpaid invoices.
- **Standard layout** — ask Xero for its standard statement layout.

### Step 9. Blend and transform data

- **Column management** — hide organisation fields the pack does not quote, retitle tracking columns, and move the amount to the front.
- **Join** — Coupler.io’s Join aligns Invoices with a shop’s orders on number or date, and writes one tab the finance dashboard can trust.
- **Append** — stack a second Xero tenant under the first when a group file needs both organisations.
- **Aggregate** — roll invoice lines up to a contact or a month before the sheet is saved.
- **Custom SQL** — net credit notes against invoices, or keep only bank lines that still need a match.

### Step 10. Google Sheets destination

Each entity and each statement brings its own columns. Coupler.io places them from the data; you name the tab and the cell.

- **Sheet** — name a new tab and it is created after the last one, or select a tab already in the spreadsheet.
- **Cell address / Range** — default start is A1. A cell such as B5 or D1 suits a tab that already has a title. An exact range such as B5:G10 holds the statement inside a fixed area.

### Step 11. Schedule

Bank lines and payroll often suit hourly or daily. A monthly board pack can stay on weekly or monthly, and every 15 minutes is there if collections must see new payments quickly. Replace the range in the sheet, or append new rows under it for a running log.

### Bonus: or just ask the AI Agent to build it for you

Use the AI Agent in the right sidebar of the Coupler.io app and describe the tab:

> *"Load the Xero Profit And Loss for this year, in date-by-row format, into Google Sheets, and refresh it each weekday morning."*

You connect Xero, scope the accounts, pick the Xero or Xero Reports source, connect Google Sheets, choose the spreadsheet in the file picker, and name the sheet. Set a cell if the import should not start at A1.

## What data can you export from Xero to Google Sheets with Coupler.io?

The Xero source offers 53 categories in the Data entity list, one flow each. Coupler.io’s Join can attach another system to those rows before they are written. Payroll is split by region below, then projects. Nine statements live on the other source.

Accounting entities:

- **Accounts** — the chart of accounts the statements add up to.
- **Bank transactions** — spend and receive money lines, which a cash tab has to see every day.
- **Bank transfers** — movements between your own bank accounts.
- **Branding themes** — the themes on documents you send, when a multi-brand file needs them.
- **Contact groups** — groups of contacts for a mailing or a collection rule.
- **Contacts** — customers and suppliers in one list.
- **Credit notes** — credits that reduce what an invoice still collects.
- **Currencies** — currencies the organisation uses.
- **Employees** — employees in the accounting API, separate from the regional payroll lists.
- **Expense claims** — staff claims waiting to be paid or already paid.
- **Invoices** — sales invoices, the open items behind receivables.
- **Items** — products and services on those invoices.
- **Journals** — journal lines, which you can bound with the journal-number filters.
- **Linked transactions** — links between documents, so a bill tied to an invoice stays visible.
- **Manual journals** — journals typed in, as opposed to journals Xero created from a document.
- **Organisation** — the organisation profile for this tenant.
- **Overpayments** — customer money that has not been allocated to an invoice yet.
- **Payments** — payments applied to invoices, the cash collections actually recorded.
- **Prepayments** — amounts paid before the bill or invoice they belong to.
- **Purchase orders** — commitments to suppliers before a bill exists.
- **Receipts** — receipts recorded against spend.
- **Repeating invoices** — invoices Xero will raise again, so you can see what is about to bill.
- **Tax rates** — the rates on transactions, for the return.
- **Tracking categories** — the categories you use to split the ledger.
- **Users** — people with access to the organisation.
- **Quotes** — quotes and their expiry window, via Expiring after and Expiring before.

Payroll (for United Kingdom or New Zealand):

- **Benefits** — benefit types set up for UK or New Zealand payroll.
- **Deductions** — deductions taken from pay in those regions.
- **Earning rates** — how earnings are rated for UK or New Zealand employees.
- **Earnings orders (Statutory deductions)** — statutory deduction orders on pay.
- **Employees (UK or NZ)** — the payroll employee list for the United Kingdom or New Zealand.
- **Leave types** — leave categories those employees can take.
- **Pay run calendars** — when pay runs fall.
- **Pay runs** — each pay run and what it contained.
- **Reimbursements** — amounts repaid to employees through payroll.
- **Accounts (UK or NZ)** — payroll accounts for the United Kingdom or New Zealand.
- **Timesheets** — time submitted for those pay runs.
- **Tracking categories (UK or NZ)** — tracking on UK or New Zealand payroll.

Payroll (for Australia):

- **Employees (AU)** — Australian payroll employees.
- **Leave applications** — leave requested by those employees.
- **Leave applications with leave periods** — the same requests with each leave period on the row.
- **Earnings rates** — Australian earnings rates, kept apart from the United Kingdom and New Zealand earning rates so a payroll sheet does not mix the two lists.
- **Deduction types** — kinds of deduction configured for Australia.
- **Leave types** — Australian leave categories.
- **Reimbursement types** — kinds of reimbursement Australian payroll can pay.
- **Pay runs** — Australian pay runs.
- **Payroll calendars** — the calendars those pay runs follow.
- **Settings** — Australian payroll settings for the organisation.
- **Accounts (AU)** — payroll accounts for Australia.
- **Tracking categories (AU)** — tracking used on Australian payroll.
- **Super funds** — superannuation funds employees are paid into.
- **Timesheets** — Australian timesheets at header level.
- **Timesheets with timesheet lines** — those timesheets with each line kept, which is the grain for hours by task.

Projects:

- **Projects** — the project list, which the Projects field on the wizard can narrow.
- **Tasks by projects** — tasks sitting under those projects.
- **Time by projects** — time recorded against projects. The status filter for this entity is titled Status.
- **Users** — users associated with projects, alongside the organisation user list above.

> **Note:** The reports below are available in the **Xero Reports** source in Coupler.io, separate from the Xero source above. Pick Xero Reports when you create the flow, then choose the statement in **Report type**.

- **Aged Payables By Contact** — what you owe one supplier, aged. Pass that supplier in Contact ID.
- **Aged Receivables By Contact** — what one customer still owes, aged the same way.
- **Balance Sheet** — assets, liabilities, and equity at Date.
- **Bank Statement** — movements on the account you pass as Bank Account ID.
- **Bank Summary** — a short view of the bank accounts, which is the cash page many teams open first.
- **Budget Summary** — budget against the periods you compare.
- **Executive Summary** — the short pack of ratios and totals Xero builds for a leadership glance.
- **Profit And Loss** — profit and loss for the range, in Xero-style format or Date-by-row format.
- **Trial Balance** — debits and credits for the period you are closing.

## Why export Xero to Google Sheets — real life cases

A finance dashboard in Data Studio — profit and loss, cash, receivables, and payables — starts from a sheet this flow refreshes. Join in Coupler.io can line a store’s sales up with Invoices first, so the report is not left to reconcile two downloads.

- **Profit and loss by month, already in rows**

  On Xero Reports, set Report type to Profit And Loss, Report structure to Date-by-row format, Period to Month, and Number of periods to compare to the span the board wants. Coupler.io refreshes the sheet on weekday mornings. Data Studio charts those rows without reshaping a Xero-style grid.

- **Cash in the bank accounts**

  Bank Summary is the headline, Bank Statement the detail for one Bank Account ID, and Bank transactions the accounting lines behind both. A daily replace keeps one current block. Data Studio shows the balance next to unreconciled lines.

- **Receivables the collections team can call**

  Aged Receivables By Contact needs a Contact ID; Invoices with Statuses Authorised, and Payments, cover the whole book in separate flows. Changed after limits a busy file to what moved. Data Studio sorts open invoices by age.

- **Payables before the payment run**

  Aged Payables By Contact plus Purchase orders shows bills you owe and commitments not billed yet. Contact ID points the aged statement at one supplier when a dispute is the question. Data Studio totals what is due this week.

- **Shop sales versus what Xero invoiced**

  Coupler.io’s Join matches Invoices to order rows on number or date and writes a single tab. Credit notes on their own flow explain gaps where a sale was reversed. The Data Studio page compares store takings with recognised invoices.

- **Tracking categories on the profit and loss**

  Set Tracking category ID, and if you need one slice of it, Tracking option ID. Period comparison turns off once a tracking category is set, so keep that flow to a single period and use another flow for the comparison. Data Studio filters the option the way operators already talk about projects or regions.

- **Balance sheet on the morning of the close**

  Balance Sheet with Date set to the period end, beside Trial Balance, is the pair the reviewer opens. Report structure can stay Xero-style format if the sheet should look like Xero. Data Studio is there for the trend; the sheet itself is the sign-off copy.

- **Payroll hours against the pay run**

  For Australia, Timesheets with timesheet lines and Pay runs land in neighboring tabs; for the United Kingdom or New Zealand, Timesheets and Pay runs do the same job. Include archived if a leaver must stay in the history. Data Studio compares hours submitted with what the pay run paid.

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
- [Connect YouTube Analytics to Google Sheets](https://github.com/coupler-io/top-google-sheets-integrations/blob/main/connect-youtube-analytics-to-google-sheets.md)
