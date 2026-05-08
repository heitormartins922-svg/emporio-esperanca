# wsCadastros — Sincronização de Cadastros

**Endpoint:** `http://wscadastros.saurus.net.br/v001/serviceCadastros.asmx`
**WSDL:** `http://wscadastros.saurus.net.br/v001/serviceCadastros.asmx?wsdl`
**Protocolo:** SOAP 1.1/1.2

> Relevância para TheADM: **baixa**. Útil se quiser exibir catálogo de produtos no dashboard.

---

## Métodos

| Método | Descrição |
|---|---|
| `retCadastros` | Retorna todos os cadastros do PDV (produtos, preços, clientes, etc.) |
| `retStatusServico` | Verifica status operacional do serviço |

---

## retCadastros — Parâmetros de entrada

| Campo | Descrição |
|---|---|
| `Dominio` | ID do cliente na Saurus |
| `TpArquivo` | Modelo do arquivo (valor: 50) |
| `ChaveCaixa` | UUID do PDV vinculado |
| `TpSync` | Tipo de sincronização |
| `DhReferencia` | Data/hora de referência — filtra apenas registros alterados desde então |

---

## Dados retornados (tabelas no XML)

| Tabela | Conteúdo |
|---|---|
| `tbProdutoDados` | Produtos: nome, categoria, tipo balança |
| `tbProdutoCodigos` | Códigos de barras / SKU |
| `tbProdutoPrecos` | Tabela de preços por produto |
| `tbProdutoImpostos` | ICMS, PIS, COFINS, IPI |
| `tbProdutoImagens` | URLs das fotos dos produtos |
| `tbProdutoKits` | Kits/bundles |
| `tbCadastroDados` | Clientes e fornecedores |
| `tbPagDados` | Formas de pagamento disponíveis |
| `tbPagPlanos` | Planos de parcelamento |
| `tbPromocaoDados` | Promoções ativas |
| `tbLojaDados` | Dados da loja (CNPJ, endereço, telefone) |
| `tbLojaConfigs` | Configurações dinâmicas da loja |
| `tbCaixaDados` | Caixas disponíveis |
| `tbCadastroLogins` | Contas de acesso e senhas |
| `tbCadastroLoginPermissoes` | Permissões por usuário |
| `tbModificadorDados` | Modificadores/adicionais de produtos |

---

## Sincronização incremental

O atributo `dReferencia` no XML de retorno contém a data do servidor. Usar esse valor como `DhReferencia` na próxima consulta para receber apenas o que mudou desde então.
