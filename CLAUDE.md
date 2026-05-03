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
- Relatórios: filtro por período, tabela com exclusão
- Sync em tempo real via Firebase Firestore

**Firebase:**
- Projeto display name: `theadm-emporio`
- Project ID: `esperanca-emporio`
- Coleção Firestore: `sales`
- Campos de cada documento: `value`, `description`, `paymentMethod`, `timestamp`, `dateKey`
- Regras: modo de teste (30 dias a partir da criação)

**Futuro:** integrar com API do Compucenter (sistema de caixa atual do mercado) para alimentar o dashboard automaticamente. Perguntar ao Compucenter se têm API ou webhook.

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
