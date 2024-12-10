# View EXPERT_PRODUTO

Definição da view responsável pelo gerenciamento dos Produtos no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_PRODUTO ("CODIGO", "CODIGOREF", "NOME", "UNIDADEPADRAO", "CODIGOGRUPO", "CODIGOFORNECEDOR", "ESTOQUEMINIMO", "ESTOQUEMAXIMO", "CONTROLAVALIDADE", "CONTROLALOTE", "CONTROLANUMSERIE", "PESOBRUTO", "PESOLIQUIDO", "SHELFLIFE", "LASTRO", "ALTURA", "QTDCX", "QTDPL", "CHECKOUT", "SEPCX", "SEPPL") AS 
  SELECT
    CAST (pcprodut.codprod AS VARCHAR(255)) codigo, 
    CAST (pcprodut.codprod AS VARCHAR(255)) codigoref,
    (pcprodut.descricao || ' ' || pcmarca.marca) nome,
    NULL unidadepadrao,
    CAST (pcprodut.codepto AS VARCHAR(255)) codigogrupo,
    CAST (pcprodut.CODFORNEC AS VARCHAR(255)) codigofornecedor,
    NULL estoqueminimo,
    NULL estoquemaximo,
    CASE WHEN COALESCE(PCPRODUT.ESTOQUEPORDTVALIDADE,'N') = 'N' THEN 0 ELSE 1 END controlavalidade,
    CASE WHEN COALESCE(PCPRODUT.ESTOQUEPORLOTE ,'N') = 'N' THEN 0 ELSE 1 END controlalote,
    0 controlanumserie,
    pcprodut.PESOBRUTO  pesobruto,
    pcprodut.PESOLIQ  pesoliquido,
    pcprodut.NUMDIASVALIDADEMIN shelflife,
    pcprodut.LASTROPAL lastro,
    pcprodut.ALTURAPAL altura,
    pcprodut.QTUNITCX qtdcx,
    pcprodut.QTTOTPAL qtdpl,
    0 checkout,
    0 sepcx,
    0 seppl
  FROM pcprodut 
  left join pcmarca on pcmarca.codmarca = pcprodut.codmarca
