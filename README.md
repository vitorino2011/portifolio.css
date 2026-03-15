# Estilos do Portfolio — Documentação CSS

**Arquivo:** `style.css`  
**Contexto:** Folha de estilos principal para página de portfólio pessoal  
**Fontes:** Inter (UI) · JetBrains Mono (código)

---

## Sumário

1. [Reset e Base](#1-reset-e-base)
2. [Variáveis CSS (Design Tokens)](#2-variáveis-css-design-tokens)
3. [Scrollbar Customizada](#3-scrollbar-customizada)
4. [Navbar](#4-navbar)
5. [Barra de Progresso](#5-barra-de-progresso)
6. [Cursor Glow](#6-cursor-glow)
7. [Particles](#7-particles)
8. [Hero Section](#8-hero-section)
9. [Cartão 3D](#9-cartão-3d)
10. [Sections (Padrão)](#10-sections-padrão)
11. [Reveal Animations](#11-reveal-animations)
12. [About Section](#12-about-section)
13. [Story Modal](#13-story-modal)
14. [Video Modal](#14-video-modal)
15. [Tablet Scroll Section](#15-tablet-scroll-section)
16. [Timeline](#16-timeline)
17. [Skills Section](#17-skills-section)
18. [Quote Section](#18-quote-section)
19. [Footer](#19-footer)
20. [Responsividade](#20-responsividade)

---

## 1. Reset e Base

```css
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
body { font-family: 'Inter', sans-serif; background: var(--bg); color: var(--text); overflow-x: hidden; line-height: 1.7; }
```

- Reset universal com `box-sizing: border-box`
- `overflow-x: hidden` evita scroll horizontal indesejado
- `line-height: 1.7` garante boa legibilidade em blocos de texto
- `strong` tem `color: #fff` para se destacar do texto mutado

---

## 2. Variáveis CSS (Design Tokens)

Definidas em `:root`, controlam toda a paleta e superfícies da página:

| Variável | Valor | Uso |
|----------|-------|-----|
| `--bg` | `#0a0a0a` | Fundo global da página |
| `--surface` | `#111` | Cards e painéis primários |
| `--surface2` | `#1a1a1a` | Superfícies secundárias / hover states |
| `--border` | `#222` | Bordas e separadores |
| `--text` | `#f0f0f0` | Texto principal |
| `--muted` | `#888` | Texto secundário / labels |
| `--accent` | `#fff` | Cor de destaque (branco puro) |

> O tema é intencionalmente **monocromático** — preto e branco com gradientes sutis. Nenhuma cor vibrante, criando uma estética minimalista e técnica.

---

## 3. Scrollbar Customizada

```css
html { scrollbar-width: thin; scrollbar-color: #333 #0a0a0a; }
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-thumb { background: #333; border-radius: 3px; }
```

- `scrollbar-width: thin` para Firefox
- `::-webkit-scrollbar` para Chrome/Safari
- Thumb de `6px` de largura, quase invisível, combinando com o fundo escuro

---

## 4. Navbar

**Elemento:** `.navbar`

```css
.navbar {
  position: fixed; top: 0; z-index: 1000;
  backdrop-filter: blur(20px);
  background: rgba(10,10,10,0.8);
}
```

**Estados:**

| Classe | Quando ativa | Efeito |
|--------|-------------|--------|
| (padrão) | Sempre | Fundo semi-transparente com blur |
| `.scrolled` | Após 100px de scroll | Fundo mais opaco + sombra |

**Links de navegação (`.nav-links a`):**
- Texto em uppercase, `letter-spacing: 0.5px`, `font-size: 0.85rem`
- Efeito hover: cor muda para `#fff` + underline animado (`width: 0 → 100%`) via `::after`

**Ícones sociais (`.nav-social a`):**
- Hover aplica `scale(1.15)` com transição suave

**Menu mobile (`.mobile-toggle`):**
- Oculto em desktop (`display: none`), visível em telas ≤900px
- `.nav-links.open` abre um menu dropdown com `position: absolute` abaixo da navbar

---

## 5. Barra de Progresso

```css
.progress-bar {
  position: fixed; top: 64px; left: 0; height: 2px;
  background: linear-gradient(to right, #555, #fff);
  z-index: 999;
}
```

- Fixada logo abaixo da navbar (64px = altura da navbar)
- Largura controlada via JavaScript conforme o scroll
- Gradiente cinza → branco dá sensação de profundidade

---

## 6. Cursor Glow

```css
.cursor-glow {
  width: 400px; height: 400px; border-radius: 50%;
  background: radial-gradient(circle, rgba(255,255,255,.03) 0%, transparent 70%);
  transform: translate(-50%, -50%);
  pointer-events: none;
}
```

- Círculo grande e suave que segue o cursor
- `pointer-events: none` garante que não interfere com cliques
- `transform: translate(-50%, -50%)` centraliza o halo no cursor
- Opacidade `0.03` — quase invisível, apenas um brilho sutil

---

## 7. Particles

```css
.particle {
  position: absolute;
  animation: floatP linear infinite;
}

@keyframes floatP {
  0%   { transform: translateY(100vh) scale(0); opacity: 0; }
  10%  { opacity: 1; }
  90%  { opacity: 1; }
  100% { transform: translateY(-10vh) scale(1); opacity: 0; }
}
```

- Partículas sobem de baixo para cima (`100vh → -10vh`)
- Fade in nos primeiros 10% da animação, fade out nos últimos 10%
- `scale(0 → 1)` dá a sensação de surgir do nada
- `pointer-events: none` no container evita interferência

---

## 8. Hero Section

```css
.hero { min-height: 100vh; display: flex; align-items: center; justify-content: center; }
```

**Camadas de fundo (empilhadas):**

| Elemento | Efeito |
|----------|--------|
| `.hero-bg` | Dois gradientes radiais sutis — um no topo central, outro na direita |
| `.hero-grid-bg` | Grade de linhas finas (60×60px) com opacidade `0.02` |

**Tipografia:**
- `.hero-heading`: `clamp(2rem, 4vw, 3.2rem)` — responsivo sem media queries
- `font-weight: 900`, `letter-spacing: -1.5px` — estilo editorial denso
- Gradiente `#fff → #666` via `-webkit-background-clip: text`

**Botões (`.btn`):**

| Classe | Estilo |
|--------|--------|
| `.btn-primary` | Fundo branco com gradiente, texto preto |
| `.btn-outline` | Fundo transparente, borda `#333` |

Ambos: `border-radius: 12px`, hover com `translateY(-2px)` e sombra

**Scroll hint:**
- Animação `scrollBounce` faz o ícone subir e descer 8px infinitamente

---

## 9. Cartão 3D

**Estrutura de camadas:**

```
.card-3d-wrapper     ← perspectiva 3D (1200px)
  └── .card-3d       ← recebe rotateX/rotateY via JS
        ├── .card-3d-img     ← foto, escala no hover
        ├── .card-overlay    ← painel que desliza da esquerda
        │     └── .card-overlay-inner  ← conteúdo (nome, bio, stats...)
        ├── .card-3d-shine   ← brilho que segue o cursor (var --mx, --my)
        └── .card-3d-border  ← borda sutil permanente
```

**Animação do overlay:**
```css
.card-overlay { width: 0%; transition: width .55s cubic-bezier(.16,1,.3,1); }
.card-3d:hover .card-overlay { width: 100%; }
```
Começa com `width: 0` (invisível) e expande para `100%` no hover, com easing `spring-like`.

O conteúdo interno (`.card-overlay-inner`) tem delay de `0.18s` e começa com `translateX(-24px)`, criando um efeito de entrada suave após o painel abrir.

**Shine effect:**
- Usa variáveis `--mx` e `--my` (atualizadas via JS) em `radial-gradient`
- `opacity: 0 → 1` no hover

---

## 10. Sections (Padrão)

```css
.section { padding: 120px 40px; max-width: 1100px; margin: 0 auto; }
```

**Padrão tipográfico:**
- `.section-label`: `0.75rem`, uppercase, `letter-spacing: 4px` — funciona como eyebrow text
- `.section-heading`: `clamp(1.8rem, 3vw, 2.8rem)`, `font-weight: 900`, gradiente `#fff → #888`
- `.section-desc`: `color: var(--muted)`, `max-width: 700px`

**Divisor:**
- `.section-divider`: altura de `120px` com pseudo-elementos `::before` e `::after` criando fades sutis
- `.divider-line-center`: linha horizontal de `1px` com gradiente `transparent → #333 → transparent`

---

## 11. Reveal Animations

Duas classes de entrada controladas via JavaScript (`IntersectionObserver`):

| Classe | Estado inicial | Estado final |
|--------|---------------|--------------|
| `.reveal` | `opacity: 0` + `translateY(60px)` | `opacity: 1` + `translateY(0)` |
| `.reveal-scale` | `opacity: 0` + `scale(0.9)` | `opacity: 1` + `scale(1)` |

Ambas usam `transition: all .8s cubic-bezier(.16, 1, .3, 1)` — easing com overshoot suave (spring).

---

## 12. About Section

**`.about-card`:**
- Grid responsivo com `minmax(220px, 1fr)`
- Hover: `translateY(-4px)` + brilho radial via `::before` (`opacity: 0 → 1`)
- Ícone de `48×48px` com `border-radius: 12px`

**`.story-trigger`:**
- Botão grande que abre o modal de história
- Background `linear-gradient(145deg, #151515, #0d0d0d)`
- Hover: `scale(1.02)` com sombra intensa + brilho radial central
- Seta animada: `scale(1.1)` no hover do container pai

---

## 13. Story Modal

```css
.story-overlay {
  position: fixed; inset: 0; z-index: 2000;
  backdrop-filter: blur(10px);
  opacity: 0; transition: opacity .4s;
}
.story-overlay.active { display: flex; opacity: 1; }
```

**Animação de entrada do modal:**
```css
.story-modal { transform: translateY(40px) scale(.95); transition: all .5s cubic-bezier(.16,1,.3,1); }
.story-overlay.active .story-modal { transform: translateY(0) scale(1); }
```

**Header sticky:**
- `position: sticky; top: 0` — permanece visível ao rolar o conteúdo do modal
- `backdrop-filter: blur(10px)` no header para legibilidade sobre o conteúdo

---

## 14. Video Modal

Estrutura:
```
.video-overlay       (z-index: 3000 — acima do story modal)
  └── .video-container
        ├── .video-top-bar
        ├── .video-wrapper    (aspect-ratio: 16/9)
        │     ├── <video>
        │     └── .video-placeholder
        └── .video-controls
```

**Controles (`.vc-btn`, `.vc-progress`, `.vc-like`):**
- Botões de `36×36px` com `border-radius: 8px`
- Barra de progresso: `height: 4px`, gradiente `#666 → #fff`
- Like: hover com tint vermelho `rgba(255,80,80,.1)`, estado `.liked` com fill `#ff5050`
- Velocidade e tempo usam `JetBrains Mono` para consistência com o tema "dev"

---

## 15. Tablet Scroll Section

A seção mais complexa do CSS — implementa um efeito de scroll com animação 3D sticky.

**Estrutura de scroll:**
```css
.tablet-scroll-container { height: 220vh; }   /* espaço para a animação ocorrer */
.tablet-sticky-wrapper   { position: sticky; top: 0; height: 100vh; }  /* prende na tela */
```

O container tem `220vh` de altura — isso cria o "espaço de scroll" que o JavaScript usa para calcular o progresso da animação. O wrapper interno fica fixo na viewport enquanto o usuário rola.

**Tablet Card (`.tablet-card`):**
```css
box-shadow:
  0 9px 20px #0000004a,
  0 37px 37px #00000042,
  0 84px 50px #00000026,   /* múltiplas sombras para profundidade realista */
  0 149px 60px #0000000a,
  0 233px 65px #00000003;
```

Sombra em camadas progressivas — técnica de "smooth shadow" que simula luz física.

**Tela interna (`.tablet-inner-screen`):**
- Barra de OS com 3 dots coloridos (`.td1` vermelho, `.td2` amarelo, `.td3` verde)
- Abas com `border-bottom: 2px` animado via `::after` na aba `.active`

**Sintaxe colorida dos painéis:**

| Classe | Cor | Uso |
|--------|-----|-----|
| `.kw` | `#c9a0dc` | Keywords (`def`, `class`, `function`) |
| `.str` | `#a8cc8c` | Strings |
| `.fn` | `#6cb6ff` | Nomes de funções |
| `.cm` | `#555` | Comentários |
| `.tag` | `#e06c75` | Tags HTML |
| `.attr` | `#d19a66` | Atributos / propriedades |
| `.val` | `#98c379` | Valores |
| `.num` | `#d19a66` | Números |
| `.prop` | `#56b6c2` | Propriedades CSS |

**Transição entre abas:**
```css
@keyframes tabFadeIn {
  from { opacity: 0; transform: translateX(16px); }
  to   { opacity: 1; transform: translateX(0); }
}
```

---

## 16. Timeline

```css
.timeline { position: relative; padding-left: 40px; }
.timeline::before { /* linha vertical */ width: 2px; background: linear-gradient(transparent, #333 10%, #333 90%, transparent); }
.timeline-item::before { /* ponto */ width: 12px; height: 12px; border-radius: 50%; left: -45px; }
.timeline-item.visible::before { background: #fff; box-shadow: 0 0 20px rgba(255,255,255,.3); }
```

- Linha vertical criada com `::before` no `.timeline`
- Ponto de cada item criado com `::before` no `.timeline-item`
- Quando o item entra na viewport (classe `.visible`), o ponto acende em branco com glow

---

## 17. Skills Section

**`.skill-card`:**
- Background com gradiente diagonal `--surface2 → --surface`
- Glow que segue o cursor via `radial-gradient` com `--mx` e `--my`
- Hover: `translateY(-4px)` + sombra de `60px`

**Barra de progresso (`.skill-bar-fill`):**
```css
.skill-bar-fill {
  width: 0;   /* começa zerada */
  transition: width 1.5s cubic-bezier(.16, 1, .3, 1);   /* animação suave */
}
```
Preenchida via JavaScript quando o card entra na viewport, usando o valor de `data-width`.

**Tags (`.skill-tag`):**
- Estilo "badge" com `JetBrains Mono`, fundo semi-transparente, borda sutil

---

## 18. Quote Section

```css
.quote-section { text-align: center; padding: 100px 40px; }
.quote-mark { font-size: 4rem; opacity: .1; font-family: Georgia, serif; }
.quote-text { font-size: clamp(1.2rem, 2.5vw, 1.8rem); font-weight: 300; font-style: italic; }
```

- `font-weight: 300` — leveza intencional para contrastar com os headings `900` do resto
- `opacity: 0.1` no símbolo `"` — decorativo, quase invisível
- `clamp` no tamanho garante responsividade sem media queries

---

## 19. Footer

- Grid de ícones sociais: `48×48px`, `border-radius: 14px`
- Hover: `translateY(-3px)` + sombra de `24px`
- Links de rodapé: `color: var(--muted)` → `#fff` no hover

---

## 20. Responsividade

### Breakpoint 900px

```css
@media (max-width: 900px) {
  .hero-content   { flex-direction: column; text-align: center; }
  .nav-links      { display: none; }      /* menu hambúrguer ativo */
  .mobile-toggle  { display: flex; }
  .section        { padding: 80px 20px; }
  .skills-grid    { grid-template-columns: 1fr; }
  .tablet-card    { height: 26rem; }
}
```

### Breakpoint 480px

```css
@media (max-width: 480px) {
  .card-3d-wrapper { width: 280px; height: 400px; }
  .tablet-card     { height: 22rem; }
  .tablet-tab      { padding: 10px 14px; font-size: .7rem; }
}
```

### Resumo de adaptações

| Componente | Desktop | Tablet (≤900px) | Mobile (≤480px) |
|-----------|---------|-----------------|-----------------|
| Hero layout | `flex` horizontal | `flex` vertical, centralizado | Padding reduzido |
| Navbar | Links visíveis | Menu hambúrguer | Menu hambúrguer |
| Skills grid | `auto-fit minmax(300px)` | 1 coluna | 1 coluna |
| Tablet card | `38rem` | `26rem` | `22rem` |
| Story modal image | `260×340px` | `100% × 220px` | Empilhado |
| Section padding | `120px 40px` | `80px 20px` | `80px 16px` |
