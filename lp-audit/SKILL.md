# Skill: lp-audit

Realiza uma **auditoria tecnica e visual** de landing pages: captura screenshots das areas problematicas, pontua 6 dimensoes (codigo, performance, SEO, acessibilidade, design e CRO) e entrega um **relatorio HTML no layout V4 Company** (Red Command Center) com as evidencias visuais e prioridades de acao.

## Quando usar

Sempre que o usuario quiser auditar uma landing page. **O fluxo padrao e sempre arquivo local** - o usuario sobe os arquivos e Claude gera o relatorio.

---

## Como executar

### 1. Coletar o alvo

O usuario sempre fornecera um arquivo local (HTML + CSS/JS opcionais). Se nao informou o caminho, pergunte:

> "Qual o caminho do arquivo HTML da landing page?"

Defina:
- `ALVO_PATH` - caminho absoluto do arquivo HTML local
- `ALVO_URL` - construa como `file:///[ALVO_PATH com barras]` para uso no Playwright
- `NOME_SLUG` - nome curto da pagina em kebab-case (ex: `emaster-lp`, `well-service-home`)

**Nunca presuma que a analise sera feita por URL publica.** Se o usuario fornecer uma URL, use-a, mas o padrao e sempre arquivo local.

---

### 2. Preparar pasta de output

```
lp-audit-output/[NOME_SLUG]/
  screenshots/
  relatorio.html
```

```powershell
New-Item -ItemType Directory -Force "lp-audit-output/[NOME_SLUG]/screenshots"
```

---

### 3. Capturar screenshots com Playwright

#### 3a. Verificar disponibilidade

```powershell
npx playwright --version
```

#### 3b. Se disponivel: capturar os 4 prints obrigatorios

Crie `lp-audit-screenshot.js` temporario:

```javascript
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const url = process.argv[2];
  const outDir = process.argv[3];

  const desktop = await browser.newPage();
  await desktop.setViewportSize({ width: 1440, height: 900 });
  await desktop.goto(url, { waitUntil: 'networkidle', timeout: 30000 });
  await desktop.screenshot({ path: `${outDir}/desktop-full.png`, fullPage: true });
  await desktop.screenshot({ path: `${outDir}/desktop-fold.png`, fullPage: false });

  const mobile = await browser.newPage();
  await mobile.setViewportSize({ width: 375, height: 812 });
  await mobile.goto(url, { waitUntil: 'networkidle', timeout: 30000 });
  await mobile.screenshot({ path: `${outDir}/mobile-full.png`, fullPage: true });
  await mobile.screenshot({ path: `${outDir}/mobile-fold.png`, fullPage: false });

  await browser.close();
  console.log('SCREENSHOTS_OK');
})();
```

Execute e remova o script apos uso:
```powershell
node lp-audit-screenshot.js "[ALVO_URL]" "lp-audit-output/[NOME_SLUG]/screenshots"
Remove-Item lp-audit-screenshot.js
```

#### 3c. Se Playwright NAO estiver disponivel

Tente instalar:
```powershell
npm install -g playwright; npx playwright install chromium
```

Se falhar, registre `SCREENSHOTS_UNAVAILABLE` e siga sem imagens - o relatorio tera placeholders explicando o que seria capturado.

---

### 4. Ler e analisar o codigo

- Arquivo local: use `Read` para o HTML; `Glob` + `Read` para CSS linkados
- URL: use `WebFetch`

Extraia: titulo, meta description, objetivo (lead/venda/agendamento), stack, analytics/pixels presentes.

---

### 5. Executar as 6 dimensoes de auditoria

Para cada dimensao atribua **nota 0-10** e liste achados com referencia ao elemento/linha.

#### D1 - Estrutura Tecnica e Codigo (peso 15%)
- HTML semantico (`<header>`, `<main>`, `<section>`, `<footer>`)
- `<h1>` unico, sequencia logica de headings
- Render-blocking (CSS/JS no `<head>` sem `async`/`defer`)
- `viewport` meta tag presente
- Inline styles excessivos
- Scripts duplicados ou conflitantes

#### D2 - Performance / Core Web Vitals (peso 20%)
- **LCP**: imagem hero com `loading="eager"` e `fetchpriority="high"`? CSS critico inline?
- **CLS**: imagens com `width`/`height` definidos? Fontes com `font-display: swap`?
- **FID/INP**: scripts pesados sem `async`/`defer`? Third-party sem lazy/idle?
- `preconnect`/`preload` para recursos criticos
- Numero de requests externos identificaveis

#### D3 - SEO On-Page (peso 15%)
- `<title>` entre 50-60 chars
- `<meta description>` entre 150-160 chars
- Open Graph completo (`og:title`, `og:description`, `og:image`, `og:url`)
- Todas as imagens com `alt` descritivo
- Canonical tag, Schema.org

#### D4 - Acessibilidade WCAG 2.1 AA (peso 10%)
- `<img>` com `alt`
- Contraste - identifique combinacoes suspeitas
- `<label>` associado a cada `<input>`
- CTAs com texto descritivo (nao apenas "Clique aqui")
- `outline` de foco nao removido sem substituto

#### D5 - Design e Hierarquia Visual (peso 20%)
- **Above the fold**: headline + subheadline + CTA primario visiveis sem scroll?
- **Tipografia**: contraste de tamanhos headline/body/CTA?
- **Proposta de valor**: clara nos primeiros 5 segundos?
- **Paleta**: coesa? CTA em cor que contrasta com o fundo?
- **Mobile**: breakpoints presentes, texto legivel, CTA acessivel?

#### D6 - CRO (peso 20%)
- CTA primario unico e dominante above the fold, com verbo de acao
- Formulario com <= 3 campos
- Prova social (depoimentos, logos, numeros)
- Urgencia/escassez (countdown, vagas limitadas)
- Garantia visivel / politica de privacidade
- Ausencia de distracoes (menu completo, links externos)

---

### 6. Calcular o Score Geral

```
Score = (D1x0.15) + (D2x0.20) + (D3x0.15) + (D4x0.10) + (D5x0.20) + (D6x0.20)
```

- >= 8.5 -> Excelente
- 7.0-8.4 -> Bom, ajustes pontuais
- 5.0-6.9 -> Mediano, revisao relevante
- < 5.0 -> Critico, revisao profunda

---

### 7. Gerar o relatorio HTML V4

Salve em `lp-audit-output/[NOME_SLUG]/relatorio.html`.

**CSS**: leia `C:\Users\marri\OneDrive\Area de Trabalho\V4\v4-design-system\tokens-relatorios-v4.css` e emita o conteudo completo dentro de `<style>` para o arquivo ser auto-contido.

**Template base**: `C:\Users\marri\OneDrive\Area de Trabalho\V4\v4-design-system\template-relatorio-v4.html`

**Estrutura obrigatoria:**

```html
<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Auditoria LP - [NOME_SLUG]</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wdth,wght@75..100,500;75..100,700&display=swap" rel="stylesheet">
  <style>
    /* CONTEUDO COMPLETO DO tokens-relatorios-v4.css AQUI */
    .screenshot-box { position: relative; border-radius: 18px; overflow: hidden; border: 1px solid var(--line); }
    .screenshot-box img { width: 100%; display: block; }
    .annotation { position: absolute; border: 2px solid var(--danger); border-radius: 6px; background: rgba(255,42,26,0.18); }
    .annotation-label { position: absolute; top: -22px; left: 0; background: var(--danger); color: #fff; font-size: 11px; font-weight: 700; padding: 2px 8px; border-radius: 4px; white-space: nowrap; }
    .screenshots-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-top: 14px; }
    .screenshot-caption { margin-top: 8px; font-size: 12px; color: var(--text-muted); text-align: center; }
    .dim-row { display: grid; grid-template-columns: 28px 1fr auto; gap: 12px; align-items: start; padding: 14px 16px; border-bottom: 1px solid var(--line); }
    .dim-score { font-size: 22px; font-weight: 700; font-stretch: 75%; line-height: 1; }
    .finding { display: flex; gap: 8px; align-items: baseline; padding: 6px 0; font-size: 13px; color: var(--text-muted); }
    .find-icon { flex-shrink: 0; }
  </style>
</head>
<body>

  <header class="topbar">
    <div class="brand">
      <span class="brand-mark">
        <img src="C:\Users\marri\OneDrive\Area de Trabalho\V4\v4-design-system\assets\v4-company-logo-branca-oficial.svg" alt="V4 Company">
      </span>
    </div>
    <nav class="nav-pills">
      <a href="#visao-geral">Visao Geral</a>
      <a href="#screenshots">Screenshots</a>
      <a href="#dimensoes">Dimensoes</a>
      <a href="#prioridades">Prioridades</a>
    </nav>
  </header>

  <main class="report-shell">

    <section class="hero" id="visao-geral">
      <div class="hero-card hero-watermark" data-watermark="LP">
        <div class="eyebrow">Auditoria de Landing Page - [DATA] - [arquivo ou URL]</div>
        <h1>Auditoria LP - [Nome da pagina].</h1>
        <p>[Objetivo detectado, stack, analytics presentes.]</p>
      </div>
      <aside class="verdict glass">
        <div>
          <div class="eyebrow">Score Geral</div>
          <strong>[X.X]</strong>
          <span>[Classificacao] - [diagnostico em 1 linha]</span>
        </div>
        <div class="pill">[Classificacao]</div>
      </aside>
    </section>

    <div class="cards" style="grid-template-columns: repeat(6, minmax(0,1fr));">
      <div class="metric"><div class="metric-label">Codigo</div><div class="metric-number [safe|care|danger]">[D1]</div><small>Estrutura tecnica</small></div>
      <div class="metric"><div class="metric-label">Performance</div><div class="metric-number [safe|care|danger]">[D2]</div><small>Core Web Vitals</small></div>
      <div class="metric"><div class="metric-label">SEO</div><div class="metric-number [safe|care|danger]">[D3]</div><small>On-page</small></div>
      <div class="metric"><div class="metric-label">Acessibilidade</div><div class="metric-number [safe|care|danger]">[D4]</div><small>WCAG 2.1 AA</small></div>
      <div class="metric"><div class="metric-label">Design</div><div class="metric-number [safe|care|danger]">[D5]</div><small>Hierarquia visual</small></div>
      <div class="metric"><div class="metric-label">CRO</div><div class="metric-number [safe|care|danger]">[D6]</div><small>Conversao</small></div>
    </div>

    <section class="callout">
      <div class="eyebrow">Diagnostico principal</div>
      <h2>[Problema de maior impacto em 1 frase]</h2>
      <p>[Por que esse problema reduz conversao e o que precisa mudar.]</p>
    </section>

    <section id="screenshots">
      <div class="section-head">
        <div><div class="eyebrow">Evidencias Visuais</div><h2>O que foi identificado nos prints.</h2></div>
        <p>Anotacoes em vermelho indicam os problemas encontrados.</p>
      </div>
      <div class="screenshots-grid">
        <div>
          <div class="screenshot-box">
            <img src="./screenshots/desktop-fold.png" alt="Desktop - above the fold">
            <!-- <div class="annotation" style="top:12%;left:4%;width:62%;height:18%;"><span class="annotation-label">Descricao do problema</span></div> -->
          </div>
          <p class="screenshot-caption">Desktop - Above the fold - 1440px</p>
        </div>
        <div>
          <div class="screenshot-box"><img src="./screenshots/mobile-fold.png" alt="Mobile - above the fold"></div>
          <p class="screenshot-caption">Mobile - Above the fold - 375px</p>
        </div>
        <div>
          <div class="screenshot-box"><img src="./screenshots/desktop-full.png" alt="Desktop - pagina completa"></div>
          <p class="screenshot-caption">Desktop - Pagina completa</p>
        </div>
        <div>
          <div class="screenshot-box"><img src="./screenshots/mobile-full.png" alt="Mobile - pagina completa"></div>
          <p class="screenshot-caption">Mobile - Pagina completa</p>
        </div>
      </div>
    </section>

    <section id="dimensoes">
      <div class="section-head"><div><div class="eyebrow">Analise por Dimensao</div><h2>Achados detalhados.</h2></div></div>
      <div class="table-card">
        <!-- Repetir este bloco para cada dimensao D1 a D6 -->
        <div class="dim-row">
          <div class="dim-score [safe|care|danger]">[nota]</div>
          <div>
            <div style="font-weight:700;margin-bottom:8px;">[Nome da dimensao]</div>
            <div class="finding"><span class="find-icon">checkmark</span><span>[achado positivo]</span></div>
            <div class="finding"><span class="find-icon">aviso</span><span>[ponto de atencao]</span></div>
            <div class="finding"><span class="find-icon">erro</span><span>[problema critico com linha/elemento]</span></div>
          </div>
          <div class="tag">Peso [X]%</div>
        </div>
      </div>
    </section>

    <section id="prioridades">
      <div class="section-head">
        <div><div class="eyebrow">Plano de Acao</div><h2>Top 5 prioridades por impacto.</h2></div>
        <p>Ordenadas do maior para o menor impacto na taxa de conversao.</p>
      </div>
      <details open>
        <summary>Prioridades de Design e CRO</summary>
        <div class="list">
          <div class="item"><span>1. [Acao concreta]</span><span class="tag bad">Alto impacto</span></div>
          <div class="item"><span>2. [Acao concreta]</span><span class="tag bad">Alto impacto</span></div>
          <div class="item"><span>3. [Acao concreta]</span><span class="tag">Medio impacto</span></div>
        </div>
      </details>
      <details open>
        <summary>Prioridades Tecnicas</summary>
        <div class="list">
          <div class="item"><span>4. [Acao concreta]</span><span class="tag">Medio impacto</span></div>
          <div class="item"><span>5. [Acao concreta]</span><span class="tag good">Quick win</span></div>
        </div>
      </details>
    </section>

    <section>
      <div class="section-head"><div><div class="eyebrow">Metodo</div><h2>Como esta auditoria foi feita.</h2></div></div>
      <div class="table-card">
        <table><tbody>
          <tr><td>Fonte</td><td class="muted">[URL ou arquivo analisado]</td></tr>
          <tr><td>Data</td><td class="muted">[Data da analise]</td></tr>
          <tr><td>Viewport</td><td class="muted">Desktop 1440px - Mobile 375px</td></tr>
          <tr><td>Screenshots</td><td class="muted">[Playwright disponivel / indisponivel]</td></tr>
          <tr><td>Analise</td><td class="muted">Estatica (HTML/CSS/JS) + inspecao visual dos screenshots</td></tr>
          <tr><td>Limitacoes</td><td class="muted">Velocidade real de rede e metricas de analytics nao verificaveis via analise estatica.</td></tr>
        </tbody></table>
      </div>
    </section>

  </main>
</body>
</html>
```

**Ao gerar o HTML final:**
1. Leia `C:\Users\marri\OneDrive\Area de Trabalho\V4\v4-design-system\tokens-relatorios-v4.css` e emita o conteudo completo dentro de `<style>`.
2. Substitua TODOS os placeholders `[...]` com dados reais.
3. Adicione `.annotation` nos screenshots para cada problema visual identificado.
4. Notas: `safe` (verde) >= 7, `care` (amarelo) 5-6.9, `danger` (vermelho) < 5.

---

### 8. Abrir o relatorio no browser

```powershell
Start-Process "lp-audit-output/[NOME_SLUG]/relatorio.html"
```

Informe ao usuario o caminho completo do arquivo gerado.

---

## Regras

1. **Analise o codigo real** - leia os arquivos antes de pontuar. Nunca presuma.
2. **Seja especifico** - cite linha, classe CSS, elemento ou atributo quando possivel.
3. **Nao infle notas** - CTA fraco = CRO <= 5, mesmo que o restante seja bom.
4. **Screenshots sao obrigatorios** - tente Playwright; so pule se ambos os fallbacks falharem.
5. **Anotacoes nos prints sao obrigatorias** - `.annotation` para cada achado de design/CRO.
6. **Top 5 prioridades sao obrigatorias** - sem esse bloco o relatorio esta incompleto.
7. **CSS V4 sempre embutido** - leia e inclua o `tokens-relatorios-v4.css` no `<style>`.
8. **Nunca invente dados** - se nao verificavel, indique "nao verificavel via analise estatica".
9. **Remova arquivos temporarios** - `lp-audit-screenshot.js` deletado apos uso.
10. **Se URL der erro (403, timeout)** - informe e peca o HTML como arquivo local.
