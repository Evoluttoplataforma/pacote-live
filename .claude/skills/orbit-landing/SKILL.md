---
name: orbit-landing
description: Cria uma landing page de captação completa no padrão visual da Orbit (design system Orbit), do briefing ao deploy. Use SEMPRE que o usuário pedir uma landing page, página de captação, página de vendas, hero de campanha, página de evento, "uma página pra rodar tráfego", ou mencionar criar/subir um site da Orbit — mesmo que não diga "landing page" explicitamente. Cobre o fluxo inteiro: entrevista de briefing, pesquisa de público com subagentes, copy de resposta direta, build em React+Tailwind, revisão visual e de copy com nota de aprovação, e deploy automático no GitHub + Vercel.
---

# Orbit Landing — fábrica de landing pages

Esta skill transforma um briefing curto em uma landing page publicada, no design system da Orbit, em poucos minutos. O trabalho pesado fica aqui na skill e nos arquivos de `references/`; o usuário só precisa disparar e responder a uma entrevista curta.

## Princípio anti-alucinação (obrigatório)

A Orbit trabalha com disciplina de evidência. Em TODO output desta skill (briefing, pesquisa, copy), marque cada afirmação relevante sobre o público/mercado como:

- `[evidência]` — veio de busca real na web nesta sessão (cite a fonte).
- `[hipótese]` — é uma suposição plausível, ainda não verificada.
- `[pendência]` — depende de algo que o usuário ainda precisa fornecer.

Nunca apresente "o que as pessoas reclamam em fóruns/Reclame Aqui" como fato sem ter buscado de verdade. Se não buscou, é `[hipótese]`. Não invente reviews, números ou dores.

## Pré-requisitos (checar no início, uma vez)

Antes da primeira página, confirme rapidamente — sem travar o fluxo:

1. **Design system Orbit** já está preenchido em `references/design-system.md` com tokens reais (dourado `#ffba1a` + dark institucional, Plus Jakarta Sans, temas escuro e claro). Só refaça o **Passo 0** se a marca mudar. Pendência conhecida: mapeamento visual EMPRESA B2B × CONSULTOR (`[pendência]`).
2. **`gh` (GitHub CLI)** autenticado: `gh auth status`. Se não, peça `gh auth login`.
3. **`vercel` CLI** instalado e logado: `vercel whoami`. Se não, peça `npm i -g vercel && vercel login`.
4. **Playwright MCP** disponível para a revisão visual. Se não estiver, faça a revisão visual via build local + screenshots e avise que a checagem é mais limitada.

Liste o que estiver faltando como `[pendência]` e siga com o que dá.

---

## Passo 0 — Manutenção do design system (só se a marca mudar)

`references/design-system.md` já foi preenchido a partir dos DS oficiais da Orbit
(tema escuro + tema claro). Não invente cores/fontes — use o arquivo.

Refaça este passo apenas se a identidade visual mudar:

1. Clone/leia o repositório de referência.
2. Extraia tokens reais: paleta (hex), tipografia (famílias, pesos, escala), raios, sombras, espaçamentos, componentes recorrentes (botão primário, card, badge), e a "vibe" (ex.: tech/confiança, alto contraste).
3. Escreva tudo em `references/design-system.md`, substituindo os placeholders.
4. Mostre ao usuário um resumo dos tokens para aprovação antes de seguir.

A partir daí, todas as páginas leem `references/design-system.md`. Atualize esse arquivo se a marca mudar.

---

## Fluxo principal

### 1. Briefing por entrevista (modo planejamento)

Não comece a buildar com base só na primeira frase do usuário — quase sempre faltam decisões. Entre em **plan mode** (Shift+Tab) ou peça `/plan` e **entreviste** o usuário, fazendo apenas as perguntas que ainda não foram respondidas. Capture:

- **Nicho/cliente** e **segmento Orbit**: EMPRESA B2B ou CONSULTOR (muda copy, prova e CTA).
- **Objetivo de conversão**: agendamento, lead/PCI, trial, inscrição em evento.
- **Oferta e diferencial-chave** (o argumento concreto, não adjetivo).
- **Prova social disponível**: depoimentos, logos, números — e o que é real vs. o que falta (`[pendência]`).
- **Ativos**: vídeos (Vimeo/YouTube), imagens, logos.
- **Domínio/URL** desejado e nome do repositório.
- **Stack alvo**: por padrão **Vite + React + Tailwind** (deploy fácil na Vercel). Use HTML estático só se o usuário pedir.

Feche o briefing em um bloco curto que o usuário aprova antes de seguir. Marque cada item como `[evidência]`/`[hipótese]`/`[pendência]`.

### 2. Pesquisa de público com subagentes (em paralelo)

Dispare subagentes **em paralelo**, cada um com um foco distinto, para reduzir tempo e diversificar perspectivas. Sugestão de divisão:

- **Subagente A** — dores e linguagem do público (busca real na web; cite fontes). Mapeie medos, objeções e o vocabulário que a persona usa.
- **Subagente B** — concorrentes/ofertas similares (o que prometem, ângulos, provas).
- **Subagente C** — referências de conversão para o objetivo definido (estrutura de página que costuma performar para esse tipo de oferta).

Quanto mais específico o escopo de cada subagente, melhor o resultado. Consolide num resumo de inteligência com tudo marcado `[evidência]`/`[hipótese]`.

> Se Playwright/web não estiver disponível para algum subagente, marque a lacuna como `[hipótese]` e siga; não fabrique dados.

### 3. Copy de resposta direta

Leia `references/copy-playbook.md` e produza a copy **completa e real** (sem Lorem Ipsum), ajustada ao segmento (B2B x Consultor). Saída esperada:

- Headline (Sistema 1) + subheadline.
- Blocos no framework PAS (Problema → Agitação → Solução).
- Bullets de benefício (transformação, não feature).
- Prova social (usar a real; se faltar, deixar slot marcado `[pendência]`, nunca inventar depoimento).
- CTA(s) alinhados ao objetivo.
- FAQ que quebra objeções levantadas na pesquisa.

### 4. Build com subagentes em áreas separadas

Para evitar que um subagente sobrescreva o trabalho do outro, **divida por área de arquivo**, não pela mesma área:

- **Subagente de estrutura/layout**: monta o esqueleto da página (Hero, VSL/vídeo, Prova Social, Grid de Benefícios, FAQ, CTA fixo/sticky), responsivo, mobile-first, componentes em arquivos separados.
- **Subagente de conteúdo/estilo**: injeta a copy do Passo 3 e aplica os tokens de `references/design-system.md`.

Regras de build:
- Aplicar **fielmente** o design system Orbit (cores, tipografia, espaçamento, componentes). Sem cores aleatórias.
- Mobile-first: empilhar colunas no mobile, alvos de toque ≥ 44px.
- Acessibilidade básica (contraste, alt, foco).
- Se a base for um repositório existente, **leia o HTML/JSX atual antes** de gerar mudanças estruturais e prefira diffs revisáveis a reescritas grandes.

### 5. Revisão (loop com nota) — antes do deploy

Crie um loop de QA explícito. Leia `references/review.md` para os critérios e gere uma **nota 0–100**:

1. **Revisão visual** via Playwright MCP: abrir a página, screenshots em desktop e mobile, checar overlaps, fontes/quebras, responsividade, e se o visual bate com o design system.
2. **Revisão de copy**: consistência entre seções, alinhamento à marca Orbit, ausência de "cara de IA"/AI-slop, CTA claro.

Limiar de aprovação: **≥ 90**. Abaixo disso, o agente que produziu volta e corrige; repita até passar (máx. 3 ciclos, depois escale ao usuário). Registre cada problema encontrado em `references/error-log.md` para a página não repetir os mesmos erros em builds futuros.

### 6. Deploy automático (GitHub + Vercel)

Deploy é determinístico → use o script. Rode `scripts/deploy.sh`:

```bash
bash scripts/deploy.sh "<nome-do-repo>" "<descrição curta>"
```

O script: inicializa git, faz commit, cria o repo no GitHub (`gh repo create`), faz push, e publica na Vercel (`vercel --prod`). Ao final, **retorne a URL de produção** ao usuário. Se algum passo falhar (auth, nome duplicado), reporte o erro exato e o comando para resolver — não tente "contornar" silenciosamente.

---

## Saída final ao usuário

Depois do deploy, entregue um resumo enxuto:

```
✅ Landing publicada
- URL de produção: <url da Vercel>
- Repositório: <url do GitHub>
- Segmento: <B2B | Consultor>
- Nota de revisão: <0–100>
- Pendências: <lista do que ainda precisa de ativo real / aprovação>
```

## Quando NÃO usar subagente ou automação

Seguindo a lógica da aula: automatize/paralelize o que é determinístico (deploy, pesquisa em paralelo, QA). Não automatize o que exige criatividade variável (a copy em si, escolha de ângulo). Não crie scripts para coisas que você roda uma vez a cada vários meses — não vale o overhead.

## Arquivos de referência

- `references/design-system.md` — tokens reais da Orbit (extrair no Passo 0). **Fonte da verdade visual.**
- `references/copy-playbook.md` — método de copy (Schwartz/Hopkins, PAS, JTBD, power words).
- `references/review.md` — rubrica de revisão visual e de copy (0–100).
- `references/error-log.md` — memória de erros recorrentes para não repetir.
- `scripts/deploy.sh` — git + GitHub + Vercel.
