# View EXPERT_EMBALAGEM

Definição da view responsável pelo gerenciamento dos clientes no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_EMBALAGEM ("ID", "CODIGO", "CODIGOPRODUTO", "CODBARRA", "QUANTIDADE", "ATIVO", "TIPO", "LARGURA", "ALTURA", "PROFUNDIDADE", "M3", "PESOBRUTO", "PESOLIQUIDO")
AS SELECT 
  DISTINCT "ID", "CODIGO", "CODIGOPRODUTO", "CODBARRA", "QUANTIDADE", "ATIVO", "TIPO", "LARGURA", "ALTURA", "PROFUNDIDADE", "M3", "PESOBRUTO", "PESOLIQUIDO" 
FROM 
  (
    SELECT 
      DISTINCT ROWNUM AS id, 
      null AS codigo, 
      CAST(pcembalagem.CODPROD AS varchar(30)) AS codigoproduto, 
      CAST(codauxiliar AS varchar(20)) AS codbarra, 
      CAST(qtunit AS numeric(10, 4)) AS quantidade, 
      1 AS ativo, 
      CASE WHEN qtunit = 1 THEN 1 ELSE 2 END AS tipo, 
      CAST(pcembalagem.LARGURA AS numeric(10, 4)) AS largura, 
      CAST(pcembalagem.ALTURA AS numeric(10, 4)) AS altura, 
      CAST(pcembalagem.COMPRIMENTO AS numeric(10, 4)) AS profundidade, 
      CAST((pcembalagem.LARGURA * pcembalagem.ALTURA * pcembalagem.COMPRIMENTO) AS numeric(10, 4)) AS m3, 
      CAST(pcembalagem.PESOBRUTO AS numeric(10, 4)) AS pesobruto, 
      CAST(pcembalagem.PESOLIQ AS numeric(10, 4)) AS pesoliquido 
    FROM 
      pcembalagem 
    WHERE 
      codauxiliar IS NOT null
  );

