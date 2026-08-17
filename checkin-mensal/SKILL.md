---

name: checkin-mensal

description: Conduz e monta o check-in mensal completo de um cliente V4, desde a entrevista consultiva até o deploy do relatório HTML no Vercel. Use esta skill sempre que o usuário mencionar "check-in mensal", "relatório mensal", "montar o check-in", "checkin do [cliente]", ou pedir para gerar/publicar o relatório de resultado do mês de qualquer cliente. Também deve ser acionada quando o usuário enviar dados mensais de um cliente e pedir para transformar em relatório ou apresentação. Ative mesmo que o usuário não mencione "skill" — se o contexto for montagem de resultado mensal de cliente, use esta skill.

---



# Check-in Mensal V4



## Objetivo



Conduzir o processo completo de montagem do check-in mensal de um cliente V4: entrevistar o gestor de conta, extrair dados das fontes ativas, gerar o HTML no design system e fazer deploy no Vercel do cliente.



O check-in não é um relatório operacional — é uma **apresentação consultiva em formato slideshow** que o cliente lê e sai com clareza sobre: onde estava, onde chegou, por que, e o que vem a seguir.



---



## Formato padrão: Slideshow/Deck



O check-in mensal usa **formato de deck com slides**, não scroll de página. Estrutura:

- Cada slide é um `<div class="slide" id="slide-N">` com `opacity:0` por padrão
- O slide ativo recebe a classe `.active` que define `opacity:1`
- Navegação via setas (`nav-arrow prev/next`), dots e `nav-pills` no header de cada slide
- `const TOTAL = N` define o total de slides para o script de navegação
- Função `goToSlide(N)` usada nos `nav-pills` e âncoras

**Template base:** `checkin-julho-2026-comp.html` em `Clientes/Compass/checkins/` — é o check-in mais completo e recente. Clone e adapte para qualquer novo cliente.



---



## Fluxo Geral



```

Fase 0 → Entrevista do mês (você fala, eu escuto)

Fase 1 → Contexto do cliente (automático via CLAUDE.md)

Fase 2 → Narrativa do mês (baseada na entrevista)

Fase 3 → Dados por seção (Growth Pack + complementos)

Fase 4 → Seções fixas (premissas, entregas, próximos passos)

Fase 5 → Publicação (HTML → Vercel → arquivamento)

```



---



## Fase 0 — Entrevista do Mês



**Execute esta fase SEMPRE, antes de abrir qualquer planilha.**



Faça as perguntas abaixo em sequência, uma por vez ou em bloco conforme o ritmo do usuário. Não pule para os dados até ter as respostas.



### Perguntas obrigatórias



1. **Performance geral:** "Como você avalia o mês de [cliente]? Foi um mês positivo, misto ou difícil?"

2. **Destaque positivo:** "O que foi bem e você quer que o cliente veja com clareza?"

3. **Gap ou risco:** "O que foi mal ou ficou abaixo do esperado? Como você quer abordar isso?"

4. **Surpresa:** "Teve algo que surpreendeu — positivo ou negativo?"

5. **Relação com o cliente:** "Como está o nível de confiança com esse cliente agora?"

6. **Tom desejado:** "O que você quer que ele sinta ao fechar o relatório? (ex: animado com o crescimento / tranquilo apesar de um mês difícil / confiante no processo)"

7. **Melhores Criativos:** "Vamos incluir a seção de Melhores Criativos (Meta Ads) neste check-in? Se sim, me manda os dados de cada criativo: nome/código, leads, CTR, CPL e valor investido, e as imagens na pasta de deploy."

8. **Impulsionamentos:** "Vamos incluir a seção de Top 3 Impulsionamentos (posts impulsionados)? Se sim, me manda os dados ou prints dos posts com maior resultado — e os frames/thumbnails na pasta `assets/vencedores/`."

9. **Plano de Ação:** "Há ações específicas em andamento para o próximo mês que merecem destaque no slide de Plano de Ação? Se sim, quantas abas precisamos? (ex: Campanha de remarketing, Status WhatsApp, Campanha regional…)"



### O que fazer com as respostas



Com as respostas em mãos, defina antes de escrever qualquer seção:



- **Tom do relatório:** celebração / estabilização / recuperação de confiança / alerta antecipado

- **Hero do mês:** qual número ou resultado vai abrir o relatório

- **Callouts:** quais 2–3 momentos merecem destaque editorial

- **Enquadramento dos gaps:** como nomear o que foi mal sem alarmar desnecessariamente



Registre internamente esses 4 elementos — eles guiam a escrita de todas as seções seguintes.



---



## Fase 1 — Contexto do Cliente



Após a entrevista, leia o `CLAUDE.md` do cliente (se disponível no contexto ou indicado pelo usuário).



O `CLAUDE.md` deve conter:

- **growth_pack_url** — link da planilha Google Sheets

- **vercel_project** — nome do projeto no Vercel (ex: `gigaclima-checkin`)

- **segmento** — tipo de operação (sales, e-commerce, híbrido, etc.)

- **seções_ativas** — quais blocos aparecem nesse cliente

- **nome_display** — como o nome do cliente aparece no relatório

- **plano_midia_url** — link externo do plano de mídia mensal (se presente, exibe slide com botão CTA dourado)



Se o `CLAUDE.md` não existir ou estiver incompleto, pergunte ao usuário os campos faltantes antes de continuar.



Confirme com o usuário:

- Mês de referência (ex: "Julho 2026")

- Período exato (ex: "01/07 a 31/07")

- Data de apresentação ao cliente



---



## Fase 2 — Narrativa do Mês



Com a entrevista (Fase 0) e o contexto (Fase 1) em mãos, escreva:



### Hero do relatório

Frase de abertura de 1–2 linhas que resume o mês com o tom certo. Exemplos:

- Tom celebração: "Julho foi o melhor mês do histórico — e os dados mostram por quê."

- Tom misto: "Julho trouxe avanços reais na geração de leads e aprendizados importantes no comercial."

- Tom difícil: "Foi um mês de ajustes. Os fundamentos seguem sólidos e os próximos passos estão claros."



### Callouts editoriais (2–3)

Bullets curtos de destaque que aparecem logo após o hero. Um por linha. Máximo 15 palavras cada.



Apresente hero + callouts ao usuário para aprovação antes de seguir.



---



## Fase 3 — Dados por Seção



Leia as seções ativas do cliente e preencha cada uma. Veja `references/secoes.md` para a estrutura detalhada de cada seção.



### Fonte principal: Growth Pack



Acesse a planilha via Google Drive MCP ou peça o link ao usuário. Aba prioritária: **ACOMPANHAMENTO MENSAL**.



Extraia:

- Meta do mês vs. realizado

- Investimento vs. retorno (ROAS / ROI)

- Leads gerados, MQLs, SQLs, vendas fechadas

- CPL, CAC, ticket médio (se disponível)



### Seções por tipo de cliente



| Seção | Sales | E-commerce | Sempre |

|---|---|---|---|

| Resultado Geral | ✓ | ✓ | ✓ |

| Funil de Vendas | ✓ | — | — |

| Funil E-commerce | — | ✓ | — |

| Projeção do Mês | ✓ | ✓ | ✓ |

| Propostas / Pipeline | ✓ | — | — |

| Performance de Mídia | ✓ | ✓ | ✓ |

| Plano de Mídia Mensal | condicional | condicional | — |

| Melhores Criativos (Meta Ads) | condicional | condicional | — |

| Top 3 Impulsionamentos | condicional | condicional | — |

| Palavras-chave (Google Ads) | condicional | condicional | — |

| Plano de Ação em Andamento | condicional | condicional | — |

| E-commerce (métricas) | — | ✓ | — |



**Plano de Mídia Mensal:** exibir se `plano_midia_url` estiver no `CLAUDE.md`.

**Melhores Criativos:** exibir se confirmado na pergunta 7 da Fase 0.

**Top 3 Impulsionamentos:** exibir se confirmado na pergunta 8 da Fase 0. Requer imagens/frames dos posts em `assets/vencedores/`.

**Palavras-chave:** exibir se o cliente tiver Google Ads com dados de conversão disponíveis.

**Plano de Ação:** exibir se confirmado na pergunta 9 da Fase 0. Usa sistema de abas — cada ação vira uma aba.



### Notas de contexto nos slides de funil



Se houver limitações de visibilidade de dados no funil (ex: SQL não rastreável porque filiais só reportam fechamentos, não propostas enviadas), adicionar nota de rodapé com asterisco `*` no rótulo da métrica afetada, e um bloco de nota discreta na base do slide:

```html
<div style="display:flex;align-items:flex-start;padding-top:9px;gap:3px;border-top:1px solid rgba(255,255,255,.06);margin-top:8px">
  <span style="font-size:9px;font-weight:700;color:rgba(255,255,255,.3);flex-shrink:0;line-height:1.5">*</span>
  <span style="font-size:9px;color:rgba(255,255,255,.28);line-height:1.6">[Explicação da limitação de dados]</span>
</div>
```



Para seções condicionais sem dados confirmados, pergunte ao usuário antes de pular.



### Checklist de dados por seção



Antes de fechar a Fase 3, confirme com o usuário:

- [ ] Resultado Geral preenchido e validado

- [ ] Funil preenchido (sales ou e-commerce)

- [ ] Projeção calculada

- [ ] Seções condicionais: dados recebidos ou confirmados como ausentes

- [ ] Mês anterior disponível para comparativo (MoM)



---



## Fase 4 — Seções Fixas



### Premissas e Riscos



Gere com base no contexto do mês. Sempre inclua:

- O que foi considerado como baseline

- Variáveis externas que impactaram (sazonalidade, concorrência, mudanças de algoritmo)

- Riscos para o próximo mês



### Entregas do Mês



**Fonte preferencial: Growth Pack (Google Sheets).** Acesse via Google Drive MCP usando o `growth_pack_url` do `CLAUDE.md`. Filtre as tarefas com `status == "Concluída"` no mês de referência.



Se o Growth Pack não estiver disponível, acesse o Ekyte ou pergunte ao usuário quais foram as principais entregas.



Categorias padrão:

- **Campanhas & Mídia:** campanhas criadas/ajustadas, criativos de ads, otimizações de budget

- **Conteúdo & Criativos:** posts, vídeos, carrosséis, materiais gráficos

- **Gestão & Estratégia:** account planning, check-ins, ligações, atendimentos



Máximo 12 itens totais. Atendimentos/ligações recorrentes agrupam-se em uma única linha.



### Próximos Passos



**Fonte preferencial: Growth Pack (Google Sheets).** Filtre tarefas com `status != "Concluída"` — ou seja, Em andamento, A fazer, Atrasada. Ordene por prazo (mais urgente primeiro).



Complementar com o que foi mal (Fase 0) + oportunidades dos dados (Fase 3).



**Volume:** até 8–10 itens com prazo no mês corrente. Itens com prazo no mês seguinte ou além entram em bloco colapsível `<details>`.



**Formato de cada item:**

- Título da ação (verbo + objeto)

- Responsável (tag visual por pessoa ou equipe)

- Tag de prazo ("até DD/MM")

- Tag `danger` apenas se o item estiver atrasado ou for bloqueante para outra entrega



---



## Fase 5 — Publicação



### 1. Gerar o HTML



**Template base:** `Clientes/Compass/checkins/checkin-julho-2026-comp.html` — clone e adapte.

Consulte `references/html-template.md` para as regras de adaptação por segmento e os padrões de cada componente.



Regras obrigatórias:

- Substituir nome do cliente, período e métricas

- Ativar/desativar slides conforme `seções_ativas` do `CLAUDE.md`

- Manter o design system V4 Red Command Center (IBM Plex Sans, tokens de cor, glass cards)

- Atualizar `const TOTAL = N` com o número correto de slides

- Seções de e-commerce só aparecem para clientes com `segmento: ecommerce` ou `segmento: híbrido`



### 2. Deploy no Vercel



```

cd Clientes/[cliente]/checkins
cp checkin-[mes]-[ano]-[sigla].html index.html
vercel --prod --yes
vercel alias set [deployment-url] checkin-[mes]-[sigla].vercel.app
```

Verificar via WebFetch que a URL retorna 200 antes de passar ao cliente.



### 3. Confirmação final



Apresente ao usuário:

- URL do relatório publicado

- Resumo do que foi gerado (slides ativos, hero, tom)

- Próximo check-in sugerido (mês seguinte)



---



## Referências



- `references/secoes.md` — estrutura detalhada de cada seção/slide do relatório

- `references/html-template.md` — regras de clonagem e adaptação do template HTML (slideshow)

- `references/tom-editorial.md` — guia de voz e tom para cada cenário de mês



Leia apenas o arquivo relevante para a fase em execução.
