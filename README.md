# Invoice-Payment Reconciliation Project (SQL + Power BI)

## Overview

This project demonstrates how to build an end-to-end financial reconciliation system that matches invoices vs. payments and highlights mismatches for resolution.
The solution was implemented using:
- Snowflake SQL → Schema design, data merges, reconciliation logic.
- Power BI → Dashboards for KPIs, trends, exception analysis.
The project solves a common finance problem: manual reconciliation is error-prone, slow, and lacks transparency. By automating with SQL and visualizing with Power BI, we can provide faster insights and reduce operational overhead.

## Business Problem

Finance teams often face:
- Missing payments (invoices unpaid)
- Partial payments (invoices underpaid)
- Overpayments (customers pay more than billed)
- Duplicate/late payments
Traditional manual reconciliation is inefficient and fails to give real-time visibility.

## Project Objectives

- Design a data model to store invoices, payments, and customers.
- Implement reconciliation rules in SQL to classify each invoice:
  - MATCHED → Invoice fully paid
  - PARTIAL → Invoice partially paid
  - OVERPAID → Payments exceed invoice
  - UNPAID → No payment received
- Build stored procedures for:
  - Data merging (idempotent loads)
  - Reconciliation with audit logs
- Create a Power BI dashboard with:
  - KPIs (Match %, Exceptions, Totals)
  - Trend line across reconciliation runs
  - Exception explorer with drilldown
  - Customer-level reconciliation matrix

## 🛠 Tools & Technologies

- Snowflake → Cloud data warehouse, SQL stored procedures
- Power BI → Data modeling, DAX, dashboards
- Excel/CSV → Sample datasets (customers, invoices, payments)

## ⚙️ Implementation Phases
### Phase 1 – Rules & Acceptance Criteria
- Defined reconciliation rules: Matched, Partial, Overpaid, Unpaid.

### Phase 2 – Schema Design
- Built canonical tables:
  - dim_customer → Customer master
  - fact_invoice → Invoice transactions
  - fact_payment → Payment transactions (extended with invoice_id)
  - recon_invoice_payment → Reconciliation results
  - recon_exceptions → Exception details

### Phase 3 – Merge Procedures
- Created idempotent merge stored procedures:
  - sp_merge_customers
  - sp_merge_invoices
  - sp_merge_payments
  - Added audit logging to track inserted/updated rows.

### Phase 4 – Reconciliation Engine
- Developed sp_reconcile_invoices_payments:
  - Compares invoices and payments.
  - Classifies results into Match statuses.
  - Logs reconciliation results and exceptions with run_id for traceability.

### Phase 5 – Power BI Dashboard
- Connected Power BI to Snowflake.
- Built pages:
  - Executive Summary: KPIs + trend line.
  - Reconciliation Heatmap: Customer vs Match Status.
  - Exception Explorer: Table of exceptions with suggested actions.
  - Root Cause Analysis: Breakdown of exception types and top customers.

## Sample Results
- Dataset Size: 200 invoices, ~180+ payments.
- Validation Query Output:
  - Total invoices = 200
  - Matched invoices = 50
  - Rest fell into Partial, Overpaid, or Unpaid.
- Power BI Findings:
  - Match % started very low (~5–8%).
  - Exceptions dominated, especially overpaid.
  - Dashboard allowed tracking exception trends and customer drilldown.

## Key Deliverables
- SQL schema and stored procedures.
- Audit logs for merges and reconciliations.
- Exception tracking table with suggested actions.
- Power BI dashboard (.pbix file).

## Achievements
- Designed and executed a full ETL + reconciliation pipeline.
- Automated exception classification with SQL.
- Built an executive-ready dashboard in Power BI.
- Hands-on learning of real-world financial data reconciliation.

## Future Enhancements
- Automate ingestion with Snowflake Tasks & Streams.
- Add scheduled refresh in Power BI Service.
- Expand dashboard with currency/system filters.
- Apply predictive analytics to forecast exception patterns.

## Conclusion
This project demonstrates how SQL and Power BI can be combined to solve a critical finance problem — invoice-payment reconciliation. The approach provides:
- Data reliability via merge procedures.
- Transparency via reconciliation and exception tracking.
- Business insights via dashboards.
It’s a showcase of applying data analytics skills to real-world financial operations.

## Project By: Shijin Ramesh
Data Analyst
