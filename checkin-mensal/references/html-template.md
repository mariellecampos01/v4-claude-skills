# HTML Template — Regras de Clonagem e Adaptação

## Template Base

O template base é o check-in da **Compass de julho/2026**: `Clientes/Compass/checkins/checkin-julho-2026-comp.html`.

É o check-in mais completo e recente, com todas as seções ativas: resultado geral, funil de vendas, funil Google, projeção, projeção de agosto, palavras-chave, top 3 impulsionamentos, plano de ação em andamento com 3 abas, entregas, próximos passos, 5W1H e NPS.

Clone este arquivo como ponto de partida para qualquer novo cliente. Adapte, não crie do zero.

---

## Formato: Slideshow/Deck

O check-in mensal usa **slides**, não scroll de página.

```js
// Controle de slides
const TOTAL = 13; // atualizar com o número real de slides

function goToSlide(n) { /* ativa slide n, desativa os demais */ }
function navigate(dir) { /* seta esquerda/direita */ }
```

Cada slide:
```html
<div class="slide" id="slide-N">
  <div class="slide-header">
    <div class="brand">
      <img src="./assets/v4-company-logo-branca-oficial.svg" alt="V4">
      <span class="brand-title">NN · Nome do Slide</span>
    </div>
    <div class="slide-nav-pills">
      <span class="nav-pill" onclick="goToSlide(1)">01 Resultados</span>
      <span class="nav-pill" onclick="goToSlide(2)">02 Funil</span>
      <span class="nav-pill active" onclick="goToSlide(N)">NN Nome</span>
    </div>
  </div>
  <div class="slide-body" style="...layout específico do slide...">
    <!-- conteúdo -->
  </div>
</div>
```

**Regra dos nav-pills:** cada slide marca com `active` apenas o pill correspondente a si mesmo. Os outros pills ficam como âncoras de atalho para os slides principais.

**Atualizar `const TOTAL`** sempre que slides forem adicionados ou removidos.

---

## Adaptações Obrigatórias por Cliente

### 1. Identidade visual
O design system V4 usa **IBM Plex Sans** (Google Fonts) com os tokens do Red Command Center. Não usar Inter, Roboto ou Arial.

O restante do design system permanece igual para todos os clientes.

### 2. Logo
Logo V4 branca no header de todos os slides:
```html
<img src="./assets/v4-company-logo-branca-oficial.svg" alt="V4 Company">
```

Assets em `assets/` (copiar da pasta do template):
- `v4-company-logo-branca-oficial.svg` — logo completo branca (uso padrão)
- `v4-company-logo-oficial.webp` — logo colorida

### 3. Slides ativos
Remover slides que não constam em `seções_ativas` do `CLAUDE.md` do cliente.

Após remover slides, atualizar:
- `const TOTAL = N`
- Os `goToSlide(N)` nos nav-pills de todos os slides restantes (renumerar)

---

## Estrutura de Slides (ordem padrão)

```
slide-0   → Capa (nome do cliente, mês, hero)
slide-1   → Resultado Geral (KPIs do mês)
slide-2   → Funil de Vendas (sales) ou Funil E-commerce
slide-3   → Funil Google Ads (se Google ativo)
slide-4   → Performance de Mídia (Meta + Google resumo)
slide-5   → Top 3 Impulsionamentos (condicional)
slide-6   → Palavras-chave Google Ads (condicional)
slide-7   → Melhores Criativos Meta Ads (condicional)
slide-8   → Projeção do Próximo Mês
slide-9   → Plano de Ação em Andamento (condicional, com abas)
slide-10  → Entregas do Mês
slide-11  → Próximos Passos / 5W1H
slide-12  → NPS / Feedback
```

Ajustar a sequência conforme o cliente. O importante é manter a lógica: resultados → análise → projeção → próximos passos.

---

## Componentes Padrão

### Cards de KPIs (glass card)
```html
<div style="background:var(--surface-glass);border:1px solid var(--line);
            border-radius:var(--radius-card);padding:28px 24px;">
  <div style="font-size:9px;font-weight:700;letter-spacing:.18em;
              text-transform:uppercase;color:var(--accent-gold);margin-bottom:6px">LEADS GERADOS</div>
  <div style="font-size:clamp(28px,4vw,42px);font-weight:700;
              color:var(--accent-yellow);letter-spacing:-.02em;line-height:1">342</div>
  <div style="font-size:13px;color:var(--safe);margin-top:6px">+18% vs. junho</div>
</div>
```

Cores de delta: `--safe` (verde, positivo) · `--danger` (vermelho, negativo) · `--text-muted` (neutro)

---

### Barra de funil (etapas)

Layout split: sidebar escura (190px) à esquerda + barras à direita.

```html
<div class="slide-body" style="padding:0;overflow:hidden;display:flex;">
  <!-- Sidebar: fundo rgba(28,0,0,0.58), KPIs principais -->
  <div style="width:190px;flex-shrink:0;background:rgba(28,0,0,.58);
              padding:28px 20px 24px;display:flex;flex-direction:column;
              border-right:1px solid rgba(255,255,255,.06)">
    <!-- KPI principal em destaque -->
  </div>
  <!-- Funil: barras horizontais com largura proporcional -->
  <div style="flex:1;padding:22px 30px;display:flex;flex-direction:column">
    <!-- Cada etapa: número grande + barra + nota de transição -->
  </div>
</div>
```

---

### Top 3 Impulsionamentos — card split

Grid de 3 colunas. Cada card tem layout horizontal:

```html
<!-- Card -->
<div style="background:rgba(255,255,255,0.07);border-radius:20px;
            display:flex;flex-direction:column;overflow:hidden;
            box-shadow:0 8px 32px rgba(0,0,0,0.30)">

  <!-- Header: medalha + nome + badge formato + link -->
  <div style="padding:14px 20px;display:flex;align-items:center;gap:8px;
              flex-shrink:0;border-bottom:1px solid rgba(255,255,255,.06)">
    <span style="font-size:13px;line-height:1;flex-shrink:0">🥇</span>
    <span style="font-size:12px;font-weight:700;font-stretch:75%;color:#fff;
                 flex:1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis">Nome do post</span>
    <span style="background:rgba(255,255,255,.1);color:rgba(255,255,255,.55);
                 font-size:8px;font-weight:700;letter-spacing:.1em;
                 padding:2px 7px;border-radius:999px;flex-shrink:0">REELS</span>
    <a href="[link-instagram]" target="_blank"
       style="color:rgba(255,255,255,.25);text-decoration:none;
              font-size:13px;flex-shrink:0">↗</a>
  </div>

  <!-- Body: imagem 55% | KPI sidebar -->
  <div style="display:flex;flex:1;min-height:0;padding:12px 8px 12px 14px;gap:12px">

    <!-- Thumbnail -->
    <div style="width:55%;flex-shrink:0;overflow:hidden;border-radius:12px">
      <img src="./assets/vencedores/nome-do-post.png"
           style="width:100%;height:100%;object-fit:cover;
                  object-position:center center;display:block">
    </div>

    <!-- KPIs -->
    <div style="flex:1;display:flex;flex-direction:column">

      <!-- Investimento -->
      <div style="flex:1;padding:10px 14px;display:flex;flex-direction:column;
                  justify-content:center;border-bottom:1px solid rgba(255,255,255,.05)">
        <div style="font-size:7px;font-weight:700;letter-spacing:.13em;
                    text-transform:uppercase;color:rgba(255,255,255,.3);margin-bottom:3px">
          💰 Investimento</div>
        <div style="font-size:clamp(13px,1.5vw,17px);font-weight:700;
                    font-stretch:75%;color:#fff;letter-spacing:-.02em;line-height:1">R$200,79</div>
      </div>

      <!-- Seguidores — destaque verde (campeão) -->
      <div style="flex:1.5;padding:10px 14px;display:flex;flex-direction:column;
                  justify-content:center;border-bottom:1px solid rgba(99,212,113,.15);
                  background:rgba(99,212,113,.09)">
        <div style="font-size:7px;font-weight:700;letter-spacing:.13em;
                    text-transform:uppercase;color:var(--safe);margin-bottom:3px">
          👥 Seguidores</div>
        <div style="font-size:clamp(18px,2.2vw,26px);font-weight:700;
                    font-stretch:75%;color:var(--safe);letter-spacing:-.02em;line-height:1">182</div>
      </div>

      <!-- Visitas -->
      <div style="flex:1;padding:10px 14px;display:flex;flex-direction:column;
                  justify-content:center;border-bottom:1px solid rgba(255,255,255,.05)">
        <div style="font-size:7px;...;color:rgba(255,255,255,.3);...">👁 Visitas</div>
        <div style="...;color:#fff">799</div>
      </div>

      <!-- Custo/Seg — dourado se melhor custo do grupo -->
      <div style="flex:1;padding:10px 14px;display:flex;flex-direction:column;
                  justify-content:center;[background:rgba(255,212,138,.08) se melhor custo]">
        <div style="...;color:var(--accent-gold);...">⚡ Custo/Seg.</div>
        <div style="...;color:var(--accent-gold)">R$1,10</div>
      </div>

    </div>
  </div>
</div>
```

**Seguidores no 2o e 3o cards:** usar fundo mais fraco (`rgba(99,212,113,.05)`) e borda `rgba(255,255,255,.05)` para diferenciar do campeão.

---

### Plano de Ação — sistema de abas

Ver `references/secoes.md § Plano de Ação em Andamento` para o código completo do sistema de abas e o script `switchPlanTab`.

---

### Nota de rodapé em slide de funil

```html
<div style="display:flex;align-items:flex-start;padding-top:9px;gap:3px;
            border-top:1px solid rgba(255,255,255,.06);margin-top:8px">
  <span style="font-size:9px;font-weight:700;color:rgba(255,255,255,.3);
               flex-shrink:0;line-height:1.5">*</span>
  <span style="font-size:9px;color:rgba(255,255,255,.28);line-height:1.6">
    [Explicação da limitação de dados em linguagem simples]
  </span>
</div>
```

---

### Imagens de criativos e posts

Padrão único para qualquer imagem — sem lightbox, sem overlay, sem hover scale:

```html
<div style="width:100%; aspect-ratio:4/5; overflow:hidden; border-radius:12px;">
  <img src="./ad01.png" alt="..." style="width:100%;height:100%;object-fit:cover;display:block;">
</div>
```

Para thumbnails de Reels (verticais): `object-position: center center`.
Para screenshots horizontais de interface: `object-position: left center`.

---

### Botão CTA (Plano de Mídia)

```html
<a href="{plano_midia_url}" target="_blank" rel="noopener"
   style="display:inline-flex;align-items:center;gap:10px;padding:14px 26px;
          border-radius:var(--radius-pill);background:var(--accent-gold);
          color:#3B0000;font-size:13px;font-weight:700;letter-spacing:.06em;
          text-transform:uppercase;text-decoration:none;">
  Acessar plano →
</a>
```

---

## Variação por Segmento

### Sales (inside sales / comercial)
- Manter: Resultado Geral, Funil de Vendas, Funil Google (se ativo), Projeção, Propostas/Pipeline, Performance de Mídia, Criativos (se dados disponíveis), Palavras-chave (se Google ativo), Impulsionamentos (se SM ativo), Plano de Ação (se houver iniciativas)
- Remover: Funil E-commerce, seção E-commerce

### E-commerce
- Manter: Resultado Geral, Funil E-commerce, Projeção, Performance de Mídia, seção E-commerce
- Remover: Funil de Vendas, Propostas/Pipeline

### Híbrido
- Manter todas as seções, ajustando labels conforme o negócio do cliente

---

## Checklist antes de publicar

- [ ] `const TOTAL = N` correto (igual ao número de slides reais)
- [ ] Todos os `goToSlide(N)` nos nav-pills renumerados corretamente
- [ ] Tipografia: IBM Plex Sans carregada via Google Fonts
- [ ] Logo V4 branca no header de todos os slides
- [ ] Slides corretos para o segmento do cliente (sem slides vazios ou de outro cliente)
- [ ] Todos os dados preenchidos (sem placeholders `[XXXX]` visíveis)
- [ ] Thumbnails de Impulsionamentos em `assets/vencedores/` e caminho correto no `src`
- [ ] Ranking de Impulsionamentos validado (🥇 > 🥈 > 🥉 em seguidores)
- [ ] Array de abas no `switchPlanTab` inclui todas as chaves criadas
- [ ] Notas de rodapé nos funis onde houver limitação de dados
- [ ] Verificar URL de deploy retorna 200 antes de enviar ao cliente
