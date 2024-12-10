# Retorno de Movimentos no Wms Expert

O sistema **Wms Expert** utiliza retornos de movimentos para garantir a integração perfeita com o ERP, dividindo-os em três categorias:

1. **Retorno após a importação**  
2. **Retorno após a exclusão**  
3. **Retorno após a finalização**

Cada categoria é implementada através de stored procedures específicas, que asseguram a sincronização de dados sem necessidade de intervenções manuais no ERP.

---

## 📝 Detalhes dos Retornos

### 1️⃣ Retorno Após a Importação

**Objetivo:** Informar ao ERP que o movimento foi recebido com sucesso.  
Após a execução correta, o movimento é removido das views correspondentes.  

#### Exemplo: Importação de Entrada

Stored Procedure:  
```sql
CREATE procedure [dbo].[sp_RetornoImpEntrada] 
@codFiliaErp varchar(20), @codNotaFiscalErp varchar(20), @codFornecedorErp varchar(20), @serie int as

begin
  update NOTAFISCALENTRADA SET WMS = 1 
  WHERE 
    codFilialERP = @codFiliaErp and 
    codNotaFiscalErp = @codNotaFiscalErp and 
    codFornecedorErp = @codFornecedorErp and
    serie = @serie
end
