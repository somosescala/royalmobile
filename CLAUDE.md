# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Royal Mobile Detailing** - Premium mobile auto detailing service landing page optimized for Google Ads conversion. Single-page HTML application serving the Seattle area.

**Target**: High conversion rate for Google Ads traffic. Mobile-first, fast-loading, premium aesthetic.

## Tech Stack

- **HTML + Tailwind CSS** (CDN): Single `index.html` file with all styles inline
- **No build process**: Direct HTML/CSS/JS - edit and refresh
- **Local development server**: `node serve.mjs` (serves at http://localhost:3000)

## Development Workflow

### Running Locally

```bash
node serve.mjs
```

- Serves at http://localhost:3000
- **Always use localhost** - never open HTML files directly in browser
- If server is already running, don't start a second instance

### Making Changes

1. Edit `index.html` directly (all CSS is inline in `<style>` tag)
2. Refresh browser to see changes
3. No build step required

## Brand Assets

All brand materials live in `brand_assets/`:

- `colors.json` - **Authoritative color palette** (use these exact values):
  - Primary: `#111827` (slate dark)
  - Accent: `#2563EB` (royal blue)
  - Background: `#FFFFFF` (white)
  - Text/Links: `#2563EB` (royal blue)

- `image.png` - Original page reference (before redesign)

**Rule**: Always reference `brand_assets/colors.json` before choosing colors. Never use default Tailwind colors.

## Design System Constraints

### Anti-Generic UI Rules (Critical)

**Colors**:
- ✅ Use exact brand colors from `brand_assets/colors.json`
- ❌ Never use default Tailwind palette (indigo-500, blue-600, etc.) UNLESS it matches brand exactly
- ✅ Custom color values stored in CSS variables: `var(--primary)`, `var(--accent)`, `var(--background)`

**Shadows**:
- ✅ Use layered shadows with color tint: `box-shadow: 0 1px 3px rgba(37, 99, 235, 0.08), 0 4px 12px rgba(37, 99, 235, 0.06), ...`
- ❌ Never use flat `shadow-md` or generic shadows
- ✅ Classes: `.shadow-layered`, `.shadow-layered-lg`

**Typography**:
- ✅ Combine different fonts for display vs body:
  - Display: `DM Serif Display` (elegant, refined) - class: `.font-display`
  - Body: `Inter` (clean, professional)
- ✅ Apply tight tracking (`letter-spacing: -0.03em`) on large headings
- ✅ Generous line-height (1.7) on body text
- ❌ Never use same font for headings and body

**Gradients**:
- ✅ Use radial gradients with multiple layers: `.gradient-radial` class
- ✅ Subtle, atmospheric backgrounds (not loud)

**Animations**:
- ✅ Only animate `transform` and `opacity` (performance)
- ❌ Never use `transition-all`
- ✅ Use spring easing: `cubic-bezier(0.34, 1.56, 0.64, 1)`
- ✅ Classes: `.animate-fadeInUp`, `.stagger-1`, `.stagger-2`, etc.

**Interactive States**:
- ✅ Every clickable element needs `cursor-pointer`
- ✅ All buttons need `hover`, `focus-visible`, and `active` states
- ✅ Hover should provide clear visual feedback (transform, shadow change)
- ❌ Avoid layout shift on hover (use `transform: translateY()` not margin)

**Images**:
- ✅ Use https://placehold.co/ for placeholder images
- Format: `https://placehold.co/WIDTHxHEIGHT/COLOR1/COLOR2?text=Description`
- ✅ Add overlay gradients for depth: `linear-gradient(180deg, transparent 50%, rgba(17, 24, 39, 0.4) 100%)`

**Spacing**:
- ✅ Use consistent spacing tokens from Tailwind (4, 6, 8, 12, 16, 24, etc.)
- ✅ Generous negative space for premium feel
- ❌ Avoid random spacing values

**Depth/Z-Index**:
- ✅ Define clear z-index scale (10, 20, 30, 50)
- ✅ Layered surfaces: base → elevated → floating

## Page Structure

Landing page sections (maintain this order):

1. **Hero** - "Seattle's Most Trusted Mobile Detailing Service" + 3 feature badges
2. **Pricing** - 3 packages (Basic $325, Standard $325, Premium $350)
3. **Before & After Gallery** - 4 images (2x2 grid)
4. **How It Works** - 3 steps with numbered badges
5. **FAQ** - 5+ common questions
6. **Final CTA** - Dark section with contact form

## Content Guidelines

- **Service Area**: Seattle and surrounding areas (30 miles)
- **Key Differentiators**:
  - Mobile service (we come to you)
  - Satisfaction guaranteed
  - Affordable pricing
  - No water/electricity needed from customer
- **Packages**: Basic ($325), Standard ($325), Premium ($350)

## Performance for Google Ads

- **Single file**: All CSS/JS inline for fast First Contentful Paint
- **Tailwind CDN**: No build step, still fast
- **Mobile-first**: Test at 375px, 768px, 1024px, 1440px
- **Clear CTAs**: "Book Now" and "Free Quote" buttons prominently placed
- **Form at bottom**: Lead capture in dark section (high contrast)

## Common Modifications

### Changing Colors
1. Update `brand_assets/colors.json` (source of truth)
2. Update CSS variables in `index.html` `<style>` section:
   ```css
   :root {
       --primary: #111827;
       --accent: #2563EB;
       --background: #FFFFFF;
   }
   ```
3. Update Tailwind arbitrary values: `text-[#2563EB]`, `bg-[#111827]`

### Adding New Sections
- Follow existing pattern: outer `<section>` with padding, inner `.max-w-7xl` container
- Use `.gradient-radial` or `bg-gradient-to-b from-white to-[#F8FAFC]` for section backgrounds
- Add stagger animations: `.animate-fadeInUp`, `.stagger-1`, `.stagger-2`

### Updating Pricing
- Edit pricing cards in Pricing Section
- Maintain 3-column grid: `.grid md:grid-cols-3 gap-8`
- Featured package uses `.pricing-card.featured` class (adds blue border + badge)

### Modifying Forms
- All form inputs styled via inline CSS (in `<style>` tag)
- Focus states: `border-color: var(--accent)` + `box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1)`
- Submit button uses `.btn-primary` class

## Pre-Delivery Checklist

Before marking work as complete:

- [ ] No emojis used as icons (use SVG instead)
- [ ] All interactive elements have `cursor-pointer`
- [ ] Hover states provide visual feedback
- [ ] Transitions are smooth (150-300ms, never `transition-all`)
- [ ] Brand colors match `brand_assets/colors.json` exactly
- [ ] Typography uses both `DM Serif Display` (display) and `Inter` (body)
- [ ] Shadows are layered with color tint
- [ ] Responsive at 375px, 768px, 1024px, 1440px
- [ ] No horizontal scroll on mobile
- [ ] Test in localhost:3000 (not file://)
- [ ] All images have alt text
- [ ] Form inputs have labels

## Typography Scale

```css
Hero Heading:     5xl md:7xl (font-display, -0.03em tracking)
Section Heading:  5xl md:6xl (font-display, -0.03em tracking)
Card Heading:     2xl (font-bold)
Body Large:       xl (line-height 1.7)
Body:             base (line-height 1.7)
Small:            sm
```

## Button Styles

**Primary** (`.btn-primary`):
- Background: `var(--accent)` (#2563EB)
- White text
- Layered shadow with blue tint
- `translateY(-2px)` on hover

**Secondary** (`.btn-secondary`):
- White background
- Blue border/text
- Fills blue on hover
- `translateY(-2px)` on hover

## Animation Classes

- `.animate-fadeInUp` - Fade in with upward motion
- `.stagger-1` through `.stagger-4` - Staggered delays (0.1s increments)
- `.shadow-layered` - Layered shadow (normal elevation)
- `.shadow-layered-lg` - Layered shadow (high elevation)
- `.gradient-radial` - Radial gradient background
- `.card` - Standard card with hover lift
- `.pricing-card` - Pricing card with top border animation
- `.feature-icon` - Icon container with rotation on card hover
- `.gallery-image` - Image with scale + overlay on hover
- `.step-number` - Circular numbered badge with gradient
- `.faq-item` - FAQ row with hover indent

## Notes

- This is a **conversion-optimized landing page** - every element serves to drive bookings
- **Google Ads context**: Users arrive with high intent, need clear path to booking/quote
- **Mobile-first critical**: Most Google Ads traffic is mobile
- **Premium aesthetic**: Service is high-end, design must reflect quality and trustworthiness
- **Single-file architecture**: Keep everything in one HTML file for maximum portability and speed
