# Drift Headband — Product Landing Page

A minimalist, Apple-inspired product landing page for the **Drift Headband**, a fictional sleep-tech product by **Sleep Dynamics**. Built as a design exercise exploring modern web aesthetics, interaction design, and AI-assisted content generation.

> The Drift Headband is an ultra-slim, breathable headband that uses bone conduction micro-transducers to deliver audio directly to your inner ear — no earbuds, no bulk, just sound sleep.

## Tech Stack

- **SvelteKit** (Svelte 5 with runes)
- **Tailwind CSS 4**
- **Lucide Svelte** for iconography
- **Vite 8**
- **TypeScript**

## Design Philosophy

The entire page follows a monochrome, light-mode aesthetic with generous whitespace, large sans-serif typography, and full-bleed sections. The goal was to channel the feel of an Apple product page — brief, witty copy, dramatic imagery, and interactions that feel inevitable rather than clever.

### Color & Typography

- **Monochrome palette** — black, white, and grays only. No accent colors.
- **Large, legible type** with tight tracking to draw attention while maintaining minimalism.
- **Sans-serif throughout** to keep things clean and contemporary.

### Layout

- **Full-bleed sections** — every section stretches edge to edge.
- **`min-h-svh`** used instead of `min-h-screen` or `min-h-dvh` to prevent layout recalculations when mobile browser address bars collapse on scroll.
- **Responsive across all common breakpoints** with mobile-first consideration.

## Sections & Design Decisions

### Navbar

- **Scroll-aware**: disappears on scroll down, reappears on scroll up.
- **Interactive logo**: On desktop, only the custom favicon (three wavy lines) is visible. Hovering over the link area causes "Sleep Dynamics" to slide out from behind the icon using `overflow-hidden` and CSS transforms. On mobile, both icon and text are statically visible.
- **Responsive navigation**: Desktop links are inline; on mobile, they collapse into a hamburger menu that opens as a full-bleed overlay with a `slide` transition.
- **Glassmorphic background**: When scrolled past the hero, the navbar gains a `backdrop-blur` frosted glass effect.

### Hero

- **AI-generated background image** showing 5 color variants of the Drift Headband tossed playfully in the air, with "DRIFT" woven into the fabric.
- **Bottom-left aligned text** — the headline, subheading ("Sound sleep."), CTA button, and price sit very close to the bottom of the viewport for a dramatic, editorial feel.
- **Gradient overlay**: A dark gradient (`from-black/90 via-black/40 via-35% to-transparent`) is concentrated at the bottom where the text sits, leaving the majority of the hero image unobstructed.
- **"Buy now" opens a dialog** instead of navigating — since the product isn't real, it shows a playful message with a like button featuring a heartbeat animation.

### Zero Pressure

- **Full-bleed background image** of a person lying on their side watching their phone while wearing the headband.
- **Same gradient treatment** as the hero to create text contrast at the bottom.
- **Centered copy** anchored to the bottom of the section.

### Features (Bento Grid)

- **Desktop**: A tasteful 2-column bento grid layout.
- **Mobile**: Transforms into a horizontally scrollable list where each card takes up 85vw (with the container bleeding to screen edges via `-mx-6 px-6`) so the next card always peeks into view as a scroll affordance.
- **AI-generated background images** for each card (macro tech fabric, bone conduction ripples, abstract equalizer waves).
- **Floating glass text cards**: The copy sits in frosted-glass panels (`bg-white/95 backdrop-blur-xl`) with generous rounded corners, layered over the images.
- **Previous/Next navigation buttons** below the cards on mobile. The "Next" button dynamically swaps to a "Redo" icon when you reach the last card, scrolling back to the start on tap.

### Technical Specifications

- A clean, Apple-style spec sheet with horizontal dividers and a two-column layout (label + value).

### Final CTA

- Re-prompts the "Buy now" action at the bottom of the page with a centered layout and the same dialog interaction as the hero.

### Footer

- **Dark theme** (`bg-black`) with organized link columns (Products, Company, Support).
- Standard copyright and legal links.

### Buy Dialog

- **Playful disclosure**: "Like the product? It's not real though 😢"
- **Like button** with a heart icon that plays a double-pulse heartbeat animation on like, but simply reverts on unlike.
- Dismissible by clicking outside or pressing Escape.

## Routing

- The root (`/`) automatically redirects to `/drift-headband` via a server-side redirect in `+page.server.js`.
- All placeholder nav links use `/#` instead of `#` to avoid SvelteKit accessibility warnings.

## Custom Assets

- **Favicon**: A custom SVG of three black wavy lines on a white background with rounded corners — doubles as the navbar logo.
- **Hero image**: AI-generated, 5 headband color variants floating in air.
- **Zero Pressure background**: AI-generated, person side-sleeping with headband.
- **Bento card images**: AI-generated (micro-transducer fabric close-up, bone conduction ripple visualization, abstract equalizer waves).

## Getting Started

```bash
# Install dependencies
pnpm install

# Start dev server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview
```

## Project Structure

```
src/
├── lib/
│   └── assets/
│       └── favicon.svg          # Custom wavy-lines logo
├── routes/
│   ├── +layout.svelte           # Global layout (navbar, footer, mobile menu)
│   ├── +layout.css              # Global styles & Tailwind imports
│   ├── +page.server.js          # Root → /drift-headband redirect
│   └── drift-headband/
│       └── +page.svelte         # Main product landing page
static/
├── hero-bg.jpg                  # Hero background image
├── zero-pressure-bg.jpg         # Zero Pressure section background
├── bento_micro_transducers.jpg  # Bento card 1 background
├── bento_direct_cochlea.jpg     # Bento card 2 background
└── bento_uncompromised_fidelity.jpg  # Bento card 3 background
```
