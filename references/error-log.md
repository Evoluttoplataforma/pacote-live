# Error Log — QA Builds

## Build: Mudancas B+C+D (FAQ gravacao + Urgency badge + WhatsApp block)
**Data:** 2026-06-27
**Arquivo:** index.html

### CORRECOES NECESSARIAS (build atual, ciclo 1)

**E1 — CSS: texto centralizado no bloco WhatsApp (VISUAL)**
- Arquivo: index.html, linha ~397
- O div do bloco WhatsApp usa `display:inline-flex` dentro de `.final` que tem `text-align:center`.
- O `<p class="note">` interno nao tem `text-align:left`, entao o texto de ~100 chars (que quebra em 2+ linhas dentro do max-width:440px) fica centralizado — alinhamento centro-justificado incomum para corpo de texto.
- Correcao: adicionar `text-align:left` no estilo inline do `<p class="note">` interno ao bloco WA, ou no proprio div container.

**E2 — ACESSIBILIDADE: SVG do WhatsApp sem aria-hidden (MENOR)**
- Arquivo: index.html, linha ~398
- O `<svg>` do icone WhatsApp e decorativo (o texto adjacente ja descreve a acao), mas nao tem `aria-hidden="true"`. Leitores de tela vao anunciar o SVG sem label — provavelmente como elemento vazio/inutil.
- Correcao: adicionar `aria-hidden="true"` ao SVG do WhatsApp.

### ITENS VERIFICADOS E APROVADOS

- HTML valido: tags details/summary balanceadas (6 open / 6 close cada).
- JS urgency badge: `getElementById`, `display:none` como default, visivel so se `diff > 0`. Correto.
- JS target date: `new Date('2026-07-02T18:00:00-03:00')` — correto.
- Copy FAQ gravacao: honesta (nao promete replay), FOMO sutil, menciona WhatsApp. Aprovado.
- Placeholder `LINK_GRUPO_WHATSAPP`: intencional, nao e erro.
- CSS urgency badge: usa `var(--glow-2)` para cor, literais rgba consistentes com o restante do design system.
- Estrutura kicker: badge aparece apos `.when-pill`, antes do H1 — ordem logica.
- `overflow-x:hidden` no body — protege contra scroll horizontal.
- Media query `@media (max-width:880px)`: `.final{padding:42px 24px}` presente.
- `prefers-reduced-motion`: regra presente e correta.
- Icones arrow com `aria-hidden="true"`: correto.
