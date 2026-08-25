# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static landing page for **Oleo Alfajorería**, a premium artisan alfajor brand based in Santiago, Chile. The site is built with pure HTML and Tailwind CSS (via CDN), focusing on elegant product presentation and WhatsApp-based sales conversion.

## Technology Stack

- **HTML5**: Pure HTML files, no build process required
- **Tailwind CSS 3.x**: Loaded via CDN (`https://cdn.tailwindcss.com`)
- **Fonts**: Plus Jakarta Sans from Google Fonts
- **No JavaScript frameworks**: Vanilla JS for simple interactions (tab switching, hero text animation)

## Custom Tailwind Configuration

Each HTML file includes an inline Tailwind config with custom brand colors:

```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: '#5A746B',    // Green (header/CTA)
        accent: '#C27253',     // Terracotta (highlights)
        sand: '#FDFBF7',       // Background
        darkBrown: '#1C1917',  // Text
        cream: '#F6F4F0',      // Alternative background
        footerBg: '#F8F3EA'    // Footer background
      },
      fontFamily: {
        sans: ['"Plus Jakarta Sans"', 'sans-serif']
      }
    }
  }
}
```

**Important**: Always use these semantic color names (e.g., `bg-primary`, `text-accent`) instead of arbitrary Tailwind colors to maintain brand consistency.

## Site Structure

- **index.html** - Homepage with hero, product catalog (3 tabs: Destacados, Para regalar, Alfajores), and footer
- **empresas.html** - Corporate gifts/B2B sales page
- **nosotros.html** - About page
- **faq.html** - Frequently asked questions
- **Img/** - Contains all product images and brand assets

## Key Components

### Navigation Header

The header is sticky and includes:
- Top banner with shipping notice: "Despacho solo sector oriente región metropolitana"
- Desktop menu (visible on md+ screens)
- Mobile menu (visible on smaller screens, compact horizontal layout)
- WhatsApp CTA button

The navigation is **shared across all pages** with identical structure. Active page links use `text-accent` class.

### Hero Section (index.html only)

- Responsive background images (desktop: `herobg.jpg`, mobile: `herobgmobil.png`)
- Dynamic word animation cycling through: "regalar", "compartir", "saborear", "sentir"
- Belgian flag emoji inline with product description

### Product Catalog (index.html only)

Tab-based catalog system with 3 sections controlled by `switchTab()` function:
1. **Destacados** - Featured products
2. **Para regalar** - Gift boxes
3. **Alfajores** - Individual alfajores

Each product card includes:
- Badge (Destacado, Individual, Agotado, Próximamente)
- Product image with hover scale effect
- 3-column info grid: Weight (80g/480g), Manjar blanco (Artesanal), Chocolate belga (44%/70%/Blanco)
- Price and WhatsApp CTA button

### Footer

Shared component with:
- Logo and tagline
- Navigation links (Inicio, Catálogo, Venta Empresas, Nosotros, FAQ)
- Social media links (Instagram: @oleochile)
- Copyright notice

## WhatsApp Integration

All CTAs link to WhatsApp: `https://wa.me/56920719565`

Pre-filled messages vary by context:
- General: `?text=Hola,%20quiero%20comprar%20alfajores%20oleo!`
- Corporate: `?text=Hola,%20quiero%20cotizar%20regalos%20corporativos`
- Product-specific: `?text=Hola,%20quiero%20comprar%20la%20Caja%20Clásica`

## Responsive Design Patterns

This site uses mobile-first responsive design:

- **Desktop navigation** (md+): Horizontal menu with logo left, links center, CTA right
- **Mobile navigation**: Stacked logo + compact horizontal menu with separators
- **Hero images**: `<picture>` element with different images for mobile/desktop
- **Product grid**: `grid-cols-1 md:grid-cols-3` pattern
- **Typography scaling**: Uses responsive font sizes (e.g., `text-3xl md:text-5xl`)
- **Spacing**: Adjusts padding/margins at breakpoints (e.g., `py-10 md:py-20`)

## Image Assets

All images are in `/Img/` directory:

- `oleologo.png` - Main logo (header)
- `logoTail.png` - Footer logo
- `favicon.png` - Site favicon
- `herobg.jpg` - Desktop hero background
- `herobgmobil.png` - Mobile hero background
- `cajaclasica.png` - Classic box product
- `cajasurtida.png` - Assorted box product
- `alfajorclasico.png` - Classic alfajor
- `alfajorbitter.png` - Bitter chocolate alfajor
- `alfajorblanco.png` - White chocolate alfajor
- `banderabelga.png` - Belgian flag icon (used inline)
- `regalocorp.jpg` - Corporate gifts image

## JavaScript Functionality

### Tab Switching (index.html)

```javascript
function switchTab(tabName) {
  // Hides all .tab-content elements
  // Resets all button styles to inactive state
  // Shows selected content
  // Applies active state to selected button
}
```

### Hero Dynamic Word Animation (index.html)

Cycles through words array with smooth fade/slide transitions every 1.8 seconds after initial 1.5s delay.

## Development Workflow

This is a **static site with no build process**. To work on it:

1. Open HTML files directly in a browser, or use a local server:
   ```bash
   python -m http.server 8000
   # or
   npx serve
   ```

2. Edit HTML files directly - changes are immediately visible on refresh

3. Test responsive design using browser DevTools device emulation

4. Verify all WhatsApp links work correctly with proper pre-filled messages

## Design System Guidelines

### Typography Hierarchy

- **Hero titles**: `text-3xl md:text-5xl font-extrabold tracking-tight`
- **Section titles**: `text-xl md:text-2xl font-bold`
- **Body text**: `text-sm md:text-base text-stone-600`
- **Labels/badges**: `text-[9px] md:text-xs uppercase tracking-widest font-bold`

### Spacing Scale

Uses Tailwind's default spacing with emphasis on:
- Sections: `py-20 md:py-32`
- Cards: `p-8 md:p-10`
- Element gaps: `gap-8`, `gap-10`, `gap-12`

### Border & Shadow Pattern

- Borders: `border-[#E6DCD0]` or `border-[#F2ECE1]`
- Shadows: `shadow-sm` for subtle depth, `shadow-[0_4px_20px_rgba(0,0,0,0.02)]` for cards
- Rounded corners: `rounded-xl` for cards, `rounded-full` for buttons

### Hover Effects

Standard pattern: `hover:scale-[1.03] transition-transform duration-500 ease-out` on images
Buttons: `hover:bg-accent transition-colors duration-300`

## Content Guidelines

### Product Specifications

Each alfajor product should specify:
1. **Weight**: Individual (80g NETOS) or Box (480g NETOS)
2. **Filling**: Manjar blanco artesanal
3. **Chocolate**: Belgian chocolate with cacao percentage (44%, 70%) or type (Blanco, Bitter)

### Badges

Available product badges:
- `bg-accent` - "Destacado" (featured)
- `bg-stone-500` - "Individual"
- `bg-stone-400` - "Agotado" (sold out) or "Próximamente" (coming soon)

## Deployment

This is a static site. Deploy by uploading all files to any static hosting service:
- GitHub Pages
- Netlify
- Vercel
- Any web server (Apache, Nginx, etc.)

Ensure the `/Img/` directory structure is preserved.

## Browser Compatibility

- Uses modern CSS features (Grid, Flexbox, Custom Properties)
- Tailwind CSS via CDN handles autoprefixing
- Tested on Chrome, Firefox, Safari, Edge
- Mobile-tested on iOS Safari and Chrome Android
