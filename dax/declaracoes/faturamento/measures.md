| TableName   | Name             | Expression                                                                                           |   DisplayFolder |   Description |
|:------------|:-----------------|:-----------------------------------------------------------------------------------------------------|----------------:|--------------:|
| Medidas     | 1_Total Faturado | SUM(bpo_auditoria_contabil_faturamento[valorfaturamento]) + 0                                        |             nan |           nan |
| Medidas     | 5_Tipo de Bolsa  | DISTINCTCOUNT(fPapers[COD_BOLSA])                                                                    |             nan |           nan |
| Medidas     | 4_Processamento  | [1_Total Faturado] - [2_Concluídos]-[3_Perícia]                                                      |             nan |           nan |
| Medidas     | 3_Perícia        | bpo_auditoria_contabil_faturamento[is_accounting_closed] in ( TRUE() )                               |             nan |           nan |
| Medidas     | 2_Concluídos     | CALCULATE([1_Total de Processos],fPapers[STATUS]="Concluído")                                        |             nan |           nan |
| Medidas     | 6_Part%%         | DIVIDE([2_Concluídos],[1_Total Faturado],0)                                                          |             nan |           nan |
| Medidas     | 9_TOP5%          | VAR  TOPtres = CALCULATE([1_Total de Processos],TOPN(3,ALL(fPapers[Local]),[1_Total de Processos]))  |             nan |           nan |
|             |                  | VAR TOTal = CALCULATE([1_Total de Processos],ALL())                                                  |                 |               |
|             |                  | RETURN                                                                                               |                 |               |
|             |                  | DIVIDE(TOPtres,TOTal,0)                                                                              |                 |               |
| Medidas     | TOP5             | CALCULATE([1_Total de Processos],TOPN(5,VALUES(fPapers[Local]),[1_Total de Processos],DESC))         |             nan |           nan |
| Medidas     | 7_Qtde Trava     | CALCULATE([1_Total Faturado],ALL())                                                                  |             nan |           nan |
| Medidas     | 8_TOP            | CALCULATE([1_Total de Processos],TOPN(3,ALL(fPapers[Local]),[1_Total de Processos]))                 |             nan |           nan |
| Medidas     | 10_Cirlulo       | UNICHAR(11036)                                                                                       |             nan |           nan |
| Medidas     | today            | TODAY()                                                                                              |             nan |           nan |