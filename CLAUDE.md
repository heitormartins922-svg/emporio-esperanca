# CLOUDE — Heitor Martins
Pasta de projetos pessoais e profissionais do Heitor Martins De Oliveira.
GitHub: https://github.com/heitormartins922-svg

---

## Estrutura do repositório

```
CLOUDE/
├── index.html                          ← TheDeck (portfólio pessoal)
├── heitor.png                          ← foto do Heitor (selfie, camisa branca, óculos arredondado)
└── emporio-esperanca/
    ├── mercado.html                    ← site público do Empório Esperança
    ├── theadm.html                     ← sistema de gestão de vendas (TheADM)
    ├── auto-imagens.html               ← ferramenta de busca em lote de imagens para produtos
    └── notas.md                        ← anotações do projeto
```

---

## Projeto 1 — TheDeck (index.html)
Portfólio pessoal. Arquivo único HTML/CSS/JS.

**Design:**
- Fundo branco `#FFFFFF`, texto preto `#0A0A0A`, acento azul `#0047FF` / `#2E6BFF`
- Fontes: `Bebas Neue` (display/headings) + `Outfit` (body) — Google Fonts
- Efeitos: rolling reveal via IntersectionObserver, parallax no hero
- Logo "TheDeck" no canto superior esquerdo

**Seções:**
1. Hero — nome, subtítulo, foto com anéis rotatórios e aura azul
2. About — fundo preto, bio + stats (18 anos, Administração, experiências)
3. Experiência — Empório Esperança (gerente) + Alka (IA)
4. Footer

**Regra:** atualizar gradualmente conforme o Heitor for adicionando projetos/habilidades. Nunca quebrar o design atual.

---

## Projeto 2 — Site do Mercado (emporio-esperanca/mercado.html)
Site público do Empório Esperança. Arquivo único HTML/CSS/JS.

**Design:**
- Cores: `--green: #0F5C2E`, `--orange: #E8500A`, fundo `--bg: #F7F5F0`
- Fontes: `Bebas Neue` + `Outfit` — Google Fonts
- Animações: `.reveal` via IntersectionObserver

**Seções:**
1. Navbar
2. Hero com destaque de ofertas
3. Delivery strip (entrega grátis — Esperança e Santa Rosa)
4. Categorias de produtos
5. Catálogo completo com filtro por categoria
6. Depoimentos
7. Sobre Nós — seção em 2 colunas, headline "Lugar feito para sua família"
   - Coluna esquerda: placeholder para foto real do mercado (ainda não tirada)
   - Coluna direita: descrição + badges + política de entrega
8. Info strip
9. Footer

**Pedidos online:** ao finalizar um pedido, `registrarVendaOnline()` salva na coleção `sales` com `source: 'online'` e os seguintes campos extras:
- `customerName`, `customerPhone`, `customerAddress`, `deliveryType` ('entrega' | 'retirada')
- `observations`, `items[]` (array com nome, unit, qty/grams, preco, subtotal de cada item)

**Pendente:** quando o Heitor tiver foto real do mercado, substituir o placeholder em `.sobre-img-wrap` por `<img>`.

---

## Projeto 3 — TheADM (emporio-esperanca/theadm.html)
Sistema de gestão de vendas do Empório Esperança. Arquivo único HTML/CSS/JS.

**Design:**
- Dark mode: fundo `#0A0A0A`, texto branco, acento azul `#0047FF`
- Mesmas fontes: `Bebas Neue` + `Outfit`
- Nome do sistema: **TheADM**

**Funcionalidades:**
- Dashboard: faturamento hoje / semana / mês em tempo real, ticket médio
- Gráfico de barras — últimos 7 dias (Chart.js)
- Nova Venda: valor, descrição, forma de pagamento (PIX / Dinheiro / Débito / Crédito)
- Nova Despesa: valor, descrição, categoria
- Relatórios: filtro por período, tabela com exclusão; sub-aba Fluxo de Caixa (entradas × saídas)
- Produtos: catálogo sincronizado do Saurus, ativar/desativar, adicionar imagem por URL. `syncProdutos()` faz 1 read total + batch commits de 499 para não estourar quota do Firestore.
- **Últimos Pedidos:** lista todos os pedidos do site (`source: 'online'`) com filtro por período; clicar no card abre modal com nome, WhatsApp (link direto), endereço, itens com subtotais, total e observações
- **Vendas Caixa:** lista vendas do Compucenter (`source: 'compucenter'`) com filtro por período; clicar no card abre modal com itens e quantidades vendidas
- Sync em tempo real via Firebase Firestore

**Firebase:**
- Projeto display name: `theadm-emporio`
- Project ID: `esperanca-emporio`
- Coleções Firestore: `sales`, `expenses`, `products`
- Campos de `sales`: `value`, `description`, `paymentMethod`, `timestamp`, `dateKey`, `source` ('online' | 'compucenter' | ausente=manual)
- Pedidos online (`source: 'online'`) têm campos extras: `customerName`, `customerPhone`, `customerAddress`, `deliveryType`, `observations`, `items[]` — array com `{nome, unit, qty/grams, preco, subtotal}`
- Vendas do caixa (`source: 'compucenter'`) têm campo `items[]` — array com `{nome, qty, valor}`, onde `qty` vem do campo `prod_qCom` do XML do Saurus (`retMovimentacoes`). Também têm `externalId` (timestamp da NF-e como chave de deduplicação).
- Regras: modo de teste (30 dias a partir da criação)

**Saurus API — notas importantes:**
- `retMovimentacoes` (wsretaguarda): vendas do caixa. Campos por item: `prod_xProd` (nome), `prod_vProd` (valor), `prod_vDesc` (desconto), `prod_qCom` (quantidade vendida), `mov_dhEmi` (timestamp da venda).
- `retCadastros` com `TpArquivo=50` (wscadastros): catálogo de produtos. **Não contém estoque** — `tbProdutoDados` tem apenas nome, categoria, medida, NCM, peso. Quantidade em estoque não está disponível neste endpoint.

**Futuro:** aprofundar integração com Saurus — investigar se existe endpoint separado para saldo de estoque.

---

## Projeto 4 — Auto-Imagens (emporio-esperanca/auto-imagens.html)
Ferramenta de uso interno para preencher imagens dos ~2200 produtos em lote. Não faz parte do mercado.html nem do theadm.html.

**Fonte:** Google Custom Search JSON API (substituiu Open Food Facts em maio/2026).

**Credenciais Google Custom Search:**
- API Key: `AIzaSyB_AfBkVT7tCdm_aCviHlq5m-SfBevZH9I` (Google Cloud projeto: My First Project)
- Search Engine ID (cx): `7455f9b9aa7694095` (mecanismo: "Empório Imagens")
- Limite: 100 buscas/dia grátis. Cota reseta à meia-noite (horário Google/PST).
- Configuração salva em `localStorage` do navegador (chaves: `emporio_google_apikey`, `emporio_google_cx`).

**Duas abas:**
- **Automático:** processa todos os produtos sem `img` em fila via Google Images API. Auto-aprova score ≥ 65%, envia o restante para revisão manual. Para automaticamente com mensagem clara se cota esgotar (429). Delay 420ms entre requisições.
- **Busca Manual (fluxo principal):** painel dois-colunas. Clicar num produto abre o Google Imagens automaticamente em nova aba com o nome do produto. Usuário copia a URL da imagem e cola no campo — `Enter` salva e avança para o próximo produto automaticamente.

**Fluxo rápido Busca Manual:**
1. Clica no produto → Google Imagens abre em nova aba
2. No Google: clica na imagem → clique direito → "Copiar endereço da imagem"
3. Volta para a ferramenta → Ctrl+V → Enter → avança automaticamente

**Bug corrigido no theadm.html (maio/2026):** sync do Saurus não sobrescreve mais `img: null` em produtos existentes — preserva a imagem já salva.

**Não hospedar publicamente** — é ferramenta interna de manutenção.

---

## Perfil do usuário
- Nome: Heitor Martins De Oliveira
- Idade: 18 anos | Curso: Administração
- Email: heitormartins922@gmail.com
- GitHub: heitormartins922-svg
- Cargo atual: Gerente — Mercado Empório Esperança (sistema de caixa: Compucenter)
- Experiência anterior: Alka (empresa de Agentes de IA) — vendeu projetos para papelarias, seguradoras e distribuidoras de bebidas

## Preferências de código
- HTML/CSS/JS puro, tudo em arquivo único por projeto
- Sem frameworks (sem React, Vue, etc.)
- Comentários apenas quando estritamente necessário
- Responsivo: mobile-first, breakpoints em 900px e 600px
