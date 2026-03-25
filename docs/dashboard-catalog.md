# Dashboard Catalog

Detailed catalog of all 11 BPO dashboards in the suite.

---

## 1. BI Controladoria (Financial Controlling)

**Purpose**: The primary financial controlling dashboard, providing a consolidated view of bank
balances, payables, receivables, and payment processing across all SPEs. This is the most
measure-rich dashboard in the suite, serving as the central hub for the Controladoria (Financial Controlling) team.

**Key DAX Measures**:
- `SaldoGerencial` -- Current management bank balance using LASTNONBLANK over account dates
- `Contas a Pagar` -- Accounts payable filtered by bank code thresholds
- `TotalPagamentos` -- Total payments processed with multi-filter context
- `Cotacao` -- Currency quotation tracking
- `ProcessoPagamento` -- Payment process status tracking

**Data Sources**: UAU-based ERP (SQL Server), SharePoint reference tables

**Complexity**: Complex (594 DAX measures, 131 PQ queries, 73 relationships)

---

## 2. BI Tesouraria (Treasury)

**Purpose**: Treasury management dashboard focused on payment operations, cash flow monitoring,
and bank reconciliation. Shares a common measure base with Controladoria (Financial Controlling) but emphasizes
treasury-specific workflows like rapid purchases and linked processes.

**Key DAX Measures**:
- `SaldoGerencial` / `SaldoGerencialHistorico` -- Balance tracking with historical view
- `TotalPagamentos` -- Payment totals across SPEs
- `CompraRapida` -- Rapid purchase tracking
- `ProcessoVinculado` -- Linked process monitoring

**Data Sources**: UAU-based ERP (SQL Server), SharePoint

**Complexity**: Complex (576 DAX measures, 90 PQ queries, 21 relationships)

---

## 3. BI DVQ

**Purpose**: DVQ (Document Verification and Quality) dashboard tracking real estate unit
inventory, sales status, and settlement across SPE portfolios. Monitors units from stock
through sale, payment, and settlement.

**Key DAX Measures**:
- `Unidades Estoque` -- Units in inventory
- `Unidades Vendidas` / `Unidades Ativas` / `Unidades Quitadas` -- Sales pipeline tracking
- `Fora de Venda` -- Units removed from sale
- `SaldoGerencial` -- Shared balance measure for financial context

**Data Sources**: UAU-based ERP (SQL Server), SharePoint

**Complexity**: Complex (370 DAX measures, 118 PQ queries, 43 relationships)

---

## 4. Painel de Qualidade (Quality Panel)

**Purpose**: Quality assurance dashboard for BPO operations, tracking SLA compliance across
invoice issuance, bank submission, payment processing, and approval workflows. Used by
team heads to monitor operational quality by typology.

**Key DAX Measures**:
- `% ENVIADOBC` -- Percentage sent to bank for collection
- `% PAGO` -- Payment completion rate
- `% EMISSAOAPRV` / `% EMISSAONAPRV` -- Approved vs. non-approved issuance rates
- `EMISSAOAPRV` / `EMISSAONAPRV` -- Absolute issuance counts

**Data Sources**: UAU-based ERP (SQL Server), SharePoint, Azure Databricks

**Complexity**: Complex (204 DAX measures, 229 PQ queries, 87 relationships)

---

## 5. Mesa de Controle (Control Desk)

**Purpose**: The operational control desk dashboard, providing the most granular view of BPO
task execution. With 422 Power Query transformations and 159 relationships, this is the most
data-intensive dashboard in the suite, pulling from the widest variety of sources.

**Key DAX Measures**:
- `% ENVIADOBC` -- Bank submission tracking
- `% PAGO` -- Payment completion metrics
- `EMISSAOAPRV` -- Approved issuance tracking
- Quality SLA measures shared with Painel de Qualidade

**Data Sources**: UAU-based ERP (SQL Server), ERP integration layer, SharePoint, Azure Databricks

**Complexity**: Complex (159 DAX measures, 422 PQ queries, 159 relationships)

---

## 6. Tesouraria (Ops)

**Purpose**: Operational treasury dashboard, distinct from BI Tesouraria (#2). While BI
Tesouraria provides analytical views, this dashboard focuses on day-to-day treasury operations
including bank submission tracking, payment status, and issuance workflows.

**Key DAX Measures**:
- `% ENVIADOBC` -- Bank submission percentage
- `% PAGO` -- Payment completion tracking
- `EMISSAOAPRV` / `EMISSAONAPRV` -- Issuance approval tracking
- `ENVIADOBC` -- Absolute bank submission count

**Data Sources**: UAU-based ERP (SQL Server), SharePoint

**Complexity**: Medium (138 DAX measures, 136 PQ queries, 51 relationships)

---

## 7. Mesa de Controle Direto (Direct Control Desk)

**Purpose**: Direct control desk for operations managed through the ERP integration layer.
A streamlined variant of Mesa de Controle (Control Desk) (#5), focused specifically on transactions that
flow through both the primary and secondary ERP systems.

**Key DAX Measures**:
- `% ENVIADOBC` -- Bank submission tracking
- `% PAGO` -- Payment completion
- `EMISSAOAPRV` / `EMISSAONAPRV` -- Issuance tracking
- Shared quality control measures

**Data Sources**: UAU-based ERP (SQL Server), ERP integration layer

**Complexity**: Medium (138 DAX measures, 70 PQ queries, 16 relationships)

---

## 8. Contabilidade (Accounting)

**Purpose**: Accounting dashboard focused on closing balances, invoice discrepancies, and
financial reconciliation. Tracks balance amounts to be discounted, payments without invoices,
and month-over-month closing comparisons.

**Key DAX Measures**:
- `SaldoDescontar` -- Balance to be discounted
- `SaldoPgtoSemNf` -- Payments without invoices (discrepancy detection)
- `SaltoTotal` -- Total balance aggregation
- `BalancFech(M-1)` / `BalancFech(M-2)` -- Closing balance comparisons with prior months
- `% BalancFech` -- Closing balance percentage variation

**Data Sources**: UAU-based ERP (SQL Server), SharePoint

**Complexity**: Medium (21 DAX measures, 198 PQ queries, 63 relationships)

---

## 9. Declaracao de Faturamento (Billing Declaration)

**Purpose**: Billing declaration dashboard supporting the generation and tracking of SPE
billing statements. Tracks total billed amounts, processing status, and completion rates
with a top-5 analysis view.

**Key DAX Measures**:
- `1_Total Faturado` -- Total billed amount
- `2_Concluidos` -- Completed declarations
- `3_Pericia` -- Under review / expert analysis
- `4_Processamento` -- In processing
- `6_Part%%` -- Participation percentage

**Data Sources**: UAU-based ERP (SQL Server)

**Complexity**: Simple (19 DAX measures, 54 PQ queries, 3 relationships)

---

## 10. Declaracao de Recebimento (Receipt Declaration)

**Purpose**: Receipt declaration dashboard, the counterpart to Faturamento (#9). Tracks
received amounts, processing status, and completion rates. Shares the same data model
structure as the Faturamento dashboard.

**Key DAX Measures**:
- `1_Total Faturado` -- Total received/billed amount
- `2_Concluidos` -- Completed declarations
- `3_Pericia` -- Under review
- `4_Processamento` -- In processing
- `9_TOP5%` -- Top 5 analysis by percentage

**Data Sources**: UAU-based ERP (SQL Server)

**Complexity**: Simple (19 DAX measures, 54 PQ queries, 3 relationships)

---

## 11. Governanca e Sistemas (Governance and Systems)

**Purpose**: System governance dashboard auditing user access, program permissions, and group
assignments across the ERP ecosystem. Despite having only 9 DAX measures, it has the highest
Power Query count (541) in the suite, reflecting the large number of system tables being
inventoried.

**Key DAX Measures**:
- `contagem programas totais` -- Total program count across systems
- `contagem programa sensivel` -- Sensitive program count (security audit)
- `ProgUser` -- Programs per user
- `ProgGrupo` -- Programs per group
- `TotalCap` -- Total capability/capacity measure

**Data Sources**: UAU-based ERP (SQL Server), ERP integration layer, system metadata tables

**Complexity**: Complex (9 DAX measures, 541 PQ queries, 90 relationships)

---

## Summary Matrix

| Dashboard | Primary Focus | DAX | PQ | Complexity |
|-----------|--------------|:---:|:--:|:----------:|
| BI Controladoria (Financial Controlling) | Financial controlling, balances | 594 | 131 | Complex |
| BI Tesouraria (Treasury) | Treasury analytics | 576 | 90 | Complex |
| BI DVQ | Unit inventory, sales pipeline | 370 | 118 | Complex |
| Painel de Qualidade | SLA quality metrics | 204 | 229 | Complex |
| Mesa de Controle | Operational control desk | 159 | 422 | Complex |
| Tesouraria (Ops) | Daily treasury operations | 138 | 136 | Medium |
| Mesa Controle Direto (Direct Control Desk) | ERP direct ops | 138 | 70 | Medium |
| Contabilidade (Accounting) | Accounting, reconciliation | 21 | 198 | Medium |
| Decl. Faturamento | Billing declarations | 19 | 54 | Simple |
| Decl. Recebimento | Receipt declarations | 19 | 54 | Simple |
| Governanca (Governance) | System access governance | 9 | 541 | Complex |
