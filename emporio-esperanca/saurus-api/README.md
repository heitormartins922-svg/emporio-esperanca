# Saurus Software — Integração com TheADM

A Compucenter usa o PDV da **Saurus Software**, que expõe 3 Web Services SOAP para integração externa.

## Contato

**Gabriel Lizze Rodrigues Marques**
+55 11 98895-3751 (Saurus Software)

## O que pedir ao Gabriel

- [ ] `xSenha` — senha criptografada de acesso à API (obrigatória em todos os requests)
- [ ] `Dominio` — identificador do cadastro do Empório Esperança na Saurus
- [ ] Confirmar se `retMovimentacoes` retorna forma de pagamento no XML completo
- [ ] Verificar se há ambiente de homologação/sandbox para testes

---

## Os 3 Web Services

| Serviço | Endpoint | Uso | Relevância |
|---|---|---|---|
| wsCadastros | `wscadastros.saurus.net.br/v001/serviceCadastros.asmx` | Baixa produtos, preços, clientes | Baixa |
| wsRecepcao | `wsrecepcao.saurus.net.br/v001/serviceRecepcao.asmx` | *Envia* vendas para o sistema | Nenhuma |
| wsRetaguarda | `wsretaguarda.saurus.net.br/v001/serviceRetaguarda.asmx` | *Consulta* vendas e movimentações | **Alta** |

## Documentação oficial

- wsCadastros: https://wscadastros.docs.saurus.com.br/arquivos/retcadastros
- wsRecepcao: https://wsrecepcao.docs.saurus.com.br/
- wsRetaguarda: https://wsretaguarda.docs.saurus.com.br/
