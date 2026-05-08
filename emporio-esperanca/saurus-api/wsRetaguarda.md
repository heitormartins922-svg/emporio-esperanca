# wsRetaguarda — Consultas de Retaguarda

**Endpoint:** `http://wsretaguarda.saurus.net.br/v001/serviceRetaguarda.asmx`
**WSDL:** `http://wsretaguarda.saurus.net.br/v001/serviceRetaguarda.asmx?wsdl`
**Protocolo:** SOAP 1.1/1.2 via HTTP POST

---

## Autenticação

Todos os métodos (exceto 1) exigem o parâmetro `xSenha` — senha criptografada fornecida pela Saurus.

---

## 10 Métodos Disponíveis

### Consultas (retornam dados)

| Método | Descrição |
|---|---|
| `retMovimentacoes` | **Consulta vendas por período** ← principal para TheADM |
| `retProdutoEstoque` | Consulta estoque de produtos em múltiplas lojas |
| `retNNfMovimentacaoAtual` | Número da NF da movimentação atual |
| `retFidelidadePendente` | Informações de fidelidade pendentes |
| `retStatusServico` | Status operacional do serviço |

### Eventos (enviam ações)

| Método | Descrição |
|---|---|
| `evProcessarFidelidade` | Processa operações de fidelidade |
| `evSalvarMovStatus` | Salva status de uma movimentação |
| `evSalvarRevisoesCaixa` | Registra revisões de caixa |
| `evSalvarPagamentoFinanceiro` | Armazena pagamento financeiro |
| `evDeletarPagamentoFinanceiro` | Remove registro de pagamento |

---

## retMovimentacoes — Detalhes

### XML de requisição

```xml
<xmlIntegracao>
    <Dominio>XXXXXX</Dominio>       <!-- ID do cliente na Saurus -->
    <TpMov>0</TpMov>                <!-- Tipo de movimentação (0 = venda) -->
    <IndStatus>0</IndStatus>         <!-- Status da movimentação -->
    <xNome>%</xNome>                 <!-- Nome do cliente (% = todos) -->
    <DInicial>2026-05-07T00:00:00</DInicial>
    <DFinal>2026-05-07T23:59:59</DFinal>
</xmlIntegracao>
```

### Campos retornados por venda

| Campo | Significado |
|---|---|
| `mov_dhEmi` | Data e hora da emissão da venda |
| `emit_idLoja` | ID da loja emitente |
| `tot_qtdItens` | Total de itens na venda |
| `tot_qCom` | Quantidade total comprada |
| `prod_vProd` | Valor bruto do produto |
| `prod_vDesc` | Desconto aplicado |
| `prod_qCom` | Quantidade comprada do produto |
| `prod_xProd` | Nome do produto |

> **Pendente:** confirmar com Gabriel se forma de pagamento (PIX, Dinheiro, Débito, Crédito) vem no XML completo de retorno ou se precisa de outro método.

---

## Protocolo técnico

```
1. Montar XML de requisição
2. Comprimir com GZip
3. Codificar em Base64
4. Enviar via SOAP POST com xSenha no header
5. Receber resposta Base64
6. Decodificar Base64
7. Descomprimir GZip
8. Parsear XML de retorno
```

### Estrutura SOAP de envio

```xml
POST /v001/serviceRetaguarda.asmx HTTP/1.1
Host: wsretaguarda.saurus.net.br
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://saurus.net.br/retMovimentacoes"

<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <retMovimentacoes xmlns="http://saurus.net.br/">
      <xBytesParametros>[BASE64_DO_XML_GZIPADO]</xBytesParametros>
      <xSenha>XXXXXX</xSenha>
    </retMovimentacoes>
  </soap:Body>
</soap:Envelope>
```

### Resposta SOAP

```xml
<soap:Envelope>
  <soap:Body>
    <retMovimentacoesResponse>
      <retMovimentacoesResult>[BASE64_DO_XML_GZIPADO]</retMovimentacoesResult>
      <xRetNumero>0</xRetNumero>   <!-- 0=sucesso, 1=erro -->
      <xRetTexto>OK</xRetTexto>
    </retMovimentacoesResponse>
  </soap:Body>
</soap:Envelope>
```
