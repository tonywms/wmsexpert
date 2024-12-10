# Retorno de Movimentos

Os retornos de movimentos no Wms Expert são fundamentais para garantir a sincronia com o ERP, evitando ações manuais. Eles estão divididos em três tipos:  
- **Retorno após a importação**  
- **Retorno após a exclusão**  
- **Retorno após a finalização do processo**  

---

## Retorno após a Importação de Movimentos

### Descrição
Após importar um movimento, o Wms notifica o ERP que o movimento foi recebido. Isso é feito via **stored procedure**, que valida o movimento e remove-o da view correspondente.

#### Movimentos de Entrada
```sql
CREATE procedure [dbo].[sp_RetornoImpEntrada] 
@codFiliaErp varchar(20), @codNotaFiscalErp varchar(20), 
@codFornecedorErp varchar(20), @serie int as

begin
  update NOTAFISCALENTRADA SET WMS = 1 
  WHERE 
    codFilialERP = @codFiliaErp and 
    codNotaFiscalErp = @codNotaFiscalErp and 
    codFornecedorErp = @codFornecedorErp and
    serie = @serie
end
