Retorno de Movimentos
Os retornos de movimentos são divididos em três categorias principais, cada uma garantindo a sincronização entre o WMS e o ERP, evitando ações manuais e mantendo o fluxo automatizado:

Retorno após a importação de movimentos
Retorno após a exclusão de movimentos
Retorno após a finalização de movimentos
1️⃣ Retorno após a Importação de Movimentos
O WMS notifica o ERP que um movimento foi recebido e importado, removendo-o das views para evitar duplicações. As procedures utilizadas para este retorno são:

Entrada

CREATE PROCEDURE [dbo].[sp_RetornoImpEntrada] 
  @codFiliaErp VARCHAR(20), 
  @codNotaFiscalErp VARCHAR(20), 
  @codFornecedorErp VARCHAR(20), 
  @serie INT
AS
BEGIN
  UPDATE NOTAFISCALENTRADA 
  SET WMS = 1 
  WHERE codFilialERP = @codFiliaErp 
    AND codNotaFiscalErp = @codNotaFiscalErp 
    AND codFornecedorErp = @codFornecedorErp 
    AND serie = @serie;
END;

Saída

CREATE PROCEDURE [dbo].[sp_RetornoImpPedido] 
  @codFiliaErp VARCHAR(20), 
  @codPedidoErp VARCHAR(20)
AS
BEGIN
  UPDATE PEDIDO 
  SET WMS = 1 
  WHERE codFilialERP = @codFiliaErp 
    AND codPedidoErp = @codPedidoErp;
END;
