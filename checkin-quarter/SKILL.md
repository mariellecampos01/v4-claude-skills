---
name: checkin-quarter
description: Gera apresentações de check-in trimestral (ROPRE) para clientes de marketing digital. Consolida resultados dos 3 meses do quarter, revisa OKRs, analisa criativos vencedores e canais, define Objetivo SMART + KRs + projeção para o próximo trimestre, levanta premissas e riscos com matriz de impacto, e mapeia backlog previsto. Use quando o usuário pedir "check-in de quarter", "ROPRE trimestral", "apresentação de quarter", "revisão trimestral de cliente", ou relatório Q1/Q2/Q3/Q4.
---

# Check-in de Quarter — ROPRE Trimestral

> **Referência canônica:** `ropre-q2-2026-alquilab.html` em `Clientes/Alquilab/checkins/`  
> **Referência de funil com comparativo de mês:** `ropre-q2-2026-comp.html` em `Clientes/Compass/checkins/` (slide-3) — padrão para funis mês vs mês anterior (seção 1.4B)  
> Sempre consultar os arquivos de referência antes de gerar um novo ROPRE.

## O que é o ROPRE

O ROPRE é a apresentação trimestral mais importante da relação V4–cliente. É um **replanejamento estratégico**, não um mero relatório. Acontece ao final de cada quarter (4x ao ano) e serve para:

- Revisão profunda dos 3 meses anteriores
- Definição de objetivo SMART + KRs para o próximo trimestre
- Coleta de NPS (agora mensal — coletar durante a call)
- Oportunidade de expansão de portfólio (Account Planning / white spaces)
- Construção de narrativa e controle do storytelling do projeto

**Duração:** 1h30. Avisar o cliente antes que a reunião é mais longa.  
**Prazo máximo:** até o dia 17 do primeiro mês do novo quarter.  
**Após a reunião:** enviar ata com todos os combinados por e-mail e/ou grupo WhatsApp.

---

## Filosofia do ROPRE

> "Nós NUNCA levamos um resultado ruim sem um plano de ação para melhorar.  
> Nós NUNCA levamos um resultado bom sem um plano de ação para seguir crescendo."

> "O cliente não renova porque está satisfeito com o agora. Ele renova quando acredita no futuro que você está construindo com ele."

### 4 Pilares do Storytelling

1. **Evidencie primeiro as vitórias** — para cada ponto negativo, apresente imediatamente um plano de ação
2. **Fundamentação com indicadores** — Growthpack, Cockpit e Breakeven 100% atualizados antes da reunião
3. **Demonstre empatia** — mostre que entende os desafios e a realidade da operação do cliente
4. **Colaboração ativa** — envolva o cliente ao longo de toda a apresentação; pergunte se está fazendo sentido

### Benefícios de um ROPRE bem feito
- Aumenta a autoridade da equipe V4 perante o cliente
- Gera rapport e proximidade
- Retém o projeto e abre espaço para expansão
- Gera recomendações e NPS positivo

---

## Princípios de Qualidade — Padrões Obrigatórios

Estes princípios foram estabelecidos na revisão do ROPRE Q2/2026 Compass e passam a vigorar em todos os decks gerados a partir desta versão da Skill.

### Narrativa por slide

Cada slide deve responder a **uma** das perguntas abaixo. Antes de escrever o conteúdo, identificar qual pergunta o slide responde:

| Slide | Pergunta que responde |
|-------|----------------------|
| Resultados (grade, funil) | O que aconteceu? |
| Gráficos, comparativo | Por que aconteceu? |
| Testes e aprendizados | O que aprendemos? |
| OKRs, 5W1H, plano de ação | O que faremos a seguir? |

Slides que apenas exibem números sem interpretação **não devem existir**. Todo slide tem título de impacto (frase executiva) e pelo menos um elemento de contexto ou diagnóstico.

### Eyebrows — sem prefixo numérico

**Regra absoluta:** o elemento `<div class="eyebrow">` nunca recebe prefixo numérico (ex: `01.1 ·`, `05.1 ·`). Escrever diretamente o nome da subseção.

```html
<!-- ERRADO -->
<div class="eyebrow">05.1 · Plano de Ação 5W1H</div>

<!-- CERTO -->
<div class="eyebrow">Plano de Ação 5W1H</div>
```

A identificação de seção fica exclusivamente no `brand-title` do `slide-header`, nunca no eyebrow.

### Bloco de contexto para indicadores

Sempre que um indicador relevante (ROAS, CPL, CPM, faturamento, CAC) apresentar variação acima de 15% em relação ao período anterior, gerar automaticamente um **bloco de contexto** após a tabela ou gráfico correspondente:

```html
<div class="glass-card-soft" style="border-left:3px solid var(--care);border-radius:0 14px 14px 0;">
  <div style="font-size:12px;color:var(--text-muted);line-height:1.65">
    <span style="color:#fff;font-weight:700">Diagnóstico:</span>
    [Explicação objetiva dos fatores que causaram a variação. Nunca deixar o cliente interpretar sozinho.]
  </div>
</div>
```

Cor da borda esquerda: `var(--safe)` para variação positiva, `var(--care)` para variação moderada/neutra, `var(--danger)` para queda ou custo elevado.

### Slide de aprendizados

Incluir apenas aprendizados com conclusão real do trimestre. Remover iniciativas ainda em andamento — elas pertencem ao 5W1H, não à tabela de testes.

Cada linha da tabela de testes deve ter:
- Um **insight claro** (o que este resultado nos ensinou)
- Uma **decisão para o próximo quarter** (pill de ação: ESCALAR / MANTER / MONITORAR / IMPLEMENTAR / PAUSAR)

Linha sem decisão não deve existir na tabela.

### Slides de planejamento mensal

Incluir apenas ações que **realmente serão executadas** no mês. Se houver menos de 4 ações, reorganizar o layout para 2 cards de maior destaque (evitar espaços vazios). Se houver mais de 6, considerar subdividir em dois slides ou usar lista compacta.

Quando houver mudança estratégica relevante no funil, representar com um bloco de fluxo visual:

```html
<!-- Fluxo de mudança estratégica -->
<div style="display:flex;align-items:center;gap:12px;padding:12px 16px;
            background:rgba(255,255,255,0.06);border-radius:14px;margin-bottom:10px;">
  <div style="text-align:center;min-width:80px;">
    <div style="font-size:20px;margin-bottom:4px">🔄</div>
    <div style="font-size:10px;font-weight:700;color:var(--accent-gold)">MUDANÇA</div>
    <div style="font-size:11px;color:#fff">[O que muda]</div>
  </div>
  <div style="font-size:18px;color:var(--text-muted)">→</div>
  <div style="text-align:center;min-width:80px;">
    <div style="font-size:20px;margin-bottom:4px">💡</div>
    <div style="font-size:10px;font-weight:700;color:var(--care)">MOTIVO</div>
    <div style="font-size:11px;color:#fff">[Por que muda]</div>
  </div>
  <div style="font-size:18px;color:var(--text-muted)">→</div>
  <div style="text-align:center;min-width:80px;">
    <div style="font-size:20px;margin-bottom:4px">📈</div>
    <div style="font-size:10px;font-weight:700;color:var(--safe)">IMPACTO</div>
    <div style="font-size:11px;color:#fff">[O que esperamos]</div>
  </div>
</div>
```

### Slides de criativos

Avaliar criativos por **eficiência** (CPL / CTR / taxa de conversão), não apenas por volume de leads.

Cada card de criativo deve incluir um insight de 1 linha explicando por que se destacou:

```html
<div style="font-size:10px;color:var(--accent-gold);margin-top:6px;font-style:italic">
  "[Motivo do destaque: gancho, formato, público, contexto]"
</div>
```

### Slides de premissas e riscos

Exibir apenas riscos relevantes para o contexto atual do cliente. Se houver 2 riscos (não 3), usar layout de 2 cards lado a lado — não forçar um terceiro vazio. A régua interativa funciona com qualquer quantidade de cards.

### Slide 5W1H

**Implementar sempre como `<table>` HTML** — nunca como cards, lista ou grid.

Regras da tabela:
- Quantidade de linhas: variável, sem limite máximo
- Cabeçalho fixo: `#` · O QUÊ · QUANDO · QUEM · COMO
- Padding das células: reduzir proporcionalmente conforme o número de linhas (até `7px 12px` para 10+ linhas, `10px 14px` para até 5 linhas)
- Coluna QUANDO colorida por urgência: `var(--safe)` verde (próximo/julho) · `var(--accent-yellow)` amarelo (mês seguinte/agosto) · `var(--text-muted)` branco (prazo longo/setembro+)
- A tabela deve usar `flex:1;display:flex;flex-direction:column;` no `.glass-card` wrapper para ocupar o espaço disponível

```html
<div class="glass-card" style="padding:0;overflow:hidden;flex:1;display:flex;flex-direction:column;">
  <table style="width:100%;border-collapse:collapse;">
    <thead>
      <tr>
        <th style="background:rgba(0,0,0,0.3);padding:8px 12px;font-size:9px;font-weight:700;
                   letter-spacing:0.14em;text-transform:uppercase;color:var(--accent-gold);
                   text-align:left;width:4%">#</th>
        <th style="...;width:24%">O Quê</th>
        <th style="...;width:10%">Quando</th>
        <th style="...;width:14%">Quem</th>
        <th style="...">Como</th>
      </tr>
    </thead>
    <tbody>
      <!-- N linhas conforme o plano de ação — sem limite -->
    </tbody>
  </table>
</div>
```

### Diagramação automática

Ao compor cada slide, verificar se há espaço vazio visível e reorganizar os componentes:

- **Cards pequenos concentrados em um canto:** redistribuir em grid ou aumentar proporção
- **Slide com 1 único elemento pequeno:** aumentar o tamanho do elemento para ocupar ao menos 60% da área do `slide-body`
- **Listas com poucos itens:** considerar aumentar `gap`, `padding` e `font-size` para ocupar o espaço
- **Grid 2 colunas com coluna vazia:** converter para layout de 1 coluna ampliada

### Linguagem executiva

Adotar linguagem incisiva em títulos, eyebrows e callouts. Evitar textos descritivos.

**Preferir:**
- "O placar mudou. Aqui está o porquê."
- "O risco está concentrado em dois pontos."
- "O esforço ainda não virou rotina."
- "Onde a cobrança ainda precisa acontecer."
- "Quem efetivamente avançou."

**Evitar:**
- "Dashboard de acompanhamento."
- "Visão geral dos dados do trimestre."
- "Relatório de resultados."
- "Análise detalhada dos indicadores."

---

## Output do ROPRE

- Apresentação HTML seguindo o **Design System V4 — Red Command Center**
  (skill `/frontend-design` + `v4-design-system/`)
- **Formato:** slideshow/deck com navegação horizontal — não scroll único
- **Arquivos gerados em `clientes/[cliente]/checkins/`:**
  - `ropre-q[N]-[ANO]-[sigla].html` — arquivo principal nomeado
  - `index.html` — cópia do arquivo acima (obrigatória para o Vercel usar como entry point)
  - `assets/v4-company-logo-branca-oficial.svg` — logo V4 branca (copiar de qualquer checkin existente)

### Deploy no Vercel

```bash
cd clientes/[cliente]/checkins
cp ropre-q[N]-[ANO]-[sigla].html index.html
vercel --prod --yes
vercel alias set <deployment-url> checkin-q[N]-[sigla-cliente].vercel.app
```

- Alias padrão: `checkin-q[N]-[sigla-cliente].vercel.app` (ex: `checkin-q2-compass.vercel.app`)
- Sempre confirmar via WebFetch que a URL retorna 200 antes de passar o link ao usuário

---

## Variações por Cliente

O Design System V4 — Red Command Center e a estrutura de 5 seções (R/O/P/E + Próximos) são **padrão fixo**. Antes de gerar qualquer HTML, confirmar as 5 variáveis que definem o deck:

### As 5 perguntas obrigatórias antes de começar

**1. Logo do cliente na capa**
Cada cliente tem sua própria identidade. A capa deve exibir a logo/nome do cliente em destaque — não apenas o logo V4.
- Verificar se existe asset da logo em `clientes/[cliente]/checkins/assets/` ou `docs/`
- Se não houver arquivo, perguntar ao usuário o caminho ou usar o nome do cliente em tipografia
- O logo V4 fica no slide-header (pequeno, canto esquerdo); a logo do cliente fica na capa em destaque

**2. Tem Social Media?**
- Sim → adicionar slide de métricas SM na seção Resultados (crescimento de seguidores, alcance, posts top 3)
- Não → omitir completamente; não criar slide vazio

**3. Tem Inside Sales?**
- Sim → incluir slide de Funil IS (split layout: Leads → WPP → MQL → Venda)
- Não → omitir funil IS, criativos IS e drawflow IS

**4. Tem E-commerce?**
- Sim → incluir slide de Funil Ecom GA4 (Sessões → View Item → Add to Cart → Checkout → Purchase)
- Não → omitir funil Ecom, criativos Ecom e drawflow Ecom

**5. Investe em quais canais?**
Afeta: pills de canal no header dos funis, breakdown de investimento na sidebar, Plano de Mídia, e distribuição de verba nos gráficos.

| Canal | Pill de canal | Cor do dot (sidebar Ecom) |
|-------|--------------|--------------------------|
| Meta Ads | pill escuro + SVG Meta azul `#1877F2` | `#1877F2` |
| Google Ads | pill branco + SVG Google colorido | `#FBBC05` |
| TikTok Ads | pill escuro + SVG TikTok | `#010101` |
| WhatsApp / IS | não aparece como pill de canal; vai no funil IS |

---

**O que nunca varia independente do cliente:**
- Design System: tokens de cor, tipografia IBM Plex Sans, glass-cards, Red Command Center
- Split layout dos funis (sidebar 190px escura + barras à direita)
- Paleta dos estágios de funil (IS e Ecom têm cores fixas documentadas nas seções 1.4 e 1.5)
- Nav pills por slide com `goToSlide(N)` corretos
- Arquitetura CSS `opacity:0` / `.active {opacity:1}`
- `const TOTAL = N` e scripts Python para renumeração segura
- Deploy `vercel --prod --yes` + alias `checkin-q[N]-[sigla-cliente].vercel.app`

Ao iniciar um ROPRE para um novo cliente: consultar o Alquilab como referência visual, responder as 5 perguntas acima, e montar o mapa de slides antes de escrever o HTML.

---

## Dados Necessários

Solicitar ao usuário ou buscar via MCP nas fontes:

### Fontes de Dados
- **Growth Pack** do cliente — planilha de acompanhamento, meses do quarter
- **Cockpit** — health score, step atual do projeto (V0/V1/V2/V3)
- **Breakeven** — projeção de ponto de equilíbrio, margem de contribuição
- **Meta Ads / Google Ads** — métricas por campanha, criativos com melhor performance
- **CRM** — leads, MQLs, SQLs, vendas, faturamento, SLA de atendimento
- **Social Media** — alcance, interações, seguidores, crescimento Q-over-Q
- **Ekyte** — entregas realizadas no quarter (tarefas concluídas por mês)
- **NotebookLM do cliente** — contexto estratégico, histórico, apostas vivas

### Dados Mínimos por Quarter
- Período: ex. Q1 2026 = Jan + Fev + Mar
- Investimento em mídia por mês + total do quarter
- Leads por mês + total + CPL médio
- MQLs por mês + total + CMQL
- SQLs + vendas + faturamento (por mês e total)
- ROAS (se e-commerce)
- OKRs do quarter passado + resultados reais atingidos
- Step atual do projeto
- Criativos top 3 com métricas (leads, CPL, impressões, CTR)
- Canais ativos e distribuição de verba
- Entregas realizadas (por mês)
- Datas sazonais do próximo quarter relevantes para o segmento
- **Se IS:** dados de funil por mês — Leads / WPP / MQL / Venda + taxas de conversão
- **Se Ecom:** dados GA4 — Sessões / View Item / Add to Cart / Checkout / Purchase + Receita

---

## Estrutura ROPRE — 5 Seções

### 01 — RESULTADOS (R)

**Título da seção:** "O que os 3 meses entregaram."

**Objetivo:** Contar a história do quarter com dados. Evidenciar vitórias primeiro.
Para cada ponto negativo, trazer plano de ação imediato — nunca apresentar perda sem solução.

#### 1.1 Grade Visual Mensal

Grid de linhas mensais com linha de total ao final. Cada linha tem:
- Rótulo do mês em destaque (pill colorido à esquerda): Janeiro / Fevereiro / Março
- Colunas: Valor Investido | Leads | CPL | MQL | CPMQL | Vendas | Faturamento | ROAS
- Linha final "GERAL" com fundo verde escuro e todos os totais/médias em destaque

Layout visual: mês como label colorido à esquerda, métricas horizontais.
Crescimento em evidência (safe/gold). Queda com cor danger.

#### 1.2 Gráficos de Destaque

Antes de gerar, perguntar ao usuário quais dados destacar em gráfico. Usar Chart.js.

Gráficos mais comuns:
- **Faturamento & ROAS** — barra + linha (eixo duplo), todos os meses históricos disponíveis
- **Funil Q-over-Q** — barras agrupadas comparando taxas de conversão do quarter anterior vs atual
- **Leads e MQL** — duas linhas mostrando tendência dos 3 meses
- **Verba por Canal** — donut quando houver mais de 1 canal ativo

Regras visuais dos gráficos:
- Canvas altura `260–320px`, responsivo
- Fundo transparente (glass-card já provê o fundo)
- Verde `#63D471` · Dourado `#FFD48A` · Danger `#FF8A80` · Grade `rgba(255,255,255,0.3)`
- Tooltip fundo `rgba(30,0,0,0.85)`, texto branco; legenda no topo

Após cada gráfico de indicador com variação > 15%, incluir bloco de contexto (ver seção "Bloco de contexto para indicadores" nos Princípios de Qualidade).

#### 1.3 Comparativo de Quarters

Tabela completa: Métrica | Mês 1 | Mês 2 | Mês 3 | Q Total | Q Anterior | Delta

Métricas: Investimento | Leads | CPL | MQL | Tx. Lead→MQL | Vendas | Faturamento | ROAS

Coluna Delta: verde (crescimento) · amarelo (variação leve) · vermelho (queda expressiva)

#### 1.4 Funil de Conversão Visual — Inside Sales (quando aplicável)

**Usar este padrão sempre que o cliente tiver canal IS com dados de funil disponíveis.**

Layout split: sidebar escura à esquerda + funil de barras à direita. Ocupa o `slide-body` inteiro (sem padding padrão).

```html
<div class="slide-body" style="padding:0;overflow:hidden;display:flex;">

  <!-- SIDEBAR: 190px, fundo escuro -->
  <div style="width:190px;flex-shrink:0;background:rgba(28,0,0,0.58);
              padding:28px 20px 24px;display:flex;flex-direction:column;
              border-right:1px solid rgba(255,255,255,0.06);">
    <!-- KPI: Faturado -->
    <div style="margin-bottom:22px">
      <div style="font-size:8px;font-weight:700;letter-spacing:0.18em;
                  text-transform:uppercase;color:var(--accent-gold);margin-bottom:5px">FATURADO</div>
      <div style="font-size:28px;font-weight:700;font-stretch:75%;
                  letter-spacing:-0.02em;color:#fff;line-height:1.05">R$ X.XXX</div>
    </div>
    <!-- KPI: Investido (gold) -->
    <!-- KPI: Vendas (var(--safe)) -->
    <!-- KPI: ROAS — cor por performance: gold se ok, care se abaixo, danger se crítico -->
    <!-- Nota rodapé separada por border-top rgba(255,255,255,0.1) -->
    <div style="margin-top:auto;padding-top:16px;border-top:1px solid rgba(255,255,255,0.1)">
      <div style="font-size:10px;color:rgba(255,255,255,0.38);line-height:1.65">
        [contexto em 1–2 linhas: diagnóstico direto]
      </div>
    </div>
  </div>

  <!-- FUNIL PRINCIPAL -->
  <div style="flex:1;padding:22px 30px;display:flex;flex-direction:column;min-width:0;">

    <!-- Header: período + título + pills de canal -->
    <div style="display:flex;justify-content:space-between;align-items:flex-start;
                margin-bottom:18px;flex-shrink:0;">
      <div>
        <div style="font-size:8px;font-weight:700;letter-spacing:0.18em;
                    text-transform:uppercase;color:rgba(255,255,255,0.5);margin-bottom:6px">
          FUNIL COMPLETO · [DD/MM] A [DD/MM/AAAA]
        </div>
        <div style="font-size:clamp(15px,2vw,22px);font-weight:700;
                    font-stretch:75%;letter-spacing:-0.02em;color:#fff;">
          INSIDE SALES — FUNIL DE CONVERSÃO
        </div>
      </div>
      <!-- Pills Google + Meta -->
    </div>

    <!-- BARRAS DO FUNIL (padrão obrigatório) -->
    <div style="flex:1;display:flex;flex-direction:column;justify-content:center;gap:0;">

      <!-- Cada estágio: [número] + [barra] -->
      <div style="display:flex;align-items:center;gap:14px;margin-bottom:3px;">
        <div style="width:46px;text-align:right;font-size:21px;font-weight:700;
                    font-stretch:75%;color:[COR_NÚMERO];flex-shrink:0;">XXX</div>
        <div style="[LARGURA];background:[COR_BARRA];border-radius:10px;
                    padding:12px 20px;font-size:12px;font-weight:700;
                    color:[TEXTO];text-align:center;letter-spacing:0.14em;">LABEL</div>
      </div>
      <!-- Nota de transição entre estágios -->
      <div style="padding:4px 0 6px 60px;font-size:10px;
                  color:[COR_NOTA];font-weight:600;letter-spacing:0.02em;">
        XX,X% Estágio A → Estágio B · [insight de 1 frase]
      </div>

    </div>
  </div>
</div>
```

**Paleta IS — estágios e números:**

| Estágio | Largura barra | `background` barra | Texto barra | Cor número |
|---------|--------------|---------------------|-------------|------------|
| LEADS | `flex:1` (100%) | `rgba(238,210,130,0.88)` | `#3A2800` | `#E8C86A` |
| WPP | `42%` | `rgba(216,88,82,0.8)` | `#fff` | `#E87878` |
| MQL | `27%` | `rgba(228,196,72,0.84)` | `#3A2800` | `#E8C86A` |
| VENDA | `27%` | `#4CAF7D` | `#fff` | `var(--safe)` |

**Cores das notas de transição:**
- Taxa ok / neutro: `rgba(255,255,255,0.48)` muted
- Atenção / intenção baixa: `rgba(255,242,0,0.75)` amarelo
- Gargalo / problema: `rgba(255,138,128,0.85)` danger
- Taxa excelente: `rgba(99,212,113,0.9)` verde

#### 1.4B Funil de Conversão — Comparativo Mês Anterior (padrão obrigatório)

**Usar quando:** o slide de funil mostra o mês mais recente comparado ao mês anterior (ex: Junho vs Maio). Aplicável a funis Google Ads, Meta Ads ou qualquer canal com dados de custo por estágio. **Este é o layout padrão para o slide de funil do mês mais recente do quarter.**

Referência viva: slide-3 do `ropre-q2-2026-comp.html` em `Clientes/Compass/checkins/`.

**Diferença do 1.4 (IS):** barras de largura fixa em pixels (não percentual), taxa de conversão na coluna esquerda da mesma linha da barra, custo com comparativo à direita. Nenhuma linha de transição separada.

**Layout split:** `slide-body` sem padding (`padding:0;overflow:hidden;display:flex`) — sidebar 220px + funil à direita.

##### Sidebar (220px, `background:rgba(20,0,0,0.62)`)

```html
<div style="width:220px;flex-shrink:0;background:rgba(20,0,0,0.62);padding:24px 18px 20px;
            display:flex;flex-direction:column;border-right:1px solid rgba(255,255,255,0.06);">
  <!-- pill do canal -->
  <div style="display:flex;align-items:center;gap:5px;background:rgba(255,255,255,0.08);
              border:1px solid rgba(255,255,255,0.12);border-radius:var(--radius-pill);
              padding:4px 10px;width:fit-content;margin-bottom:18px;">
    <svg width="12" height="12" ...><!-- SVG do canal --></svg>
    <span style="font-size:9px;font-weight:700;color:#fff;letter-spacing:0.1em">GOOGLE ADS</span>
  </div>
  <!-- KPI principal -->
  <div style="margin-bottom:18px;">
    <div style="font-size:8px;font-weight:700;letter-spacing:0.18em;text-transform:uppercase;
                color:var(--accent-gold);margin-bottom:5px">FATURADO · [MÊS]</div>
    <div style="font-size:28px;font-weight:700;font-stretch:75%;letter-spacing:-0.02em;
                color:#fff;line-height:1.05">R$XX.XXX</div>
    <div style="font-size:10px;color:rgba(255,138,128,0.75);margin-top:4px">↓ R$XX.XXX em [mês ant.]</div>
  </div>
  <!-- KPIs secundários -->
  <div style="display:flex;flex-direction:column;gap:9px;margin-bottom:18px;">
    <!-- Cada KPI: justify-content:space-between + border-bottom -->
    <!-- Investido (accent-gold) | TCV (safe) | ROAS (danger/care/safe por performance) -->
  </div>
  <!-- rodapé -->
  <div style="margin-top:auto;padding-top:14px;border-top:1px solid rgba(255,255,255,0.08);">
    <div style="font-size:9px;font-weight:700;letter-spacing:0.15em;text-transform:uppercase;
                color:rgba(255,255,255,0.28);margin-bottom:3px">COMPARAÇÃO</div>
    <div style="font-size:11px;color:rgba(255,255,255,0.46)">[Mês Atual] vs [Mês Anterior] [Ano]</div>
    <div style="font-size:10px;color:rgba(255,255,255,0.26);margin-top:3px">
      Valor atual / <span style="opacity:0.7">mês anterior</span></div>
  </div>
</div>
```

##### Área do funil

Header (margin-bottom 14px): eyebrow `FUNIL COMPLETO · [MÊS ANO]` + título `[CANAL] — FUNIL DE CONVERSÃO`.

Container das barras: `display:flex;flex-direction:column;justify-content:center;gap:6px`.

Legenda discreta antes das barras (uma linha, não conta como estágio):
```html
<div style="display:flex;align-items:center;gap:0;margin-bottom:2px;">
  <div style="width:70px;flex-shrink:0;"></div>
  <div style="font-size:8px;...;color:rgba(255,255,255,0.22);">Taxa de entrada</div>
  <div style="flex:1;"></div>
  <div style="font-size:8px;...;color:rgba(255,255,255,0.22);width:130px;">Jun · Mai · Var</div>
</div>
```

**Cada estágio = uma linha:** `[70px rate-col][Npx bar fixo][130px cost-col]`

```html
<div style="display:flex;align-items:center;gap:0;">
  <!-- COLUNA TAXA (70px) — vazia no primeiro estágio -->
  <div style="width:70px;flex-shrink:0;text-align:right;padding-right:8px;">
    <div style="font-size:11px;font-weight:700;color:[COR_TAXA];line-height:1.2;">[Taxa atual]</div>
    <div style="font-size:9px;color:rgba(255,255,255,0.30);line-height:1.2;">[Taxa prev]</div>
    <div style="font-size:7px;font-weight:700;letter-spacing:0.06em;color:[COR_LABEL];
                text-transform:uppercase;">[LABEL]</div>
  </div>
  <!-- BARRA (largura fixa) -->
  <div style="width:[N]px;flex-shrink:0;height:50px;background:[COR_BARRA];border-radius:9px;
              display:flex;align-items:center;padding:0 14px;">
    <span style="font-size:22px;font-weight:700;color:[TEXTO];letter-spacing:-0.02em;">[VOL]</span>
    <span style="font-size:8px;font-weight:700;letter-spacing:0.1em;color:[TEXTO];
                 opacity:0.4;text-transform:uppercase;margin-left:8px;">[ESTÁGIO]</span>
  </div>
  <!-- COLUNA CUSTO (130px) -->
  <div style="flex-shrink:0;padding-left:12px;width:130px;">
    <div style="font-size:11px;font-weight:700;color:#fff;">[R$ atual] <span style="font-size:8px;
         opacity:0.45;font-weight:400;">[MÉTRICA]</span></div>
    <div style="font-size:9px;color:rgba(255,255,255,0.35);">[R$ prev]</div>
    <div style="font-size:12px;font-weight:700;color:[COR_DELTA];">[±X,X%] [↑↓]</div>
  </div>
</div>
```

**Paleta de barras — funil Google Ads completo (6 estágios):**

| Estágio | Largura | Background | Texto número |
|---------|---------|------------|--------------|
| Impressões | 400px | `rgba(200,205,215,0.18)` | `rgba(255,255,255,0.85)` |
| Cliques | 356px | `rgba(175,185,200,0.18)` | `rgba(255,255,255,0.80)` |
| Leads | 268px | `rgba(238,210,130,0.82)` | `#3A2800` |
| MQL | 224px | `rgba(100,155,230,0.72)` | `#fff` |
| SQL | 176px | `rgba(228,196,72,0.78)` | `#3A2800` |
| Venda | 140px | `#4CAF7D` | `#fff` |

Para funis com menos estágios: manter as últimas N linhas da paleta e escalar proporcionalmente.

**Regra de cor do delta (coluna direita):**
- Métricas de custo (CPM, CPC, CPL, CMQL, CSQL, CAC): `var(--safe)` se ↓, `var(--danger)` se ↑
- Taxas de conversão (coluna esquerda): `var(--safe)` se ↑, `var(--danger)` se ↓
- Exceção: Close Rate (SQL→Venda) é verde se ↑

**Rodapé do funil:**
```html
<div style="display:flex;align-items:center;gap:0;padding-top:2px;">
  <div style="width:70px;flex-shrink:0;"></div>
  <div style="font-size:10px;color:rgba(255,255,255,0.38);">
    Tx. geral Lead→Venda: <span style="color:var(--danger);font-weight:700">9,1%</span>
    <span style="color:rgba(255,255,255,0.25)"> / 10,9% em [mês ant.]</span>
  </div>
</div>
```

#### 1.5 Funil de Conversão Visual — E-commerce GA4 (quando aplicável)

**Mesma estrutura split da seção 1.4, adaptada para funil GA4.**

Sidebar: Receita / Investido (breakdown por canal com dot colorido: Meta azul, Google amarelo) / Compras / ROAS

Título: `E-COMMERCE — FUNIL DE CONVERSÃO`  
Pills de canal: Meta + Google + GA4

**Paleta Ecom — estágios GA4:**

| Estágio | Largura barra | `background` barra | Texto | Cor número |
|---------|--------------|---------------------|-------|------------|
| SESSÕES | `flex:1` | `rgba(140,185,245,0.82)` | `#0a1a35` | `#B8D8FF` |
| VIEW ITEM | `52%` | `rgba(100,155,230,0.78)` | `#fff` | `#B8D8FF` |
| ADD TO CART | `34%` | `rgba(238,195,72,0.82)` | `#3A2800` | `var(--accent-gold)` |
| CHECKOUT | `24%` | `rgba(216,110,60,0.8)` | `#fff` | `var(--care)` |
| PURCHASE | `14%` | `#4CAF7D` | `#fff` | `var(--safe)` |

Após PURCHASE, adicionar inline a taxa de conversão geral:
```html
<div style="font-size:10px;color:rgba(255,255,255,0.45);white-space:nowrap;">
  Tx. Conversão Geral: <span style="color:var(--danger);font-weight:700">X,XX%</span>
</div>
```

**ROAS na sidebar por performance:**
- ≥ meta estabelecida → `var(--safe)` verde
- Abaixo da meta mas ≥ 1 → `var(--care)` amarelo
- < 1 (gastando mais do que receita) → `var(--danger)` vermelho

#### 1.6 Performance por Canal

Dentro de `glass-card`, 2 colunas:
- Esquerda: donut Chart.js com distribuição percentual de budget por canal
- Direita: cards empilhados por canal — nome + tipo + métrica principal + alerta em danger quando anomalia

#### 1.7 Criativos Vencedores

Avaliar criativos por **eficiência** (CPL / CTR / taxa de conversão), não apenas por volume de leads. Um criativo com CPL 40% abaixo da média é mais relevante do que um com mais leads absolutos.

Duas camadas:
1. **3 pills de resumo** (Total Leads, Investimento, CPL Médio)
2. **Grid de cards por criativo** — preview visual + código + métricas 2×2

Card vencedor: `border: 1px solid rgba(255,212,138,0.4)` + badge "MAIS EFICIENTE" (ou "MAIS LEADS" se eficiência for similar)

Métricas por célula: LEADS (dourado se melhor) · CPL (verde se melhor) · CTR · INVESTIDO

**Insight obrigatório por criativo destacado:**
```html
<div style="font-size:10px;color:var(--accent-gold);margin-top:6px;font-style:italic;
            border-top:1px solid rgba(255,212,138,0.15);padding-top:6px;">
  "[Por que este criativo se destacou: gancho, formato, público, contexto específico]"
</div>
```

#### 1.8 Projetado × Realizado — Último Mês do Quarter

Tabela: MÉTRICA | PESSIMISTA | DESEJADO | OTIMISTA | REALIZADO

Coluna REALIZADO colorida por desempenho vs cenários (verde/amarelo/vermelho).
Lógica invertida para métricas onde menos é melhor (CPL, CPM, Custo por MQL).

Após a tabela, incluir bloco de diagnóstico executivo (ver Princípios de Qualidade — Bloco de contexto).

#### 1.9 Projeção para o Próximo Quarter

Tabela: MÉTRICA | DESEJADO MÊS1 | DESEJADO MÊS2 | DESEJADO MÊS3 | DESEJADO Q[N]

Coluna Q Total em bold, fundo levemente diferenciado.

#### 1.10 Palavras-chave Google Ads (quando Google Ads ativo)

Header com número watermark + 4 pills de resumo + tabela de keywords.

Status das keywords: pill "Qualificada" (safe) · "Lim. qualidade" (care) · "Não qualificada" (muted)

#### 1.11 Testes e Aprendizados do Quarter

Incluir apenas aprendizados com **conclusão real** no quarter. Iniciativas ainda em andamento pertencem ao 5W1H, não aqui.

Tabela: Teste / Iniciativa | Status | Insight | Decisão Q[próximo]

Cada linha deve ter:
- **Insight:** o que este resultado nos ensinou (frase direta, não "foi testado e os resultados foram...")
- **Decisão:** pill de ação obrigatório

Pills de ação para Q[próximo]: **ESCALAR** (safe verde) · **MANTER** (gold) · **MONITORAR** (care) · **IMPLEMENTAR** (`rgba(100,180,255,0.2)` azul claro) · **PAUSAR** (muted)

Usar `action-pill` + classe por ação. Adicionar botão "↗ Ver Estratégia" inline quando houver link de estratégia associado ao teste.

---

### 02 — OBJETIVOS (O)

#### 2.1 Review das OKRs do Quarter Passado

Para cada KR: Meta definida → Resultado atingido → Status (Atingido / Parcial / Não atingido)
KR não atingida: incluir como prioridade no Q seguinte.

Layout: slide com coluna de OKRs (esquerda) + linha bezier SVG + KRs com status (direita).

#### 2.2 Step do Projeto

- **V0 — Fundação:** sem estrutura digital. Objetivo: checklist V4 + cliente
- **V1 — Encontrando:** sem indicadores claros. Objetivo: mapear CPL/CMQL/CPVenda, atingir breakeven
- **V2 — Maturando:** indicadores estabelecidos. Objetivo: otimizar taxas de conversão
- **V3 — Escalando:** 6+ meses de dados. Objetivo: escalar faturamento com previsibilidade

#### 2.3 Novo Objetivo SMART + KRs

```
Em 3 meses, [ação estratégica focada em faturamento/receita],
atingindo [meta quantificada] até [mês de fechamento do quarter].

KR 1: [topo de funil — leads, alcance, volume]
KR 2: [meio de funil — MQLs, taxas, engajamento]
KR 3: [fundo de funil — vendas, faturamento, ROAS]
```

#### 2.4 Projeção do Próximo Quarter

3 cenários (Pessimista / Desejado / Otimista) baseados no histórico do próprio cliente.

#### 2.5 Drawflow (quando cliente tem funil mapeado)

Diagrama visual do fluxo completo de conversão — IS e/ou Ecom. Ver implementação de referência no slide-15/16 do Alquilab.

#### 2.6 Plano de Mídia Q[próximo]

Tabela de distribuição de verba por canal + objetivo por canal no quarter.

#### 2.7 Breakeven (quando cliente ainda não atingiu)

Curva de crescimento + ponto de equilíbrio projetado com base em margem de contribuição + fee V4 + investimento.

---

### 03 — PREMISSAS E RISCOS (P)

**Tom:** consultivo, não acusatório.

**Layout:** cards clicáveis + régua de risco interativa.

- 2 riscos → 2 cards lado a lado (max-width ~460px por card, `align-items:stretch` para equalizar altura)
- 3 riscos → 3 cards lado a lado
- Nunca forçar um card vazio para "completar" o layout

Cada card tem:
- Título da premissa
- Causa / Risco / Efeito
- Pontuação P × I (probabilidade × impacto, escala 1–10)
- Clicar no card move a régua para o score do card (animação CSS `bottom: score%`)

**Régua interativa (gauge):**
- Barra vertical `position:relative` com needle `position:absolute;bottom:0`
- JS: `needle.style.bottom = score + '%'` + cor dinâmica (safe/care/danger por faixa)
- Inicializar no primeiro card via `setTimeout(80ms)` após DOM renderizado
- Scores: 0–19 → safe (Aceitar) · 20–49 → care (Mitigar) · 50+ → danger (Prevenir ou Transferir)

Equalizar altura dos cards com `align-items:stretch` no container flex, não `align-items:center`.

**Premissas típicas:**
- Verba e meio de pagamento disponíveis
- Aprovação ágil de materiais (SLA 48h)
- Alimentação correta do CRM
- Boas práticas de atendimento dos leads

Adicionar premissas específicas do contexto do cliente.

---

### 04 — ENTREGAS (E)

#### 4.1 Entregas Realizadas

Subtítulo fixo: **"Tudo que foi feito em Q[N]."**

Listar por mês: usar grade de 3 colunas (uma por mês) quando houver 3 meses no quarter. Cada item usa:
```html
<div class="entrega-item">
  <div class="entrega-dot"></div>
  <div class="entrega-text">
    <span style="font-size:10px;color:var(--text-muted);margin-right:4px">DD/mmm</span>
    <span class="entrega-tag">SIGLA</span>
    Descrição da entrega
  </div>
</div>
```

Fonte dos dados: Ekyte (tarefas concluídas por mês, via MCP ou screenshot). Listar exatamente as entregas realizadas — não resumir nem parafrasear.

#### 4.2 Planos de Ação Realizados (Testes)

Usar a mesma tabela de testes (seção 1.11) mas com foco nas iniciativas concluídas. Incluir botão "↗ Ver Estratégia" quando houver documento vinculado.

#### 4.3 Account Planning — Expansão

White spaces: oportunidades identificadas no quarter para o cliente crescer com novos serviços V4.

Referência: https://portfolio.v4company.com/

Exemplos: SEO/GEO · CRM + automação · Social Media · Produção de vídeo · Inbound/conteúdo

---

### 05 — PRÓXIMOS PASSOS

#### 5.1 Plano de Ação 5W1H

**Implementação obrigatória: `<table>` HTML — nunca cards, lista ou grid.**

Colunas: `#` | O QUÊ | QUANDO | QUEM | COMO

Quantidade de linhas: variável, sem limite. Incluir todas as ações do trimestre (julho, agosto, setembro) em uma única tabela ordenada por data.

Padding das células por quantidade de linhas:
- ≤ 5 linhas: `padding:12px 14px`
- 6–8 linhas: `padding:9px 12px`
- 9–12 linhas: `padding:7px 12px`
- 13+ linhas: `padding:5px 10px;font-size:11px`

QUANDO colorido por urgência:
- Mês 1 do quarter / urgente → `var(--safe)` verde
- Mês 2 do quarter → `var(--accent-yellow)` amarelo
- Mês 3 do quarter / prazo longo → `var(--text-muted)` branco/muted

```html
<div class="slide-body" style="overflow:hidden;">
  <div class="eyebrow">Plano de Ação 5W1H</div>
  <div class="section-title" style="margin-bottom:14px;">O que acontece agora</div>
  <div class="glass-card" style="padding:0;overflow:hidden;flex:1;display:flex;flex-direction:column;">
    <table style="width:100%;border-collapse:collapse;">
      <thead>
        <tr>
          <th style="background:rgba(0,0,0,0.3);padding:8px 12px;font-size:9px;font-weight:700;
                     letter-spacing:0.14em;text-transform:uppercase;color:var(--accent-gold);
                     text-align:left;width:4%">#</th>
          <th style="...;width:24%">O Quê</th>
          <th style="...;width:10%">Quando</th>
          <th style="...;width:14%">Quem</th>
          <th style="...">Como</th>
        </tr>
      </thead>
      <tbody>
        <!-- N linhas — quantidade conforme o plano real do trimestre -->
        <tr>
          <td style="padding:[P];font-size:11px;border-bottom:1px solid var(--line);
                     color:var(--accent-gold);font-weight:700">01</td>
          <td style="padding:[P];font-size:12px;border-bottom:1px solid var(--line);
                     font-weight:700">[O quê]</td>
          <td style="padding:[P];font-size:11px;border-bottom:1px solid var(--line);
                     color:[COR_QUANDO];font-weight:700">[Quando]</td>
          <td style="padding:[P];font-size:11px;border-bottom:1px solid var(--line);
                     color:var(--text-muted)">[Quem]</td>
          <td style="padding:[P];font-size:11px;border-bottom:1px solid var(--line);
                     color:var(--text-muted)">[Como]</td>
        </tr>
        <!-- última linha sem border-bottom -->
      </tbody>
    </table>
  </div>
</div>
```

#### 5.2 NPS

Card com eyebrow "NPS" + botão dourado pill "→ Acessar pesquisa" abrindo em nova aba.
Se não houver link, usar `href="#"` + comentário HTML `<!-- INSERIR LINK NPS -->`.

---

## Arquitetura Slideshow (obrigatória)

### Estrutura CSS base

```css
/* Reset */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html, body { width: 100%; height: 100%; overflow: hidden; background: var(--bg-depth); }

/* Deck wrapper */
.deck { position: fixed; inset: 0; }

/* Slides — opacity-based (não display:none) */
.slide {
  position: absolute; inset: 0;
  display: flex; flex-direction: column;
  opacity: 0; pointer-events: none;
  transition: opacity 0.45s ease, transform 0.45s ease;
}
.slide.active { opacity: 1; pointer-events: auto; }

/* Header por slide */
.slide-header {
  display: flex; align-items: center; justify-content: space-between;
  padding: 14px 32px; border-bottom: 1px solid var(--line);
  background: rgba(0,0,0,0.2); backdrop-filter: blur(8px);
  flex-shrink: 0;
}

/* Body por slide */
.slide-body {
  flex: 1; overflow-y: auto; overflow-x: hidden;
  padding: 28px 40px 80px;
}

/* Para slides full-bleed (funil, drawflow) — override no inline: */
/* style="padding:0;overflow:hidden;display:flex;" */
```

### Estrutura HTML de cada slide

```html
<div class="slide" id="slide-N">
  <div class="slide-header">
    <div class="brand">
      <img src="./assets/v4-company-logo-branca-oficial.svg" alt="V4" style="height:20px">
      <span class="brand-title">[Seção] · [Subtítulo]</span>
    </div>
    <div class="slide-nav-pills">
      <span class="nav-pill [active]" onclick="goToSlide(1)">01 Resultados</span>
      <span class="nav-pill" onclick="goToSlide(X)">02 Objetivos</span>
      <span class="nav-pill" onclick="goToSlide(X)">03 Premissas</span>
      <span class="nav-pill" onclick="goToSlide(X)">04 Entregas</span>
      <span class="nav-pill" onclick="goToSlide(X)">05 Próximos Passos</span>
    </div>
  </div>
  <div class="slide-body">
    <!-- EYEBROW: nunca incluir prefixo numérico (01.1 ·, 05.1 · etc.) -->
    <div class="eyebrow">Subtítulo da Subseção</div>
    <div class="section-title">Frase de impacto.<br>Em duas linhas.</div>
    <!-- conteúdo do slide -->
  </div>
</div>
```

**Regras:**
- Nav pill da seção atual recebe classe `active` (dourado)
- O `goToSlide(X)` de cada pill aponta para o **primeiro slide da seção**
- `const TOTAL = N;` deve ser atualizado sempre que slides forem adicionados ou removidos
- Slides usam `id="slide-0"`, `id="slide-1"` ... `id="slide-N"`
- **Eyebrow nunca recebe prefixo numérico** — identificação de seção fica no `brand-title` do header

### JS de navegação

```javascript
const TOTAL = N; // atualizar ao adicionar/remover slides
let current = 0;

function goToSlide(n) {
  if (n < 0 || n >= TOTAL || n === current) return;
  document.getElementById('slide-' + current).classList.remove('active');
  document.getElementById('slide-' + n).classList.add('active');
  current = n;
  updateDots();
}

function navigate(dir) { goToSlide(current + dir); }

// Setas do teclado
document.addEventListener('keydown', e => {
  if (e.key === 'ArrowRight') navigate(1);
  if (e.key === 'ArrowLeft')  navigate(-1);
});

// Swipe touch (threshold 50px)
let touchStartX = 0;
document.addEventListener('touchstart', e => { touchStartX = e.touches[0].clientX; });
document.addEventListener('touchend', e => {
  const dx = e.changedTouches[0].clientX - touchStartX;
  if (Math.abs(dx) > 50) navigate(dx < 0 ? 1 : -1);
});

// Dots
function updateDots() {
  document.querySelectorAll('.dot').forEach((d, i) => {
    d.classList.toggle('active', i === current);
  });
}
function buildDots() {
  const wrap = document.getElementById('dots');
  for (let i = 0; i < TOTAL; i++) {
    const d = document.createElement('span');
    d.className = 'dot' + (i === 0 ? ' active' : '');
    d.onclick = () => goToSlide(i);
    wrap.appendChild(d);
  }
}
document.addEventListener('DOMContentLoaded', () => {
  buildDots();
  document.getElementById('slide-0').classList.add('active');
});
```

### Setas e dots (HTML fixo)

```html
<!-- Posição fixa, fora dos slides -->
<button class="nav-arrow prev" onclick="navigate(-1)">←</button>
<button class="nav-arrow next" onclick="navigate(1)">→</button>
<div class="dots-wrap" id="dots"></div>
```

### Chart.js — inicialização lazy

Não inicializar gráficos em slides `opacity:0` — o canvas não tem dimensão. Usar flag:

```javascript
let chartsInited = false;
const CHART_SLIDE = N; // índice do slide com gráficos

// Dentro do goToSlide, após trocar o slide:
if (current === CHART_SLIDE && !chartsInited) {
  initCharts();
  chartsInited = true;
}
```

---

## Gestão de Slides por Python (ao inserir ou remover slides)

Quando for necessário inserir ou deletar slides no meio do deck (não apenas no final), usar script Python para renumerar com segurança. **Nunca fazer substituição manual** — erros de numeração quebram a navegação.

### Padrão de inserção de novo slide após slide-N

```python
import re, sys
sys.stdout.reconfigure(encoding='utf-8')

path = r'c:\...\ropre-q[N]-[ANO]-[sigla].html'
with open(path, 'r', encoding='utf-8') as f:
    content = f.read()

# 1) Renumerar ids >= PONTO_DE_INSERÇÃO + 1
INSERIR_APOS = N  # número do slide APÓS o qual inserir
def shift_ids(m):
    n = int(m.group(1))
    return f'id="slide-{n+1}"' if n > INSERIR_APOS else m.group(0)
content = re.sub(r'id="slide-(\d+)"', shift_ids, content)

# 2) Atualizar goToSlide(X) nas nav pills, do maior para o menor
# (evita conflito: goToSlide(20) → 21 antes de goToSlide(19) → 20)
nav_map = [
    ('onclick="goToSlide(20)">05 Próximos Passos', 'onclick="goToSlide(21)">05 Próximos Passos'),
    ('onclick="goToSlide(19)">04 Entregas',          'onclick="goToSlide(20)">04 Entregas'),
    # ... continuar do maior para o menor
]
for old, new in nav_map:
    content = content.replace(old, new)

# 3) Atualizar TOTAL
content = content.replace(f'const TOTAL = {TOTAL_ANTES};', f'const TOTAL = {TOTAL_ANTES + 1};')

# 4) Inserir novo slide antes do slide agora renumerado (INSERIR_APOS + 2)
NEW_SLIDE = '''<!-- HTML do novo slide aqui -->'''
marker = f'<div class="slide" id="slide-{INSERIR_APOS + 2}">'
idx = content.find(marker)
content = content[:idx] + NEW_SLIDE + content[idx:]

with open(path, 'w', encoding='utf-8') as f:
    f.write(content)
```

**Regras do script:**
- Processar substituições de goToSlide **sempre do maior para o menor** número
- Testar com `grep 'id="slide-' arquivo.html | wc -l` que o total de slides está correto após o script
- Após qualquer script, conferir `const TOTAL` e os goToSlide das nav pills de cada seção

---

## Slide de Capa (slide-0 — obrigatório)

```
eyebrow:  R · O · P · R · E  ·  Q[N] [ANO]  ·  [NomeCliente]
título:   CHECK IN
          QUARTER
```

- Título em `clamp(60px, 11vw, 128px)`, `font-stretch: 75%`, `letter-spacing: -.04em`
- Layout 2 colunas: esquerda (eyebrow + título + subtexto com vitória principal) · direita (card com 3 métricas-chave do quarter)
- Watermark decorativa "Q[N]" enorme e opaca no fundo: `color: rgba(255,255,255,0.04)`
- **Não usar a métrica como título** — "CHECK IN QUARTER" é fixo; a vitória vai no subtexto

---

## Ordem Sugerida de Slides

Esta é a **ordem de referência**, não um template rígido. Adicionar, remover ou reordenar slides conforme os canais, dados disponíveis e necessidade narrativa de cada cliente. O que importa é que as 5 seções (R/O/P/E + Próximos) apareçam nessa ordem e que os goToSlide nas nav pills reflitam os índices reais.

```
slide-0:  Capa
─── SEÇÃO 01 · RESULTADOS ──────────────────────────────────────────
slide-1:  Grade Visual Mensal
slide-2:  Gráficos (Chart.js)
slide-3:  Comparativo de Quarters
slide-4:  Funil IS — [mês mais recente]        (se IS ativo)
slide-5:  Funil Ecom GA4 — [mês mais recente]  (se Ecom ativo)
slide-6:  Criativos Vencedores IS               (se IS ativo)
slide-7:  Criativos Vencedores Ecom             (se Ecom ativo)
slide-8:  Projetado × Realizado
slide-9:  Projeção Q[próximo]
slide-10: Plano de Ação Q[próximo] · Mês 1     (1 slide por mês)
slide-11: Plano de Ação Q[próximo] · Mês 2
slide-12: Plano de Ação Q[próximo] · Mês 3
─── SEÇÃO 02 · OBJETIVOS ───────────────────────────────────────────
slide-13: OKRs Review                           ← nav pill "02 Objetivos"
slide-14: OKRs Q[próximo]
slide-15: Drawflow IS                           (se IS ativo)
slide-16: Drawflow Ecom                         (se Ecom ativo)
slide-17: Plano de Mídia Q[próximo]
─── SEÇÃO 03 · PREMISSAS ───────────────────────────────────────────
slide-18: Premissas e Riscos                    ← nav pill "03 Premissas"
─── SEÇÃO 04 · ENTREGAS ────────────────────────────────────────────
slide-19: Entregas Q[passado]                   ← nav pill "04 Entregas"
─── SEÇÃO 05 · PRÓXIMOS PASSOS ─────────────────────────────────────
slide-20: 5W1H Plano de Ação                    ← nav pill "05 Próximos Passos"
slide-21: NPS
```

**Variações comuns:**
- Cliente só IS (sem Ecom): remover slides 5 e 7 → deck fica com ~19 slides
- Cliente só Ecom (sem IS): remover slides 4 e 6 → deck fica com ~19 slides
- Cliente sem drawflow mapeado: remover slides 15 e 16 → saltar de OKRs para Plano de Mídia
- Cliente com Google Ads: adicionar slide de Palavras-chave após Criativos Ecom
- Cliente com Social Media ativo: adicionar slide de Métricas Social após Criativos

Após qualquer adição ou remoção, atualizar `const TOTAL` e os `goToSlide(N)` de todos os slides via script Python.

---

## Tom de Voz

Consultivo · Estratégico · Confiante · Empático · Narrativo

**Preferir:**
- "No Q[N], construímos a fundação. No Q[N+1], vamos maturar os indicadores."
- "A curva de crescimento está fazendo sentido — evoluímos X% Q-over-Q."
- "Identificamos onde o gargalo está concentrado e temos um plano para isso."
- "Para o próximo quarter, o foco único é [objetivo]."
- "O que ainda falta para converter é [ação específica e acionável]."
- "O placar mudou. Aqui está o porquê."
- "O esforço ainda não virou rotina."
- "Onde a cobrança ainda precisa acontecer."

**Evitar:** "Os resultados do trimestre foram..." / "Durante este período..." / "Análise detalhada..." / "Dashboard de acompanhamento." / "Visão geral dos dados."

---

## Regras de Ouro

1. Nunca levar resultado ruim sem plano de ação
2. Nunca levar resultado bom sem estratégia de continuidade/escala
3. O ROPRE é replanejamento, não relatório — é tomada de decisão para 3 meses
4. Antecipe datas e entregas — se o cliente cobrou, já está atrasado
5. Incluir stakeholder-chave — convidar o dono do contrato
6. Tudo alinhado no ROPRE vai para o Cockpit — sem isso, o plano se perde
7. NPS mensal: coletar sempre durante a call
8. Enviar ata após a reunião — e-mail + WhatsApp com combinados, prazos e responsáveis

---

## Fluxo de Geração

### Passo 0 — Definir o modelo do cliente (obrigatório antes de qualquer HTML)

Responder as 5 perguntas da seção "Variações por Cliente":
1. Logo do cliente — existe asset? Qual caminho?
2. Tem Social Media? (sim/não)
3. Tem Inside Sales? (sim/não)
4. Tem E-commerce? (sim/não)
5. Investe em quais canais? (Meta / Google / TikTok / outro)

Com base nas respostas, montar o **mapa de slides** (lista numerada de slide-0 a slide-N) antes de escrever o HTML. Isso evita renumeração posterior.

### Passo 1 — Entender o contexto

- Cliente e sigla
- Quarter e ano (ex: Q2 2026 = Abr/Mai/Jun)
- Step atual (V0/V1/V2/V3)
- Dados disponíveis (Growth Pack, Cockpit, CRM, Ads, GA4, Ekyte)

### Passo 2 — Coletar dados

Buscar via MCP (Growth Pack, Cockpit, Ekyte) ou solicitar ao usuário:
- Métricas dos 3 meses
- OKRs do quarter passado + resultados reais
- Lista de entregas (Ekyte) — listar exatamente como vieram, sem resumir
- Criativos vencedores com métricas
- **Perguntar:** "Quais dados quer destacar em gráfico?" (faturamento mês a mês, funil Q-over-Q, leads vs MQL, ROAS)
- **Perguntar:** "Tem o link da pesquisa de NPS?" — se sim, usar no botão da seção 5.2; se não, `href="#"`
- Se IS ativo: dados de Leads / WPP / MQL / Venda + taxas por mês
- Se Ecom ativo: GA4 — Sessões / View Item / Add to Cart / Checkout / Purchase + Receita por mês

### Passo 3 — Análise e síntese

1. Calcular consolidado do quarter (soma e médias dos 3 meses)
2. Comparar com quarter anterior (delta %)
3. Identificar indicadores com variação > 15% → preparar bloco de contexto
4. Avaliar cada KR: atingida / parcial / não atingida
5. Identificar gargalo principal do funil (IS e/ou Ecom)
6. Definir Objetivo SMART + 3–5 KRs para próximo quarter
7. Montar projeção com 3 cenários baseados em histórico
8. Listar apenas premissas/riscos ativos e relevantes (2 ou 3, não forçar quantidade)
9. Organizar entregas por mês (dados do Ekyte, na íntegra)
10. Mapear white spaces para Account Planning
11. Identificar aprendizados com conclusão real (não iniciativas em andamento)

### Passo 4 — Gerar HTML

Acionar skill `/frontend-design` com Design System V4 — Red Command Center.

Seguir a arquitetura documentada neste skill. Para cada slide:
- Copiar o padrão `slide-header` + `slide-body` do Alquilab
- Manter nav pills com goToSlide corretos para os índices reais do deck deste cliente
- **Eyebrows: nunca incluir prefixo numérico**
- Slides de funil (IS e Ecom): usar `padding:0;overflow:hidden;display:flex` no slide-body
- Slides padrão: usar `padding: 28px 40px 80px` do CSS base
- Slides com muitos itens (entregas, 5W1H com 10+ linhas): verificar aproveitamento de espaço e ajustar padding/font-size

### Passo 5 — Deploy

```bash
cd clientes/[cliente]/checkins
cp ropre-q[N]-[ANO]-[sigla].html index.html
vercel --prod --yes
vercel alias set <deployment-url> checkin-q[N]-[sigla-cliente].vercel.app
```

Confirmar via WebFetch que a URL retorna 200 antes de enviar ao cliente.

---

## Checklist Final

- [ ] Consolidado dos 3 meses calculado
- [ ] Comparativo com quarter anterior (delta %)
- [ ] Indicadores com variação > 15% têm bloco de contexto/diagnóstico
- [ ] Cada KR passada avaliada com honestidade
- [ ] Objetivo SMART correto (específico, mensurável, temporal, focado em receita)
- [ ] Projeção com 3 cenários baseados em dados históricos
- [ ] Step do projeto correto e explicado
- [ ] Premissas/riscos: apenas os relevantes, 2 ou 3 cards (não forçar terceiro vazio)
- [ ] Cards de premissas com `align-items:stretch` para equalizar altura
- [ ] Funil do mês mais recente usa layout 1.4B (barras px fixos, taxa na linha, custo à direita, gap:6px)
- [ ] Funil IS com split layout (se canal IS ativo e sem comparativo de mês)
- [ ] Funil Ecom GA4 com split layout (se canal Ecom ativo e sem comparativo de mês)
- [ ] ROAS da sidebar colorido por performance (safe/care/danger)
- [ ] Delta de custo verde se ↓, vermelho se ↑ (lógica invertida vs volume)
- [ ] Criativos avaliados por eficiência + insight de 1 linha por card destacado
- [ ] Tabela de Testes: apenas aprendizados concluídos, cada linha tem insight + decisão
- [ ] Tabela de Testes com action-pills corretos (ESCALAR/MANTER/MONITORAR/IMPLEMENTAR/PAUSAR)
- [ ] Botões "↗ Ver Estratégia" vinculados nos testes com documento associado
- [ ] Entregas listadas por mês com dados reais do Ekyte (data + sigla + descrição)
- [ ] Entregas em grade 3 colunas (uma por mês)
- [ ] 5W1H implementado como `<table>` HTML (nunca cards)
- [ ] 5W1H com todas as ações do trimestre (sem limite de linhas)
- [ ] 5W1H com QUANDO colorido por urgência
- [ ] 5W1H com padding das células ajustado conforme número de linhas
- [ ] NPS com botão dourado (link ou `href="#"` com comentário)
- [ ] **Nenhum eyebrow contém prefixo numérico** (01.1 ·, 05.1 · etc.)
- [ ] Slides sem espaços vazios relevantes — layout ajustado para ocupar o espaço
- [ ] HTML segue Design System V4 — Red Command Center
- [ ] Slides com `position:absolute;opacity:0` + `.active {opacity:1}` (não display:none)
- [ ] Nav pills por slide (não header global) com `goToSlide(N)` corretos
- [ ] `const TOTAL = N` atualizado
- [ ] Chart.js lazy init (só ao entrar no slide de gráficos)
- [ ] Slides full-bleed (funil, drawflow) com `padding:0;overflow:hidden;display:flex` no slide-body
- [ ] Capa com "CHECK IN QUARTER" fixo + eyebrow com R·O·P·R·E·Q[N]
- [ ] `ropre-q[N]-[ANO]-[sigla].html` salvo em `clientes/[cliente]/checkins/`
- [ ] `index.html` copiado do arquivo principal
- [ ] `assets/v4-company-logo-branca-oficial.svg` presente
- [ ] Deploy `vercel --prod --yes` + alias `checkin-q[N]-[sigla-cliente].vercel.app`
- [ ] URL confirmada via WebFetch (200) antes de enviar ao cliente
