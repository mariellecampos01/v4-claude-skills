# v4-claude-skills

Skills do Claude Code usadas no dia a dia de atendimento/account da V4 Company. Cada pasta é uma skill autocontida (`SKILL.md` + assets/scripts quando aplicável), seguindo o formato de [Claude Skills](https://docs.claude.com/claude/docs/claude-code-skills).

## Skills

- **atendimento-diario-consultivo** — gera mensagens diárias de atendimento consultivo transformando métricas em visão estratégica.
- **checkin-mensal** — conduz e monta o check-in mensal completo de um cliente, da entrevista consultiva ao deploy do relatório HTML.
- **checkin-quarter** — gera apresentações de check-in trimestral (ROPRE): resultados do quarter, OKRs, criativos vencedores, projeção do próximo trimestre.

## Segurança

Nenhuma skill deste repositório contém tokens ou credenciais reais. Onde aparecem exemplos de token (ex: `eyJhbGc...`, `<EKYTE_TOKEN>`), são placeholders de instrução — os valores reais vivem em `.env` ou `~/.claude/mcp.json`, fora deste repositório.
