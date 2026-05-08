# Plano de Integração: TheADM + Saurus

## Objetivo

Eliminar o lançamento manual de vendas no TheADM conectando-o ao caixa real da Compucenter (Saurus Software).

---

## Fase 0 — Pré-requisitos (antes de codar)

- [ ] Obter `xSenha` com Gabriel Lizze (+55 11 98895-3751)
- [ ] Obter `Dominio` (ID do Empório Esperança na Saurus)
- [ ] Confirmar se `retMovimentacoes` retorna forma de pagamento no XML completo
- [ ] Verificar se há ambiente de sandbox/homologação

---

## Fase 1 — Conector Saurus → Firestore

Criar função `syncFromSaurus()` em `theadm.html`:

1. Montar XML de requisição com `DInicial` e `DFinal` (últimas X horas)
2. GZip comprimir + Base64 encode o XML
3. Enviar via `fetch()` como SOAP POST para `wsRetaguarda`
4. Receber resposta → Base64 decode → GZip decomprimir → parsear XML
5. Para cada movimentação: criar documento em Firestore `sales`
6. Usar `idMovimentacao` como ID do documento para evitar duplicatas

### Dependência JS

```html
<!-- pako: GZip em JS puro, sem Node.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pako/2.1.0/pako.min.js"></script>
```

---

## Fase 2 — UI no TheADM

- Botão **"Sincronizar Caixa"** no dashboard
- Label: última sincronização + quantas vendas importadas
- Opcional: sync automático a cada 15 min (`setInterval`)

---

## Fase 3 — Mapeamento de campos

| Campo Saurus | Campo Firestore (TheADM) |
|---|---|
| `mov_dhEmi` | `timestamp` |
| `prod_vProd` − `prod_vDesc` | `value` |
| `prod_xProd` (lista de produtos) | `description` |
| forma de pagamento *(a confirmar)* | `paymentMethod` |
| data do `mov_dhEmi` (YYYYMMDD) | `dateKey` |

---

## Verificação

1. Chamar `retMovimentacoes` com data de hoje → comparar com fechamento do caixa Compucenter
2. Rodar sync duas vezes → confirmar que Firestore não duplica registros
3. Dashboard deve mostrar faturamento correto automaticamente após sync

---

## Arquivo a modificar

`emporio-esperanca/theadm.html` — único arquivo do TheADM
