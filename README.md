# Power BI Real Estate BPO Suite

**11 integrated dashboards for real estate SPE financial operations**

Author: Vitor Rodovalho

## Overview

This repository contains the extracted knowledge artifacts (DAX measures, Power Query / M code,
data model schemas, and relationship maps) from a production Power BI suite built for a
Brazilian real estate BPO (Business Process Outsourcing) operation.

The suite manages financial operations for multiple SPEs (Sociedades de Proposito Especifico --
special-purpose entities used in Brazilian real estate development). It covers the full cycle
from Controladoria (Financial Controlling) and Tesouraria (Treasury) through compliance, quality assurance, and governance.

**This is not runnable code.** The `.pbix` files are excluded by design. Instead, this repo
serves as a reference library of:

- DAX measure patterns for real estate finance
- Power Query (M) ETL patterns connecting to UAU-based ERP (SQL Server) and Azure Databricks
- Data model designs showing table schemas and relationships

## Tech Stack

- **Power BI** (Import and DirectQuery modes)
- **SQL Server** -- UAU-based ERP (primary data source)
- **Azure Databricks** -- advanced analytics layer
- **SharePoint** -- supplemental data sources
- **ERP integration layer** -- secondary ERP integration

## Dashboard Inventory

| # | Dashboard | DAX Measures | PQ Queries | Columns | Relationships | Complexity |
|---|-----------|:------------:|:----------:|:-------:|:-------------:|:----------:|
| 1 | BI Controladoria (Financial Controlling) | 594 | 131 | 679 | 73 | Complex |
| 2 | BI Tesouraria (Treasury) | 576 | 90 | 309 | 21 | Complex |
| 3 | BI DVQ | 370 | 118 | 454 | 43 | Complex |
| 4 | Painel de Qualidade (Quality Panel) | 204 | 229 | 925 | 87 | Complex |
| 5 | Mesa de Controle (Control Desk) | 159 | 422 | 1708 | 159 | Complex |
| 6 | Tesouraria (Ops) | 138 | 136 | 619 | 51 | Medium |
| 7 | Mesa de Controle Direto (Direct Control Desk) | 138 | 70 | 247 | 16 | Medium |
| 8 | Contabilidade (Accounting) | 21 | 198 | 728 | 63 | Medium |
| 9 | Declaracao de Faturamento (Billing Declaration) | 19 | 54 | 80 | 3 | Simple |
| 10 | Declaracao de Recebimento (Receipt Declaration) | 19 | 54 | 80 | 3 | Simple |
| 11 | Governanca (Governance) e Sistemas | 9 | 541 | 770 | 90 | Complex |
| | **Total** | **2,247** | **2,043** | **6,599** | **609** | |

## Repository Structure

```
powerbi-real-estate-bpo/
├── README.md                          # This file
├── LICENSE                            # MIT License
├── ANONYMIZATION_RULES.md             # Anonymization methodology and rules
├── .gitignore
├── docs/
│   ├── architecture.md                # System architecture and data flow
│   ├── business-case.md               # Industry context and value proposition
│   └── dashboard-catalog.md           # Detailed catalog of all 11 dashboards
├── dax/                               # DAX measures organized by dashboard
│   ├── controladoria/
│   ├── tesouraria/
│   ├── mesa-de-controle/
│   ├── qualidade/
│   ├── dvq/
│   ├── contabilidade/
│   ├── declaracoes/
│   │   ├── faturamento/
│   │   └── recebimento/
│   ├── governanca/
│   ├── tesouraria-ops/
│   └── mesa-de-controle-direto/
├── power-query/                       # Power Query (M) code per dashboard
│   ├── etl-patterns/
│   └── connections/
├── data-model/
│   ├── schema/                        # Table and column definitions (CSV)
│   └── relationships/                 # Relationship maps (CSV)
└── assets/
    └── screenshots/
```

## How to Use This Repo

1. **Browse DAX patterns**: Each `dax/<area>/measures.md` contains all DAX measures with
   their expressions, table names, and display folders.
2. **Study ETL**: The `power-query/` directory has the full M code for every query in each
   dashboard, showing connection patterns to SQL Server, Databricks, and SharePoint.
3. **Understand the data model**: CSV files in `data-model/` document every column (with types)
   and every relationship between tables.
4. **Read the docs**: `docs/` provides architecture context, business case, and a per-dashboard
   catalog with complexity ratings.

## Anonymization

All files have been sanitized to remove proprietary information. Internal IPs, cloud workspace
URLs, company names, tenant identifiers, and personal paths have been replaced with generic
placeholders. See [ANONYMIZATION_RULES.md](ANONYMIZATION_RULES.md) for the complete ruleset.

> **Note:** Original DAX and Power Query (M) code preserves Portuguese identifiers as-is from the source Power BI models.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
