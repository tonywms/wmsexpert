# View EXPERT_GRUPO

Definição da view responsável pelo gerenciamento de Grupos no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_GRUPO ("CODIGO", "NOME", "ATIVO") AS 
  SELECT
   CAST (pcdepto.codepto AS VARCHAR(255)) codigo,
   pcdepto.descricao nome,
   1 ativo
  from pcdepto
  ;
