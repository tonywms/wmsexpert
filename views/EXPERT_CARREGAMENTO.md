# View EXPERT_CARREGAMENTO

Definição da view responsável pelo gerenciamento de Carregamento no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_CARREGAMENTO AS 
SELECT
    CODIGO,
    MOTORISTA,
    AJUDANTE1,
    AJUDANTE2,
    AJUDANTE3,
    DATAGERACAO,
    DATASAIDA,
    DATACHEGADA,
    DESTINO,
    KMINICIAL,
    KMFINAL,
    CODFILIAL,
    CODIGOPEDIDO
FROM CARREGAMENTO;
```
**CODIGO** : *O campo deve ser **VARCHAR(255)**, o mesmo e a chave primaria.****<font color="red"> - obrigartorio</font>***<br/>
**MOTORISTA** : *O campo deve ser **VARCHAR(100)**, contendo o nome do motorista.*<br/>
**AJUDANTE1** : *O campo deve ser **VARCHAR(100)**, contendo o nome do ajudante.*<br/>
**AJUDANTE2** : *O campo deve ser **VARCHAR(100)**, contendo o nome do ajudante.*<br/>
**AJUDANTE3** : *O campo deve ser **VARCHAR(100)**, contendo o nome do ajudante.*<br/>
**DATAGERACAO** : *O campo deve ser **DATE**, trazendo a data de geração do carregamento.****<font color="red"> - obrigartorio</font>***<br/>
**DATASAIDA** : *O campo deve ser **DATE**, trazendo a data de saida do carregamento.*<br/>
**DATACHEGADA** : *O campo deve ser **DATE**, trazendo a data de chegada do carregamento.*<br/>
**DESTINO** : *O campo deve ser **VARHCAR(20)**, trazendo o destino do carregamento.*<br/>
**KMINICIAL** : *O campo deve ser **VARHCAR(10)**, trazendo o destino do carregamento.*<br/>
**KMFIM** : *O campo deve ser **VARHCAR(10)**, trazendo o destino do carregamento.* <br/> 
**CODFILIAL** : *O campo deve ser **VARHCAR(30)**, trazendo o destino do carregamento.****<font color="red"> - obrigartorio</font>***<br/>
**CODIGOPEDIDO** : *O campo deve ser **VARHCAR(30)**, trazendo o destino do carregamento.****<font color="red"> - obrigartorio</font>***<br/>
