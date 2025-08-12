Step 1: Design Brief Summary
BSR needs a calm, low-friction, Mac/iPad-first web UI where teachers can file in 10–15s, students complete a simple 4-question kiosk reflection (no logins), and teachers/admins review in real time. Accessibility (WCAG 2.2 AA), color-blind safety, and clear focus states are non-negotiable, with reduced-motion and Retina optimizations.

Step 2: Generate Color Palettes
Palette 1: Pacific Calm (teal + slate)
• Primary: #0E7490 – Deep Teal – Primary actions, links, focus ring
• Secondary: #475569 – Slate 600 – Headers, icons, secondary buttons
• Accent: #047857 – Emerald 800 – Success, confirm, positive chips
• Neutral Dark: #0F172A – Slate 900 – Body text on light, key labels
• Neutral Light: #F1F5F9 – Slate 100 – App background, cards
• Accessibility (contrast ratios):
  ◦ Primary on white: 5.36:1, white on Primary: 5.36:1
  ◦ Secondary on white: 7.58:1
  ◦ Accent on white: 5.48:1
  ◦ Neutral Dark on Neutral Light: 16.30:1
• Emotional Impact: Supportive, trustworthy, non-punitive.
• Best For: Default theme for staff dashboards and kiosk UI.

Palette 2: Civic Warm (deep blue-green + gold)
• Primary: #264653 – Deep Blue-Green – Primary actions, nav
• Secondary: #E9C46A – Warm Gold – Badges, highlights (as background)
• Accent: #287271 – Teal 700 – Affordances, selection states
• Neutral Dark: #1F2937 – Gray 800 – Body text
• Neutral Light: #F9FAFB – Gray 50 – Background
• Accessibility:
  ◦ Primary on white: 10.08:1
  ◦ Use Neutral Dark text on Gold backgrounds: 8.79:1
  ◦ Accent on white: 5.62:1
  ◦ Neutral Dark on Neutral Light: 14.05:1
• Emotional Impact: Warm authority, clarity without severity.
• Best For: Admin views, weekly reports, export templates.

Palette 3: Indigo Focus (indigo + sky + emerald)
• Primary: #4F46E5 – Indigo 600 – Primary buttons, tabs
• Secondary: #0369A1 – Sky 700 – Selected states, charts
• Accent: #047857 – Emerald 800 – Success states
• Neutral Dark: #111827 – Gray 900 – Text
• Neutral Light: #FAFAFA – Gray 50 – Background
• Accessibility:
  ◦ Primary on white: 6.29:1
  ◦ Secondary on white: 5.93:1
  ◦ Accent on white: 5.48:1
  ◦ Neutral Dark on Neutral Light: 17.00:1
• Emotional Impact: Concentration, forward momentum.
• Best For: Teacher review screens and approval workflows.
All contrasts meet WCAG 2.2 AA for normal text when used as specified (avoid gold text on white; use it as a background with dark text).

Step 3: Typography Pairings
Pairing 1: Native Calm (system)
• Heading: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial
• Body: same stack
• Why They Work: Feels native on macOS/iPadOS (SF Pro), zero download, crisp at Retina sizes; consistent across staff and kiosk devices.
• Personality: Professional, invisible UI.
• Usage Guidelines:
  ◦ H1 28/32, H2 22/28, H3 18/24, Body 16/24, Small 14/20
  ◦ Weights: Headings 600, Body 400/500, Buttons 600

Pairing 2: Humanist Clarity
• Heading: Manrope (Google Fonts)
• Body: Inter (Google Fonts)
• Why They Work: Wide apertures, strong legibility at small sizes; Manrope’s geometric headings balance Inter’s workhorse body.
• Personality: Clear, modern, friendly.
• Usage Guidelines: H1 30/36 (700), H2 24/32 (600), Body 16/26 (400/500), UI labels 13–14/18 (600).

Pairing 3: Friendly Workhorse
• Heading: Source Sans 3 (Google Fonts)
• Body: Source Sans 3 (same family)
• Why They Work: One-family simplicity with broad weights and excellent hinting; great for dense tables.
• Personality: Calm, institutional without feeling cold.
• Usage Guidelines: H1 28/34 (700), H2 20/28 (600), Body 15/24 (400), Buttons 16/20 (600).

Step 4: Micro-Interaction Patterns
Button Behaviors
• Default: Solid Primary background, white text, 8px radius, 44px min height (kiosk: 48–52px), shadow-sm.
• Hover (pointer): Elevation +1 (shadow), background darken ~6%.
• Active/Pressed: Compress shadow, translateY(1px), background darken ~10%.
• Disabled: 50–60% opacity, no shadow, cursor: not-allowed; maintain 3:1 contrast against background.
• Focus: 2px outline + 2px offset using Primary (or white on dark), always visible (not just box-shadow).
• Transition: 200ms ease (respect reduced motion).

Loading States
• Skeletons: Cards, tables, and reflection form fields.
• Progress Indicators:
  ◦ Teacher actions: subtle linear bar top-of-card.
  ◦ Kiosk reflection: step dots + discreet spinner for network waits.
• Animation: 1.2s shimmer (reduced to none under prefers-reduced-motion).

Feedback Patterns
• Success: Brief toast (3–4s), ‘Reflection submitted. Awaiting review.’ Include Undo when safe.
• Error: Inline, specific, non-shaming (‘Please answer question 3 before submitting.’). Keep field help text visible.
• Tooltips: On hover/focus; not required for kiosk. 250ms open delay.
• Validation: Real-time for kiosk fields after first blur; server errors mapped to fields; ARIA live region (role="status", aria-live="polite") for queue changes.

Step 5: Implementation Guide (CSS Tokens + Patterns)
```css
/* ===== Theme Tokens ===== */
:root {
  /* --- Palette: Pacific Calm (default) --- */
  --color-primary: #0E7490;
  --color-secondary: #475569;
  --color-accent: #047857;
  --color-text: #0F172A;
  --color-bg: #F1F5F9;
  --color-card: #FFFFFF;
  --color-border: #E5E7EB;
  --color-focus: var(--color-primary);

  /* Semantic */
  --color-success: #047857;
  --color-danger: #B91C1C;   /* ensure AA against white */
  --color-warning: #E9C46A;  /* use with dark text */

  /* Typography */
  --font-heading: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  --font-body: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;

  /* Type scale (staff) */
  --fs-h1: 28px; --lh-h1: 32px; --fw-h1: 600;
  --fs-h2: 22px; --lh-h2: 28px; --fw-h2: 600;
  --fs-h3: 18px; --lh-h3: 24px; --fw-h3: 600;
  --fs-body: 16px; --lh-body: 24px; --fw-body: 400;
  --fs-small: 14px; --lh-small: 20px; --fw-small: 400;

  /* Type scale (kiosk) */
  --fs-kiosk-body: 18px; --lh-kiosk-body: 26px;

  /* Spacing + Radius */
  --space-1: 4px; --space-2: 8px; --space-3: 12px; --space-4: 16px; --space-6: 24px; --space-8: 32px;
  --radius: 8px;

  /* Elevation */
  --shadow-sm: 0 1px 2px rgba(0,0,0,0.06);
  --shadow-md: 0 2px 6px rgba(0,0,0,0.10);

  /* Transitions */
  --transition-base: 200ms ease;
}

/* Optional alt themes */
[data-theme="civic-warm"]{
  --color-primary:#264653; --color-secondary:#E9C46A; --color-accent:#287271;
  --color-text:#1F2937; --color-bg:#F9FAFB; --color-card:#FFFFFF; --color-border:#E5E7EB;
  --color-success:#287271; --color-warning:#E9C46A;
}
[data-theme="indigo-focus"]{
  --color-primary:#4F46E5; --color-secondary:#0369A1; --color-accent:#047857;
  --color-text:#111827; --color-bg:#FAFAFA; --color-card:#FFFFFF; --color-border:#E5E7EB;
}

/* --- Base --- */
html, body {
  background: var(--color-bg);
  color: var(--color-text);
  font-family: var(--font-body);
  font-size: var(--fs-body);
  line-height: var(--lh-body);
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
}

h1, h2, h3 {
  font-family: var(--font-heading);
  margin: 0 0 var(--space-3);
  color: var(--color-text);
}
h1 { font-size: var(--fs-h1); line-height: var(--lh-h1); font-weight: var(--fw-h1); }
h2 { font-size: var(--fs-h2); line-height: var(--lh-h2); font-weight: var(--fw-h2); }
h3 { font-size: var(--fs-h3); line-height: var(--lh-h3); font-weight: var(--fw-h3); }

.card {
  background: var(--color-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  box-shadow: var(--shadow-sm);
  padding: var(--space-4);
}

/* --- Buttons --- */
.button {
  display: inline-flex; align-items: center; justify-content: center;
  min-height: 44px; padding: 0 var(--space-4);
  border-radius: var(--radius);
  border: 1px solid transparent;
  font-weight: 600;
  transition: background var(--transition-base), transform var(--transition-base), box-shadow var(--transition-base);
}
.button--primary {
  background: var(--color-primary); color: #fff; box-shadow: var(--shadow-sm);
}
.button--primary:hover { filter: brightness(0.94); box-shadow: var(--shadow-md); }
.button--primary:active { transform: translateY(1px); filter: brightness(0.90); }
.button[disabled], .button[aria-disabled="true"] {
  opacity: .6; box-shadow: none; cursor: not-allowed;
}
:focus-visible {
  outline: 2px solid var(--color-focus);
  outline-offset: 2px;
}

/* --- Forms --- */
.input, .select, .textarea {
  width: 100%;
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: var(--space-3);
  background: #fff;
}
.field-error { color: #B91C1C; font-size: var(--fs-small); line-height: var(--lh-small); margin-top: var(--space-2); }

/* --- Skeletons --- */
.skeleton {
  background: linear-gradient(90deg, rgba(0,0,0,0.06) 25%, rgba(0,0,0,0.10) 37%, rgba(0,0,0,0.06) 63%);
  background-size: 400% 100%;
  animation: shimmer 1.2s infinite linear;
  border-radius: var(--radius);
}
@keyframes shimmer { 0% { background-position: 100% 0; } 100% { background-position: -100% 0; } }

/* --- Reduced motion --- */
@media (prefers-reduced-motion: reduce) {
  * { animation: none !important; transition: none !nimportant; }
}

/* --- Kiosk sizing --- */
.kiosk .button { min-height: 48px; padding: 0 var(--space-6); font-size: 18px; }
.kiosk body { font-size: var(--fs-kiosk-body); line-height: var(--lh-kiosk-body); }
```

Usage notes
• Keep tap targets ≥ 44×44px (iPad).
• Never rely on color alone—pair icons + labels.
• Use ARIA live regions (aria-live="polite", role="status") for queue/assignment changes.
• Respect prefers-color-scheme if you later add dark mode; all palettes above convert cleanly.
If you want, I can drop this into a Canvas with a tiny component kit (buttons, inputs, card, skeleton) wired to these tokens.
