# Architecture

## System Overview

```
                    DATA SOURCES                          POWER BI LAYER
               ┌──────────────────┐
               │   UAU ERP        │
               │   (SQL Server)   │──── DirectQuery ──────┐
               │   - SPE data     │                       │
               │   - Financials   │──── Import (scheduled)│
               │   - Operations   │                       │
               └──────────────────┘                       │
                                                          ▼
               ┌──────────────────┐              ┌──────────────────────┐
               │ Azure Databricks │              │                      │
               │ (Analytics Layer)│── Import ──► │   11 BPO Dashboards  │
               │ - SQL Warehouse  │              │                      │
               │ - Cross-SPE agg. │              │  ┌─ Controladoria    │
               └──────────────────┘              │  ├─ Tesouraria       │
                                                 │  ├─ DVQ              │
               ┌──────────────────┐              │  ├─ Qualidade        │
               │   SharePoint     │              │  ├─ Mesa de Controle │
               │ - Reference data │── Import ──► │  ├─ Tesouraria Ops   │
               │ - Config tables  │              │  ├─ Mesa Ctrl Direto │
               │ - Excel files    │              │  ├─ Contabilidade    │
               └──────────────────┘              │  ├─ Decl. Faturamento│
                                                 │  ├─ Decl. Recebimento│
               ┌──────────────────┐              │  └─ Governanca       │
               │ ERP Integration  │              │                      │
               │ Layer            │── via SQL ─► └──────────────────────┘
               └──────────────────┘
```

## Data Connection Modes

### DirectQuery
Used primarily in the Controladoria (Financial Controlling) and Tesouraria (Treasury) dashboards for real-time bank balance and
payment status data. DirectQuery connections target the ERP SQL Server directly.

### Import (Scheduled Refresh)
Most dashboards use Import mode with scheduled refreshes. This applies to:
- Databricks warehouse queries (analytics layer)
- SharePoint data sources (reference tables, Excel files)
- Historical and aggregated views

### Hybrid
Some dashboards combine both modes -- DirectQuery for operational data that must be current,
and Import for reference tables and historical data that can tolerate refresh latency.

## Master Template Pattern

The BPO suite follows a **master template with variants** design:

```
Master Template (shared foundation)
├── Core date dimension (dCalendario)
├── Shared DAX measure library (~140 common measures)
├── Standard color theme and formatting
│
├── Variant 1: BI Controladoria (594 DAX, full financial controlling)
├── Variant 2: BI Tesouraria (576 DAX, treasury-focused)
├── Variant 3: BI DVQ (370 DAX, compliance/DVQ)
├── ...
└── Variant 11: Governanca e Sistemas (9 DAX, 541 PQ, system governance)
```

Core measures (e.g., `SaldoGerencial`, `TotalPagamentos`, `% ENVIADOBC`) appear across multiple
dashboards. Domain-specific dashboards then add specialized measures on top.

## ETL Patterns

### Date Dimension
All dashboards share a common date dimension (`dCalendario` or similar) built in DAX or M,
with Brazilian fiscal calendar support.

### Currency Formatting
Brazilian Real (R$) formatting is applied consistently using DAX format strings. Measures
handling currency use `FORMAT(value, "R$ #,##0.00")` or locale-aware formatting.

### SPE Parameterization
Connections to the ERP are parameterized by SPE, allowing the same dashboard to serve
multiple entities by switching the connection parameter.

### Databricks Integration
Newer dashboards query an Azure Databricks SQL Warehouse for cross-SPE aggregation and
analytics that would be too expensive to run against the operational database directly.

### SharePoint Integration
Reference data (mapping tables, configuration, exception lists) is stored in SharePoint
and loaded via Power Query's SharePoint connector. This includes Excel files and
SharePoint lists used as lookup tables.

## Data Model Characteristics

| Dashboard | Tables (implied by columns) | Relationships | Star Schema |
|-----------|:---------------------------:|:-------------:|:-----------:|
| BI Controladoria | ~50+ | 73 | Partial |
| BI Tesouraria | ~30+ | 21 | Partial |
| BI DVQ | ~40+ | 43 | Partial |
| Painel de Qualidade | ~70+ | 87 | Yes |
| Mesa de Controle | ~100+ | 159 | Yes |
| Tesouraria (Ops) | ~40+ | 51 | Partial |
| Mesa Controle Direto | ~20+ | 16 | Yes |
| Contabilidade | ~50+ | 63 | Partial |
| Decl. Faturamento | ~10 | 3 | Simple |
| Decl. Recebimento | ~10 | 3 | Simple |
| Governanca | ~60+ | 90 | Yes |

Most models follow a partial star schema with fact tables connected to shared dimensions
(date, SPE, accounts). The larger dashboards (Mesa de Controle, Qualidade) have the most
complex models with cross-filtering and bidirectional relationships.
