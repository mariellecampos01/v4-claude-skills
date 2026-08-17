# Estrutura Detalhada das Seções do Check-in

## Resultado Geral

**Presente em:** todos os clientes

### Campos obrigatórios
- Meta do mês (valor ou volume)
- Realizado (valor ou volume)
- % de atingimento
- Investimento total em mídia
- ROAS ou ROI (se aplicável)
- Comparativo MoM (mês anterior)

### Campos opcionais
- Comparativo YoY (mesmo mês ano anterior)
- Projeção de fechamento (se mês ainda em curso)

### Tom editorial
- Acima de 100%: celebrar com clareza, não exagerar
- Entre 80–99%: "sólido" ou "em ritmo", mostrar trajetória
- Abaixo de 80%: nomear o gap sem alarmar, focar nos próximos passos

---

## Funil de Vendas (Sales)

**Presente em:** clientes com operação inside sales / SDR / closer

### Campos obrigatórios
- Leads gerados (total do mês)
- MQLs (leads qualificados pelo marketing)
- SQLs (leads aceitos pelo comercial)
- Propostas enviadas
- Vendas fechadas
- Taxa de conversão entre cada etapa

### Campos opcionais
- Ciclo médio de vendas (dias)
- Ticket médio
- CAC (custo de aquisição)
- LTV estimado

### Lógica de análise
Identificar qual etapa do funil tem a maior perda proporcional. Nomear o gargalo na narrativa.

### Notas de rodapé
Se alguma métrica do funil tiver visibilidade limitada (ex: filiais reportam só fechamentos, não propostas enviadas; CRM descontinuado), marcar o rótulo da métrica com `*` e adicionar nota discreta na base do slide. Ver padrão de nota em `SKILL.md § Fase 3`.

---

## Funil E-commerce

**Presente em:** clientes com loja virtual (Shopify, WooCommerce, VTEX etc.)

### Campos obrigatórios
- Sessões no site
- Taxa de conversão (sessões → pedidos)
- Pedidos realizados
- Receita total
- Ticket médio
- Taxa de abandono de carrinho

### Campos opcionais
- Receita por canal (orgânico, pago, email, direto)
- Produtos mais vendidos (top 3)
- Receita de clientes recorrentes vs. novos

---

## Projeção do Mês

**Presente em:** todos os clientes

### Cálculo padrão
```
Pace esperado = (dias úteis transcorridos / dias úteis totais) × meta
Projeção de fechamento = (realizado / dias transcorridos) × dias totais
```

### Campos a apresentar
- Pace atual (% do mês transcorrido vs. % da meta atingida)
- Projeção de fechamento no ritmo atual
- O que precisa acontecer para bater a meta (se abaixo do pace)

---

## Propostas / Pipeline

**Presente em:** clientes com operação sales

### Campos obrigatórios
- Propostas em aberto (volume e valor total)
- Propostas enviadas no mês
- Propostas ganhas no mês
- Propostas perdidas no mês (com motivo, se disponível)

### Fonte
Planilha de backup de leads ou CRM do cliente (RD Station, Pipedrive, HubSpot).

---

## Performance de Mídia

**Presente em:** todos os clientes com mídia paga ativa

### Meta Ads
- Investimento
- Impressões
- Cliques
- CTR
- CPL ou CPA
- ROAS (e-commerce) ou CPL (lead gen)

### Google Ads
- Investimento
- Impressões
- Cliques
- CTR
- CPC médio
- Conversões
- CPL ou CPA

### Comparativo MoM obrigatório para cada canal ativo

---

## Plano de Mídia Mensal

**Presente em:** clientes que têm `plano_midia_url` no `CLAUDE.md`

### Estrutura
Um parágrafo descritivo (2–3 frases) explicando a lógica do mix de canais do mês — por que o peso está distribuído dessa forma entre Google e Meta. Foco em estratégia, não em números (os números já aparecem em Performance de Mídia).

Seguido de um botão CTA dourado ("Acessar plano") apontando para o `plano_midia_url`.

### Tom
"Google captura quem já busca. Meta constrói presença e gera os leads mais qualificados." — frase de ancoragem que orienta o raciocínio antes do botão.

### Posição no deck
Slide logo após "Performance de Mídia" e antes de "Melhores Criativos".

---

## Melhores Criativos | Meta Ads

**Presente em:** clientes com Meta Ads ativo quando o usuário fornecer os dados de performance por criativo

### Dados necessários (pedir ao usuário)
Para cada criativo: nome/código (ex: AD01, AD02, AD03), leads gerados, CTR, CPL, valor investido.

### Estrutura visual
**Barra de resumo** (acima dos cards): 3 métricas agregadas — Total de Leads, Investimento Total, CPL Médio.

**Cards de criativos** em grid 3 colunas iguais (`grid-template-columns: repeat(3, 1fr)`):
- Imagem do criativo: `aspect-ratio: 4/5; overflow: hidden; object-fit: cover` — sem lightbox, sem overlay, sem hover scale
- Badge "Mais leads" no card campeão (mais leads gerados), com borda dourada
- Métricas em grid 2×2: Leads (destaque amarelo) · CPL (verde ou amarelo conforme abaixo da meta) · CTR · Investido

**Regra dos cards:** todos os 3 cards têm a mesma largura — nunca aumentar o campeão.

### Tom editorial
Nomear o criativo campeão no eyebrow da seção: "AD03 concentrou 79% dos leads." O restante da análise fica nos cards.

### Critério de destaque por métrica
- Leads: `--accent-yellow` (amarelo)
- CPL abaixo da média: `--safe` (verde)
- CPL acima da média: `--care` (amarelo)
- CTR e Investido: texto muted padrão

---

## Top 3 Impulsionamentos (Posts Pagos)

**Presente em:** clientes com Social Media + impulsionamentos ativos, quando o usuário fornecer dados e imagens dos posts

### Dados necessários (pedir ao usuário)
Para cada post: nome/título, formato (REELS, CARROSSEL, FOTO), link do Instagram, métricas (investimento, seguidores ganhos, visitas ao perfil, custo por seguidor), e a imagem/frame do post em `assets/vencedores/`.

### Estrutura visual — barra de resumo (topo do slide)
3 stats compactos lado a lado: Total Investido · Seguidores Ganhos · Custo Médio/Seg.

### Estrutura visual — cards (grid 3 colunas)

**Layout split horizontal dentro de cada card:**
- Thumbnail à esquerda: `width: 55%`, `object-fit: cover`, `border-radius: 12px`
- Sidebar KPIs à direita: `flex: 1`, coluna com 4 linhas (Investimento · Seguidores · Visitas · Custo/Seg.)

**Header do card:** medalha (🥇🥈🥉) + nome do post + badge de formato (REELS/CARROSSEL/FOTO) + link externo (↗)

**Ranking por seguidores ganhos** (métrica principal). Medalha 🥇 = mais seguidores.

**Destaque de Seguidores:** usar `flex: 1.5` (maior) + `background: rgba(99,212,113,.09)` + `border-bottom: rgba(99,212,113,.15)` para o card com mais seguidores (geralmente o 🥇).

**Destaque de Custo/Seg.:** usar `background: rgba(255,212,138,.08)` dourado no card com melhor custo/seg (pode ser qualquer posição).

**Seguidores no card 2 e 3:** fundo mais fraco (`rgba(99,212,113,.05)`) para diferenciar do campeão.

### Imagens
Copiar para `assets/vencedores/` (dentro da pasta de deploy do cliente). Usar `object-position: center center` para frames verticais de Reels.

### Verificação do ranking
Sempre conferir: o card de maior posição (🥇) deve ter MAIS seguidores que o 🥈, e o 🥈 mais que o 🥉. Erros de ranking invalidam o slide.

---

## Palavras-chave | Google Ads

**Presente em:** clientes com Google Ads ativo e dados de conversão disponíveis por keyword

### Fonte
Screenshot do painel Google Ads (aba Palavras-chave) ou export CSV enviado pelo usuário. Pedir se não recebeu antes de montar a seção.

### Barra de resumo (acima da tabela)
3 métricas agregadas: Total de Conversões · Total de Cliques · CPA Médio

### Tabela principal
Colunas: Palavra-chave · Impressões · Cliques · CTR · Conversões · CPA

**Linha destaque (gold):** palavra com maior volume de impressões ou maior número de conversões. Indicar com badge "Melhor performance".

**Palavras sem conversão:** exibir normalmente, sem ocultar — são dados relevantes para otimização.

**Palavras "Não qualificada" ou com qualidade muito baixa:** exibir com opacidade reduzida (0.55) e badge visual distinto. Colocar ao final da tabela, separadas das palavras ativas.

### Lógica de análise
Se houver palavras com volume alto de impressões e zero conversão, nomear na narrativa: "Alto volume, sem retorno. Ajuste de match type ou landing page indicado."

---

## Plano de Ação em Andamento

**Presente em:** clientes com ações específicas de médio prazo que merecem destaque executivo (não apenas próximos passos operacionais)

### Quando usar
Quando há 2 ou mais iniciativas em andamento para o próximo mês que têm contexto, objetivo e status próprios — campanhas específicas, projetos paralelos, ações regionais, iniciativas comerciais novas.

### Estrutura: sistema de abas

Cada ação vira uma **aba** com botão e painel próprio. Botão ativo: fundo dourado translúcido + borda dourada. Botão inativo: fundo escuro + opacidade 50% no ícone.

**Número de abas:** 2 a 4. Mais que 4 abas num único slide fica apertado.

**Estrutura HTML de cada aba (botão):**
```html
<button id="plan-tab-[chave]" onclick="switchPlanTab('[chave]')"
  style="flex:1;display:flex;align-items:center;gap:12px;padding:13px 18px;
         background:rgba(0,0,0,.28);border:1px solid rgba(255,255,255,.10);
         border-radius:14px;cursor:pointer;text-align:left">
  <div class="tab-icon" style="width:40px;height:40px;background:[cor];
       border-radius:10px;display:flex;align-items:center;justify-content:center;
       flex-shrink:0;font-size:22px;line-height:1;opacity:.5">[emoji]</div>
  <span class="tab-title" style="font-size:14px;font-weight:700;font-stretch:75%;
       letter-spacing:-.01em;color:rgba(255,255,255,.45)">[Nome da ação]</span>
</button>
```

**Estrutura de cada painel:**
```html
<div id="plan-panel-[chave]" style="display:none;flex:1;min-height:0;gap:0;overflow:hidden">
  <!-- Coluna esquerda 42%: Contexto + Status -->
  <!-- Divisor: 1px rgba(255,255,255,.08) -->
  <!-- Coluna direita flex:1: Objetivo + Entregáveis (ou Métricas) -->
</div>
```

**Script de troca (atualizar o array com as chaves de todas as abas):**
```js
function switchPlanTab(tab){
  ['aba1','aba2','aba3'].forEach(function(t){
    var panel=document.getElementById('plan-panel-'+t);
    var btn=document.getElementById('plan-tab-'+t);
    var on=t===tab;
    panel.style.display=on?'flex':'none';
    btn.style.background=on?'rgba(255,212,138,.12)':'rgba(0,0,0,.28)';
    btn.style.borderColor=on?'rgba(255,212,138,.40)':'rgba(255,255,255,.10)';
    btn.querySelector('.tab-title').style.color=on?'#fff':'rgba(255,255,255,.45)';
    btn.querySelector('.tab-icon').style.opacity=on?'1':'0.5';
  });
}
```

### Conteúdo do painel — coluna esquerda (42%)
- **CONTEXTO:** caixa com fundo escuro, texto explicativo de 2–4 linhas sobre a origem/razão da ação
- **STATUS:** pills coloridas empilhadas (PRONTO verde / AGUARD. amarelo / DESIGN azul / EM ANDAMENTO etc.)

### Conteúdo do painel — coluna direita (flex:1)
- **OBJETIVO:** caixa descritiva de 2–3 linhas
- **ENTREGÁVEIS:** lista com ícone emoji + descrição do que será entregue
- Alternativa: **MÉTRICAS** em grid 3 colunas (para abas de campanhas já ativas com dados reais)

### Pills de status
```html
<!-- Verde — concluído -->
<span style="background:rgba(30,80,40,.85);border:1px solid rgba(99,212,113,.38);color:var(--safe);...">
  <svg ...>✓</svg> PRONTO
</span>

<!-- Amarelo — aguardando -->
<span style="background:rgba(80,55,0,.85);border:1px solid rgba(255,209,102,.35);color:var(--care);...">
  <svg ...>⏱</svg> AGUARD.
</span>
```

### Footer bar (abaixo das abas)
Linha de foco do mês com ícone 💡 e frase executiva curta.

---

## Premissas e Riscos

**Presente em:** todos os clientes

### Premissas (o que foi assumido)
- Período de veiculação considerado
- Sazonalidade do segmento no mês
- Qualquer variável externa relevante (datas comerciais, férias, feriados)

### Riscos para o próximo mês
- 2–4 itens
- Formato: "Risco: [descrição]. Mitigação: [ação prevista]."

---

## Entregas do Mês

**Presente em:** todos os clientes

### Fonte preferencial
Growth Pack (Google Sheets) via Google Drive MCP. Filtrar tarefas com `status == "Concluída"` no mês de referência. Se não disponível, acessar Ekyte ou perguntar ao usuário.

### Categorias
- **Campanhas & Mídia:** campanhas criadas/ajustadas, otimizações de budget, criativos de ads
- **Conteúdo & Criativos:** posts, vídeos, carrosséis, materiais gráficos, scripts
- **Gestão & Estratégia:** account planning, check-ins, atendimentos, ligações, reuniões

### Regras de formatação
- Máximo 12 itens totais distribuídos entre as categorias
- Atendimentos e ligações recorrentes individuais agrupam-se em uma linha única
- Itens concisos: verbo + objeto, sem explicações longas

---

## Próximos Passos

**Presente em:** todos os clientes

### Fonte preferencial
Growth Pack (Google Sheets) via Google Drive MCP. Filtrar tarefas com `status != "Concluída"` (Em andamento, A fazer, Atrasada). Ordenar por prazo, mais urgente primeiro. Complementar com o que foi identificado na Fase 0 e nos dados.

### Volume e organização
- Até 8–10 itens com prazo no mês corrente → exibir normalmente, numerados
- Itens com prazo no mês seguinte ou além → agrupar em bloco `<details>` colapsível com label "Ver também — [Mês] e além"

### Formato de cada item
1. Título da ação (verbo + objeto, sem parágrafo de explicação)
2. Responsável (tag por pessoa: nome ou dupla "Pessoa A · Pessoa B")
3. Tag de prazo ("até DD/MM")
4. Tag `danger` apenas se o item estiver atrasado ou for bloqueante para outra entrega — não usar `danger` por padrão

### Exemplo
- Ativar campanha de remarketing para leads frios · **V4** · até 10/08
- Aprovar criativos do ciclo 2 · **Cliente** · até 06/08 `[ATRASADO]`
- Revisar script do SDR com base nos motivos de perda · **V4 + Cliente** · até 15/08
