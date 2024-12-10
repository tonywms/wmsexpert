# View EXPERT_CLIENTE

Definição da view responsável pelo gerenciamento dos clientes no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_CLIENTE ("CODIGO", "CPFCNPJ", "NOME", "CODCIDADE", "NOMECIDADE", "ENDERECO", "COMPLEMENTO", "NUMERO", "BAIRRO", "CEP", "TELEFONE", "EMAIL", "ATIVO", "LATITUDE", "LONGETUDE", "SHELFLIFE", "CODROTA", "NOMEROTA") AS 
  SELECT
    CAST(pcclient.codcli AS VARCHAR(255)) codigo,
    pcclient.cgcent cpfcnpj,
    pcclient.cliente nome,
    pcclient.codmunicipio codcidade,
    PCCIDADE.NOMECIDADE nomecidade,
    pcclient.enderent endereco,
    pcclient.complementoent complemento,
    pcclient.NUMEROENT numero,
    pcclient.bairroent bairro,
    pcclient.cepent cep,
    pcclient.TELCOB telefone,
    pcclient.EMAIL email,
    1 ativo,
    NULL latitude,
    NULL longetude,
    pcclient.QTDIASAVENCERPRODUTO shelflife ,
    PCROTAEXP.codrota as CodRota,
    PCROTAEXP.descricao as NomeRota
  FROM pcclient
  left join pcpraca on pcpraca.codpraca = pcclient.codpraca
  left join PCROTAEXP on PCROTAEXP.codrota = pcpraca.rota
  LEFT JOIN PCCIDADE ON pcclient.CODCIDADE = PCCIDADE.CODCIDADE
  where pcclient.dtexclusao is null![image](https://github.com/user-attachments/assets/fed6a84b-4e1f-4d64-894b-0210e52fb193)
