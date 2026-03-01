---
name: brand-identity
description: Apply the user's brand identity and visual guidelines to any project, design, document, or creative output. Use this skill whenever the user asks to create, design, or style anything — websites, presentations, documents, components, logos, banners, social media posts, dashboards, or any visual content. Always use this skill when the user mentions "minha identidade visual", "minhas cores", "brand", "cor da marca", "estilo visual", or when building any UI, frontend, or document. This skill ensures consistent use of brand colors, typography, and visual language across all outputs.
---

# Brand Identity — Identidade Visual

## 🎨 Paleta de Cores Principal

### Preto — `#0A0A0A`
- **Uso:** Fundos principais, textos primários, elementos de destaque, headers
- **Variações:**
  - Preto puro: `#000000`
  - Preto suave (recomendado): `#0A0A0A`
  - Cinza escuro (superfícies): `#111111`
  - Cinza carvão (cards/containers): `#1A1A1A`
  - Cinza médio (bordas/divisores): `#2A2A2A`

### Laranja — `#FF6B00`
- **Uso:** CTAs, destaques, acentos, ícones ativos, hover states, títulos em fundo escuro
- **Variações:**
  - Laranja vibrante (principal): `#FF6B00`
  - Laranja intenso (hover): `#E55A00`
  - Laranja suave (backgrounds suaves): `#FF8C33`
  - Laranja claro (tints/badges): `#FFA559`
  - Laranja muito claro (backgrounds sutis, modo escuro): `#1A0A00`

### Neutros e Suporte
- Branco puro: `#FFFFFF`
- Off-white (textos em fundo escuro): `#F5F5F5`
- Cinza texto secundário: `#A0A0A0`
- Cinza texto desabilitado: `#555555`

---

## 🖼️ Combinações de Cores Recomendadas

| Contexto | Fundo | Texto/Elemento | Destaque |
|---|---|---|---|
| Hero / Banner principal | `#0A0A0A` | `#F5F5F5` | `#FF6B00` |
| Card padrão | `#1A1A1A` | `#F5F5F5` | `#FF8C33` |
| Botão primário (CTA) | `#FF6B00` | `#FFFFFF` | — |
| Botão secundário | `#1A1A1A` | `#FF6B00` | `#FF6B00` (border) |
| Seção clara / contraste | `#F5F5F5` | `#0A0A0A` | `#FF6B00` |
| Badge / Tag | `#1A0A00` | `#FF8C33` | — |

---

## ✍️ Tipografia Recomendada

- **Títulos:** Inter Bold ou Montserrat Bold — use em maiúsculas para impacto
- **Corpo:** Inter Regular ou System UI
- **Código/Tech:** JetBrains Mono ou Fira Code
- **Hierarquia de peso:** `900` títulos hero → `700` subtítulos → `500` labels → `400` corpo

---

## 🎯 Princípios de Design

1. **Dark-first:** Prefira fundos escuros como base — a combinação preto + laranja brilha mais em modo escuro
2. **Contraste alto:** Garanta sempre contraste suficiente (mínimo WCAG AA)
3. **Laranja com moderação:** Use o laranja como acento estratégico, não como cor de fundo principal em grandes áreas
4. **Espaçamento generoso:** Margens amplas reforçam a sensação premium
5. **Minimalismo:** Poucos elementos com muito impacto — a identidade é forte e não precisa de ornamentos

---

## 💻 CSS Custom Properties (copie e use)

```css
:root {
  /* Brand Colors */
  --brand-black: #0A0A0A;
  --brand-orange: #FF6B00;
  --brand-orange-hover: #E55A00;
  --brand-orange-light: #FF8C33;
  --brand-orange-pale: #FFA559;
  --brand-orange-bg: #1A0A00;

  /* Surfaces */
  --surface-primary: #111111;
  --surface-secondary: #1A1A1A;
  --surface-tertiary: #2A2A2A;
  --surface-border: #333333;

  /* Text */
  --text-primary: #F5F5F5;
  --text-secondary: #A0A0A0;
  --text-disabled: #555555;
  --text-inverse: #0A0A0A;

  /* Gradients */
  --gradient-brand: linear-gradient(135deg, #FF6B00 0%, #E55A00 100%);
  --gradient-dark: linear-gradient(135deg, #0A0A0A 0%, #1A1A1A 100%);
  --gradient-hero: linear-gradient(135deg, #0A0A0A 60%, #1A0A00 100%);
}
```

---

## 🧩 Tailwind Config (se aplicável)

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          black: '#0A0A0A',
          orange: '#FF6B00',
          'orange-hover': '#E55A00',
          'orange-light': '#FF8C33',
          'orange-pale': '#FFA559',
          'orange-bg': '#1A0A00',
        },
        surface: {
          primary: '#111111',
          secondary: '#1A1A1A',
          tertiary: '#2A2A2A',
          border: '#333333',
        }
      }
    }
  }
}
```

---

## 📐 Exemplo de Componente — Botão Primário

```html


  Ação Principal




  Ação Secundária

```

---

## 📋 Checklist ao Criar Qualquer Projeto

- [ ] Fundo principal usa tom de preto (`#0A0A0A` / `#111111`)
- [ ] CTAs e destaques usam laranja (`#FF6B00`)
- [ ] Textos em fundo escuro usam off-white (`#F5F5F5`)
- [ ] Hover states do laranja usam `#E55A00`
- [ ] Não usar laranja como fundo de grandes áreas de texto
- [ ] Manter espaçamento generoso entre elementos
- [ ] Contraste suficiente em todos os textos

---

*Identidade visual: Preto + Laranja — Impacto, energia e modernidade.*