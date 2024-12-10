# View EXPERT_NOTAITEM

Definição da view responsável pelo gerenciamento dos itens das Notas Fiscais no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_NOTAITEM ("ID", "CODIGONOTA", "ITEM", "CODIGOPRODUTO", "CODIGOFILIAL", "TIPO", "CODIGOFORNECEDOR", "QUANTIDADE", "VALUNITARIO", "VALIDADE", "FABRICACAO", "LOTE", "NUMSERIE", "EMBALAGEM") AS 
  select DISTINCT
  ROWNUM AS id,
  CAST(pcmov.numnota AS varchar(30)) codigonota,
  pcmov.SEQMOV item,
  CAST(pcmov.CODPROD AS varchar(30)) codigoproduto,
  CAST(pcnfent.CODFILIAL AS varchar(30)) codigofilial,
  case when pcmov.codoper = 'ED' then 2
    	 WHEN pcmov.CODOPER = 'ET' THEN 3
    else 1 
  end as tipo,
  CAST(case when pcmov.codoper = 'ED' then to_number('900'||to_char(pcnfent.CODFORNEC))
       else pcnfent.CODFORNEC
  END AS varchar(30)) codigofornecedor,
  CAST(sum(pcmov.qt) AS numeric(10,4)) quantidade,
  CAST(coalesce(pcmov.valorultent,0) AS numeric(10,4)) valunitario,
  pcmov.DATAVALIDADE validade,
  pcmov.DATAFABRICACAO fabricacao,
  pcmov.NUMLOTE lote,
  NULL numserie,
  NULL embalagem
  from pcmov
  Join pcnfent on pcmov.numtransent=pcnfent.numtransent and pcmov.numnota=pcnfent.NUMNOTA
  where ((pcmov.codoper='E') or (pcmov.codoper='EB') or (pcmov.codoper='ET') or (pcmov.codoper='EF') or (pcmov.codoper='ED'))
    and (pcnfent.especie <> 'OE')  and pcnfent.dtent >= to_date('01/10/2024','dd/mm/yyyy')
  GROUP BY ROWNUM , pcmov.SEQMOV, pcmov.numnota, pcnfent.CODFILIAL,  pcnfent.CODFORNEC, pcmov.CODPROD, pcmov.valorultent,
  pcmov.DATAVALIDADE, pcmov.DATAFABRICACAO, pcmov.NUMLOTE, pcmov.codoper
