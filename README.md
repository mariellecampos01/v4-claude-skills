# v4-claude-skills

Skills do Claude Code usadas no dia a dia de atendimento/account da V4 Company. Cada pasta é uma skill autocontida (`SKILL.md` + assets/scripts quando aplicável), seguindo o formato de [Claude Skills](https://docs.claude.com/claude/docs/claude-code-skills).

## Skills

### Onboarding e KB de cliente
- **account-handoff** — primeira skill rodada ao receber cliente novo de vendas: lê form de kickoff + transcript da reunião de vendas e gera a KB inicial (resumo, CLAUDE.md/AGENTS.md, Mission Control preliminar, deck de kickoff).
- **account-pesquisa-profunda-cliente** — pesquisa profunda de cliente (Deep Research) para KB acionável, a partir dos dados já coletados no handoff.
- **contexto** — lê todos os arquivos de uma KB (cliente/squad/projeto) e gera/atualiza CLAUDE.md, AGENTS.md e Mission Control.
- **novo-cliente** — cria a estrutura de pastas padrão para um cliente novo (CLAUDE.md, links, calls, checkins, docs, campanhas).
- **outra-notebooklm-cadastrar** — cadastra/atualiza em massa os links de NotebookLM de clientes existentes.
- **cs-notebooklm-consulta-cliente** — consulta o NotebookLM de um cliente específico para trazer contexto sem carregar arquivos locais.

### Atendimento e relatórios
- **atendimento-diario-consultivo** — gera mensagens diárias de atendimento consultivo transformando métricas em visão estratégica.
- **checkin-quarter** — gera apresentações de check-in trimestral (ROPRE): resultados do quarter, OKRs, criativos vencedores, projeção do próximo trimestre.
- **dados-kommo-audit** — auditoria de atendimento comercial no Kommo (CRM): pipeline, timing de resposta, canal de origem, qualidade das conversas.
- **lp-audit** — auditoria técnica e visual de landing pages com relatório HTML no padrão V4.
- **gigaclima-dash-update** — atualiza o dashboard de tarefas da Gigaclima publicado no Vercel.

### Ekyte
- **ekyte-task** — cria tarefas no Ekyte via MCP com briefing estruturado no padrão Colli&Co.
- **ekyte-briefing** — monta briefings ricos para tarefas do Ekyte (usada como subskill da ekyte-task).
- **ekyte-briefing-refresh** — atualiza os caches de Drive e backups de CRM usados pela ekyte-briefing.
- **ekyte-templates-refresh** — atualiza os templates de briefing por sigla.
- **ekyte-refresh** — atualiza o cache local da ekyte-task (workspaces, projetos do trimestre, tipos de tarefa, fluxos).
- **gestao-ekyte-rename-tasks** — renomeia títulos de tarefas em lote via MCP.
- **gestao-ekyte-tags** — aplica etiquetas padronizadas em tarefas em lote via MCP.

### Frontend
- **frontend-design** — cria interfaces frontend de alta qualidade visual (base para relatórios/apresentações HTML no Design System V4 - Red Command Center).

## Segurança

Nenhuma skill deste repositório contém tokens ou credenciais reais. Onde aparecem exemplos de token (ex: `eyJhbGc...`, `<EKYTE_TOKEN>`), são placeholders de instrução — os valores reais vivem em `.env` ou `~/.claude/mcp.json`, fora deste repositório.
