# Wms Expert - Documentação de Views

Este repositório contém as definições detalhadas de views utilizadas no sistema **Wms Expert** para integração com ERPs.  

## 📄 Lista de Views

Clique no nome da view para ver os detalhes:

1. [EXPERT_CARGA](views/EXPERT_CARGA.md)  
2. [EXPERT_CLIENTE](views/EXPERT_CLIENTE.md)  
3. [EXPERT_EMBALAGEM](views/EXPERT_EMBALAGEM.md)  
4. [EXPERT_FORNECEDOR](views/EXPERT_FORNECEDOR.md)  
5. [EXPERT_GRUPO](views/EXPERT_GRUPO.md)  
6. [EXPERT_NOTA](views/EXPERT_NOTA.md)  
7. [EXPERT_NOTAITEM](views/EXPERT_NOTAITEM.md)  
8. [EXPERT_PEDIDO](views/EXPERT_PEDIDO.md)  
9. [EXPERT_PEDIDOSITEM](views/EXPERT_PEDIDOSITEM.md)  
10. [EXPERT_PRODUTO](views/EXPERT_PRODUTO.md)  

---

Acesse cada link acima para detalhes sobre a criação e funcionalidade de cada view.

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

