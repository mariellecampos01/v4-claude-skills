---
name: gigaclima-dash-update
description: Atualiza o dashboard de tarefas da Gigaclima (gigaclima.vercel.app/dashboard-tarefas.html) buscando tarefas ativas e concluídas via MCP Ekyte, regera a tabela HTML completa com filtros e coluna CONCLUÍDA EM, e faz deploy no Vercel. Use quando a usuária pedir para atualizar, recarregar ou sincronizar o dashboard da Gigaclima.
---

# Gigaclima — Atualização do Dashboard de Tarefas

## O que esse skill faz

Busca tarefas ativas (situation=10) e concluídas (situation=30) dos projetos Gigaclima no Ekyte, gera a tabela HTML completa com 7 colunas + filtros JS, e publica em `gigaclima.vercel.app/dashboard-tarefas.html`.

**Arquivo local:** `c:\Users\marri\OneDrive\Área de Trabalho\V4\Clientes\Gigaclima\dashboard-tarefas.html`  
**Backup antes de qualquer alteração:** `dashboard-tarefas.BACKUP.html` (mesma pasta)

---

## Passo 1 — Buscar tarefas ativas

Chamar `mcp__ekyte-api__list_tasks` com:
```
situation: "10"
ctcTaskProjectId: "289385,302907,304570"
limit: 100
```

Se retornar erro de tamanho, salvar resultado em arquivo temp e parsear com PowerShell `ConvertFrom-Json`.

Campos relevantes por tarefa:
- `id` → número da tarefa (#)
- `name` → título (limpar prefixos — ver regras abaixo)
- `responsible[0].name` → RESPONSÁVEL (normalizar — ver regras abaixo)
- `phaseDueDate` → base para calcular PRAZO: **phaseDueDate + 2 dias**, formato DD/MM
- `currentPhaseName` → ETAPA (renomear — ver regras abaixo)
- `situation` → 10 = Em Andamento

---

## Passo 2 — Buscar tarefas concluídas

Chamar `mcp__ekyte-api__list_tasks` com:
```
situation: "30"
ctcTaskProjectId: "289385,302907,304570"
limit: 200
```

Campos adicionais relevantes:
- `phaseStartDate` → usar como **CONCLUÍDA EM** (aproximação de resolvedDate, boa o suficiente)
- `currentDueDate` → usar como **PRAZO** para concluídas (DD/MM, sem cálculo de +2 dias)

---

## Passo 3 — Regras de processamento

### Limpeza de título (`name`)
Remover prefixos e sufixos padrão do Ekyte:
- Regex `^\[0\d\]\[..\]\s*(Gigaclima\s*[|–-]\s*)?` → remover
- `^\|\s*` (pipe no início) → remover
- `⚠️\s*` e `🔴\s*` e similares → remover
- Trim final

### Normalização de RESPONSÁVEL
| Raw Ekyte | Exibir como |
|---|---|
| `wendel` / `Wendel Lima` | `Wendel` |
| `leonardo` / `Leonardo Lima` | `Leonardo` |
| `Filipe  Santana` / `Filipe Santana` | `Filipe` |
| `Beatriz Vieira` | `Beatriz` |
| `Marielle` / `Marielle Campos` | `Marielle` |
| `Simão` / qualquer variante | `Simão` |
| `Igor` / qualquer variante | `Igor` |
| `Matheus Jordan` | `Matheus Jordan` |

Para o `data-resp` (atributo de filtro JS), usar apenas o primeiro nome — ex: `Matheus` para `Matheus Jordan`.

### Rename de ETAPA (`currentPhaseName`)
| Raw Ekyte | Exibir como |
|---|---|
| `Aprovação` | `Aprovação do Cliente` |
| `Gestor de Tráfego` | `Gestão de Tráfego` |
| `Copywriting` | `Copywriter` |
| `Análise` | `Análise de Dados` |
| Demais | manter como está |

### Override de etapa por ID
As tasks abaixo têm etapa forçada para **"Aprovação interna"** independente do que vier do Ekyte:
- `9524939`, `9524947`, `9524945`, `9524950`

---

## Passo 4 — Gerar o HTML da tabela

Substituir **apenas** o bloco da tabela dentro do arquivo, mantendo todo o restante intacto (header, KPIs, Gantt, etc.).

### Marcador de início e fim do bloco
- Início: `<div style="overflow-x:auto">`
- Fim: `</div>` imediatamente antes de `<!-- GANTT CHART -->`

### Estrutura do bloco

```html
  <div style="overflow-x:auto">
  <div id="filter-summary" style="font-size:12px;color:var(--muted);margin-bottom:8px;min-height:18px"></div>
  <table class="tasks-table" id="tasks-main-table">
    <thead>
      <tr>
        <th style="width:60px">#</th>
        <th>TAREFA</th>
        <th style="width:120px">RESPONSÁVEL</th>
        <th style="width:70px">PRAZO</th>
        <th style="width:130px">ETAPA</th>
        <th style="width:110px">STATUS</th>
        <th style="width:105px">CONCLUÍDA EM</th>
      </tr>
      <tr class="filter-row">
        <td></td>
        <td><input type="text" id="f-tarefa" class="tbl-filter" placeholder="Buscar tarefa…" oninput="filterTasks()"></td>
        <td><select id="f-resp" class="tbl-filter" onchange="filterTasks()">
          <option value="">Todos</option>
          <!-- uma <option> por responsável distinto encontrado nos dados -->
        </select></td>
        <td></td>
        <td><select id="f-etapa" class="tbl-filter" onchange="filterTasks()">
          <option value="">Todas</option>
          <!-- uma <option> por etapa distinta encontrada nos dados -->
        </select></td>
        <td><select id="f-status" class="tbl-filter" onchange="filterTasks()">
          <option value="">Todos</option>
          <option>Em Andamento</option>
          <option>Concluída</option>
        </select></td>
        <td></td>
      </tr>
    </thead>
    <tbody id="task-tbody">

    <!-- grupo ativas -->
    <tr class="tt-group tt-section"><td colspan="7">⚡ Em Andamento (N) — Projetos 289385 · 302907 · 304570</td></tr>
    <!-- uma <tr> por tarefa ativa (ver formato abaixo) -->

    <!-- grupo concluídas -->
    <tr class="tt-group tt-section tt-group-done"><td colspan="7">✅ Concluídas (N) — Q2 2026 · Social 2026</td></tr>
    <!-- uma <tr> por tarefa concluída (ver formato abaixo) -->

    </tbody>
  </table>
  </div>
```

### Formato de cada linha — tarefa ativa
```html
<tr data-tarefa="TÍTULO" data-resp="PRIMEIRO_NOME" data-etapa="ETAPA" data-status="em andamento">
  <td class="tt-num">ID</td>
  <td class="tt-name">TÍTULO</td>
  <td class="tt-resp">NOME_EXIBIÇÃO</td>
  <td class="tt-date">DD/MM</td>
  <td class="tt-etapa">ETAPA</td>
  <td><span class="st-tag st-prog">Em Andamento</span></td>
  <td class="tt-concluded">—</td>
</tr>
```

### Formato de cada linha — tarefa concluída
```html
<tr data-tarefa="TÍTULO" data-resp="PRIMEIRO_NOME" data-etapa="ETAPA" data-status="concluída">
  <td class="tt-num">ID</td>
  <td class="tt-name">TÍTULO</td>
  <td class="tt-resp">NOME_EXIBIÇÃO</td>
  <td class="tt-date">DD/MM</td>
  <td class="tt-etapa">ETAPA</td>
  <td><span class="st-tag st-done">Concluída</span></td>
  <td class="tt-concluded">DD/MM/YYYY</td>
</tr>
```

`data-status` sempre em minúsculas. `data-etapa` igual ao texto exibido. `data-resp` só primeiro nome.

---

## Passo 5 — Atualizar contadores no arquivo

Após regerar a tabela, atualizar também:
1. Meta-pill: `📋 N em andamento · N concluídas`
2. KPI "Em Andamento": `<div class="kpi-num kn-blue">N</div>`
3. Cabeçalhos de grupo já embutidos na tabela (Passo 4)

Buscar por regex/string única para não afetar outras ocorrências.

---

## Passo 6 — Atualizar a data "Hoje" no arquivo

Atualizar a linha que exibe a data atual:
```html
<div class="meta-pill">📅 Hoje: DD/MM/YYYY</div>
```
e o texto do Gantt:
```html
linha vermelha = hoje (DD/MM)
```
Usar a data real da execução.

---

## Passo 7 — Deploy no Vercel

```powershell
cd "c:\Users\marri\OneDrive\Área de Trabalho\V4\Clientes\Gigaclima"
vercel --prod --yes
```

Confirmar que a saída contenha `Aliased` apontando para `gigaclima.vercel.app`.

---

## Passo 8 — Confirmar URL ao vivo

Após o deploy, informar à usuária:
- URL: `https://gigaclima.vercel.app/dashboard-tarefas.html`
- Quantas tarefas ativas e concluídas foram incluídas
- Data de referência (hoje)

---

## Regras gerais

- **Nunca remover** o bloco de Gantt, os KPIs de tráfego/investimento, o header fixo, as abas, ou qualquer outro bloco fora da tabela de tarefas.
- **Nunca incluir** tarefas com `situation=40` (canceladas).
- Se o resultado do Ekyte vier vazio (0 tarefas ativas), avisar a usuária antes de publicar uma tabela vazia.
- Se `phaseDueDate` vier nulo em alguma tarefa ativa, usar `currentDueDate` como fallback para o PRAZO.
- Se `phaseStartDate` vier nulo em tarefa concluída, exibir `—` na coluna CONCLUÍDA EM.
- A substituição do bloco da tabela deve ser feita via PowerShell (`IndexOf` / `Substring`) para evitar problemas de encoding com o Edit tool em arquivos grandes.

---

## Estrutura de arquivos relevantes

```
c:\Users\marri\OneDrive\Área de Trabalho\V4\Clientes\Gigaclima\
  dashboard-tarefas.html          ← arquivo principal
  dashboard-tarefas.BACKUP.html   ← backup gerado por este skill
  index.html                      ← check-in (não mexer)
  assets\                         ← logo e imagens (não mexer)
```

## IDs dos projetos Ekyte — Gigaclima

| Projeto | ID |
|---|---|
| Q2 - 2026 | 289385 |
| Social Media 2026 | 302907 |
| Site / LP 2026 | 304570 |
