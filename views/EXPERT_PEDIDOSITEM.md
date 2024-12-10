# View EXPERT_PEDIDOSITEM

Definição da view responsável pelo gerenciamento dos itens dos Pedidos no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_PEDIDOSITEM ("ID", "CODIGOPEDIDO", "ITEMPEDIDO", "CODIGOFILIAL", "CODIGOPRODUTO", "QUANTIDADE", "QTDSEPARADA", "QTDCONFERIDA", "QTDCORTADA") AS 
  SELECT 
  ROWNUM AS id,
  CAST(PCPEDI.NUMPED AS varchar(30)) codigopedido,
  CAST(PCPEDI.NUMSEQ AS varchar(30)) itempedido,  
  CAST(pcpedc.CODFILIAL  AS varchar(30)) codigofilial,
  CAST(PCPEDI.CODPROD  AS varchar(30)) codigoproduto,
  CAST(PCPEDI.QT AS numeric(10,4)) quantidade,
  CAST(0 AS numeric(10,4)) qtdseparada,
  CAST(0 as numeric(10,4)) qtdconferida,
  CAST(0 as numeric(10,4)) qtdcortada
 FROM PCPEDI 
 JOIN PCPEDC ON PCPEDC.NUMPED = PCPEDI.NUMPED
 WHERE pcpedc.LOCALIZACAOPEDIDO is NULL
   -- AND pcpedc.DTEMISSAOMAPA IS NOT NULL
    AND pcpedc."DATA" >= (sysdate - 90)
    AND PCPEDC.CODCLI <> 3;
