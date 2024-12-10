# View EXPERT_CARGA

Definição da view responsável pelo gerenciamento de cargas no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_CARGA (
  "CODIGOCARGA", 
  "CODIGOFILIAL", 
  "DATAINICIOCONF", 
  "DATAFIMCONF", 
  "DATAEXPORTACAOERP", 
  "QTDVOLUMES"
) AS 
  SELECT 
    CAST(PCBONUSC.NUMBONUS AS VARCHAR(20)) codigocarga,
    CAST(PCBONUSC.CODFILIAL AS VARCHAR(20)) codigofilial,
    CAST (NULL AS TIMESTAMP) datainicioconf,
    CAST (NULL AS TIMESTAMP) datafimconf,
    CAST (NULL AS TIMESTAMP) dataexportacaoerp,
    CAST(0 AS integer) qtdvolumes
  FROM PCBONUSC  
  WHERE pcbonusc.DATABONUS >= TO_DATE('01/10/2024', 'dd/mm/yyyy');
