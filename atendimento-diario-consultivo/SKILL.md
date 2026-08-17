---
name: atendimento-diario-consultivo
description: Gera mensagens diárias de atendimento consultivo para clientes de marketing digital, transformando métricas em visão estratégica de negócio. Use sempre que o usuário quiser criar, redigir ou gerar mensagens de atendimento diário, daily update, relatório diário de cliente, mensagem consultiva para WhatsApp, análise de performance mensal, ou qualquer variação de comunicação diária estratégica com cliente. Também deve ser usada quando o usuário enviar prints de métricas, dados do CRM, Growth Pack, pacing, ou solicitar análise de funil e próximos passos para clientes.
---

# Atendimento Diário Consultivo

## Objetivo

Gerar mensagens de atendimento diário para clientes de marketing digital com **visão consultiva, estratégica e orientada a crescimento**.

A resposta deve transformar métricas e dados operacionais em:
- Visão de negócio
- Leitura de funil
- Pacing e ritmo da meta
- Direcionamento estratégico
- Próximos passos claros e acionáveis

## Contexto da Função

O atendimento diário faz parte da rotina de Account/Growth Manager.

**O objetivo NÃO é apenas reportar números.**

O objetivo é:
- Gerar percepção de acompanhamento ativo
- Demonstrar domínio da operação
- Conectar marketing + comercial
- Mostrar direcionamento estratégico
- Antecipar gargalos
- Reforçar próximos passos

## Roteamento por Dia da Semana

Antes de qualquer coisa, verificar a data atual (`currentDate`) e determinar o dia da semana:

| Dia | Fonte de dados | Tipo de mensagem |
|---|---|---|
| Segunda, Quinta | Growth Pack (planilha) | Analítica — métricas, pacing, funil |
| Terça, Quarta | Ekyte (tarefas ativas do mês) | Operacional — demandas ativas, resumos de reuniões |
| Sexta | Ekyte + GP (semana) | Compilado semanal + confirmação de agendas |

Seguir o fluxo correspondente abaixo.

---

## Fluxo TERÇA e QUARTA — Dados do Ekyte

### 1. Identificar o projeto do cliente no Ekyte
Consultar o arquivo `clientes/_skill-ekyte/cache.md` para obter o ID do projeto do cliente no mês vigente.

### 2. Buscar tarefas ativas do mês via MCP Ekyte
Usar `mcp__ekyte-api__list_project_tasks` com o ID do projeto, filtrando pelo mês atual. Focar em tarefas com status **ativo** (em andamento, em revisão, aguardando aprovação — excluir canceladas).

### 3. Estruturar os dados operacionais
Focar só no que está **ativo agora** (em andamento, em revisão, aguardando aprovação). Não separar em entregues/pendentes/próximos passos — a mensagem de Ter/Qui é só um retrato rápido do que está em produção no mês.

### 4. Gerar a mensagem operacional (estrutura para Ter/Qui)

```
Bom dia, time!! ☀️
[Abertura amigável e calorosa — 1-2 frases com substância real: ritmo do time, volume de frentes, energia da semana]

[SE HOUVER REUNIÃO/CALL NA SEMANA — incluir este bloco, omitir se não houver:
📋 RECAP — [NOME DA REUNIÃO OU CALL]
> [ponto 1 do alinhamento]
> [ponto 2 do alinhamento]
]

🛠️ EM ANDAMENTO — [MÊS]
> [tarefa 1 — contexto breve]
> [tarefa 2 — contexto breve]
> [tarefa 3 — contexto breve]
...

[Fechamento com "estamos de olho" — reforçar acompanhamento próximo e disponibilidade]

[Fechamento do dia: Terça="Excelente terça-feira! 🚀" / Quarta="Excelente quarta-feira! 🚀"]
```

**Diretrizes da mensagem operacional:**
- Lista do que está em andamento é sucinta e direta — uma linha de contexto por tarefa, sem enrolação
- Se houver reunião ou call que aconteceu nesta semana, incluir o bloco de recap antes das tarefas — 2 a 3 pontos principais, sem ata completa. Omitir o bloco se não houver reunião
- Abertura e fechamento podem ser mais amigáveis e humanos — é o que dá calor à mensagem curta, não enche ela de seções
- A abertura precisa ter substância — nunca só repetir "[dia da semana] na [cliente]". Ancorar em algo real: ritmo do time, volume de frentes rodando, energia da semana, ou um fato do próprio mês. Evitar frase genérica e vazia
- Sem seções de entregues, pendentes, próximos passos ou alinhamento — isso fica para o fluxo analítico (Seg/Qui)
- Tom executivo mas próximo — o cliente precisa sentir que a operação está rodando e que tem alguém de olho, sem precisar de um relatório longo

---

## Fluxo SEXTA — Compilado Semanal

### 1. Coletar os dados da semana
Reunir o que for disponível:
- Tarefas Ekyte que avançaram, foram entregues ou estão travadas
- Movimentações relevantes de resultado (se houver dado fresco de GP)
- Reuniões ou calls que aconteceram na semana (pontos principais)

### 2. Coletar agenda da semana seguinte
Usar o contexto disponível ou o que a Marielle informar:
- Reuniões agendadas com o cliente
- Entregas previstas
- Calls marcadas

### 3. Estrutura da mensagem de sexta

```
Bom dia, time!! ☀️
[Abertura de encerramento — balanço da semana, energia de virada, tom mais leve mas ainda profissional]

📋 SEMANA EM RETROSPECTO
> [destaque 1 — entrega, avanço, resultado da semana]
> [destaque 2]
> [destaque 3]

📅 SEMANA QUE VEM
> Segunda: update de resultados
> Terça: [reunião específica se houver, senão "demandas em andamento"]
> Quarta: [reunião específica se houver, senão "demandas em andamento"]
> Quinta: update de resultados
> Sexta: compilado

[Se houver reuniões/calls específicas confirmadas, mencionar no bloco acima junto ao dia correspondente]

[Fechamento: "Bom final de semana! 🚀"]
```

**Diretrizes da mensagem de sexta:**
- Compilado com 3 a 5 pontos: o suficiente para dar sensação de semana produtiva, sem ser exaustivo
- Agenda da semana seguinte confirma o padrão de dias + acrescenta reuniões específicas quando houver
- Se não houver dados de agenda específica, manter só o padrão (Seg/Qui resultados, Ter/Qua operacional)
- Tom mais leve que os outros dias, ainda executivo. É uma mensagem de virada de semana.

---

## Fluxo Automático — Busca de Dados no Growth Pack

**Quando o usuário pedir atendimento diário sem fornecer dados manualmente**, seguir este fluxo:

### 1. Identificar o cliente solicitado
Mapear o nome do cliente para o link pubhtml correto:

| Cliente | pubhtml |
|---|---|
| Alquilab Pharma | https://docs.google.com/spreadsheets/d/e/2PACX-1vSLVScJ-IolhZZQBBDB8ZjHg5PBqm8XQ2SAV9qzEsOewNKUWzGH_dB6wA1KTpskYHEKPV1CDmEzVZV_/pubhtml |
| Compass | https://docs.google.com/spreadsheets/d/e/2PACX-1vTSiG5OvWfB6iBDqM3TEnfWXMjjAK3Pz-XjCF2LgIcjkz4KuXQYhNDYh_4JjF1i256fYRLHC_YIxiA_/pubhtml |
| Durcon | https://docs.google.com/spreadsheets/d/e/2PACX-1vS0n3HsVTwwZkNEY_W7f_4msqfckpeMVbubfmXEjVrdgRk8Yuu0DSeJCo8ol4AR_NSL58pwsh7V4aCz/pubhtml |
| Elysion SPA (Manaus) | https://docs.google.com/spreadsheets/d/e/2PACX-1vQC83Kt62vYJmO9Rcj56r1NTX_zvaJFaInb7fY3MF9qtUyziCG0kD_w_GjmOOTN15OV31vLjlp8JCwR/pubhtml |
| Elysion SPA (Curitiba) | https://docs.google.com/spreadsheets/d/e/2PACX-1vQlYj8k-K5FK1KVX6PT6TdF9mzh_uIGHZrCuYpoDB7D2UPqXs2chrCvcd6DAVDGkiUA7XTXCkbSUc6-/pubhtml |
| Prata Nobre | https://docs.google.com/spreadsheets/d/e/2PACX-1vRtS9FgAFSp60lRj3NmGGT1CHCCnVfoRVhz06SSyoJmFIsaD3pe7zWzwMOA_bNMh--mWD7XUmytUgJF/pubhtml |
| Sementes Premix | https://docs.google.com/spreadsheets/d/e/2PACX-1vTaM5Pp8IYVi9jmPA_n1Z-qUlEhfdTIXzPX699gcLISH8y90Kn1Jt0BiEW-oikCEULX5MIHehThFGnI/pubhtml |

> **Elysion SPA:** buscar as duas planilhas (Manaus + Curitiba) e gerar uma única mensagem unificada para o cliente.

### 2. Buscar o Growth Pack via WebFetch — formato CSV com range fixo

**SOLUÇÃO DEFINITIVA PARA O PROBLEMA DE PARSING:** os valores monetários brasileiros (ex: "R$ 1.937,59") contêm vírgula e deslocam a contagem de colunas no CSV completo. Para evitar isso, buscar APENAS a coluna do mês atual usando o parâmetro `range` na URL — retorna uma única coluna, sem risco de deslocamento.

**Coluna por mês (aba Acompanhamento Mensal — estrutura com Jan/2023 na coluna B):**
| Mês | Coluna |
|---|---|
| Junho/2026 | AQ |
| Julho/2026 | AR |
| Agosto/2026 | AS |
| Setembro/2026 | AT |

**Mês atual: Agosto/2026 = coluna AS**

**GIDs por cliente:**
| Cliente | gid |
|---|---|
| Alquilab Pharma | 1422566774 |
| Compass | 1422566774 |
| Durcon | 1422566774 |
| Elysion SPA (Manaus) | 1422566774 |
| Elysion SPA (Curitiba) | 1422566774 |
| Prata Nobre | 1422566774 |
| Sementes Premix | 1422566774 |

**Metas de Agosto/2026 por cliente (usar na seção 2 — Meta & Pace):**
| Cliente | Meta | Tipo |
|---|---|---|
| Alquilab Pharma | a confirmar | Faturamento |
| Compass | a confirmar | Faturamento |
| Durcon | 10 SQLs | SQLs |
| Elysion SPA (Manaus) | R$ 100.000,00 | Faturamento |
| Elysion SPA (Curitiba) | R$ 40.000,00 | Faturamento |
| Prata Nobre | 88 leads | Leads |
| Sementes Premix | 13 SQLs | SQLs |

> Atualizar esta tabela sempre que novas metas mensais forem confirmadas pela Marielle.

**Formato da URL (busca coluna AQ + coluna A para labels):**
```
1ª chamada (coluna de junho — AQ):
https://docs.google.com/spreadsheets/d/e/2PACX-.../pub?output=csv&gid=<GID>&range=AQ1:AQ50
→ recebe redirect 307
2ª chamada: URL do redirect imediatamente

3ª chamada (mês anterior para comparação — AP = maio):
https://docs.google.com/spreadsheets/d/e/2PACX-.../pub?output=csv&gid=<GID>&range=AP1:AP50
→ recebe redirect 307
4ª chamada: URL do redirect imediatamente
```

> **Atenção:** as URLs de redirect expiram em segundos. Fazer cada segunda chamada imediatamente após receber o redirect da primeira.

### 3. Prompt correto para extração dos dados

Cada fetch de range retorna uma única coluna CSV. Usar o mapa fixo de linhas abaixo para extrair os valores:

```
Este CSV contém UMA ÚNICA COLUNA: os valores do mês para o Growth Pack.
Mapeamento fixo de linhas (ignorar linhas vazias ou de cabeçalho):
- Linha 1: Ano
- Linha 2: Data início do mês
- Linha 3: Data fim do mês
- Linha 4: Nome do mês
- Linha 6: Fee V4
- Linha 7: Plano de Mídia Mês
- Linha 8: Orçamento diário mínimo
- Linha 9: Investimento realizado
- Linha 10: Média de investido diário
- Linha 11: Saldo do mês
- Linha 29: Impressões
- Linha 31: Cliques
- Linha 32: Leads
- Linha 33: MQLs
- Linha 34: SQLs (ou Conexões em alguns clientes)
- Linha 35: SQLs
- Linha 36: Vendas (MANUAL)
- Linha 37: Faturamento V4 (MANUAL)
- Linha 38: ROAS
- Linha 39: CTR
- Linha 40: Taxa de Conversão
- Linha 28: Ticket Médio

Retorne cada valor exatamente como aparece na linha correspondente.
Se a linha estiver vazia ou zero, informe como zero.
```

> **Por que range funciona:** ao buscar apenas `AQ1:AQ50`, o Google retorna somente essa coluna. Não há múltiplas colunas para deslocar, eliminando o problema das vírgulas nos valores monetários.

> **FALLBACK OBRIGATÓRIO:** se o redirect expirar ou o valor parecer inconsistente, pedir à usuária um print da coluna AQ — mais rápido do que múltiplas tentativas.

### 4. Identificar o mês atual e calcular pacing
- A data atual está disponível no contexto (`currentDate`)
- O mês mais recente retornado = dados do mês em curso (parcial) ou do mês anterior (fechado)
- Calcular dias úteis transcorridos vs total → pacing
- Se houver coluna de **projeção/meta de faturamento**, compará-la com o realizado

### 5. Extrair as métricas
- **Plano de Mídia** = meta de investimento do mês
- **Realizado até o momento** (acumulado do mês)
- **% atingido** = realizado / meta × 100
- Métricas de funil: investimento, impressões, cliques, leads, MQLs, SQLs, vendas, faturamento, CAC/CPA

### 5. Comparar Realizado vs Projeção do Mês
Sempre que a planilha tiver projeção mensal:
- Calcular desvio: `(realizado - projeção) / projeção × 100`
- Se acima: destacar positivamente com contexto
- Se abaixo: identificar gap e incluir no diagnóstico e direcionamentos

### 6. Prosseguir com a estrutura de 7 seções normalmente
Usar os dados extraídos para gerar a mensagem consultiva.

> **Regra importante:** se o WebFetch retornar erro ou a planilha não tiver dados do mês atual, avisar o usuário e pedir os dados manualmente antes de gerar a mensagem.

---

## Inputs Aceitos

A IA pode receber qualquer combinação de:
- **Prints do CRM** (RD Station, HubSpot, Pipedrive, etc.)
- **Prints do Growth Pack** (planilha de acompanhamento mensal)
- **Dados de pacing/meta** (realizado vs meta do mês)
- **Demandas em andamento** (ajustes de campanha, criativos, testes)
- **Campanhas ativas** (Meta Ads, Google Ads, LinkedIn)
- **Observações comerciais** (status de negociações, follow-ups)
- **Status de produção** (criativos, landing pages, aprovações)
- **Prints de métricas** (dashboards, relatórios)
- **Contexto operacional** do cliente (segmento, ticket médio, ciclo de vendas)

### Fonte de Dados Padrão

Quando disponível, extrair dados da **planilha Growth Pack do cliente**, aba **ACOMPANHAMENTO MENSAL**.

Exemplo de URL:
```
https://docs.google.com/spreadsheets/d/15BJDWsGvFPf6Yf9biMAozaZ-YQ3wElFQ0NqOO2uMP8Q/edit?gid=1422566774#gid=1422566774
```

## Lógica de Análise

Ao receber os dados, seguir este raciocínio:

### 1. Comparar Realizado vs Meta
- Qual o percentual atingido?
- Estamos acima/abaixo/no ritmo esperado?
- Quantos dias úteis restam no mês?

### 2. Avaliar Pacing (Ritmo do Mês)

> **REGRA CRÍTICA:** Pacing é SEMPRE sobre **faturamento realizado vs meta de faturamento**. Nunca usar pace de investimento de mídia como proxy de resultado. Investimento é insumo, faturamento é resultado.

- **Pacing adequado:** faturamento realizado proporcional aos dias transcorridos
- **Acima do pace:** possibilidade de superar meta de faturamento
- **Abaixo do pace:** necessário acelerar conversão comercial ou revisar meta

Cálculo:
```
Pace esperado de faturamento = (dias úteis transcorridos / dias úteis totais) × meta de faturamento
Projeção do mês = (faturamento realizado / dias úteis transcorridos) × dias úteis totais
```

Para clientes com meta em SQLs (ex: Durcon, Premix): aplicar o mesmo cálculo sobre SQLs realizados vs meta de SQLs.

### 3. Identificar Gargalos do Funil

Analisar a conversão em cada etapa:
- **Impressões → Cliques:** Problema de criativo/oferta/copy?
- **Cliques → Leads:** Problema de landing page/formulário?
- **Leads → MQLs:** Problema de qualificação/segmentação?
- **MQLs → SQLs:** Problema comercial/tempo de resposta?
- **SQLs → Vendas:** Problema de abordagem/oferta/pricing?

### 4. Classificar o Tipo de Problema

O gargalo é de:
- **Volume:** Poucos leads sendo gerados
- **Conversão:** Muitos leads, poucas vendas
- **Comercial:** Pipeline travado, falta follow-up
- **Qualificação:** Leads de baixa qualidade
- **Operação:** Lentidão no atendimento/processo

### 5. Relacionar Campanhas com Comportamento do Funil

- Campanhas recém-lançadas podem explicar oscilações
- Mudanças de criativo/copy impactam CTR e conversão
- Ajustes de público influenciam qualidade dos leads
- Sazonalidade e eventos do mercado importam

### 6. Gerar Próximos Passos Acionáveis

Nunca deixar o cliente sem direção. Sempre incluir:
- O que será feito (ação concreta)
- Quando será feito (prazo/frequência)
- Qual o objetivo esperado (resultado)

### 7. Evitar Leitura Fria de Métricas

❌ **Ruim:** "Tivemos 35 leads nesta semana."

✅ **Bom:** "Geramos 35 leads na semana, mantendo o ritmo necessário para atingir a meta de 120 leads no mês. Se sustentarmos esse volume + melhorarmos a taxa de conversão comercial, fechamos maio acima da meta."

### 8. Trazer Visão Consultiva e Estratégica

Sempre conectar **números → diagnóstico → ação → resultado esperado**.

## Estrutura Obrigatória da Resposta

A mensagem deve seguir **exatamente** esta estrutura:

### 1. Abertura Profissional
Saudação + motivação para o dia/semana.

**Exemplo:**
```
Bom dia, time!! ☀️
Uma excelente segunda-feira a todos! Começamos a semana com foco total em manter o ritmo da operação e acelerar o pace da meta de maio. 🚀
```

### 2. Visão dos Resultados do Mês
Apresentar os números principais de forma organizada e visual.

**Exemplo:**
```
📊 1. RESULTADOS DE MAIO

> 💰 Investimento realizado: R$ 1.463,40
> 👁️ Impressões: 8.917
> 🖱️ Cliques: 596
> 📩 Leads gerados: 35
> 🎯 MQLs: 24
> 🤝 Leads CRM: 27
> 💵 Vendas realizadas: 2 vendas
> 💰 Faturamento fechado: R$ 4.890,00
```

**Diretrizes:**
- Usar emojis para facilitar leitura visual
- Usar `>` para criar blocos destacados
- Apresentar métricas de forma hierárquica (topo do funil → fundo do funil)

### 3. Leitura de Pacing/Meta

> **REGRA CRÍTICA — META & PACE:**
> Esta seção compara **FATURAMENTO realizado vs meta de faturamento**, com projeção ao fim do mês.
> **NUNCA** mostrar pace de investimento de mídia aqui. Investimento é insumo, não resultado.
> Pace de investimento vai apenas na seção 1 (Resultados), como dado informativo.

**Fórmula de projeção:**
```
Projeção do mês = (faturamento realizado / dias úteis passados) × dias úteis totais do mês
```

**Formato para clientes com meta em faturamento (R$):**
```
🎯 2. META & PACE — [MÊS]

> Meta de faturamento: R$ X.000
> Faturamento realizado: R$ X.XXX (X% da meta)
> Projeção ao fim do mês: R$ X.XXX (ritmo atual)
> Status: [acima do ritmo / no ritmo / abaixo do ritmo necessário]
```

**Formato para clientes com meta em SQLs (ex: Durcon, Premix):**
```
🎯 2. META & PACE — [MÊS]

> Meta: X SQLs
> Realizados: X SQLs (X% da meta)
> Projeção ao fim do mês: X SQLs (ritmo atual)
> Faturamento em pipeline: R$ X.XXX
```

**Exemplo prático (faturamento):**
```
🎯 2. META DE MAIO & PACE

> Meta de faturamento: R$ 7.700,00
> Faturamento realizado: R$ 4.890,00 (63% da meta)
> Projeção ao fim do mês: R$ 8.153,00 (ritmo atual)
> Status: no ritmo — projeção acima da meta se o comercial mantiver cadência

O cenário segue positivo, com projeção de superar a meta. O time já mostrou capacidade de entrega; agora é manter ritmo, acompanhamento comercial e velocidade no atendimento.
```

**Diretrizes:**
- Sempre mostrar faturamento realizado vs meta de faturamento
- Sempre calcular e mostrar a projeção ao fim do mês
- Sempre indicar percentual atingido e status do ritmo
- Contextualizar se o ritmo está adequado para bater a meta
- Trazer perspectiva consultiva (não apenas os números)
- Ser realista mas motivador

### 4. Insights de Performance
Análise consultiva dos indicadores-chave.

**Exemplo:**
```
📈 3. INSIGHTS DE PERFORMANCE

> CTR atual em 16,29%, mostrando boa aderência entre campanha e público
> Taxa de conversão geral em 5,71%, mantendo qualidade na geração de demanda
> CAC atual em R$ 227,64, mantendo aquisição saudável para o ticket da operação
```

**Diretrizes:**
- Sempre **interpretar** os números (não apenas listá-los)
- Conectar métricas com contexto do negócio
- Indicar se o desempenho está saudável/adequado/necessita ajuste
- Usar benchmarks quando possível (ticket médio, CAC aceitável, etc.)

### 5. Direcionamentos da Semana
Próximos passos claros e acionáveis.

**Exemplo:**
```
🚀 4. DIRECIONAMENTOS DA SEMANA

> Continuidade das otimizações das campanhas Meta e Google
> Acompanhamento próximo do fundo do funil para acelerar novas vendas
> Monitoramento diário do pace da meta e evolução dos MQLs
> Seguimos acompanhando a operação comercial junto ao Fernando para evolução das oportunidades
```

**Diretrizes:**
- Mínimo de 3 próximos passos
- Serem específicos (nomear plataformas, pessoas, ações)
- Indicar frequência quando relevante (diário, semanal)
- Conectar ações com objetivos (para quê estamos fazendo isso)

### 6. Alinhamento Operacional
Solicitar informações ou confirmar próximos alinhamentos.

**Exemplo:**
```
💬 Caso existam atualizações comerciais ou movimentações no funil, aguardamos atualização ou alinhamos tudo no acompanhamento comercial com o Fernando. 🤝
```

**Diretrizes:**
- Deixar canal aberto para feedback do cliente
- Reforçar que estamos acompanhando ativamente
- Mencionar próximas reuniões/calls quando aplicável

### 7. Fechamento Consultivo
Encerramento motivador e profissional.

**Exemplo:**
```
Boa semana! 🚀
```

**Diretrizes:**
- Breve e energético
- Usar o fechamento correto conforme o dia da semana:
  - Segunda: "Excelente semana pra gente! 🚀"
  - Terça: "Excelente terça-feira! 🚀"
  - Quarta: "Excelente quarta-feira! 🚀"
  - Quinta: "Excelente quinta-feira! 🚀"
  - Sexta: "Bom final de semana. 🚀"

## Tom de Voz

A comunicação deve ser:

✅ **Consultiva:** Trazer visão além dos números
✅ **Executiva:** Objetiva, direta, sem rodeios
✅ **Estratégica:** Conectar ações com resultados de negócio
✅ **Próxima:** Usar "nós", "seguimos", "vamos"
✅ **Profissional:** Manter seriedade sem ser engessado
✅ **Confiante:** Mostrar domínio da operação
✅ **Clara:** Evitar jargões desnecessários

❌ **Evitar:**
- Tom robótico ou padronizado demais
- Excesso de emojis (usar com moderação e propósito)
- Apenas repetir métricas sem interpretação
- Frases genéricas do tipo "continuamos trabalhando duro"
- Passividade ("aguardamos", "esperamos que") sem direcionamento
- Travessões (—) em excesso — dão cara de texto gerado por IA; preferir vírgulas, ponto e vírgula ou ponto simples para separar ideias

## Regras Importantes

### Regra 1: Sempre Contextualizar os Números
Nunca apresentar uma métrica sem interpretá-la.

❌ **Ruim:** "CAC de R$ 150"
✅ **Bom:** "CAC de R$ 150, abaixo do ticket médio de R$ 800, garantindo margem saudável"

### Regra 2: Sempre Conectar Métricas com Ação
Todo diagnóstico deve vir acompanhado de direcionamento.

❌ **Ruim:** "Taxa de conversão de leads em vendas está em 5%"
✅ **Bom:** "Taxa de conversão de leads em vendas está em 5%. Para acelerar, vamos reforçar o follow-up comercial e testar novas abordagens de qualificação."

### Regra 3: Sempre Trazer Direcionamento
Nunca deixar o cliente sem próximos passos claros.

### Regra 4: Sempre Mostrar Acompanhamento Ativo
Reforçar que a operação está sendo monitorada de perto.

**Exemplo:**
- "Seguimos acompanhando..."
- "Monitoramento diário do..."
- "Estamos de olho em..."

### Regra 5: Sempre Considerar a Meta do Cliente
Toda análise deve ser orientada ao objetivo final (meta de vendas/faturamento).

### Regra 6: Sempre Considerar Pacing do Mês
Avaliar se o ritmo atual é suficiente para atingir a meta.

### Regra 7: Sempre Considerar o Impacto Comercial
Não importa apenas quantos leads geramos, mas quantos se convertem em vendas.

## Exemplos de Raciocínio por Cenário

### Cenário 1: Muitos MQLs + Poucos SQLs
**Diagnóstico:** Gargalo comercial (qualificação ou velocidade de resposta)

**Direcionamento:**
- Acelerar tempo de primeira resposta
- Revisar script de qualificação
- Aumentar frequência de follow-up
- Alinhar critérios de SQL com comercial

### Cenário 2: Baixo Volume de Leads
**Diagnóstico:** Problema de topo de funil (alcance, criativo, oferta)

**Direcionamento:**
- Revisar campanhas e criativos
- Testar novas segmentações de público
- Ajustar orçamento/lances
- Validar se a oferta está competitiva

### Cenário 3: Bom Pacing
**Diagnóstico:** Operação no ritmo certo

**Direcionamento:**
- Reforçar continuidade das ações
- Buscar oportunidades de escala
- Manter acompanhamento próximo
- Preparar para aceleração final do mês

### Cenário 4: Pipeline Parado (SQLs sem evoluir)
**Diagnóstico:** Falta de follow-up ou objeções não tratadas

**Direcionamento:**
- Incentivar retomada ativa de oportunidades
- Propor novos argumentos/ofertas
- Revisar critérios de qualificação
- Alinhar com comercial sobre barreiras

### Cenário 5: Alto CAC
**Diagnóstico:** Aquisição custosa (pode ser segmentação ou criativo)

**Direcionamento:**
- Revisar públicos (podem estar saturados)
- Testar novos criativos/copy
- Avaliar canais alternativos
- Considerar otimização de lances

### Cenário 6: Boa Conversão mas Baixo Ticket
**Diagnóstico:** Estamos vendendo, mas o valor está abaixo do esperado

**Direcionamento:**
- Revisar estratégia de upsell
- Focar em produtos/serviços de maior ticket
- Trabalhar objeções relacionadas a preço
- Segmentar campanhas para público com maior poder aquisitivo

## Formato Final

A saída deve ser uma **mensagem pronta para envio no WhatsApp**.

### Checklist Final Antes de Enviar

Antes de gerar a resposta, confirmar:

- [ ] A mensagem está estruturada conforme as 7 seções obrigatórias?
- [ ] Os números foram interpretados (não apenas listados)?
- [ ] O pacing foi calculado e contextualizado?
- [ ] Há próximos passos claros e acionáveis?
- [ ] O tom está consultivo (não apenas operacional)?
- [ ] Mencionei possíveis gargalos ou oportunidades?
- [ ] A mensagem conecta marketing + comercial?
- [ ] O cliente sabe exatamente o que esperar desta semana/período?

## Instruções de Uso

### Para o Usuário

Para usar esta skill, envie:

1. **Nome do cliente** (ex: "Compass", "Alquilab Pharma", "Prata Nobre")
2. Opcionalmente: contexto adicional, observações comerciais, demandas em andamento

Claude buscará automaticamente os dados do mês atual no Growth Pack do cliente via WebFetch e gerará a mensagem.

Se preferir fornecer dados manualmente:
```
"Gere a mensagem diária para o cliente XYZ com base nestes dados do Growth Pack"
[anexar print ou dados]
```

### Para Claude

Ao identificar a solicitação:

1. **Se não houver dados fornecidos manualmente:**
   - Identificar o cliente
   - Fazer WebFetch no link pubhtml correspondente
   - Extrair dados do mês atual
   - Calcular pacing e comparar com projeção

2. **Se houver dados fornecidos:**
   - Usar os dados fornecidos diretamente

3. **Extrair/solicitar dados essenciais:**
   - Meta do mês
   - Realizado até o momento
   - Métricas de funil (impressões, cliques, leads, MQLs, SQLs, vendas)
   - Investimento
   - CAC/CPA
   - Faturamento

4. **Calcular pacing:**
   ```
   % atingido = (realizado / meta) × 100
   Dias transcorridos vs dias totais do mês
   ```

5. **Analisar funil e identificar gargalos**

6. **Gerar a mensagem seguindo a estrutura de 7 seções**

7. **Revisar com o checklist final**

## Variações e Adaptações

### Para Diferentes Segmentos

A skill pode adaptar linguagem e foco conforme o segmento:

**E-commerce:**
- Foco em ROAS, ticket médio, taxa de conversão
- Mencionar sazonalidade e datas comemorativas

**Inside Sales / SaaS:**
- Foco em MQLs, SQLs, ciclo de vendas
- Mencionar pipeline e funil comercial

**Campanha de Mensagem (WhatsApp/SMS):**
- Foco em disparos, taxa de resposta, conversas ativas
- Mencionar scripts e abordagens

**Geração de Demanda B2B:**
- Foco em qualificação, ICP, fit de leads
- Mencionar ciclo de vendas mais longo

### Para Diferentes Momentos do Mês

**Início do mês (dias 1-10):**
- Foco em estabelecer ritmo
- Expectativa de aceleração
- Ajustes de campanha

**Meio do mês (dias 11-20):**
- Foco em manter pace
- Correções de rota se necessário
- Intensificar o que está funcionando

**Final do mês (dias 21-30):**
- Foco em fechar forte
- Acelerar follow-ups comerciais
- Push final para bater/superar meta

---

## Exemplo Completo de Output

```
Bom dia, time!! ☀️
Uma excelente segunda-feira a todos! Começamos a semana com foco total em manter o ritmo da operação e acelerar o pace da meta de maio. 🚀

📊 1. RESULTADOS DE MAIO

> 💰 Investimento realizado: R$ 1.463,40
> 👁️ Impressões: 8.917
> 🖱️ Cliques: 596
> 📩 Leads gerados: 35
> 🎯 MQLs: 24
> 🤝 Leads CRM: 27
> 💵 Vendas realizadas: 2 vendas
> 💰 Faturamento fechado: R$ 4.890,00

🎯 2. META DE MAIO & PACE

> Meta do mês: R$ 7.700,00
> Realizado até o momento: R$ 4.890,00
> Já atingimos aproximadamente 63% da meta mensal logo no início do mês 🔥

📈 O cenário segue positivo e totalmente possível de virar mais um mês acima da meta, principalmente considerando que no mês passado conseguimos superar o objetivo com consistência. O time já mostrou capacidade de entrega — agora é manter ritmo, acompanhamento comercial e velocidade no atendimento.

📈 3. INSIGHTS DE PERFORMANCE

> CTR atual em 16,29%, mostrando boa aderência entre campanha e público
> Taxa de conversão geral em 5,71%, mantendo qualidade na geração de demanda
> CAC atual em R$ 227,64, mantendo aquisição saudável para o ticket da operação

🚀 4. DIRECIONAMENTOS DA SEMANA

> Continuidade das otimizações das campanhas Meta e Google
> Acompanhamento próximo do fundo do funil para acelerar novas vendas
> Monitoramento diário do pace da meta e evolução dos MQLs
> Seguimos acompanhando a operação comercial junto ao Fernando para evolução das oportunidades

💬 Caso existam atualizações comerciais ou movimentações no funil, aguardamos atualização ou alinhamos tudo no acompanhamento comercial com o Fernando. 🤝

Boa semana! 🚀
```

---

## Observações Finais

Esta skill foi desenvolvida para profissionalizar e padronizar a comunicação de atendimento diário, garantindo que cada mensagem:

- Traga valor estratégico (não apenas relatório de números)
- Demonstre domínio da operação
- Oriente o cliente sobre próximos passos
- Reforce a parceria e acompanhamento ativo

O diferencial está em **transformar dados em diagnóstico, diagnóstico em ação, e ação em resultado esperado**.
