# Design System Orbit — fonte da verdade visual

Extraído dos design systems oficiais da Orbit Gestão (produto Financeiro · v1):
- **Tema Escuro (default)** — base Tailwind, identidade "hero/produto".
- **Tema Claro (Variant B)** — base CSS vars, estrutura institucional/long-form (Templum/Aura).

Mesma marca nos dois: **dourado `#ffba1a` + dark institucional**, tipografia **Plus Jakarta Sans**.
O dourado é reservado para CTAs, destaques e a IA "Olívia" — não é cor de fundo de seção.
`[evidência]` = valores lidos direto dos arquivos enviados pelo Marco.

---

## 1. Cor

### Dourado (PRIMARY · CTA) — escala completa `[evidência]`
| Token | Hex |
|---|---|
| 50  | `#fff8e6` |
| 100 | `#fff0c2` |
| 200 | `#ffe487` |
| 300 | `#ffd64a` |
| 400 | `#ffca4a` |
| **500 / DEFAULT** | **`#ffba1a`** |
| 600 | `#e6a200` |
| 700 | `#b87f00` (hover/pressed) |
| 800 | `#8a5e00` |
| 900 | `#5c3f00` |

Acentos pontuais (tema claro): `--gold-mid #ffca4a`, `--gold-light #ffd66b`, `--amber #e6a200`, `--gold-bright #FFE066`, `--cream #FFF8E6`, `--cream-2 #FFFAF0`.

### Dark institucional (neutros — estilo GitHub dark) `[evidência]`
| Token | Hex | Uso |
|---|---|---|
| black | `#0D1117` | fundo principal (tema escuro) |
| black-soft | `#161B22` | superfícies elevadas |
| black-card | `#1C2333` | cards |
| gray-200 | `#30363D` | bordas |
| gray-300 | `#484F58` | bordas fortes |
| gray-500 | `#8B949E` | texto suave |
| gray-700 | `#C9D1D9` | texto secundário |
| gray-900 | `#E6EDF3` | texto claro |

### Tema claro — superfícies e texto `[evidência]`
- Fundo/paper: `#FFFFFF`; calor pontual: `--surface-warm #FFFAF0`
- Texto: `--text #18191B`, `--text-2 #3F424B`, `--text-mid rgba(24,25,27,.62)`, `--text-soft .42`, `--text-faint .18`
- Bordas: `rgba(24,25,27,.08)` / `.14` / `.22`

### Feedback (vale nos dois temas) `[evidência]`
- Sucesso: `#3FB950` · Erro/Perigo: `#F85149`

### Seleção de texto
- `::selection` → fundo dourado `#ffba1a`, texto `#0D1117`.

---

## 2. Tipografia `[evidência]`
- **Família única:** `Plus Jakarta Sans` (sans / display / headings). Pesos 400–800.
- **Mono (tema escuro):** `JetBrains Mono` — números, specs, labels técnicas.
- Headings: peso 600–800, `letter-spacing` negativo (-0.025 a -0.04em), `line-height` apertado (~1).

### Escala responsiva (clamp — usar em landing) `[evidência]`
| Classe | font-size | weight | line-height | tracking |
|---|---|---|---|---|
| display-1 | `clamp(56px,7vw,96px)` | 700 | .94 | -0.04em |
| display-2 | `clamp(44px,5.4vw,80px)` | 700 | .95 | -0.035em |
| h1 | `clamp(36px,4.4vw,64px)` | 700 | .98 | -0.03em |
| h2 | `clamp(30px,3.6vw,48px)` | 700 | 1 | -0.03em |
| h3 | `clamp(22px,2.4vw,32px)` | 700 | 1.1 | -0.022em |
| h4 | `20px` | 600 | 1.2 | -0.018em |
| paragraph | `17px` | 400 | 1.6 | — (cor text-2) |
| reg-l / reg-m / reg-s | 15 / 13 / 12px | 400 | 1.5–1.55 | — |
| label-caps (eyebrow) | `11px` | 700 | 1 | 0.14em UPPERCASE |

> Padrão de hero: badge "eyebrow" (label-caps) → display/h1 com a palavra-chave em dourado → subheadline em `paragraph`/`text-gray-400`.

---

## 3. Forma e profundidade `[evidência]`
- **Raios:** 12 / 16 / 20 / 24 / 32 / 40 px. No Tailwind (tema escuro): `orbit=16px`, `orbit-lg=24px`, `orbit-xl=32px`. Forma "arch" pontual: `7rem`.
- **Pílula:** botões e badges usam `border-radius: 999px`.
- **Sombras (tema escuro · glow dourado):**
  - `gold-glow`: `0 0 20px rgba(255,186,26,.5), inset 0 0 10px rgba(255,186,26,.2)`
  - `gold-strong`: `0 0 35px rgba(255,186,26,.6), inset 0 0 20px rgba(255,186,26,.4)`
  - `gold-soft`: `0 0 40px -10px rgba(255,186,26,.5)`
- **Sombras (tema claro):**
  - `shadow-soft`, `shadow-card`, `shadow-lift` (neutras)
  - `shadow-cta`: `0 15px 25px -10px rgba(255,186,26,.55), inset 0 4px 8px rgba(255,221,138,.65), inset 0 -4px 8px rgba(255,162,0,.55)`
- **Easings:** `--ease-soft cubic-bezier(.22,1,.36,1)`, `--ease-snap cubic-bezier(.4,0,.2,1)`.
- **Atmosfera de hero (tema escuro):** glow radial dourado de fundo (`.gold-atmos`) atrás do conteúdo.

---

## 4. Componentes recorrentes `[evidência]`

### Botão (pílula, `border-radius:999px`)
- **Base:** `display:inline-flex; gap:8px; font-weight:600; font-size:14px; padding:12px 22px`. Ícone desliza no hover (`translateX(3px)`). Foco: `outline:2px solid #ffba1a; offset:3px`.
- **Primário (CTA):** gradiente radial dourado `radial-gradient(120% 140% at 50% 0%, #FFE49A, #FFD24A 38%, #FFBA1A)`, texto `#0D1117`, `shadow-cta`; hover sobe 1px.
  - Tema escuro também usa primário sólido: `bg-primary text-orbit-black hover:bg-primary-400 shadow-gold-glow`, e um "beam button" com conic-gradient dourado girando na borda para o CTA principal do hero.
- **Dark:** fundo `#0D1117`, texto cream.
- **Ghost:** fundo translúcido + borda neutra (`btn--ghost` / `btn--ghost-onDark`).
- **Tamanhos:** sm `9/16 · 13px` · md (base) · lg `14/26 · 15px` · xl `16/30 · 16px`. Ícone: `44×44` pílula (alvo de toque ok).

### Badge (pílula, uppercase)
`padding:6px 12px; font-size:11px; weight:700; letter-spacing:.06em; text-transform:uppercase`.
Variantes: `default`, `gold` (bg dourado/.14, texto `#b87f00`), `gold-solid` (bg dourado, texto preto), `cream`, `dark`, `amber`, `success`, **`ai`** (fundo preto + texto dourado — usado para Olívia/IA).

### Card
Tema escuro: `rounded-xl/2xl`, fundo `#0A0A0C`/`#101018`, `border-white/10`, hover `border-primary/30`, `shadow-lg`. Card de destaque usa gradiente dourado (`from-primary to-primary-600`) com texto preto.
Tema claro: superfície branca, `shadow-card`, bordas neutras.

### Nav
Pílula flutuante fixa no topo, `bg-black/90`, `border-white/10`, `rounded-full`, `backdrop-blur`. CTA à direita.

### Containers (tema claro) `[evidência]`
`max-width`: xl `1300px` · lg `1180px` · md `1024px` · sm `760px`; padding lateral `24px`.

### Ícones
- Tema escuro: **Lucide** (stroke, `stroke-width` 1.5–2.5; cor herda `currentColor`).
- Tema claro: **Iconify** (`iconify-icon`).
- Padrão de "icon container": quadrado `rounded-lg/xl`, fundo sutil, borda; versão dourada com `bg-primary/10 border-primary/30`.

---

## 5. "Vibe" da marca `[evidência]`
Tech, confiança institucional, B2B sério porém moderno. Base escura GitHub-like com dourado usado com parcimônia (CTA, números-chave, IA). Movimento suave (fade-up, blur-in, glow pulsante). A IA **"Olívia"** tem tratamento próprio (badge `ai`: preto + dourado).

## 6. Variação por segmento `[pendência]`
Os dois arquivos são variações de **superfície** (escuro vs claro), não de segmento. O mapeamento visual **EMPRESA B2B × CONSULTOR** ainda não está documentado nos arquivos.
- Recomendação default até confirmar: **tema escuro** para hero/campanha de alto impacto; **tema claro (Variant B)** para páginas institucionais/long-form.
- `[pendência]` Confirmar com Marco se há paleta/tom distinto por segmento.

---

## 7. Tailwind config (colar em projeto Vite novo) `[evidência]`
```js
// tailwind.config.js
export default {
  darkMode: 'class',
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
  theme: {
    extend: {
      fontFamily: {
        sans: ['"Plus Jakarta Sans"', 'system-ui', 'sans-serif'],
        display: ['"Plus Jakarta Sans"', 'system-ui', 'sans-serif'],
        mono: ['"JetBrains Mono"', 'ui-monospace', 'SFMono-Regular', 'monospace'],
      },
      colors: {
        primary: {
          DEFAULT: '#ffba1a',
          50:'#fff8e6',100:'#fff0c2',200:'#ffe487',300:'#ffd64a',400:'#ffca4a',
          500:'#ffba1a',600:'#e6a200',700:'#b87f00',800:'#8a5e00',900:'#5c3f00',
        },
        orbit: {
          black:'#0D1117','black-soft':'#161B22','black-card':'#1C2333',
          'gray-200':'#30363D','gray-300':'#484F58','gray-500':'#8B949E',
          'gray-700':'#C9D1D9','gray-900':'#E6EDF3',
        },
        success: '#3FB950',
        error: '#F85149',
      },
      borderRadius: { orbit:'16px','orbit-lg':'24px','orbit-xl':'32px' },
      boxShadow: {
        'gold-glow':'0 0 20px rgba(255,186,26,.5), inset 0 0 10px rgba(255,186,26,.2)',
        'gold-strong':'0 0 35px rgba(255,186,26,.6), inset 0 0 20px rgba(255,186,26,.4)',
        'gold-soft':'0 0 40px -10px rgba(255,186,26,.5)',
      },
    },
  },
}
```
Fontes via `<link>`: `Plus+Jakarta+Sans:wght@400;500;600;700;800` (+ `JetBrains+Mono:wght@400;500` se usar mono).
