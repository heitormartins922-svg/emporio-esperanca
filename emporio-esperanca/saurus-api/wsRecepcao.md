# wsRecepcao — Envio de Vendas

**Endpoint:** `http://wsrecepcao.saurus.net.br/v001/serviceRecepcao.asmx`
**Protocolo:** SOAP 1.1/1.2

> Relevância para TheADM: **nenhuma**. Este serviço envia dados *para* o caixa, não lê de lá.
> Seria útil apenas se quiséssemos criar vendas pelo TheADM e empurrar para o caixa físico.

---

## Método principal: envArqIntegracao

Responsável por envio e alteração de vendas, movimentações de caixa e transações TEF.

### Parâmetros

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `xBytesParametros` | base64Binary | XML comprimido em GZip com os dados da venda |
| `xSenha` | string | Senha criptografada fornecida pela Saurus |

### Exemplo de XML interno

```xml
<xmlIntegracao>
    <Dominio>XXXXXX</Dominio>
    <IdLoja>1</IdLoja>
    <IdCaixa>1</IdCaixa>
    <NumCaixa>1</NumCaixa>
    <IdReg>UUID-DA-VENDA</IdReg>
    <ChaveTerminal>UUID-DO-TERMINAL</ChaveTerminal>
    <TpLanc>0</TpLanc>
    <TpArqXml>20</TpArqXml>
</xmlIntegracao>
```

### Resposta

| Campo | Valores | Significado |
|---|---|---|
| `xRetNumero` | 0 ou 1 | 0 = sucesso, 1 = erro |
| `xRetTexto` | string | Descrição do resultado |
