# View EXPERT_NOTA

Definição da view responsável pelo gerenciamento de Notas Fiscais no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_NOTA ("ID", "CODIGO", "CODFILIAL", "TIPO", "CARGA", "DATAEMISSAO", "QUANTIDADE", "NUMERONOTAFISCAL", "SERIE", "QUANTIDADEVOLUME", "VALTOTALPRODUTO", "VALTOTALNOTA", "PESOBRUTO", "PESOLIQUIDO", "SITUACAO", "QTDVOLUMECONF", "CODIGOFORNECEDOR") AS 
  select 
  	distinct 
  	CAST (pcnfent.NUMNOTA AS VARCHAR(30)) || CAST(pcnfent.CODFILIAL AS VARCHAR(30))
  	|| CAST (case when pcmov.codoper = 'ED' then to_number('900'||to_char(pcnfent.CODFORNEC))
    else pcnfent.CODFORNEC
    END AS VARCHAR(30)) || pcnfent.SERIE AS Id,
    CAST (pcnfent.NUMNOTA AS VARCHAR(30)) codigo,
    CAST(pcnfent.CODFILIAL AS VARCHAR(30)) codfilial,
    case when pcmov.codoper = 'ED' then 2
    	 WHEN pcmov.CODOPER = 'ET' THEN 3
    else 1 
    end as tipo,
    CAST(pcnfent.NUMBONUS AS varchar(20)) carga,
    pcnfent.dtent dataemissao,
    CAST (0 AS numeric(10,2)) quantidade,
    CAST (pcnfent.NUMNOTA AS VARCHAR(30)) numeronotafiscal,
    pcnfent.SERIE serie,
    pcnfent.NUMVOL quantidadevolume,
    pcnfent.VLTOTAL valtotalproduto,
    pcnfent.VLTOTAL valtotalnota,
    pcnfent.TOTPESO pesobruto,
    pcnfent.TOTPESOLIQ pesoliquido,
    1 situacao,
    CAST (0 AS numeric(10,2)) qtdvolumeconf,    
    CAST (case when pcmov.codoper = 'ED' then to_number('900'||to_char(pcnfent.CODFORNEC))
    else pcnfent.CODFORNEC
    END AS VARCHAR(30)) codigofornecedor  
  from pcnfent
  Join pcmov on pcmov.numtransent=pcnfent.numtransent and pcmov.numnota=pcnfent.NUMNOTA
  where ((pcmov.codoper='E') or (pcmov.codoper='EB') or (pcmov.codoper='ET')  or (pcmov.codoper='EF') or (pcmov.codoper='ED'))    and (pcnfent.especie <> 'OE')
  and pcnfent.dtent >= to_date('01/10/2024','dd/mm/yyyy') ;
