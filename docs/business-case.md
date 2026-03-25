# Business Case

## Industry Context

The Brazilian real estate development industry operates through **incorporadoras** (real estate developers) that create individual **SPEs** (Sociedades de Proposito Especifico -- special-purpose
entities) for each project. These SPEs are legally independent entities requiring full financial
management: accounting, treasury, tax compliance, and reporting.

**BPO (Business Process Outsourcing)** providers manage the financial back-office for dozens or
hundreds of SPEs simultaneously, demanding scalable, standardized processes and real-time
visibility across all entities.

## Problem Statement

Each SPE needs centralized financial visibility across multiple operational areas:

- **Controladoria (Financial Controlling)**: bank balances, payables, receivables, budget tracking
- **Tesouraria (Treasury)**: payment processing, cash flow, bank reconciliation
- **Compliance**: quality metrics, SLA tracking, audit trails
- **Contabilidade (Accounting)**: closing balances, invoice validation, discrepancy detection
- **Governance**: user access management, system permissions, program tracking

Without centralized dashboards, BPO teams rely on manual ERP queries across hundreds of SPEs,
leading to slow reporting, inconsistent metrics, and missed SLAs.

## Solution

A suite of **11 Power BI dashboards** connected to the **UAU-based ERP** via SQL Server,
with an **Azure Databricks** layer for advanced analytics on newer dashboards.

The dashboards follow a **master template with 9 variants** pattern -- a core data model and
measure library is shared, with domain-specific dashboards extending or filtering as needed.

## Value Delivered

- **Consolidated BPO operations** across all SPEs in a single pane of glass
- **Real-time visibility** into Controladoria (Financial Controlling), Tesouraria (Treasury), and compliance metrics
- **Quality management** with automated SLA tracking and exception flagging
- **Governance control** with user/program access auditing across systems
- **Standardized reporting** reducing manual effort and human error

## Tech Stack

| Component | Technology | Role |
|-----------|-----------|------|
| Primary data source | SQL Server (UAU-based ERP) | Operational data for all SPEs |
| Analytics layer | Azure Databricks | Advanced queries, cross-SPE aggregation |
| Supplemental data | SharePoint | Reference tables, configuration files |
| Visualization | Power BI | Import and DirectQuery modes |
| Direct integrations | ERP integration layer | Extended ERP functionality |

## Scale

- **2,247** DAX measures across all dashboards
- **2,043** Power Query (M) transformations
- **6,599** data model columns
- **609** inter-table relationships
- Multiple SPEs managed simultaneously through parameterized connections
