Definição da view responsável pelo gerenciamento dos -- no sistema.  

## Código SQL

```sql
CREATE VIEW EXPERT_FORNECEDOR ("CODIGO", "NOME", "NOMEFANTASIA", "CPF", "IE", "ESTADO", "CODCIDADE", "BAIRRO", "ENDERECO", "NUMERO", "TELEFONE") AS 
  SELECT
   CAST (pcfornec.codfornec AS VARCHAR(255)) codigo,
   pcfornec.fornecedor nome,
   pcfornec.fantasia nomefantasia,
   pcfornec.cgc cpf,
   pcfornec.IE ie,
   pcfornec.estado estado,
   NULL codcidade,
   pcfornec.bairro bairro,
   pcfornec.ender endereco,
   null numero,
   NULL telefone
  from pcfornec
  WHERE pcfornec.dtexclusao IS NULL
UNION
SELECT
    CAST (to_number('900' || to_char(pcclient.codcli)) AS varchar(255))codigo,
    pcclient.cliente nome,
    pcclient.FANTASIA nomefantasia,
    pcclient.cgcent cpf,
    pcclient.IEENT ie ,
    pccidade.UF estado,
    pcclient.codmunicipio codcidade,
    pcclient.bairroent bairro,
    pcclient.enderent endereco,
    pcclient.NUMEROENT numero,
    pcclient.TELCOB telefone
  FROM pcclient
  left join pcpraca on pcpraca.codpraca = pcclient.codpraca
  left join PCROTAEXP on PCROTAEXP.codrota = pcpraca.rota
  LEFT JOIN PCCIDADE ON pcclient.CODCIDADE = PCCIDADE.CODCIDADE
  where pcclient.dtexclusao is null![image](https://github.com/user-attachments/assets/37ab4054-fbc6-431b-b259-7cc6843cef16)


1. **CODIGO** - VARCHAR2(255)
2. **NOME** - VARCHAR2(60)
3. **NOMEFANTASIA** - VARCHAR2(60)
4. **CPF** - VARCHAR2(18)
5. **IE** - VARCHAR2(15)
6. **ESTADO** - VARCHAR2(2)
7. **CODCIDADE** - NUMBER
8. **BAIRRO** - VARCHAR2(40)
9. **ENDERECO** - VARCHAR2(40)
10. **NUMERO** - VARCHAR2(6)
11. **TELEFONE** - VARCHAR2(13)![image](https://github.com/user-attachments/assets/d55e590f-f997-4518-af58-b778f0490aff)

