# Architecture-
دليل عملي بالرسم التدريجي لتعلم الرسم المعماري
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="artifact-type" content="narrative">
  <meta name="design-style" content="aurora">
  <title>دليل الرسم المعماري — منهجية البناء المتدرج</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700;800&family=Geist+Mono:wght@400;500;600&family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@1.43.0/dist/umd/lucide.min.js"></script>
  <style>
    :root {
      color-scheme: dark;

      /* Aurora / Blueprint mineral-slate surfaces */
      --background: #0a1116;
      --surface-container-low: #0f1920;
      --surface-container: #14222b;
      --surface-container-high: #1a2d38;

      /* Text */
      --on-surface: #edf3f5;
      --on-surface-variant: #94a8b0;

      /* Borders & Blueprint Grid */
      --outline: #38515c;
      --outline-variant: #20333d;
      --grid-minor: rgba(56, 81, 92, 0.14);
      --grid-major: rgba(45, 212, 191, 0.09);

      /* Accents: Build-Up Turquoise & Semantic */
      --primary: #2dd4bf;
      --on-primary: #061816;
      --primary-container: #123a3d;
      --on-primary-container: #b9f6ee;
      --secondary: #687d87;
      --tertiary: #87d69b;
      --error: #f27474;
      --on-error: #1a0606;
      --positive: #87d69b;
      --warning: #e8b954;
      --focus: #2dd4bf;

      /* Build-Up Drawing Colors */
      --svg-prev: #6a7e88;
      --svg-prev-faint: rgba(106, 126, 136, 0.35);
      --svg-curr: #2dd4bf;
      --svg-curr-glow: rgba(45, 212, 191, 0.25);
      --svg-final-cut: #edf3f5;
      --svg-final-vis: #94a8b0;
      --svg-ground: #e8b954;
      --svg-paper: #080e12;

      /* Data series */
      --data-1: #2dd4bf;
      --data-2: #87d69b;
      --data-3: #e8b954;
      --data-4: #f08c70;
      --data-context: #415861;

      /* Fonts */
      --font-headline: 'Cairo', 'Tajawal', sans-serif;
      --font-body: 'Tajawal', 'Cairo', sans-serif;
      --font-label: 'Geist Mono', 'Cairo', monospace;

      /* Type scale */
      --display-size: clamp(2rem, 1.4rem + 2.4vw, 3.1rem);
      --headline-size: clamp(1.4rem, 1.15rem + 1vw, 1.95rem);
      --subhead-size: clamp(1.1rem, 1rem + 0.4vw, 1.3rem);
      --body-size: clamp(1rem, 0.96rem + 0.18vw, 1.08rem);
      --label-size: 0.8rem;

      /* Radii */
      --rounded: 0.5rem;
      --rounded-lg: 0.75rem;
      --rounded-full: 9999px;

      /* Effects */
      --hairline: 1px solid var(--outline-variant);
      --hairline-strong: 1px solid var(--outline);
      --panel-gradient: linear-gradient(180deg, #16252e 0%, #101b22 100%);
      --cyan-tint: color-mix(in srgb, var(--primary) 13%, transparent);
      --sage-tint: color-mix(in srgb, var(--tertiary) 13%, transparent);
      --amber-tint: color-mix(in srgb, var(--warning) 13%, transparent);
      --error-tint: color-mix(in srgb, var(--error) 13%, transparent);

      /* Spacing scale */
      --space-xs: 0.25rem;
      --space-sm: 0.5rem;
      --space-md: 1rem;
      --space-lg: 1.5rem;
      --space-xl: 2.5rem;
      --space-2xl: 4rem;

      /* Motion */
      --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
      --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
      --dur-micro: 120ms;
      --dur-short: 220ms;
      --dur-long: 420ms;
    }

    *, *::before, *::after { box-sizing: border-box; }
    html, body {
      overflow-x: clip;
      margin: 0;
      padding: 0;
      background-color: var(--background);
      color: var(--on-surface);
      font-family: var(--font-body);
      font-size: var(--body-size);
      line-height: 1.65;
      background-image:
        linear-gradient(to right, var(--grid-major) 1px, transparent 1px),
        linear-gradient(to bottom, var(--grid-major) 1px, transparent 1px),
        linear-gradient(to right, var(--grid-minor) 1px, transparent 1px),
        linear-gradient(to bottom, var(--grid-minor) 1px, transparent 1px);
      background-size: 96px 96px, 96px 96px, 24px 24px, 24px 24px;
    }

    header { position: static !important; }
    button, input, select, textarea { font-family: inherit; }

    :focus-visible {
      outline: 2px solid var(--focus);
      outline-offset: 2px;
    }

    /* Splash Screen */
    .splash-overlay {
      position: fixed;
      inset: 0;
      z-index: 900;
      background-color: var(--background);
      background-image:
        linear-gradient(to right, var(--grid-major) 1px, transparent 1px),
        linear-gradient(to bottom, var(--grid-major) 1px, transparent 1px),
        linear-gradient(to right, var(--grid-minor) 1px, transparent 1px),
        linear-gradient(to bottom, var(--grid-minor) 1px, transparent 1px);
      background-size: 80px 80px, 80px 80px, 20px 20px, 20px 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: var(--space-lg);
      padding: var(--space-lg);
      transition: opacity var(--dur-long) var(--ease-out), transform var(--dur-long) var(--ease-out);
    }

    .splash-overlay.is-docking {
      opacity: 0;
      transform: translateY(-28px) scale(0.96);
      pointer-events: none;
    }

    .splash-overlay.is-hidden {
      display: none;
    }

    .splash-logo-wrap {
      width: min(360px, 86vw);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: var(--space-md);
    }

    .splash-svg {
      width: 100%;
      height: auto;
      overflow: visible;
    }

    .stroke-draw {
      fill: none;
      stroke: var(--primary);
      stroke-width: 2.2;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke-dasharray: 900;
      stroke-dashoffset: 900;
      animation: drawStroke 1.35s var(--ease-out) forwards;
    }

    .stroke-draw-secondary {
      fill: none;
      stroke: var(--on-surface-variant);
      stroke-width: 1.4;
      stroke-dasharray: 500;
      stroke-dashoffset: 500;
      animation: drawStroke 1.1s 0.25s var(--ease-out) forwards;
    }

    .splash-text-fade {
      opacity: 0;
      transform: translateY(8px);
      animation: fadeSlideUp 0.55s 0.55s var(--ease-out) forwards;
      text-align: center;
    }

    .splash-title {
      font-family: var(--font-headline);
      font-weight: 800;
      font-size: clamp(1.35rem, 1.1rem + 1vw, 1.85rem);
      color: var(--on-surface);
      margin: 0;
    }

    .splash-sub {
      font-family: var(--font-body);
      font-size: 0.95rem;
      color: var(--primary);
      margin: var(--space-xs) 0 0;
    }

    .splash-skip {
      background: transparent;
      border: var(--hairline-strong);
      color: var(--on-surface-variant);
      border-radius: var(--rounded-full);
      padding: var(--space-xs) var(--space-md);
      font-size: var(--label-size);
      cursor: pointer;
      min-height: 44px;
      transition: background-color var(--dur-micro), color var(--dur-micro);
    }
    .splash-skip:hover {
      background-color: var(--surface-container-high);
      color: var(--on-surface);
    }

    @keyframes drawStroke {
      to { stroke-dashoffset: 0; }
    }
    @keyframes fadeSlideUp {
      to { opacity: 1; transform: translateY(0); }
    }

    /* Main Layout */
    .page-grid {
      display: grid;
      grid-template-columns: minmax(0, 1fr);
      gap: var(--space-xl);
      padding: var(--space-lg);
      max-width: 1240px;
      margin: 0 auto;
    }
    .page-grid * { min-width: 0; }

    /* Top Site Header */
    .site-header {
      border-bottom: var(--hairline);
      padding-bottom: var(--space-lg);
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-lg);
    }

    .brand-lockup {
      display: flex;
      align-items: center;
      gap: var(--space-md);
    }

    .header-svg-logo {
      width: 64px;
      height: 52px;
      flex-shrink: 0;
    }

    .brand-title {
      font-family: var(--font-headline);
      font-weight: 800;
      font-size: var(--display-size);
      line-height: 1.15;
      margin: 0;
      color: var(--on-surface);
    }

    .brand-sub {
      margin: var(--space-xs) 0 0;
      color: var(--on-surface-variant);
      max-width: 60ch;
      font-size: var(--body-size);
    }

    .header-meta {
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      gap: var(--space-sm);
    }

    .progress-pill {
      background: var(--surface-container);
      border: var(--hairline);
      border-radius: var(--rounded);
      padding: var(--space-sm) var(--space-md);
      display: flex;
      align-items: center;
      gap: var(--space-md);
    }

    .progress-label {
      font-size: var(--label-size);
      color: var(--on-surface-variant);
    }

    .progress-value {
      font-family: var(--font-label);
      font-weight: 600;
      color: var(--primary);
      font-variant-numeric: tabular-nums;
    }

    .progress-track {
      width: 140px;
      height: 8px;
      background: var(--background);
      border-radius: var(--rounded-full);
      border: var(--hairline);
      overflow: hidden;
    }

    .progress-fill {
      height: 100%;
      background: var(--primary);
      border-radius: var(--rounded-full);
      transition: width var(--dur-short) var(--ease-out);
      width: 0%;
    }

    /* Quick Jump Navigation */
    .quick-nav {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-sm);
      align-items: center;
    }

    .nav-anchor {
      display: inline-flex;
      align-items: center;
      gap: var(--space-xs);
      padding: var(--space-sm) var(--space-md);
      min-height: 44px;
      background: var(--surface-container-low);
      border: var(--hairline);
      border-radius: var(--rounded);
      color: var(--on-surface-variant);
      text-decoration: none;
      font-size: 0.92rem;
      font-weight: 500;
      transition: background-color var(--dur-micro), color var(--dur-micro), border-color var(--dur-micro);
    }
    .nav-anchor:hover {
      background: var(--surface-container-high);
      color: var(--on-surface);
      border-color: var(--outline);
    }

    /* Section Headings */
    .section-head {
      display: flex;
      flex-wrap: wrap;
      align-items: flex-end;
      justify-content: space-between;
      gap: var(--space-md);
      margin-bottom: var(--space-md);
    }

    .section-title {
      font-family: var(--font-headline);
      font-weight: 700;
      font-size: var(--headline-size);
      line-height: 1.2;
      margin: 0;
      color: var(--on-surface);
    }

    .section-desc {
      margin: var(--space-xs) 0 0;
      color: var(--on-surface-variant);
      max-width: 65ch;
    }

    .panel {
      background: var(--panel-gradient);
      border: var(--hairline);
      border-radius: var(--rounded-lg);
      padding: var(--space-lg);
    }

    /* Intro Method Legend */
    .method-banner {
      display: grid;
      grid-template-columns: minmax(0, 1.4fr) minmax(0, 1fr);
      gap: var(--space-lg);
      align-items: center;
    }

    .legend-pair {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: var(--space-md);
    }

    .legend-card {
      background: var(--background);
      border: var(--hairline);
      border-radius: var(--rounded);
      padding: var(--space-md);
      display: flex;
      align-items: center;
      gap: var(--space-sm);
    }

    .swatch-gray {
      width: 18px;
      height: 18px;
      border-radius: 4px;
      background: var(--svg-prev);
      flex-shrink: 0;
    }
    .swatch-cyan {
      width: 18px;
      height: 18px;
      border-radius: 4px;
      background: var(--svg-curr);
      box-shadow: 0 0 10px var(--svg-curr-glow);
      flex-shrink: 0;
    }

    /* Interactive Build-Up Simulator */
    .module-tabs {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-sm);
      margin-bottom: var(--space-lg);
    }

    .module-btn {
      display: inline-flex;
      align-items: center;
      gap: var(--space-sm);
      min-height: 44px;
      padding: var(--space-sm) var(--space-md);
      background: var(--surface-container-low);
      border: var(--hairline);
      border-radius: var(--rounded);
      color: var(--on-surface-variant);
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      transition: background-color var(--dur-micro), color var(--dur-micro), border-color var(--dur-micro);
    }

    .module-btn:hover {
      background: var(--surface-container-high);
      color: var(--on-surface);
    }

    .module-btn.is-active {
      background: var(--cyan-tint);
      border-color: var(--primary);
      color: var(--on-primary-container);
    }

    .module-badge {
      font-family: var(--font-label);
      font-size: 0.75rem;
      padding: 2px 7px;
      border-radius: var(--rounded-full);
      background: var(--background);
      color: var(--on-surface-variant);
      border: var(--hairline);
    }
    .module-btn.is-active .module-badge {
      background: var(--primary);
      color: var(--on-primary);
      border-color: var(--primary);
    }

    .simulator-grid {
      display: grid;
      grid-template-columns: minmax(0, 1.35fr) minmax(0, 1fr);
      gap: var(--space-lg);
      align-items: start;
    }

    /* Drawing Canvas Well */
    .canvas-panel {
      background: var(--svg-paper);
      border: var(--hairline-strong);
      border-radius: var(--rounded-lg);
      padding: var(--space-md);
      display: flex;
      flex-direction: column;
      gap: var(--space-md);
    }

    .canvas-toolbar {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-sm);
      border-bottom: var(--hairline);
      padding-bottom: var(--space-sm);
    }

    .canvas-meta {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: var(--space-sm);
    }

    .scale-chip {
      font-family: var(--font-label);
      font-size: var(--label-size);
      background: var(--cyan-tint);
      color: var(--primary);
      border: 1px solid color-mix(in srgb, var(--primary) 35%, transparent);
      border-radius: var(--rounded);
      padding: 3px var(--space-sm);
    }

    .view-toggle-group {
      display: flex;
      gap: var(--space-xs);
    }

    .btn-ghost {
      min-height: 44px;
      padding: var(--space-xs) var(--space-md);
      background: var(--surface-container-low);
      border: var(--hairline);
      border-radius: var(--rounded);
      color: var(--on-surface-variant);
      cursor: pointer;
      font-size: 0.88rem;
      display: inline-flex;
      align-items: center;
      gap: var(--space-xs);
      transition: background-color var(--dur-micro), color var(--dur-micro);
    }
    .btn-ghost:hover {
      background: var(--surface-container-high);
      color: var(--on-surface);
    }
    .btn-ghost.is-active {
      background: var(--primary-container);
      color: var(--on-primary-container);
      border-color: var(--primary);
    }

    .svg-stage-box {
      width: 100%;
      min-height: 420px;
      background-color: var(--svg-paper);
      background-image:
        linear-gradient(to right, var(--grid-minor) 1px, transparent 1px),
        linear-gradient(to bottom, var(--grid-minor) 1px, transparent 1px);
      background-size: 20px 20px;
      border-radius: var(--rounded);
      border: var(--hairline);
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      position: relative;
      padding: var(--space-sm);
    }

    .arch-svg {
      width: 100%;
      height: auto;
      max-height: 500px;
      display: block;
    }

    /* Architectural SVG Classes (No inline hex!) */
    .layer-prev { opacity: 0.92; }
    .layer-prev .st-cut,
    .layer-prev .st-vis,
    .layer-prev .st-thin,
    .layer-prev .st-axis,
    .layer-prev .st-hatch,
    .layer-prev .st-dim {
      stroke: var(--svg-prev);
    }
    .layer-prev .st-fill-poche { fill: var(--svg-prev-faint); stroke: var(--svg-prev); }
    .layer-prev .st-txt { fill: var(--svg-prev); }
    .layer-prev .st-fill-solid { fill: var(--svg-prev); }

    .layer-curr .st-cut,
    .layer-curr .st-vis,
    .layer-curr .st-thin,
    .layer-curr .st-axis,
    .layer-curr .st-hatch,
    .layer-curr .st-dim {
      stroke: var(--svg-curr);
    }
    .layer-curr .st-fill-poche { fill: var(--svg-curr-glow); stroke: var(--svg-curr); }
    .layer-curr .st-txt { fill: var(--svg-curr); }
    .layer-curr .st-fill-solid { fill: var(--svg-curr); }

    /* Final Ink Mode */
    .final-ink .layer-prev .st-cut,
    .final-ink .layer-curr .st-cut { stroke: var(--svg-final-cut); }
    .final-ink .layer-prev .st-vis,
    .final-ink .layer-curr .st-vis { stroke: var(--svg-final-vis); }
    .final-ink .layer-prev .st-thin,
    .final-ink .layer-curr .st-thin { stroke: var(--secondary); }
    .final-ink .layer-prev .st-axis,
    .final-ink .layer-curr .st-axis { stroke: var(--outline); }
    .final-ink .layer-prev .st-dim,
    .final-ink .layer-curr .st-dim { stroke: var(--tertiary); }
    .final-ink .layer-prev .st-hatch,
    .final-ink .layer-curr .st-hatch { stroke: var(--secondary); }
    .final-ink .layer-prev .st-fill-poche,
    .final-ink .layer-curr .st-fill-poche { fill: var(--outline); stroke: var(--svg-final-cut); }
    .final-ink .layer-prev .st-txt,
    .final-ink .layer-curr .st-txt { fill: var(--on-surface); }

    .st-cut { stroke-width: 2.6; fill: none; stroke-linecap: square; }
    .st-vis { stroke-width: 1.4; fill: none; }
    .st-thin { stroke-width: 0.9; fill: none; }
    .st-axis { stroke-width: 0.9; stroke-dasharray: 12 4 2 4; fill: none; }
    .st-hidden { stroke-dasharray: 5 4; }
    .st-break { stroke-width: 1.3; fill: none; }
    .st-hatch { stroke-width: 0.8; fill: none; }
    .st-dim { stroke-width: 0.9; fill: none; }
    .st-ground { stroke: var(--svg-ground) !important; stroke-width: 3; }
    .st-txt {
      font-family: var(--font-label);
      font-size: 10px;
      text-anchor: middle;
      dominant-baseline: central;
    }
    .st-txt-ar {
      font-family: var(--font-body);
      font-size: 11px;
      font-weight: 600;
      text-anchor: middle;
    }

    /* Stepper Bar */
    .stepper-row {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-sm);
    }

    .stage-dots {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-xs);
    }

    .stage-dot {
      min-width: 44px;
      min-height: 44px;
      border-radius: var(--rounded);
      border: var(--hairline);
      background: var(--surface-container-low);
      color: var(--on-surface-variant);
      font-family: var(--font-label);
      font-weight: 600;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      transition: background-color var(--dur-micro), color var(--dur-micro), border-color var(--dur-micro);
    }
    .stage-dot:hover {
      background: var(--surface-container-high);
      color: var(--on-surface);
    }
    .stage-dot.is-current {
      background: var(--primary);
      color: var(--on-primary);
      border-color: var(--primary);
    }
    .stage-dot.is-done {
      border-color: var(--tertiary);
      color: var(--tertiary);
      background: var(--sage-tint);
    }

    .nav-btns {
      display: flex;
      gap: var(--space-sm);
    }

    .btn-primary {
      min-height: 44px;
      padding: var(--space-sm) var(--space-lg);
      background: var(--primary);
      color: var(--on-primary);
      border: 1px solid var(--primary);
      border-radius: var(--rounded);
      font-weight: 700;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: var(--space-xs);
      transition: filter var(--dur-micro), opacity var(--dur-micro);
    }
    .btn-primary:hover:not(:disabled) { filter: brightness(1.08); }
    .btn-primary:disabled, .btn-ghost:disabled {
      opacity: 0.4;
      cursor: not-allowed;
    }

    /* Pedagogical Guide Rail */
    .guide-rail {
      display: flex;
      flex-direction: column;
      gap: var(--space-md);
    }

    .stage-header-card {
      border-right: 4px solid var(--primary);
    }

    .stage-kicker {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--primary);
      margin-bottom: var(--space-xs);
      display: block;
    }

    .stage-title {
      font-family: var(--font-headline);
      font-weight: 700;
      font-size: var(--subhead-size);
      margin: 0 0 var(--space-xs);
      color: var(--on-surface);
    }

    .checklist-group {
      display: flex;
      flex-direction: column;
      gap: var(--space-sm);
    }

    .check-item {
      display: flex;
      align-items: flex-start;
      gap: var(--space-sm);
      padding: var(--space-sm) var(--space-md);
      background: var(--background);
      border: var(--hairline);
      border-radius: var(--rounded);
      cursor: pointer;
      min-height: 44px;
      transition: border-color var(--dur-micro), background-color var(--dur-micro);
    }
    .check-item:hover {
      border-color: var(--outline);
    }
    .check-item.is-checked {
      border-color: color-mix(in srgb, var(--tertiary) 45%, transparent);
      background: var(--sage-tint);
    }
    .check-item input[type="checkbox"] {
      width: 20px;
      height: 20px;
      margin-top: 3px;
      accent-color: var(--primary);
      flex-shrink: 0;
      cursor: pointer;
    }

    .rules-split {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: var(--space-md);
    }

    .callout-gold {
      background: var(--amber-tint);
      border: 1px solid color-mix(in srgb, var(--warning) 35%, transparent);
      border-radius: var(--rounded);
      padding: var(--space-md);
    }
    .callout-gold strong { color: var(--warning); display: block; margin-bottom: var(--space-xs); }

    .callout-err {
      background: var(--error-tint);
      border: 1px solid color-mix(in srgb, var(--error) 35%, transparent);
      border-radius: var(--rounded);
      padding: var(--space-md);
    }
    .callout-err strong { color: var(--error); display: block; margin-bottom: var(--space-xs); }

    .tip-box {
      background: var(--cyan-tint);
      border: 1px solid color-mix(in srgb, var(--primary) 30%, transparent);
      border-radius: var(--rounded);
      padding: var(--space-md);
    }
    .tip-box strong { color: var(--primary); }

    .checkpoint-box {
      background: var(--background);
      border: var(--hairline-strong);
      border-radius: var(--rounded);
      padding: var(--space-md);
      display: flex;
      flex-direction: column;
      gap: var(--space-sm);
    }

    /* Interactive Schedules Section */
    .schedules-grid {
      display: grid;
      grid-template-columns: minmax(0, 1fr);
      gap: var(--space-lg);
    }

    .table-wrap {
      overflow-x: auto;
      border: var(--hairline);
      border-radius: var(--rounded);
      background: var(--background);
    }

    table {
      width: 100%;
      border-collapse: collapse;
      text-align: right;
      font-size: 0.94rem;
    }
    th {
      font-family: var(--font-label);
      font-size: var(--label-size);
      color: var(--on-surface-variant);
      background: var(--surface-container-low);
      padding: var(--space-sm) var(--space-md);
      border-bottom: var(--hairline-strong);
      white-space: nowrap;
    }
    td {
      padding: var(--space-sm) var(--space-md);
      border-bottom: var(--hairline);
      color: var(--on-surface);
    }
    tr.schedule-row {
      cursor: pointer;
      transition: background-color var(--dur-micro);
    }
    tr.schedule-row:hover {
      background: var(--surface-container);
    }
    tr.schedule-row.is-selected {
      background: var(--cyan-tint);
    }
    .code-tag {
      font-family: var(--font-label);
      font-weight: 600;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      padding: 2px 10px;
      border-radius: var(--rounded-full);
      background: var(--primary-container);
      color: var(--on-primary-container);
      border: 1px solid color-mix(in srgb, var(--primary) 40%, transparent);
    }

    /* Line Weights Reference */
    .lines-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(290px, 100%), 1fr));
      gap: var(--space-md);
    }

    .line-card {
      background: var(--background);
      border: var(--hairline);
      border-radius: var(--rounded);
      padding: var(--space-md);
      display: flex;
      flex-direction: column;
      gap: var(--space-sm);
    }

    .line-sample-svg {
      width: 100%;
      height: 28px;
      display: block;
    }

    /* Calculators */
    .calc-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: var(--space-lg);
    }

    .form-row {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: var(--space-md);
      align-items: end;
      margin-bottom: var(--space-md);
    }

    .field-group {
      display: flex;
      flex-direction: column;
      gap: var(--space-xs);
    }

    .field-label {
      font-size: 0.9rem;
      font-weight: 600;
      color: var(--on-surface-variant);
    }

    .field-input, .field-select {
      min-height: 44px;
      background: var(--background);
      border: var(--hairline-strong);
      border-radius: var(--rounded);
      color: var(--on-surface);
      padding: var(--space-xs) var(--space-md);
      font-size: 1rem;
      font-variant-numeric: tabular-nums;
    }

    .calc-result-box {
      background: var(--background);
      border: var(--hairline);
      border-radius: var(--rounded);
      padding: var(--space-md);
      display: flex;
      flex-direction: column;
      gap: var(--space-xs);
    }

    .metric-big {
      font-family: var(--font-headline);
      font-weight: 800;
      font-size: clamp(1.6rem, 1.3rem + 1vw, 2.2rem);
      color: var(--primary);
      font-variant-numeric: tabular-nums;
      line-height: 1.2;
    }

    .status-chip {
      display: inline-flex;
      align-items: center;
      gap: var(--space-xs);
      width: fit-content;
      border-radius: var(--rounded);
      padding: 3px var(--space-sm);
      font-size: var(--label-size);
      font-weight: 600;
    }
    .status-ok {
      background: var(--sage-tint);
      color: var(--tertiary);
      border: 1px solid color-mix(in srgb, var(--tertiary) 35%, transparent);
    }
    .status-warn {
      background: var(--amber-tint);
      color: var(--warning);
      border: 1px solid color-mix(in srgb, var(--warning) 35%, transparent);
    }

    /* Glossary & Final Checklist */
    .two-col-bottom {
      display: grid;
      grid-template-columns: minmax(0, 1fr) minmax(0, 1.1fr);
      gap: var(--space-lg);
      align-items: start;
    }

    .glossary-list {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(min(200px, 100%), 1fr));
      gap: var(--space-sm);
      max-height: 360px;
      overflow-y: auto;
      padding-left: var(--space-xs);
    }

    .glossary-item {
      background: var(--background);
      border: var(--hairline);
      border-radius: var(--rounded);
      padding: var(--space-sm) var(--space-md);
      display: flex;
      flex-direction: column;
      gap: 2px;
    }
    .glossary-en {
      font-family: var(--font-label);
      font-size: 0.82rem;
      color: var(--primary);
    }

    .site-footer {
      border-top: var(--hairline);
      padding-top: var(--space-lg);
      padding-bottom: var(--space-xl);
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: var(--space-md);
      color: var(--on-surface-variant);
      font-size: 0.92rem;
    }

    /* Responsive Breakpoints */
    @media (max-width: 960px) {
      .simulator-grid,
      .method-banner,
      .calc-grid,
      .two-col-bottom {
        grid-template-columns: minmax(0, 1fr);
      }
      .header-meta {
        align-items: flex-start;
      }
    }

    @media (max-width: 640px) {
      .page-grid {
        padding: var(--space-md);
        gap: var(--space-lg);
      }
      .rules-split,
      .legend-pair,
      .form-row {
        grid-template-columns: minmax(0, 1fr);
      }
      .svg-stage-box {
        min-height: 300px;
      }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
        scroll-behavior: auto !important;
      }
    }
  </style>
</head>
<body>
  <!-- Splash Screen: Blueprint SVG Stroke Animation -->
  <div id="splash-screen" class="splash-overlay" role="dialog" aria-label="شاشة الترحيب الهندسية">
    <div class="splash-logo-wrap">
      <svg class="splash-svg" viewBox="0 0 360 170" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <!-- Blueprint corner ticks -->
        <path class="stroke-draw-secondary" d="M 16 32 L 16 14 L 34 14 M 326 14 L 344 14 L 344 32 M 16 138 L 16 156 L 34 156 M 326 156 L 344 156 L 344 138" />
        <!-- Plan axes grid -->
        <path class="stroke-draw-secondary" d="M 55 85 L 305 85 M 180 20 L 180 150" stroke-dasharray="10 5 2 5" />
        <!-- Isometric Architectural Building + Drafting Set-Square -->
        <path class="stroke-draw" d="M 110 120 L 110 58 L 180 28 L 250 58 L 250 120 Z" />
        <path class="stroke-draw" d="M 180 28 L 180 120 M 110 58 L 180 86 L 250 58" />
        <path class="stroke-draw" d="M 134 120 L 134 84 L 160 94 L 160 120" />
        <path class="stroke-draw" d="M 200 94 L 228 82 L 228 106 L 200 116 Z" />
        <!-- Drafting compass arc -->
        <path class="stroke-draw-secondary" d="M 88 128 A 102 102 0 0 1 272 128" />
      </svg>
      <div class="splash-text-fade">
        <h2 class="splash-title">دليل الرسم المعماري — البناء المتدرج</h2>
        <p class="splash-sub">من المحاور الأولى إلى اللوحة التنفيذية المتكاملة</p>
      </div>
    </div>
    <button type="button" class="splash-skip" onclick="dismissSplash()">ابدأ التعلّم الآن</button>
  </div>

  <div class="page-grid">
    <!-- Header -->
    <header class="site-header">
      <div class="brand-lockup">
        <svg class="header-svg-logo" viewBox="0 0 120 96" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
          <rect x="4" y="4" width="112" height="88" rx="6" fill="none" stroke="var(--outline)" stroke-width="1.5" />
          <path d="M 22 74 L 22 34 L 60 16 L 98 34 L 98 74 Z" fill="none" stroke="var(--primary)" stroke-width="2.5" stroke-linejoin="round" />
          <path d="M 60 16 L 60 74 M 22 34 L 60 50 L 98 34" fill="none" stroke="var(--primary)" stroke-width="1.6" />
          <path d="M 34 74 L 34 52 L 49 58 L 49 74" fill="none" stroke="var(--tertiary)" stroke-width="1.5" />
        </svg>
        <div>
          <h1 class="brand-title">دليل الرسم المعماري بالبناء المتدرج</h1>
          <p class="brand-sub">محاكي تفاعلي لتعلّم رسم مبنى سكني متكامل خطوة بخطوة (مهندس/ أشرف عبد الجواد)</p>
        </div>
      </div>

      <div class="header-meta">
        <div class="progress-pill">
          <div>
            <div class="progress-label">تقدّم المراجعة الذاتية</div>
            <div id="overall-progress-text" class="progress-value">0 / 29 مرحلة</div>
          </div>
          <div class="progress-track" aria-hidden="true">
            <div id="overall-progress-fill" class="progress-fill"></div>
          </div>
        </div>
        <nav class="quick-nav" aria-label="أقسام الدليل">
          <a class="nav-anchor" href="#simulator-section">المحاكي المتدرج</a>
          <a class="nav-anchor" href="#schedules-section">الجداول والتشطيبات</a>
          <a class="nav-anchor" href="#lines-section">لغة الخطوط</a>
          <a class="nav-anchor" href="#calculators-section">حاسبة المقياس والدرج</a>
          <a class="nav-anchor" href="#glossary-section">المراجعة والقاموس</a>
        </nav>
      </div>
    </header>

    <!-- Method Overview -->
    <section class="panel method-banner" aria-label="منهجية البناء المتدرج">
      <div>
        <h2 class="section-title" style="font-size: var(--subhead-size);">لماذا منهجية البناء المتدرج (Build-Up Method)؟</h2>
        <p style="margin: var(--space-sm) 0 0; color: var(--on-surface-variant);">
          بدلًا من عرض اللوحة النهائية دفعة واحدة وما قد تسببه من ارتباك وتداخل في الخطوط، تنمو اللوحة أمامك مرحلة بعد مرحلة. يظهر ما أُنجز سابقًا باللون الرمادي الهادئ، وما يُضاف في المرحلة الحالية باللون التركوازي المضيء حتى تكتمل اللوحة جاهزة للتنفيذ.
        </p>
      </div>
      <div class="legend-pair">
        <div class="legend-card">
          <span class="swatch-gray" aria-hidden="true"></span>
          <div>
            <strong style="display:block; font-size:0.95rem;">المراحل السابقة</strong>
            <span style="font-size:0.85rem; color:var(--on-surface-variant);">رمادي — مرجع هندسي ثابت</span>
          </div>
        </div>
        <div class="legend-card">
          <span class="swatch-cyan" aria-hidden="true"></span>
          <div>
            <strong style="display:block; font-size:0.95rem; color:var(--primary);">المرحلة الحالية</strong>
            <span style="font-size:0.85rem; color:var(--on-surface-variant);">تركوازي — ما نضيفه الآن</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Interactive Build-Up Drawing Viewer -->
    <section id="simulator-section" aria-labelledby="sim-heading">
      <div class="section-head">
        <div>
          <h2 id="sim-heading" class="section-title">المحاكي التفاعلي للوحات المعمارية</h2>
          <p class="section-desc">اختر اللوحة المعمارية، ثم تنقّل بين مراحل رسمها المتدرج وطبق خطوات التنفيذ ونقطة المراجعة.</p>
        </div>
      </div>

      <!-- Module Selector -->
      <div id="module-tabs" class="module-tabs" role="tablist" aria-label="اللوحات المعمارية"></div>

      <div class="simulator-grid">
        <!-- Drawing Canvas -->
        <div class="canvas-panel">
          <div class="canvas-toolbar">
            <div class="canvas-meta">
              <span id="canvas-module-title" style="font-weight:700; color:var(--on-surface);">المسقط الأفقي</span>
              <span id="canvas-scale-badge" class="scale-chip">مقياس 1:50</span>
            </div>
            <div class="view-toggle-group">
              <button type="button" id="btn-mode-buildup" class="btn-ghost is-active" onclick="setRenderMode('buildup')">وضع البناء المتدرج</button>
              <button type="button" id="btn-mode-final" class="btn-ghost" onclick="setRenderMode('final')">الحبر النهائي</button>
            </div>
          </div>

          <div id="svg-stage-box" class="svg-stage-box" aria-live="polite"></div>

          <div class="stepper-row">
            <div id="stage-dots" class="stage-dots" aria-label="مراحل اللوحة"></div>
            <div class="nav-btns">
              <button type="button" id="btn-prev-stage" class="btn-ghost" onclick="stepStage(-1)">السابق</button>
              <button type="button" id="btn-next-stage" class="btn-primary" onclick="stepStage(1)">المرحلة التالية</button>
            </div>
          </div>
        </div>

        <!-- Pedagogical Guide Rail -->
        <div class="guide-rail">
          <div class="panel stage-header-card">
            <span id="stage-counter" class="stage-kicker">المرحلة 1 من 6</span>
            <h3 id="stage-title" class="stage-title">—</h3>
            <p id="stage-goal" style="margin:0; color:var(--on-surface-variant);"></p>
          </div>

          <div class="panel">
            <h4 style="margin:0 0 var(--space-sm); font-size:1rem;">خطوات التنفيذ المطلوبة</h4>
            <div id="stage-checklist" class="checklist-group"></div>
          </div>

          <div class="rules-split">
            <div class="callout-gold">
              <strong>القاعدة الذهبية</strong>
              <span id="stage-golden" style="font-size:0.93rem;"></span>
            </div>
            <div class="callout-err">
              <strong>تجنّب هذا الخطأ</strong>
              <span id="stage-mistake" style="font-size:0.93rem;"></span>
            </div>
          </div>

          <div class="tip-box">
            <strong>نصيحة المهندس: </strong>
            <span id="stage-tip" style="font-size:0.93rem;"></span>
          </div>

          <div class="checkpoint-box">
            <div style="font-weight:700; color:var(--on-surface);">نقطة المراجعة قبل الانتقال</div>
            <p id="stage-checkpoint" style="margin:0; font-size:0.93rem; color:var(--on-surface-variant);"></p>
            <button type="button" id="btn-mark-verified" class="btn-ghost" onclick="toggleStageVerified()">تأكيد اجتياز هذه المرحلة</button>
          </div>
        </div>
      </div>
    </section>

    <!-- Schedules Section -->
    <section id="schedules-section" class="panel" aria-labelledby="sched-heading">
      <div class="section-head">
        <div>
          <h2 id="sched-heading" class="section-title">الجداول المعمارية والربط بالمسقط</h2>
          <p class="section-desc">اضغط على أي صف في جدول الفتحات أو التشطيبات لعرض بطاقة المواصفات التنفيذية الكاملة لمبنى التدريب (5 أبواب، 8 شبابيك، 5 فراغات).</p>
        </div>
      </div>

      <div id="schedule-detail-banner" class="tip-box" style="margin-bottom: var(--space-lg);">
        <strong>معاينة المواصفات: </strong>
        <span id="schedule-inspector-text">اختر أي باب أو شباك أو غرفة من الجداول أدناه لقراءتها كما يقرأها المهندس المنفذ في الموقع.</span>
      </div>

      <div class="schedules-grid">
        <div>
          <h3 style="margin:0 0 var(--space-sm); font-size:var(--subhead-size);">6-1 جدول الأبواب والشبابيك (Door &amp; Window Schedule)</h3>
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>الرمز</th>
                  <th>النوع / الموضع</th>
                  <th>العرض × الارتفاع (م)</th>
                  <th>الجلسة (م)</th>
                  <th>العدد</th>
                  <th>الخامة</th>
                  <th>طريقة الفتح</th>
                </tr>
              </thead>
              <tbody id="dw-schedule-body"></tbody>
            </table>
          </div>
        </div>

        <div>
          <h3 style="margin:0 0 var(--space-sm); font-size:var(--subhead-size);">6-2 جدول التشطيبات (Finishing Schedule)</h3>
          <div class="table-wrap">
            <table>
              <thead>
                <tr>
                  <th>رقم الغرفة</th>
                  <th>الفراغ</th>
                  <th>الأرضية</th>
                  <th>الوزرة</th>
                  <th>الحوائط</th>
                  <th>السقف</th>
                  <th>ملاحظات</th>
                </tr>
              </thead>
              <tbody id="finish-schedule-body"></tbody>
            </table>
          </div>
        </div>
      </div>
    </section>

    <!-- Line Weights & Types -->
    <section id="lines-section" class="panel" aria-labelledby="lines-heading">
      <div class="section-head">
        <div>
          <h2 id="lines-heading" class="section-title">لغة الخطوط وسلّم السماكات (ISO 128)</h2>
          <p class="section-desc">الخط في الرسم المعماري يحمل دلالة: المقطوع هو الأسمك، والمرئي متوسط، والمحاور والأبعاد والتهشير رفيعة.</p>
        </div>
      </div>
      <div id="lines-grid" class="lines-grid"></div>
    </section>

    <!-- Calculators: Scale Converter & Stair Formula -->
    <section id="calculators-section" aria-labelledby="calc-heading">
      <div class="section-head">
        <div>
          <h2 id="calc-heading" class="section-title">الحاسبة الهندسية المصغّرة</h2>
          <p class="section-desc">تحويل الأطوال الحقيقية إلى سنتيمترات على الورق بمقياس الرسم، واختبار راحة الدرج بمعادلة <bdi dir="ltr">2R + G</bdi>.</p>
        </div>
      </div>

      <div class="calc-grid">
        <!-- Scale Calculator -->
        <div class="panel">
          <h3 style="margin:0 0 var(--space-md); font-size:var(--subhead-size);">حاسبة مقياس الرسم (Scale Converter)</h3>
          <div class="form-row">
            <div class="field-group">
              <label for="calc-real-meters" class="field-label">الطول الحقيقي (بالمتر)</label>
              <input id="calc-real-meters" type="number" step="0.05" min="0.05" max="500" value="7.45" class="field-input" oninput="updateScaleCalc()">
            </div>
            <div class="field-group">
              <label for="calc-scale-select" class="field-label">مقياس الرسم المطلوب</label>
              <select id="calc-scale-select" class="field-select" onchange="updateScaleCalc()">
                <option value="20">1:20 (تفاصيل — × 5)</option>
                <option value="25">1:25 (تفاصيل متوسطة — × 4)</option>
                <option value="50" selected>1:50 (مسقط وقطاع وواجهة — × 2)</option>
                <option value="100">1:100 (مسقط عام وسطوح — × 1)</option>
                <option value="200">1:200 (الموقع العام — × 0.5)</option>
              </select>
            </div>
          </div>

          <div class="calc-result-box">
            <span style="font-size:0.88rem; color:var(--on-surface-variant);">الطول المرسوم على الورق</span>
            <div id="scale-output-cm" class="metric-big">14.90 سم</div>
            <div id="scale-formula-note" style="font-family:var(--font-label); font-size:0.85rem; color:var(--on-surface-variant);"></div>
          </div>

          <div style="display:flex; flex-wrap:wrap; gap:var(--space-xs); margin-top:var(--space-md);">
            <button type="button" class="btn-ghost" onclick="loadScalePreset(3.60, 50)">محور A–B (3.60 م @1:50)</button>
            <button type="button" class="btn-ghost" onclick="loadScalePreset(0.25, 20)">حائط 25 سم @1:20</button>
            <button type="button" class="btn-ghost" onclick="loadScalePreset(4.50, 100)">4.50 م @1:100</button>
          </div>
        </div>

        <!-- Stair Formula Calculator -->
        <div class="panel">
          <h3 style="margin:0 0 var(--space-md); font-size:var(--subhead-size);">حاسبة معادلة الدرج (<bdi dir="ltr">2R + G</bdi>)</h3>
          <div class="form-row">
            <div class="field-group">
              <label for="calc-floor-height" class="field-label">ارتفاع الدور (متر)</label>
              <input id="calc-floor-height" type="number" step="0.05" min="2.4" max="5.0" value="3.00" class="field-input" oninput="updateStairCalc()">
            </div>
            <div class="field-group">
              <label for="calc-risers-count" class="field-label">عدد القوائم (Risers)</label>
              <input id="calc-risers-count" type="number" step="1" min="10" max="30" value="18" class="field-input" oninput="updateStairCalc()">
            </div>
          </div>
          <div class="form-row">
            <div class="field-group">
              <label for="calc-going-cm" class="field-label">عرض النائمة G (سم)</label>
              <input id="calc-going-cm" type="number" step="1" min="20" max="36" value="28" class="field-input" oninput="updateStairCalc()">
            </div>
            <div class="field-group">
              <span class="field-label">ارتفاع القائمة المحسوب (R)</span>
              <div id="stair-riser-cm" class="field-input" style="display:flex; align-items:center; color:var(--primary); font-weight:700;">16.7 سم</div>
            </div>
          </div>

          <div class="calc-result-box">
            <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:var(--space-sm);">
              <div>
                <span style="font-size:0.88rem; color:var(--on-surface-variant);">ناتج معادلة الراحة (2R + G)</span>
                <div id="stair-formula-val" class="metric-big">61.4 سم</div>
              </div>
              <div id="stair-comfort-chip" class="status-chip status-ok">درج مريح ومتوازن (60–64 سم)</div>
            </div>
            <svg id="stair-preview-svg" viewBox="0 0 280 95" style="width:100%; height:95px; margin-top:var(--space-xs);" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"></svg>
          </div>
        </div>
      </div>
    </section>

    <!-- Final Checklist & Glossary -->
    <section id="glossary-section" class="two-col-bottom" aria-label="قائمة المراجعة النهائية وقاموس المصطلحات">
      <div class="panel">
        <div style="display:flex; justify-content:space-between; align-items:center; gap:var(--space-sm); margin-bottom:var(--space-md);">
          <h2 class="section-title" style="font-size:var(--subhead-size);">قائمة المراجعة النهائية للوحة</h2>
          <button type="button" id="btn-reset-all" class="btn-ghost" onclick="resetProgress(this)">إعادة تعيين التقدم</button>
        </div>
        <div id="final-checklist-box" class="checklist-group"></div>
      </div>

      <div class="panel">
        <h2 class="section-title" style="font-size:var(--subhead-size); margin-bottom:var(--space-sm);">قاموس المصطلحات المعمارية</h2>
        <div class="field-group" style="margin-bottom:var(--space-md);">
          <label for="glossary-search" class="field-label">ابحث بالعربية أو بالإنجليزية</label>
          <input id="glossary-search" type="text" class="field-input" placeholder="مثال: عتب، Lintel، قطاع..." oninput="filterGlossary(this.value)">
        </div>
        <div id="glossary-list" class="glossary-list"></div>
      </div>
    </section>

    <footer class="site-footer">
      <div>مستند إلى «الدليل العملي للرسم المعماري بأسلوب البناء المتدرج (Build-Up Method)» — م. أشرف عبد الجواد.</div>
      <div>أرقام الجداول والارتفاعات إرشادية للتدريب وتُعتمد حسب اشتراطات كل مشروع.</div>
    </footer>
  </div>

  <api-shim></api-shim>
  <script>
    // =========================================================================
    // 1. ARCHITECTURAL DATA MODEL (100% Grounded in Source Material)
    // =========================================================================
    const MODULES = [
      {
        id: `floorplan`,
        name: `المسقط الأفقي`,
        scale: `1:50`,
        subtitle: `مبنى التدريب (7.45 × 7.05 م)`,
        viewBox: `0 0 600 440`,
        stages: [
          {
            title: `تأسيس المحاور (Grid & Axes)`,
            goal: `رسم الشبكة الهندسية الأساسية للمشروع وتحديد مراكز الحوائط بدقة متناهية قبل أي تفاصيل.`,
            steps: [
              `ثبّت الورقة بالشريط اللاصق واستخدم قلم 2H برأس مدبب جيدًا.`,
              `ارسم المحاور الرأسية A و B و C على بعد 7.2 سم من بعضها (3.60 م)، والأفقية 1 و 2 و 3 على بعد 6.0 سم ثم 7.6 سم (3.00 م و 3.80 م).`,
              `اجعل المحور شرطة طويلة ثم نقطة بخط رفيع، وانهِه بدائرة قطرها نحو 1 سم تحمل الحرف أو الرقم.`
            ],
            golden: `المحاور تمر في منتصف سمك الحائط غالبًا، فهي مراجع للقياس لا حوائط.`,
            mistake: `الضغط الزائد على القلم في هذه المرحلة فيصعب مسح الخطوط ويترك أثرًا في الورقة.`,
            tip: `تأكد أن الشبكة مستطيلة بقياس القطرين: يجب أن يتساويا، فإن اختلفا فالزوايا ليست قائمة.`,
            checkpoint: `هل الخطوط خفيفة ونظيفة ومتعامدة بدقة والمسافات مطابقة للمحاور A-B-C و 1-2-3؟`
          },
          {
            title: `تحديد سمك الحوائط (Walls)`,
            goal: `رسم حدود الحوائط الخارجية والداخلية حول المحاور بسمكها الحقيقي.`,
            steps: [
              `ارسم الحوائط الخارجية بسمك 25 سم (0.5 سم على الورق): 0.25 سم على كل جانب من المحور.`,
              `ارسم الحوائط الداخلية بسمك 12 سم (0.24 سم على الورق) بنفس الطريقة.`,
              `ارسم الحوائط كلها أفقيًا ثم كلها رأسيًا لتسريع العمل بالمسطرة T والمثلث، بقلم HB بضغط خفيف.`
            ],
            golden: `الحائط خطان متوازيان على جانبي المحور بمقدار نصف السمك لكل جانب.`,
            mistake: `رسم سمك الحائط كله على جانب واحد من المحور، فتتغير أبعاد الغرف وتختل المحاور.`,
            tip: `التزم بسمك الحوائط المحدد لمشروعك (25 سم خارجي / 12 سم داخلي) وثبّته في كل الرسومات.`,
            checkpoint: `هل تلتقي الحوائط في الأركان وفي التقاطعات من غير ثغرات ولا خطوط زائدة؟`
          },
          {
            title: `فتح الفتحات: الأبواب والشبابيك (Openings)`,
            goal: `إنشاء الفتحات في الحوائط ورسم رمز كل باب وشباك بعرضه الحقيقي.`,
            steps: [
              `حدد عرض كل فتحة على الحائط (مثل الشباك 1.20 م = 2.4 سم) وامسح خطوط الحائط داخل العرض.`,
              `أغلق جانبي الفتحة بخطين قصيرين عموديين (Jambs).`,
              `الشباك: ثلاثة خطوط متوازية. الباب: ضلفة بخط سميك وقوس ربع دائرة نصف قطره يساوي عرض الباب يبين اتجاه الفتح.`
            ],
            golden: `نفتح الفتحات قبل التظليل، فبعد التظليل يصعب التعديل.`,
            mistake: `رسم قوس باب يصطدم بحائط أو بباب آخر أو بالأثاث الثابت.`,
            tip: `استخدم الفرجار أو شبلونة الدوائر لرسم أقواس الأبواب لتخرج متساوية ونظيفة.`,
            checkpoint: `هل يستطيع كل باب أن يفتح بالكامل دون عائق؟ وهل عرض كل فتحة مطابق لجدول الأبواب والشبابيك؟`
          },
          {
            title: `إبراز الحوائط المقطوعة (Poche)`,
            goal: `إظهار الحوائط التي قطعها مستوى القطع بأقوى عنصر في اللوحة.`,
            steps: [
              `اختر لونًا غامقًا أو خطًا سميكًا (0.5 – 0.7 مم) للحوائط المقطوعة.`,
              `ظلّل الحوائط بين خطي الحائط ولا تدخل في فتحات الأبواب والشبابيك.`,
              `أغلق نهايات الحوائط عند الفتحات بنفس القوة والوضوح.`
            ],
            golden: `الذي يتقطع فقط هو الذي يتظلل، فالمقطوع هو أسمك عنصر في المسقط.`,
            mistake: `تظليل فتحات الأبواب أو الشبابيك أو أرضية الغرف، مما يضيع معنى القطع.`,
            tip: `إن كنت تستخدم قلمًا حبريًا فالأفضل التظليل في النهاية لأن المحو بعده صعب.`,
            checkpoint: `انظر إلى اللوحة من مسافة متر: هل يظهر مخطط المبنى بوضوح من الحوائط وحدها؟`
          },
          {
            title: `الأثاث والتجهيزات (Furniture & Fixtures)`,
            goal: `إعطاء إحساس بالمقياس والاستخدام بوضع الأثاث والأجهزة الصحية بأحجامها الحقيقية.`,
            steps: [
              `ارسم الأثاث بخط رفيع (2H أو HB خفيف): السرير 2.00 × 1.40 م، وطاولة السفرة نحو 1.20 × 1.00 م.`,
              `ارسم المطبخ (حوض وموقد وثلاجة) والحمام (مغسلة ومرحاض ودش).`,
              `راقب مسارات الحركة وحيّز فتح الأبواب في كل غرفة.`
            ],
            golden: `الأثاث لا يُقطع فيُرسم بخط أرفع من خط الحوائط والفتحات.`,
            mistake: `رسم الأثاث بحجم أكبر أو أصغر من الحقيقي، أو وضع سرير أمام الباب فيمنع فتحه.`,
            tip: `اصنع ورقة قوالب (Template) للأثاث بالمقياس 1:50 وانقلها بالتتبع في كل مشروع.`,
            checkpoint: `هل يمكن لشخص المرور بين الأثاث وفتح الأبواب بسهولة (ممر لا يقل عن نحو 60 سم)؟`
          },
          {
            title: `التهشير والأبعاد والبيانات النصية (Final Detailing)`,
            goal: `إخراج اللوحة بشكل احترافي: خطوط الأبعاد الثلاثة وأسماء الفراغات والرموز.`,
            steps: [
              `ارسم على كل ضلع خارجي ثلاثة خطوط أبعاد: تفصيلي (فتحات)، ثم المحاور، ثم الكلي (7.45 م).`,
              `استخدم علامة نهاية مائلة 45° وأرقامًا فوق خطوط الأبعاد.`,
              `اكتب أسماء الفراغات وأرقامها (1–5) ورموز الأبواب والشبابيك، ثم رمز الشمال وعلامة القطاع A-A.`
            ],
            golden: `الكتابة من أسفل اللوحة أو من يمينها، ولا تتقاطع الأرقام مع خطوط الرسم.`,
            mistake: `كتابة الأرقام بخط يد عشوائي أو بخطوط سميكة تطغى على حدود الحائط.`,
            tip: `ارسم خطين إرشاديين خفيفين قبل الكتابة لضمان استقامة الحروف وتوحيد ارتفاعها.`,
            checkpoint: `هل مجموع الأبعاد التفصيلية يساوي البعد الكلي (7.45 م)؟ وهل كل رقم واضح ومقروء؟`
          }
        ]
      },
      {
        id: `stairplan`,
        name: `مسقط الدرج وتفصيلته`,
        scale: `1:50 و 1:5`,
        subtitle: `بئر الدرج (290 × 360 سم) وتفصيلة الدرجة`,
        viewBox: `0 0 600 420`,
        stages: [
          {
            title: `بئر الدرج والمحاور (Stair Well)`,
            goal: `رسم المساحة التي سيوضع فيها الدرج: المحاوران وحوائط البئر.`,
            steps: [
              `ارسم المحورين 1 و 2 والمسافة بينهما 2.40 م (4.8 سم بمقياس 1:50).`,
              `ارسم الحوائط بسمك 25 سم من ثلاث جهات، واترك جهة الدخول مفتوحة (طول البئر 3.60 م = 7.2 سم).`,
              `علّم مستوى بداية الدرج ±0.00 بخط خفيف.`
            ],
            golden: `نرسم البئر أولًا لأن مقاسه هو الذي يحدد عدد الدرجات وعرض الطيران.`,
            mistake: `رسم الدرجات قبل حساب طول البئر، فلا يتسع الدرج في النهاية.`,
            tip: `احسب قبل الرسم: ارتفاع الدور 3.00 م ÷ 18 قائمًا = 16.7 سم للقائم الواحد.`,
            checkpoint: `هل طول البئر وعرضه يكفيان لطيرانين وبسطة؟ وهل المحاور مطابقة لمحاور المسقط؟`
          },
          {
            title: `الطيران الأول: الدرجات المقطوعة (Flight 1)`,
            goal: `رسم الدرجات التي يراها القارئ أسفل خط القطع.`,
            steps: [
              `قسّم طول الطيران على عدد الدرجات: 8 درجات × 28 سم = 224 سم.`,
              `ارسم خطوط الدرجات بعرض 110 سم (2.2 سم بمقياس 1:50)؛ كل خط يمثل حرف درجة.`,
              `ابدأ من أول درجة عند ±0.00 وارسم 7 درجات بخط متصل.`
            ],
            golden: `الدرجات التي تقع تحت مستوى القطع تُرسم بخط متصل.`,
            mistake: `رسم الدرجات بتباعد غير متساوٍ فيختل مقياس الطيران.`,
            tip: `ارسم خطًا خفيفًا بطول الطيران ثم قسّمه بالفرجار إلى أجزاء متساوية.`,
            checkpoint: `هل كل الدرجات متساوية في العرض؟ وهل عددها يطابق الحساب؟`
          },
          {
            title: `البسطة والطيران العلوي (Landing & Upper Flight)`,
            goal: `إظهار ما يقع فوق مستوى القطع وخط القطع المائل.`,
            steps: [
              `ارسم البسطة بعرض البئر وبعمق لا يقل عن عرض الطيران (110 سم).`,
              `ارسم الطيران الثاني على الجهة الأخرى بخط متقطع (Hidden) لأنه أعلى من القطع.`,
              `ارسم خط القطع المائل (Break Line) على الطيران الأول عند ارتفاع 1.00 – 1.20 م.`
            ],
            golden: `ما يقع فوق مستوى القطع يُرسم بخط متقطع رفيع، وما تحته بخط متصل.`,
            mistake: `رسم كل الدرجات بخط متصل، فيظن القارئ أن الدرج بلا بسطة أو في منسوب واحد.`,
            tip: `خط القطع المائل يمتد خارج الحائط قليلًا ليراه القارئ بوضوح.`,
            checkpoint: `هل يميّز القارئ بين الدرجات المتصلة والدرجات المتقطعة فوق القطع؟`
          },
          {
            title: `سهم الاتجاه وأرقام الدرجات (Direction Arrow)`,
            goal: `إخبار القارئ من أين يبدأ الدرج وإلى أين يصعد.`,
            steps: [
              `ارسم خطًا من منتصف أول درجة حتى خط القطع، يبدأ بنقطة وينتهي بسهم.`,
              `اكتب كلمة UP (صعود) بجوار السهم.`,
              `رقّم الدرجات من 1 إلى 7 بحجم صغير ومنتظم داخلها.`
            ],
            golden: `السهم يبدأ بنقطة عند أول درجة ويشير دائمًا إلى جهة الصعود.`,
            mistake: `وضع السهم بلا نقطة بداية، أو توجيهه في اتجاه معاكس للصعود.`,
            tip: `في المسقط الأرضي اكتب UP، وفي الأدوار العليا اكتب UP و DN حسب الاتجاه.`,
            checkpoint: `هل يعرف القارئ من السهم أين يبدأ الصعود وإلى أين يتجه؟`
          },
          {
            title: `الأبعاد والمناسيب لمسقط الدرج (Dimensions & Levels)`,
            goal: `كتابة الأبعاد والمناسيب وربط المسقط بتفصيلة الدرجة.`,
            steps: [
              `اكتب عرض الدرجة 28 سم وطول الطيران 224 سم وعرض الطيران 110 سم والفانوس 20 سم، والأبعاد الكلية 290 × 360 سم.`,
              `اكتب منسوب بداية الدرج ±0.00 ومنسوب البسطة +1.50 وعدد القوائم 18 قائمًا (16.7 سم).`,
              `ضع رمز تفصيلة الدرجة ST-1 / D-05.`
            ],
            golden: `المناسيب هي التي تربط المسقط بالقطاع؛ لوحة بلا مناسيب لا تُنفَّذ.`,
            mistake: `نسيان منسوب البسطة أو كتابة الأبعاد داخل الدرجات فتختلط بأرقامها.`,
            tip: `راجع المجموع فورًا: 224 + 136 = 360 سم، و 110 + 20 + 110 + 50 = 290 سم.`,
            checkpoint: `هل 18 قائمًا × 16.7 سم = 3.00 م؟ وهل رمز التفصيلة مكتوب بوضوح؟`
          },
          {
            title: `تفصيلة الدرجة المكبرة (Step Detail 1:5)`,
            goal: `تكبير الدرجة الواحدة بمقياس 1:5 لإظهار البلاطة المائلة وطبقات الرخام والمونة والأبعاد.`,
            steps: [
              `ارسم 3 درجات خرسانية بارتفاع 16.7 سم وعرض 28 سم فوق بلاطة مائلة بسمك عمودي 15 سم.`,
              `أضف رخام النائمة 2 سم ببروز (Nosing) 2 سم، ورخام القائمة 2 سم ومونة 2 سم، ولياسة السقف 2 سم.`,
              `هشّر الخرسانة والمونة والرخام، واكتب الأبعاد وتحقق من القاعدة 2R + G = 61.4 سم.`
            ],
            golden: `2 × القائم + العرض ≈ 60 – 64 سم لدرج مريح، والدرجة الخرسانية أصغر بمقدار التشطيب.`,
            mistake: `قياس سمك البلاطة أفقيًا بدل قياسه عموديًا على الميل، أو عمل بروز كبير للرخام.`,
            tip: `المقياس 1:5 يعني أن كل 20 سم في الواقع تُرسم 4 سم على الورق لوضوح الطبقات.`,
            checkpoint: `هل ترتيب الطبقات صحيح من الخرسانة المسلحة حتى الرخام، ومعادلة 2R + G محققة؟`
          }
        ]
      },
      {
        id: `section`,
        name: `القطاع المعماري`,
        scale: `1:50`,
        subtitle: `القطاع A-A مطل على الشمال`,
        viewBox: `0 0 600 410`,
        stages: [
          {
            title: `خط الأرض والمناسيب والمحاور (Datum Lines)`,
            goal: `رسم المراجع الرأسية والأفقية التي سيُبنى عليها القطاع كله.`,
            steps: [
              `ارسم خط الأرض بخط خفيف (سيُسمَّك لاحقًا) بطول يزيد عن عرض المبنى.`,
              `ارفع منسوب الدور ±0.00 فوق خط الأرض بـ 0.50 م (1.0 سم بمقياس 1:50)، ثم +3.00، ثم +4.00.`,
              `انقل المحاور A و B و C من المسقط بنفس المسافات (7.2 سم).`
            ],
            golden: `القطاع يأخذ عرضه من المسقط وارتفاعاته من المناسيب؛ لا يُرسم من الخيال.`,
            mistake: `نسيان خط الأرض أو رسم الأساسات تحته في القطاع المعماري.`,
            tip: `استعمل شريطًا ورقيًا (Paper Strip) تنقل عليه مواضع المحاور من المسقط إلى القطاع بلا قياس جديد.`,
            checkpoint: `هل تطابق مواضع المحاور هنا مواضعها في المسقط بالضبط؟`
          },
          {
            title: `حدود العناصر المقطوعة (Cut Elements)`,
            goal: `رسم الحوائط والبلاطة والسور والعتب التي قطعها المستوى بحدودها الحقيقية.`,
            steps: [
              `ارسم الحوائط الخارجية بسمك 25 سم والحائط الداخلي 12 سم عند موضعه.`,
              `ارسم بلاطة السقف بسمك 15 سم وسور السطح بارتفاع 1.00 م.`,
              `اترك مكان الشباك بين جلسته 1.00 م ورأسه 2.20 م، وارسم العتب (15 سم) فوقه والجلسة تحته.`
            ],
            golden: `العناصر المقطوعة هي الأسمك في القطاع (0.5 – 0.7 مم).`,
            mistake: `تقطيع الحائط عند الشباك كاملًا وكأنه فتحة بلا عتب وبلا جلسة.`,
            tip: `ارسم حدود العناصر أولًا بدون تهشير، فهذا يسمح لك بالتصحيح بسهولة.`,
            checkpoint: `هل منسوب أعلى كل الشبابيك واحد (+2.20 م) والعتب فوقه مباشرة؟`
          },
          {
            title: `الفتحات وطبقات الأرضية والسقف (Openings & Layers)`,
            goal: `إضافة الزجاج وطبقات التشطيب التي تعطي القطاع معناه المعماري.`,
            steps: [
              `ارسم الزجاج بخطين رفيعين متوازيين داخل فتحة الشباك.`,
              `ارسم طبقات الأرضية: بلاط + مونة + خرسانة عادية + رمل (حتى -0.50).`,
              `ارسم طبقات السطح: خرسانة ميول + عزل مائي (خط سميك) + طبقة تشطيب، وغطاء السور.`
            ],
            golden: `مقياس الرسم يحدد التفاصيل: في 1:50 نُظهر الطبقات الرئيسية فقط والباقي في لوحة التفاصيل.`,
            mistake: `تفصيل كل طبقة بسمكها الدقيق في مقياس صغير فيزدحم الرسم وتختلط الخطوط.`,
            tip: `إن كانت الطبقة أرفع من 0.3 مم في المقياس فارسمها بخط واحد واضح.`,
            checkpoint: `هل تمثل طبقات الأرضية والسطح ترتيبًا صحيحًا من الأسفل إلى الأعلى؟`
          },
          {
            title: `تهشير المقطوع (Hatching)`,
            goal: `الدلالة على مادة كل عنصر مقطوع بنمط التهشير المناسب.`,
            steps: [
              `هشّر الطوب بخطوط مائلة 45° رفيعة (0.13 – 0.18 مم).`,
              `هشّر الخرسانة المسلحة للبلاطة والعتب بنمط الخرسانة، والرمل بالنقاط.`,
              `ارسم رمز الردم أو التربة تحت خط الأرض.`
            ],
            golden: `كل مادة بنمط واحد في كل اللوحات، ويُكتب مفتاح الرموز على اللوحة.`,
            mistake: `خلط الأنماط أو تغيير اتجاه التهشير في العنصر الواحد.`,
            tip: `تباعد خطوط التهشير متساوٍ نحو 2 – 3 مم؛ استعمل ورقة مسطرة تحت الشفاف لتوحيد التباعد.`,
            checkpoint: `هل يمكن لقارئ اللوحة معرفة المادة من النمط دون شرح شفهي؟`
          },
          {
            title: `ما وراء القطع: العناصر المرئية (Beyond the Cut)`,
            goal: `رسم ما نراه خلف مستوى القطع بخط أرفع لإعطاء القطاع عمقًا ومقياسًا.`,
            steps: [
              `ارسم الأبواب التي نراها على الحائط خلف القطع بخط رفيع بلا تهشير.`,
              `ارسم الكابينة والثلاجة وما يظهر من الأثاث الثابت في الواجهة الداخلية.`,
              `أضف شكل إنسان (1.70 م) لإعطاء مقياس بصري حي للمبنى.`
            ],
            golden: `ما لم يُقطع لا يُهشّر ويُرسم بخط أرفع من المقطوع.`,
            mistake: `رسم الأبواب الخلفية بخط سميك فتبدو كأنها مقطوعة في الحائط.`,
            tip: `لا تبالغ في تفاصيل الأثاث، فالقطاع المعماري يركز على الارتفاعات والفراغ.`,
            checkpoint: `هل يميز القارئ بسهولة بين المقطوع (سميك ومهشّر) والمرئي (رفيع بلا تهشير)؟`
          },
          {
            title: `المناسيب والأبعاد والنصوص (Dimensions & Levels)`,
            goal: `كتابة الارتفاعات والمناسيب لتصبح اللوحة قابلة للتنفيذ.`,
            steps: [
              `ارسم علامات المناسيب (مثلثًا مع رقم): -0.50 و ±0.00 و +3.00 و +4.00.`,
              `ارسم سلسلتين من الأبعاد الرأسية: تفصيلية (0.50 + 3.00 + 1.00) وكلية (4.50 م).`,
              `أضف أبعاد الشباك (جلسة 1.00 م وارتفاع 1.20 م) وعنوان القطاع ومقياسه.`
            ],
            golden: `المنسوب رقم بالمتر بدقتين عشريتين وبعلامة موجب أو سالب واضحة.`,
            mistake: `كتابة المناسيب بوحدات مختلفة (سم في موضع ومتر في آخر).`,
            tip: `راجع مجموع الارتفاعات: 0.50 + 3.00 + 1.00 = 4.50 م يجب أن يطابق البعد الكلي.`,
            checkpoint: `هل تتطابق المناسيب وأعلى السور مع ما سنرسمه في الواجهة؟`
          }
        ]
      },
      {
        id: `elevation`,
        name: `الواجهة الجنوبية`,
        scale: `1:50`,
        subtitle: `منظر خارجي بلا قطع (عرض من المسقط + ارتفاع من القطاع)`,
        viewBox: `0 0 600 390`,
        stages: [
          {
            title: `جسم المبنى (Building Mass)`,
            goal: `رسم شكل المبنى العام: خط الأرض والبلنث والحوائط والبلاطة والسور.`,
            steps: [
              `ارسم خط الأرض بطول يزيد على عرض المبنى، وانقل عرض المبنى (7.45 م = 14.9 سم) من المسقط.`,
              `ارفع الارتفاعات من القطاع: البلنث حتى ±0.00، الحوائط حتى +3.00، السور حتى +4.00.`,
              `ارسم حد البلاطة وغطاء السور.`
            ],
            golden: `الواجهة بلا تهشير للقطع، فهي منظر خارجي لا قطع فيه.`,
            mistake: `تغيير عرض المبنى عن المسقط أو تغيير ارتفاعاته عن القطاع.`,
            tip: `استخدم خطوط الإسقاط خفيفة بقلم 2H من المسقط والقطاع ثم امسحها.`,
            checkpoint: `هل عرض المبنى وارتفاعاته مطابقان للمسقط والقطاع؟`
          },
          {
            title: `الأبواب والشبابيك (Openings)`,
            goal: `تحديد مواضع الفتحات وأبعادها بدقة على الواجهة.`,
            steps: [
              `أسقط مواضع الفتحات رأسيًا من المسقط (من المحاور والأبعاد).`,
              `ارفع الجلسة والرأس أفقيًا من القطاع: جلسة 1.00 م ورأس 2.20 م (وفي الحمام الجلسة 1.50 م).`,
              `ارسم باب المدخل 1.00 × 2.20 م مع درجتي الصعود.`
            ],
            golden: `كل فتحة في الواجهة يقابلها فتحة في المسقط بنفس العرض وفي القطاع بنفس الارتفاع.`,
            mistake: `رسم شباك في الواجهة غير موجود في المسقط أو بارتفاع عتب مختلف.`,
            tip: `ضع علامة (✓) على المسقط عند نقل كل فتحة حتى لا تنسى شيئًا.`,
            checkpoint: `هل عدد الفتحات وأبعادها تطابق المسقط تمامًا؟`
          },
          {
            title: `الخامات والتفاصيل المرئية (Materials & Details)`,
            goal: `تمثيل الخامات (زجاج، خشب، حجر) والأشجار والإنسان لإضفاء الواقعية والمقياس.`,
            steps: [
              `ارسم القواطع والمفصلات في الشبابيك وضلف الأبواب بخطوط خفيفة.`,
              `ارسم رموز الخامات بالتظليل الخفيف أو بخطوط التقسيم (حجر البلنث السفلي).`,
              `أضف إنسانًا وشجرة لتوضيح المقياس البصري للواجهة.`
            ],
            golden: `الخطوط المتدرجة: خط الأرض الأسمك، ثم محيط المبنى، ثم الفتحات، ثم الخامات.`,
            mistake: `الإفراط في تظليل الواجهة حتى تضيع الخطوط المعمارية الرئيسية.`,
            tip: `أضف ظلًا خفيفًا تحت غطاء السور والجلسات ليعطي عمقًا بلا تعقيد.`,
            checkpoint: `هل تبدو الواجهة مفهومة بالخطوط وحدها حتى لو أزلنا تفاصيل التظليل؟`
          },
          {
            title: `المناسيب والمحاور والبيانات (Levels & Notes)`,
            goal: `إكمال اللوحة بالمناسيب والمحاور وعنوان الواجهة.`,
            steps: [
              `ارسم المحاور A و B و C بنفس مواضعها في المسقط.`,
              `ارسم علامات المناسيب: -0.50 و ±0.00 و +3.00 و +4.00.`,
              `اكتب العنوان (الواجهة الجنوبية) والمقياس 1:50 وملاحظات الخامات.`
            ],
            golden: `مناسيب الواجهة هي نفسها مناسيب القطاع.`,
            mistake: `اختلاف منسوب السور أو خط الأرض بين الواجهة والقطاع.`,
            tip: `أطلق على كل واجهة اسم الجهة الجغرافية (جنوبية، شمالية…) كما في سهم الشمال.`,
            checkpoint: `هل تتطابق مناسيب الواجهة مع القطاع A-A بالضبط؟`
          }
        ]
      },
      {
        id: `details`,
        name: `لوحات التفاصيل 1:20`,
        scale: `1:20`,
        subtitle: `قطاع الحائط والسقف والسور + قطاع الحمام`,
        viewBox: `0 0 600 420`,
        stages: [
          {
            title: `تفصيلة الحائط والسور: الحدود والكسر`,
            goal: `رسم حدود الأجزاء المقطوعة بمقياس 1:20 حول الحائط عند البلاطة والسور.`,
            steps: [
              `ارسم الحائط بسمك 25 سم (1.25 سم بمقياس 1:20) ثم البلاطة 15 سم (0.75 سم).`,
              `ارسم سور السطح بارتفاع 1.00 م (5 سم) وسمكه 25 سم، ثم غطاء السور بنتوء 4 سم من كل جانب.`,
              `ارسم خط الكسر عند نهاية الجزء المعروض من البلاطة وأسفل الحائط.`
            ],
            golden: `نكبّر جزءًا فقط من المبنى ونكسر ما بعده بخط كسر (Break Line).`,
            mistake: `رسم القطاع كله بمقياس 1:20 فلا يتسع في الورقة.`,
            tip: `المقياس 1:20 يعني 1 سم على الورق = 20 سم حقيقية، فالمعامل هنا × 5.`,
            checkpoint: `هل تتطابق الأبعاد الرئيسية مع القطاع A-A (25 و 15 و 100 سم)؟`
          },
          {
            title: `تفصيلة الحائط والسور: الطبقات والتهشير والأبعاد`,
            goal: `إظهار طبقات السطح واللياسة والعزل وتنقيط الغطاء بالأبعاد والمناسيب.`,
            steps: [
              `رتّب طبقات السطح من الأسفل: لياسة سقف 2 سم، بلاطة 15 سم، خرسانة ميول، عزل مائي (خط سميك)، بلاط حماية.`,
              `هشّر الطوب والخرسانة المسلحة والرمل والمونة، وارسم مجرى تنقيط الغطاء (Drip) بميل للخارج.`,
              `اكتب أبعاد الطبقات والمناسيب (+3.00 و +4.00) ورمز التفصيلة 1/D-01 بمقياس 1:20.`
            ],
            golden: `رتّب الطبقات بترتيبها الحقيقي في التنفيذ، ولا تحذف العزل المائي أبدًا رغم صغر سمكه.`,
            mistake: `كتابة النص فوق التهشير فيصعب قراءته، أو إهمال رمز التفصيلة المرجعي.`,
            tip: `اترك مساحة بيضاء خلف النص أو اقطع التهشير حوله، واذكر أن الوحدات بالسنتيمتر.`,
            checkpoint: `هل كل طبقة لها سمك ومادة واضحان بحيث ينفذها المقاول دون سؤال إضافي؟`
          },
          {
            title: `قطاع الحمام: البلاطة المنخفضة والعزل (1:20)`,
            goal: `تخفيض بلاطة الحمام 10 سم وإظهار العزل المائي المرتد على الحائط وميل 1%.`,
            steps: [
              `ارسم الحائط 25 سم واخفض سطح بلاطة الحمام 10 سم عن بلاطة الغرف المجاورة.`,
              `ارسم العزل المائي بخط سميك فوق البلاطة ويرتد على الحائط 30 سم على الأقل.`,
              `ارسم خرسانة الميول بميل 1% نحو البالوعة (Floor Drain) مع البلاط 2 سم.`
            ],
            golden: `الحمام أخفض من الغرف ليحبس الماء، والعزل يرتد على الحائط ولا يتوقف عند الأرض.`,
            mistake: `رسم بلاطة الحمام بنفس منسوب بلاطة الغرف أو نسيان ميل الأرضية فتتجمع المياه.`,
            tip: `اكتب «ميل 1%» وارسم سهمًا صغيرًا يشير نحو البالوعة.`,
            checkpoint: `هل بلاطة الحمام أخفض بوضوح والعزل مرسوم متصلًا من الأرض إلى الحائط؟`
          },
          {
            title: `قطاع الحمام: العتبة والتبليط والتجهيزات`,
            goal: `إظهار عتبة الباب الرخام وتبليط الحوائط حتى +2.10 م والتجهيزات بخط رفيع.`,
            steps: [
              `ارسم بلاط الحائط حتى ارتفاع 2.10 م، وعتبة رخام عند الباب ترتفع 10 سم لحجز الماء.`,
              `ارسم الدش بارتفاع 2.00 م والخلاط 1.10 م والحوض 0.85 م بخط رفيع لأنها لا تُقطع.`,
              `اكتب المناسيب (-0.10 و ±0.00 و +2.10) وهشّر الطوب والخرسانة والرخام.`
            ],
            golden: `عتبة الباب تفصل الحمام وتمنع خروج الماء، وما لم يُقطع يُرسم بخط أرفع ولا يُهشّر.`,
            mistake: `نسيان العتبة أو رسم التجهيزات بخط سميك فتطغى على الحوائط المقطوعة.`,
            tip: `ارسم إنسانًا بارتفاع 1.70 م بجوار الدش والحوض للمقارنة البصرية.`,
            checkpoint: `هل ارتفاعات الدش والحوض والخلاط مطابقة للأبعاد المكتوبة؟`
          }
        ]
      },
      {
        id: `tagging`,
        name: `الترميز والربط بالجداول`,
        scale: `1:50`,
        subtitle: `رموز الأبواب (D) والشبابيك (W) وأرقام الغرف (1–5)`,
        viewBox: `0 0 600 440`,
        stages: [
          {
            title: `ترميز الفتحات والغرف (Tagging)`,
            goal: `إعطاء كل نوع من الأبواب والشبابيك رمزًا، وكل غرفة رقمًا، ليتصل المسقط بالجداول.`,
            steps: [
              `أعطِ كل نوع فتحة رمزًا: الأبواب D1 و D2 و D3 و D4، والشبابيك W1 و W2 و W3 و W4 (النوع المتكرر يأخذ الرمز نفسه).`,
              `ضع رمز الباب داخل دائرة ورمز الشباك داخل مسدس بجوار الفتحة دون أن يغطي خطوطها.`,
              `اكتب رقم كل غرفة داخل دائرة صغيرة تحت اسمها من 1 إلى 5 لربطه بجدول التشطيبات.`
            ],
            golden: `الرمز الواحد يعني مواصفات واحدة: إن اختلف المقاس أو الخامة فهذا رمز جديد.`,
            mistake: `إعطاء رمز مختلف لعناصر متطابقة، أو رمز واحد لعناصر مختلفة المقاس.`,
            tip: `اكتب الرموز بحجم متساوٍ وفي مكان ثابت بالنسبة للفتحة ليسهل البحث عنها.`,
            checkpoint: `هل لكل فتحة رمز؟ وهل مجموع الأعداد يطابق الجدول (5 أبواب و 8 شبابيك)؟`
          }
        ]
      }
    ];

    const DOOR_WINDOW_SCHEDULE = [
      { code: `D1`, type: `باب المدخل`, size: `1.00 × 2.20`, sill: `—`, count: 1, mat: `خشب مصمت`, swing: `للداخل` },
      { code: `D2`, type: `باب غرفة النوم`, size: `0.90 × 2.20`, sill: `—`, count: 2, mat: `خشب`, swing: `للداخل` },
      { code: `D3`, type: `باب المطبخ`, size: `0.80 × 2.20`, sill: `—`, count: 1, mat: `خشب`, swing: `للمعيشة` },
      { code: `D4`, type: `باب الحمام`, size: `0.80 × 2.20`, sill: `—`, count: 1, mat: `PVC (بشيش)`, swing: `للحمام` },
      { code: `W1`, type: `شباك غرف النوم والمعيشة والمدخل`, size: `1.20 × 1.20`, sill: `1.00`, count: 4, mat: `ألومنيوم + زجاج`, swing: `ضلفتان مفصليتان` },
      { code: `W2`, type: `شباك المعيشة (الجنوب)`, size: `1.10 × 1.20`, sill: `1.00`, count: 1, mat: `ألومنيوم + زجاج`, swing: `منزلق` },
      { code: `W3`, type: `شباك المطبخ`, size: `0.90 × 1.20`, sill: `1.00`, count: 1, mat: `ألومنيوم + زجاج`, swing: `ضلفة مفصلية` },
      { code: `W4`, type: `شباك الحمام`, size: `0.70 × 0.70`, sill: `1.50`, count: 1, mat: `ألومنيوم + زجاج`, swing: `علوي` }
    ];

    const FINISH_SCHEDULE = [
      { num: `1`, space: `غرفة نوم 1`, floor: `باركيه`, skirt: `خشب 10 سم`, walls: `بياض ودهان`, ceil: `بياض ودهان`, notes: `—` },
      { num: `2`, space: `غرفة نوم 2`, floor: `باركيه`, skirt: `خشب 10 سم`, walls: `بياض ودهان`, ceil: `بياض ودهان`, notes: `—` },
      { num: `3`, space: `المعيشة والسفرة`, floor: `باركيه`, skirt: `خشب 10 سم`, walls: `بياض ودهان`, ceil: `بياض ودهان`, notes: `—` },
      { num: `4`, space: `مطبخ`, floor: `سيراميك`, skirt: `سيراميك 10 سم`, walls: `سيراميك حتى 1.50 م ثم دهان`, ceil: `بياض ودهان`, notes: `رخامة فوق الكابينة` },
      { num: `5`, space: `حمام`, floor: `سيراميك مانع للانزلاق`, skirt: `—`, walls: `سيراميك حتى 2.10 م ثم دهان`, ceil: `بياض مقاوم للرطوبة`, notes: `ميل 1% نحو البالوعة` }
    ];

    const LINE_TYPES = [
      { name: `خط الحوائط المقطوعة (Cut Line)`, weight: `0.70 مم`, dash: ``, widthPx: 4.5, color: `var(--on-surface)`, desc: `إبراز الحوائط والأعمدة التي يقطعها مستوى القطع والأجزاء المقطوعة.` },
      { name: `خط الأرض (Ground Line)`, weight: `0.70 مم`, dash: ``, widthPx: 4.5, color: `var(--warning)`, desc: `تمثيل مستوى سطح الأرض الطبيعية تحت الواجهات والقطاعات.` },
      { name: `خط مستوى القطع (Section Line)`, weight: `0.50 / 0.25 مم`, dash: `18 6 3 6`, widthPx: 3.0, color: `var(--primary)`, desc: `تحديد موضع القطاع A-A وتشير الأسهم إلى اتجاه النظر.` },
      { name: `خط الحواف المرئية (Visible Line)`, weight: `0.35 مم`, dash: ``, widthPx: 2.2, color: `var(--on-surface-variant)`, desc: `الحواف غير المقطوعة: الأبواب، الشبابيك، الأثاث والتجهيزات.` },
      { name: `الخط المخفي (Hidden Line)`, weight: `0.25 مم`, dash: `7 5`, widthPx: 1.6, color: `var(--on-surface-variant)`, desc: `العناصر المختفية أو الدرجات الواقعة فوق مستوى القطع.` },
      { name: `خط الإسقاط العلوي (Overhead)`, weight: `0.25 مم`, dash: `14 4 2 4 2 4`, widthPx: 1.6, color: `var(--tertiary)`, desc: `العناصر الواقعة فوق مستوى القطع كالكمرات والبلكونات البارزة.` },
      { name: `المحاور الإنشائية (Axis / Centre)`, weight: `0.18 مم`, dash: `16 4 2 4`, widthPx: 1.2, color: `var(--primary)`, desc: `تحديد مراكز الأعمدة والحوائط وتنتهي بدوائر مرقمة A-B-C و 1-2-3.` },
      { name: `خطوط الأبعاد والتهشير`, weight: `0.13 مم`, dash: ``, widthPx: 0.9, color: `var(--secondary)`, desc: `خطوط الامتداد والأبعاد بعلامة مائلة 45°، وتهشير المواد بزاوية 45°.` }
    ];

    const FINAL_CHECKLIST = [
      `عام: إطار اللوحة وعنوانها (Title Block) ورقمها والمقياس والتاريخ`,
      `الخطوط: السمك مناسب للنوع، والمحاور شرطة-نقطة، والمخفي مختلف عن العلوي`,
      `المسقط: قطع عند منتصف الدور، حوائط متصلة، فتحات عليها رموزها وأبعادها`,
      `القطاع: تهشير كل مقطوع، لا أساسات، مناسيب رأسية، عتب فوق الفتحات`,
      `الواجهة: خط أرض سميك، ارتفاعات متطابقة مع القطاع، بلا تهشير للأسطح المرئية`,
      `التفاصيل: مقياس 1:20، ترتيب طبقات صحيح مع العزل المائي ورمز مرجعي`,
      `الجداول: كل رمز في المسقط موجود في الجدول والأعداد مطابقة (5 أبواب / 8 شبابيك)`,
      `الربط: تطابق الأبعاد والمناسيب بين المسقط والقطاع والواجهة`
    ];

    const GLOSSARY = [
      { ar: `الرسم المعماري`, en: `Architectural Drawing` },
      { ar: `المسقط الأفقي`, en: `Floor Plan` },
      { ar: `القطاع المعماري`, en: `Section` },
      { ar: `الواجهة`, en: `Elevation` },
      { ar: `الموقع العام`, en: `Site Plan` },
      { ar: `مسقط السطح`, en: `Roof Plan` },
      { ar: `لوحة التفاصيل`, en: `Detail Drawing` },
      { ar: `مقياس الرسم`, en: `Scale` },
      { ar: `المحور الإنشائي`, en: `Axis / Centre Line` },
      { ar: `التهشير`, en: `Hatching` },
      { ar: `الخط المخفي`, en: `Hidden Line` },
      { ar: `خط الكسر`, en: `Break Line` },
      { ar: `خط الأرض`, en: `Ground Line` },
      { ar: `المنسوب`, en: `Level` },
      { ar: `العتب الخرساني`, en: `Lintel` },
      { ar: `جلسة الشباك`, en: `Sill` },
      { ar: `سور السطح / الدروة`, en: `Parapet` },
      { ar: `غطاء السور`, en: `Coping` },
      { ar: `النائمة (عرض الدرجة)`, en: `Going` },
      { ar: `القائمة (ارتفاع الدرجة)`, en: `Rise` },
      { ar: `الوزرة`, en: `Skirting` },
      { ar: `جدول الأبواب والشبابيك`, en: `Door & Window Schedule` },
      { ar: `جدول التشطيبات`, en: `Finish Schedule` },
      { ar: `نقطة التوقيع`, en: `Start Point` }
    ];

    // =========================================================================
    // 2. APPLICATION STATE & PERSISTENCE
    // =========================================================================
    let appState = {
      activeModuleId: `floorplan`,
      activeStageIndex: 0,
      renderMode: `buildup`, // 'buildup' | 'final'
      checkedSteps: {},      // { "floorplan-0-0": true, ... }
      verifiedStages: {},    // { "floorplan-0": true, ... }
      finalChecklist: {},    // { "0": true, ... }
      selectedScheduleTag: ``
    };

    const TOTAL_STAGES_COUNT = MODULES.reduce((acc, m) => acc + m.stages.length, 0);

    async function persistState() {
      if (window.notebookAppApi && typeof window.notebookAppApi.setAppState === `function`) {
        try {
          await window.notebookAppApi.setAppState(appState);
        } catch (e) {
          // Graceful fallback if host rejects
        }
      }
    }

    // =========================================================================
    // 3. ARCHITECTURAL SVG GENERATORS (Previous = Gray, Current = Turquoise)
    // =========================================================================
    function wrapLayer(content, layerIdx, currentStageIdx) {
      if (layerIdx > currentStageIdx) return ``;
      const cls = layerIdx === currentStageIdx ? `layer-curr` : `layer-prev`;
      return `<g class="${cls}">${content}</g>`;
    }

    function buildFloorPlanSVG(stageIdx, showTagsStage = false) {
      const effectiveIdx = showTagsStage ? 6 : stageIdx;
      // Coordinates: Building outer bounds X: 110..490 (380px ≈ 7.45m), Y: 80..360 (280px ≈ 7.05m)
      // Axes: A=118, B=300, C=482 | 1=88, 2=210, 3=352
      const L0 = `
        <line x1="118" y1="45" x2="118" y2="395" class="st-axis" />
        <line x1="300" y1="45" x2="300" y2="395" class="st-axis" />
        <line x1="482" y1="45" x2="482" y2="395" class="st-axis" />
        <line x1="75" y1="88" x2="525" y2="88" class="st-axis" />
        <line x1="75" y1="210" x2="525" y2="210" class="st-axis" />
        <line x1="75" y1="352" x2="525" y2="352" class="st-axis" />
        <circle cx="118" cy="34" r="11" class="st-vis" /><text x="118" y="34" class="st-txt">A</text>
        <circle cx="300" cy="34" r="11" class="st-vis" /><text x="300" y="34" class="st-txt">B</text>
        <circle cx="482" cy="34" r="11" class="st-vis" /><text x="482" y="34" class="st-txt">C</text>
        <circle cx="62" cy="88" r="11" class="st-vis" /><text x="62" y="88" class="st-txt">1</text>
        <circle cx="62" cy="210" r="11" class="st-vis" /><text x="62" y="210" class="st-txt">2</text>
        <circle cx="62" cy="352" r="11" class="st-vis" /><text x="62" y="352" class="st-txt">3</text>
      `;

      // Stage 1 (index 1): Walls (outer 25cm -> 12px visual, inner 12cm -> 6px visual)
      // Before Stage 2 (openings), walls are continuous; from Stage 2 onward, walls have openings carved cleanly.
      const wallsContinuous = `
        <rect x="112" y="82" width="376" height="276" class="st-vis" />
        <rect x="124" y="94" width="352" height="252" class="st-vis" />
        <line x1="297" y1="94" x2="297" y2="346" class="st-vis" />
        <line x1="303" y1="94" x2="303" y2="346" class="st-vis" />
        <line x1="124" y1="207" x2="476" y2="207" class="st-vis" />
        <line x1="124" y1="213" x2="476" y2="213" class="st-vis" />
        <line x1="220" y1="94" x2="220" y2="207" class="st-vis" />
        <line x1="226" y1="94" x2="226" y2="207" class="st-vis" />
      `;

      // Segmented wall outlines with openings carved:
      // Top wall: W1 left (175..210), W4 bath (245..275), W1 right (365..425)
      // Bottom wall: Door D1 entrance (250..290), W2 living (365..420)
      // Left wall: W1 bedroom2 (130..175), W1 bedroom1 (255..305)
      // Right wall: W3 kitchen (125..165), W1 living (260..305)
      const wallPolygons = [
        // Top-left segment to W1
        `M 112 82 H 175 V 94 H 124 V 130 H 112 Z`,
        // Top segment between W1 and W4
        `M 210 82 H 245 V 94 H 210 Z`,
        // Top segment between W4 and right W1
        `M 275 82 H 365 V 94 H 275 Z`,
        // Top-right corner down to W3
        `M 425 82 H 488 V 125 H 476 V 94 H 425 Z`,
        // Right middle between W3 and W1
        `M 476 165 H 488 V 260 H 476 Z`,
        // Right-bottom corner
        `M 476 305 H 488 V 358 H 420 V 346 H 476 Z`,
        // Bottom middle between D1 and W2
        `M 290 346 H 365 V 358 H 290 Z`,
        // Bottom-left corner up to left W1
        `M 112 305 H 124 V 346 H 250 V 358 H 112 Z`,
        // Left middle between W1s
        `M 112 175 H 124 V 255 H 112 Z`,
        // Inner vertical wall B (with door D2 top-left and D3 kitchen)
        `M 297 94 H 303 V 150 H 297 Z`,
        `M 297 190 H 303 V 255 H 297 Z`,
        `M 297 295 H 303 V 346 H 297 Z`,
        // Inner horizontal wall 2 (with D2 bedroom2 and D4 bath)
        `M 124 207 H 165 V 213 H 124 Z`,
        `M 205 207 H 240 V 213 H 205 Z`,
        `M 275 207 H 297 V 213 H 275 Z`,
        `M 303 207 H 476 V 213 H 303 Z`,
        // Partition between Bedroom 2 & Bath
        `M 220 94 H 226 V 207 H 220 Z`
      ];

      const wallsCarved = wallPolygons.map(d => `<path d="${d}" class="st-vis" />`).join(``);
      const wallsPoche = wallPolygons.map(d => `<path d="${d}" class="st-fill-poche" />`).join(``);

      // Stage 2 (index 2): Windows (3 parallel lines) & Doors (leaf + 90deg arc)
      const openingsContent = `
        <!-- Windows Top: W1, W4, W1 -->
        <g>
          <rect x="175" y="84" width="35" height="8" class="st-vis" /><line x1="175" y1="88" x2="210" y2="88" class="st-thin" />
          <rect x="245" y="84" width="30" height="8" class="st-vis" /><line x1="245" y1="88" x2="275" y2="88" class="st-thin" />
          <rect x="365" y="84" width="60" height="8" class="st-vis" /><line x1="365" y1="88" x2="425" y2="88" class="st-thin" />
        </g>
        <!-- Windows Left: W1, W1 -->
        <g>
          <rect x="114" y="130" width="8" height="45" class="st-vis" /><line x1="118" y1="130" x2="118" y2="175" class="st-thin" />
          <rect x="114" y="255" width="8" height="50" class="st-vis" /><line x1="118" y1="255" x2="118" y2="305" class="st-thin" />
        </g>
        <!-- Windows Right: W3, W1 -->
        <g>
          <rect x="478" y="125" width="8" height="40" class="st-vis" /><line x1="482" y1="125" x2="482" y2="165" class="st-thin" />
          <rect x="478" y="260" width="8" height="45" class="st-vis" /><line x1="482" y1="260" x2="482" y2="305" class="st-thin" />
        </g>
        <!-- Window Bottom: W2 -->
        <g>
          <rect x="365" y="348" width="55" height="8" class="st-vis" /><line x1="365" y1="352" x2="420" y2="352" class="st-thin" />
        </g>
        <!-- Doors: D1 Entrance (bottom 250..290) -->
        <line x1="250" y1="346" x2="250" y2="306" class="st-cut" />
        <path d="M 250 306 A 40 40 0 0 1 290 346" class="st-thin" />
        <!-- D2 Bedroom 1 (on B 255..295) -->
        <line x1="297" y1="255" x2="257" y2="255" class="st-cut" />
        <path d="M 257 255 A 40 40 0 0 0 297 295" class="st-thin" />
        <!-- D2 Bedroom 2 (on wall2 165..205) -->
        <line x1="165" y1="207" x2="165" y2="167" class="st-cut" />
        <path d="M 165 167 A 40 40 0 0 1 205 207" class="st-thin" />
        <!-- D4 Bath (on wall2 240..275) -->
        <line x1="240" y1="207" x2="240" y2="172" class="st-cut" />
        <path d="M 240 172 A 35 35 0 0 1 275 207" class="st-thin" />
        <!-- D3 Kitchen (on B 150..190) -->
        <line x1="303" y1="190" x2="343" y2="190" class="st-cut" />
        <path d="M 343 190 A 40 40 0 0 0 303 150" class="st-thin" />
        <!-- Entrance steps -->
        <rect x="242" y="358" width="56" height="12" class="st-vis" />
        <line x1="242" y1="364" x2="298" y2="364" class="st-thin" />
      `;

      // Stage 4 (index 4): Furniture & Fixtures
      const furnitureContent = `
        <!-- Bedroom 2 (top left) -->
        <rect x="132" y="102" width="66" height="48" rx="2" class="st-thin" />
        <rect x="136" y="106" width="22" height="14" rx="2" class="st-thin" />
        <rect x="164" y="106" width="22" height="14" rx="2" class="st-thin" />
        <!-- Bath (top middle) -->
        <rect x="230" y="98" width="62" height="24" rx="4" class="st-thin" />
        <ellipse cx="282" cy="148" rx="8" ry="11" class="st-thin" />
        <rect x="232" y="136" width="16" height="22" rx="2" class="st-thin" />
        <!-- Kitchen (top right) -->
        <path d="M 390 94 H 476 V 180 H 448 V 118 H 390 Z" class="st-thin" />
        <rect x="404" y="98" width="24" height="16" class="st-thin" />
        <circle cx="462" cy="138" r="5" class="st-thin" /><circle cx="462" cy="154" r="5" class="st-thin" />
        <rect x="330" y="98" width="32" height="28" class="st-thin" />
        <!-- Bedroom 1 (bottom left) -->
        <rect x="132" y="226" width="76" height="58" rx="2" class="st-thin" />
        <rect x="138" y="232" width="24" height="16" rx="2" class="st-thin" />
        <rect x="168" y="232" width="24" height="16" rx="2" class="st-thin" />
        <!-- Living & Dining (bottom right) -->
        <rect x="395" y="230" width="68" height="26" rx="3" class="st-thin" />
        <rect x="444" y="264" width="26" height="52" rx="3" class="st-thin" />
        <rect x="345" y="275" width="60" height="40" rx="2" class="st-thin" />
        <circle cx="358" cy="268" r="5" class="st-thin" /><circle cx="390" cy="268" r="5" class="st-thin" />
        <circle cx="358" cy="322" r="5" class="st-thin" /><circle cx="390" cy="322" r="5" class="st-thin" />
      `;

      // Stage 5 (index 5): 3 Dimension Lines + Room Names + Section Line A-A + North
      const dimsAndTextContent = `
        <!-- 3 Bottom Dimension lines -->
        <line x1="112" y1="376" x2="488" y2="376" class="st-dim" />
        <line x1="112" y1="396" x2="488" y2="396" class="st-dim" />
        <line x1="112" y1="416" x2="488" y2="416" class="st-dim" />
        <text x="180" y="370" class="st-txt">2.75</text><text x="270" y="370" class="st-txt">1.00</text><text x="392" y="370" class="st-txt">1.10</text>
        <text x="209" y="390" class="st-txt">3.60</text><text x="391" y="390" class="st-txt">3.60</text>
        <text x="300" y="410" class="st-txt">7.45 م</text>
        <!-- Right overall dim -->
        <line x1="518" y1="82" x2="518" y2="358" class="st-dim" />
        <text x="536" y="220" class="st-txt">7.05 م</text>
        <!-- Section cut A-A -->
        <line x1="86" y1="150" x2="514" y2="150" class="st-axis" />
        <polygon points="86,150 96,140 96,160" class="st-fill-solid" />
        <polygon points="514,150 504,140 504,160" class="st-fill-solid" />
        <text x="86" y="132" class="st-txt">A</text><text x="514" y="132" class="st-txt">A</text>
        <!-- North Arrow -->
        <g transform="translate(555,58)">
          <circle cx="0" cy="0" r="16" class="st-vis" />
          <polygon points="0,-13 -5,6 0,2 5,6" class="st-fill-solid" />
          <text x="0" y="-22" class="st-txt">N</text>
        </g>
        <!-- Room labels -->
        <text x="172" y="176" class="st-txt-ar st-txt">غرفة نوم 2</text>
        <text x="260" y="182" class="st-txt-ar st-txt">حمام</text>
        <text x="385" y="160" class="st-txt-ar st-txt">مطبخ</text>
        <text x="195" y="316" class="st-txt-ar st-txt">غرفة نوم 1</text>
        <text x="385" y="254" class="st-txt-ar st-txt">المعيشة والسفرة</text>
      `;

      // Stage 6 (only for Tagging module): Door circles, Window hexagons, Room numbers
      const tagsContent = `
        <!-- Room Number Circles -->
        <circle cx="195" cy="332" r="9" class="st-vis" /><text x="195" y="332" class="st-txt">1</text>
        <circle cx="172" cy="192" r="9" class="st-vis" /><text x="172" y="192" class="st-txt">2</text>
        <circle cx="385" cy="272" r="9" class="st-vis" /><text x="385" y="272" class="st-txt">3</text>
        <circle cx="385" cy="178" r="9" class="st-vis" /><text x="385" y="178" class="st-txt">4</text>
        <circle cx="260" cy="196" r="9" class="st-vis" /><text x="260" y="196" class="st-txt">5</text>
        <!-- Door Tags (circles) -->
        <circle cx="272" cy="326" r="10" class="st-cut" /><text x="272" y="326" class="st-txt">D1</text>
        <circle cx="277" cy="275" r="10" class="st-cut" /><text x="277" y="275" class="st-txt">D2</text>
        <circle cx="185" cy="190" r="10" class="st-cut" /><text x="185" y="190" class="st-txt">D2</text>
        <circle cx="323" cy="170" r="10" class="st-cut" /><text x="323" y="170" class="st-txt">D3</text>
        <circle cx="258" cy="188" r="10" class="st-cut" /><text x="258" y="188" class="st-txt">D4</text>
        <!-- Window Tags (hexagons) -->
        <polygon points="192,62 204,68 204,78 192,84 180,78 180,68" class="st-cut" /><text x="192" y="73" class="st-txt">W1</text>
        <polygon points="260,62 272,68 272,78 260,84 248,78 248,68" class="st-cut" /><text x="260" y="73" class="st-txt">W4</text>
        <polygon points="395,62 407,68 407,78 395,84 383,78 383,68" class="st-cut" /><text x="395" y="73" class="st-txt">W1</text>
        <polygon points="94,142 106,148 106,158 94,164 82,158 82,148" class="st-cut" /><text x="94" y="153" class="st-txt">W1</text>
        <polygon points="94,270 106,276 106,286 94,292 82,286 82,276" class="st-cut" /><text x="94" y="281" class="st-txt">W1</text>
        <polygon points="506,135 518,141 518,151 506,157 494,151 494,141" class="st-cut" /><text x="506" y="146" class="st-txt">W3</text>
        <polygon points="392,360 404,366 404,376 392,382 380,376 380,366" class="st-cut" /><text x="392" y="371" class="st-txt">W2</text>
      `;

      let svg = ``;
      svg += wrapLayer(L0, 0, effectiveIdx);
      if (effectiveIdx === 1) {
        svg += wrapLayer(wallsContinuous, 1, effectiveIdx);
      } else if (effectiveIdx >= 2) {
        // Show walls as previous in gray if stage >= 2 and < 3, or Poche at stage 3+
        if (effectiveIdx === 2) {
          svg += wrapLayer(wallsCarved, 1, effectiveIdx);
        } else {
          svg += wrapLayer(wallsCarved, 1, effectiveIdx);
          svg += wrapLayer(wallsPoche, 3, effectiveIdx);
        }
        svg += wrapLayer(openingsContent, 2, effectiveIdx);
      }
      svg += wrapLayer(furnitureContent, 4, effectiveIdx);
      svg += wrapLayer(dimsAndTextContent, 5, effectiveIdx);
      if (showTagsStage) {
        svg += wrapLayer(tagsContent, 6, 6);
      }
      return svg;
    }

    function buildStairSVG(stageIdx) {
      // Stages 0..4: Stair Plan; Stage 5: Step Detail 1:5
      if (stageIdx === 5) {
        // Step Detail 1:5 — 3 concrete steps + 15cm inclined slab + 2cm marble + nosing + hatching + 2R+G
        return `
          <g class="layer-prev">
            <path d="M 110 310 V 250 H 215 V 190 H 320 V 130 H 425" class="st-cut" />
            <line x1="95" y1="340" x2="425" y2="175" class="st-cut" />
            <line x1="110" y1="310" x2="95" y2="340" class="st-break" />
            <line x1="425" y1="130" x2="425" y2="175" class="st-break" />
          </g>
          <g class="layer-curr">
            <!-- Marble treads (with 2cm nosing) & risers + mortar -->
            <path d="M 102 240 H 207 V 250 H 110 V 300 H 102 Z" class="st-vis" />
            <path d="M 207 180 H 312 V 190 H 215 V 240 H 207 Z" class="st-vis" />
            <path d="M 312 120 H 425 V 130 H 320 V 180 H 312 Z" class="st-vis" />
            <!-- Plaster below slab -->
            <line x1="98" y1="348" x2="428" y2="183" class="st-thin" />
            <!-- Concrete aggregate hatch -->
            <circle cx="170" cy="285" r="2" class="st-hatch" /><circle cx="235" cy="240" r="2.5" class="st-hatch" />
            <circle cx="290" cy="215" r="2" class="st-hatch" /><circle cx="355" cy="175" r="2.5" class="st-hatch" />
            <path d="M 140 295 L 146 289 L 150 297 Z M 265 225 L 271 219 L 275 227 Z M 370 165 L 376 159 L 380 167 Z" class="st-hatch" />
            <!-- Dimensions -->
            <line x1="207" y1="95" x2="312" y2="95" class="st-dim" />
            <text x="260" y="83" class="st-txt">G = 28 سم</text>
            <line x1="450" y1="120" x2="450" y2="180" class="st-dim" />
            <text x="488" y="150" class="st-txt">R = 16.7 سم</text>
            <line x1="250" y1="245" x2="268" y2="278" class="st-dim" />
            <text x="296" y="275" class="st-txt">بلاطة 15 سم</text>
            <text x="295" y="365" class="st-txt-ar st-txt">تفصيلة الدرجة (1:5) — 2R + G = 61.4 سم</text>
          </g>
        `;
      }

      // Stair Plan (0..4)
      const L0 = `
        <line x1="120" y1="120" x2="480" y2="120" class="st-axis" />
        <line x1="120" y1="300" x2="480" y2="300" class="st-axis" />
        <circle cx="102" cy="120" r="11" class="st-vis" /><text x="102" y="120" class="st-txt">1</text>
        <circle cx="102" cy="300" r="11" class="st-vis" /><text x="102" y="300" class="st-txt">2</text>
        <path d="M 150 105 H 445 V 315 H 150" class="st-cut" />
        <path d="M 150 125 H 425 V 295 H 150" class="st-cut" />
        <line x1="150" y1="105" x2="150" y2="125" class="st-cut" />
        <line x1="150" y1="295" x2="150" y2="315" class="st-cut" />
        <text x="132" y="255" class="st-txt">±0.00</text>
      `;

      let flight1 = ``;
      for (let i = 0; i < 8; i++) {
        const x = 165 + i * 24;
        flight1 += `<line x1="${x}" y1="220" x2="${x}" y2="295" class="st-vis" />`;
      }
      flight1 += `<line x1="165" y1="220" x2="333" y2="220" class="st-vis" />`;

      let flight2 = `
        <line x1="333" y1="125" x2="333" y2="295" class="st-vis" />
        <line x1="165" y1="200" x2="333" y2="200" class="st-vis" />
      `;
      for (let i = 0; i < 8; i++) {
        const x = 165 + i * 24;
        flight2 += `<line x1="${x}" y1="125" x2="${x}" y2="200" class="st-vis st-hidden" />`;
      }
      // Diagonal break line
      flight2 += `<path d="M 272 302 L 296 208" class="st-break" />`;

      const arrowAndNums = `
        <circle cx="177" cy="258" r="4" class="st-fill-solid" />
        <path d="M 177 258 H 382 V 162 H 165" class="st-vis" />
        <polygon points="165,162 177,156 177,168" class="st-fill-solid" />
        <text x="230" y="246" class="st-txt">UP</text>
        <text x="177" y="282" class="st-txt">1</text>
        <text x="201" y="282" class="st-txt">2</text>
        <text x="225" y="282" class="st-txt">3</text>
        <text x="249" y="282" class="st-txt">4</text>
        <text x="273" y="282" class="st-txt">5</text>
      `;

      const dimsAndTags = `
        <line x1="165" y1="340" x2="333" y2="340" class="st-dim" />
        <line x1="333" y1="340" x2="445" y2="340" class="st-dim" />
        <line x1="150" y1="365" x2="445" y2="365" class="st-dim" />
        <text x="249" y="330" class="st-txt">224 سم</text>
        <text x="389" y="330" class="st-txt">136 سم</text>
        <text x="297" y="356" class="st-txt">360 سم</text>
        <line x1="472" y1="105" x2="472" y2="315" class="st-dim" />
        <text x="506" y="210" class="st-txt">290 سم</text>
        <text x="386" y="210" class="st-txt">+1.50</text>
        <circle cx="515" cy="70" r="18" class="st-cut" />
        <text x="515" y="64" class="st-txt">ST-1</text>
        <text x="515" y="77" class="st-txt">D-05</text>
      `;

      let svg = ``;
      svg += wrapLayer(L0, 0, stageIdx);
      svg += wrapLayer(flight1, 1, stageIdx);
      svg += wrapLayer(flight2, 2, stageIdx);
      svg += wrapLayer(arrowAndNums, 3, stageIdx);
      svg += wrapLayer(dimsAndTags, 4, stageIdx);
      return svg;
    }

    function buildSectionSVG(stageIdx) {
      // Ground Y=335, ±0.00 Y=305, +3.00 Y=140, +4.00 Y=85
      // Left Wall X: 112..126, Mid Wall X: 297..304, Right Wall X: 474..488
      const L0 = `
        <line x1="45" y1="335" x2="555" y2="335" class="st-vis st-ground" />
        <line x1="75" y1="305" x2="525" y2="305" class="st-axis" />
        <line x1="75" y1="140" x2="525" y2="140" class="st-axis" />
        <line x1="75" y1="85" x2="525" y2="85" class="st-axis" />
        <line x1="119" y1="45" x2="119" y2="365" class="st-axis" />
        <line x1="300" y1="45" x2="300" y2="365" class="st-axis" />
        <line x1="481" y1="45" x2="481" y2="365" class="st-axis" />
        <circle cx="119" cy="33" r="10" class="st-vis" /><text x="119" y="33" class="st-txt">A</text>
        <circle cx="300" cy="33" r="10" class="st-vis" /><text x="300" y="33" class="st-txt">B</text>
        <circle cx="481" cy="33" r="10" class="st-vis" /><text x="481" y="33" class="st-txt">C</text>
      `;

      const cutElements = `
        <!-- Left & Right Walls with Window gaps (Y: 185..250), Lintels (Y: 175..185) -->
        <rect x="112" y="85" width="14" height="100" class="st-cut" />
        <rect x="112" y="250" width="14" height="85" class="st-cut" />
        <rect x="112" y="175" width="14" height="10" class="st-fill-poche" />
        <rect x="474" y="85" width="14" height="100" class="st-cut" />
        <rect x="474" y="250" width="14" height="85" class="st-cut" />
        <rect x="474" y="175" width="14" height="10" class="st-fill-poche" />
        <!-- Mid wall -->
        <rect x="297" y="140" width="7" height="165" class="st-cut" />
        <!-- Roof slab (Y: 140..152) -->
        <rect x="112" y="140" width="376" height="12" class="st-cut" />
        <!-- Parapet caps -->
        <rect x="108" y="81" width="22" height="4" class="st-cut" />
        <rect x="470" y="81" width="22" height="4" class="st-cut" />
        <!-- Floor slab -->
        <rect x="126" y="305" width="348" height="30" class="st-cut" />
      `;

      const openingsAndLayers = `
        <!-- Window Glass left & right -->
        <rect x="116" y="185" width="6" height="65" class="st-vis" />
        <line x1="119" y1="185" x2="119" y2="250" class="st-thin" />
        <rect x="478" y="185" width="6" height="65" class="st-vis" />
        <line x1="481" y1="185" x2="481" y2="250" class="st-thin" />
        <!-- Roof waterproofing & screed -->
        <line x1="126" y1="136" x2="474" y2="136" class="st-cut" />
        <line x1="126" y1="132" x2="474" y2="132" class="st-thin" />
        <!-- Floor layers -->
        <line x1="126" y1="312" x2="474" y2="312" class="st-thin" />
        <line x1="126" y1="322" x2="474" y2="322" class="st-thin" />
      `;

      const hatching = `
        <!-- Masonry diagonal 45 deg hatch in walls -->
        <path d="M113,100 L125,112 M113,118 L125,130 M113,262 L125,274 M113,280 L125,292 M475,100 L487,112 M475,118 L487,130 M475,262 L487,274 M475,280 L487,292" class="st-hatch" />
        <!-- Earth hatch below ground line -->
        <path d="M60,335 L52,347 M70,335 L62,347 M180,335 L172,347 M190,335 L182,347 M320,335 L312,347 M330,335 L322,347 M440,335 L432,347 M450,335 L442,347 M530,335 L522,347" class="st-hatch" />
        <!-- Slab hatch -->
        <path d="M140,141 L148,151 M180,141 L188,151 M220,141 L228,151 M260,141 L268,151 M340,141 L348,151 M380,141 L388,151 M420,141 L428,151" class="st-hatch" />
      `;

      const beyondCut = `
        <!-- Doors seen behind cut plane (thin lines) -->
        <rect x="165" y="185" width="38" height="120" class="st-vis" />
        <rect x="242" y="185" width="34" height="120" class="st-vis" />
        <!-- Kitchen cabinets & fridge -->
        <rect x="330" y="210" width="32" height="95" class="st-thin" />
        <rect x="395" y="255" width="70" height="50" class="st-thin" />
        <rect x="395" y="175" width="70" height="30" class="st-thin" />
        <!-- Scale human figure 1.70m -->
        <circle cx="218" cy="222" r="7" class="st-thin" />
        <path d="M 218 229 V 272 M 208 242 H 228 M 218 272 L 211 305 M 218 272 L 225 305" class="st-thin" />
      `;

      const dimsAndLevels = `
        <!-- Levels -->
        <polygon points="72,335 64,325 80,325" class="st-vis" /><text x="48" y="330" class="st-txt">-0.50</text>
        <polygon points="72,305 64,295 80,295" class="st-vis" /><text x="48" y="300" class="st-txt">±0.00</text>
        <polygon points="72,140 64,130 80,130" class="st-vis" /><text x="48" y="135" class="st-txt">+3.00</text>
        <polygon points="72,85 64,75 80,75" class="st-vis" /><text x="48" y="80" class="st-txt">+4.00</text>
        <!-- Vertical Dimension Chains -->
        <line x1="518" y1="85" x2="518" y2="335" class="st-dim" />
        <line x1="548" y1="85" x2="548" y2="335" class="st-dim" />
        <text x="532" y="112" class="st-txt">1.00</text>
        <text x="532" y="220" class="st-txt">3.00</text>
        <text x="532" y="320" class="st-txt">0.50</text>
        <text x="568" y="210" class="st-txt">4.50 م</text>
        <text x="300" y="382" class="st-txt-ar st-txt">القطاع المعماري A-A (مقياس 1:50)</text>
      `;

      let svg = ``;
      svg += wrapLayer(L0, 0, stageIdx);
      svg += wrapLayer(cutElements, 1, stageIdx);
      svg += wrapLayer(openingsAndLayers, 2, stageIdx);
      svg += wrapLayer(hatching, 3, stageIdx);
      svg += wrapLayer(beyondCut, 4, stageIdx);
      svg += wrapLayer(dimsAndLevels, 5, stageIdx);
      return svg;
    }

    function buildElevationSVG(stageIdx) {
      // Ground Y=325, ±0.00 Y=295, +3.00 Y=135, +4.00 Y=80
      const L0 = `
        <line x1="40" y1="325" x2="560" y2="325" class="st-vis st-ground" />
        <rect x="112" y="80" width="376" height="245" class="st-cut" />
        <line x1="112" y1="295" x2="488" y2="295" class="st-vis" />
        <line x1="112" y1="135" x2="488" y2="135" class="st-vis" />
        <rect x="108" y="75" width="384" height="5" class="st-cut" />
      `;

      const openings = `
        <!-- Entrance Door D1 (250..290, Y: 175..295) + steps -->
        <rect x="250" y="175" width="40" height="120" class="st-vis" />
        <rect x="242" y="295" width="56" height="15" class="st-vis" />
        <rect x="236" y="310" width="68" height="15" class="st-vis" />
        <!-- Window W1 left & W2 right -->
        <rect x="155" y="175" width="55" height="65" class="st-vis" />
        <rect x="365" y="175" width="55" height="65" class="st-vis" />
      `;

      const materialsAndScale = `
        <!-- Window mullions & Door panels -->
        <line x1="182" y1="175" x2="182" y2="240" class="st-thin" />
        <rect x="160" y="180" width="45" height="55" class="st-thin" />
        <line x1="392" y1="175" x2="392" y2="240" class="st-thin" />
        <rect x="370" y="180" width="45" height="55" class="st-thin" />
        <rect x="256" y="182" width="28" height="45" class="st-thin" />
        <rect x="256" y="234" width="28" height="52" class="st-thin" />
        <!-- Plinth stone pattern -->
        <path d="M135,295 V325 M175,295 V325 M215,295 V325 M335,295 V325 M375,295 V325 M415,295 V325 M455,295 V325" class="st-thin" />
        <!-- Tree & Human Scale -->
        <circle cx="525" cy="215" r="24" class="st-thin" />
        <line x1="525" y1="239" x2="525" y2="325" class="st-vis" />
        <circle cx="80" cy="238" r="7" class="st-thin" />
        <path d="M 80 245 V 290 M 70 260 H 90 M 80 290 L 73 325 M 80 290 L 87 325" class="st-thin" />
      `;

      const levelsAndAxes = `
        <line x1="119" y1="45" x2="119" y2="80" class="st-axis" />
        <line x1="300" y1="45" x2="300" y2="80" class="st-axis" />
        <line x1="481" y1="45" x2="481" y2="80" class="st-axis" />
        <circle cx="119" cy="34" r="10" class="st-vis" /><text x="119" y="34" class="st-txt">A</text>
        <circle cx="300" cy="34" r="10" class="st-vis" /><text x="300" y="34" class="st-txt">B</text>
        <circle cx="481" cy="34" r="10" class="st-vis" /><text x="481" y="34" class="st-txt">C</text>
        <text x="530" y="80" class="st-txt">+4.00</text>
        <text x="530" y="135" class="st-txt">+3.00</text>
        <text x="530" y="295" class="st-txt">±0.00</text>
        <text x="530" y="325" class="st-txt">-0.50</text>
        <text x="300" y="362" class="st-txt-ar st-txt">الواجهة الجنوبية — مبنى التدريب (مقياس 1:50)</text>
      `;

      let svg = ``;
      svg += wrapLayer(L0, 0, stageIdx);
      svg += wrapLayer(openings, 1, stageIdx);
      svg += wrapLayer(materialsAndScale, 2, stageIdx);
      svg += wrapLayer(levelsAndAxes, 3, stageIdx);
      return svg;
    }

    function buildDetailsSVG(stageIdx) {
      // Stages 0..1: Wall-Roof-Parapet Detail (1:20)
      if (stageIdx <= 1) {
        const L0 = `
          <!-- Wall 25cm (220..275) + Parapet up to Y=70 + Slab (275..450, Y:230..265) -->
          <path d="M 220 370 V 70 H 275 V 230 H 455" class="st-cut" />
          <path d="M 275 265 H 455" class="st-cut" />
          <path d="M 220 265 V 370" class="st-cut" />
          <!-- Coping with 4cm overhang -->
          <rect x="208" y="54" width="79" height="16" class="st-cut" />
          <!-- Break lines -->
          <path d="M 210 370 H 285 M 455 215 V 275" class="st-break" />
        `;
        const L1 = `
          <!-- Layers: Plaster 2cm, Screed, Waterproofing (thick), Protection tiles -->
          <line x1="214" y1="70" x2="214" y2="370" class="st-thin" />
          <line x1="281" y1="70" x2="281" y2="210" class="st-thin" />
          <line x1="275" y1="222" x2="455" y2="222" class="st-cut" />
          <line x1="275" y1="212" x2="455" y2="212" class="st-thin" />
          <line x1="275" y1="202" x2="455" y2="202" class="st-vis" />
          <line x1="275" y1="272" x2="455" y2="272" class="st-thin" />
          <!-- Hatching -->
          <path d="M225,95 L270,120 M225,125 L270,150 M225,155 L270,180 M225,295 L270,320 M225,325 L270,350" class="st-hatch" />
          <circle cx="310" cy="248" r="2.5" class="st-hatch" /><circle cx="360" cy="245" r="2.5" class="st-hatch" /><circle cx="410" cy="252" r="2.5" class="st-hatch" />
          <!-- Dimensions & Notes -->
          <line x1="160" y1="70" x2="160" y2="230" class="st-dim" /><text x="128" y="150" class="st-txt">السور 100</text>
          <line x1="480" y1="230" x2="480" y2="265" class="st-dim" /><text x="515" y="248" class="st-txt">بلاطة 15</text>
          <text x="130" y="62" class="st-txt">+4.00</text>
          <text x="130" y="230" class="st-txt">+3.00</text>
          <text x="365" y="185" class="st-txt-ar st-txt">عزل مائي + خرسانة ميول + بلاط</text>
          <circle cx="515" cy="90" r="18" class="st-cut" /><text x="515" y="90" class="st-txt">1/D-01</text>
        `;
        let svg = ``;
        svg += wrapLayer(L0, 0, stageIdx);
        svg += wrapLayer(L1, 1, stageIdx);
        return svg;
      }

      // Stages 2..3: Bathroom Section (1:20)
      const localIdx = stageIdx - 2;
      const B0 = `
        <!-- Left Wall 25cm (130..175), Right Door Wall (425..465), Recessed slab (-10cm) -->
        <rect x="130" y="75" width="45" height="275" class="st-cut" />
        <rect x="425" y="75" width="40" height="75" class="st-cut" />
        <rect x="425" y="285" width="40" height="65" class="st-cut" />
        <path d="M 175 315 H 425 V 345 H 175 Z" class="st-cut" />
        <path d="M 465 295 H 535 V 325 H 465 Z" class="st-cut" />
        <!-- Waterproofing turned up 30cm on walls + 1% slope -->
        <path d="M 179 255 V 311 H 421 V 255" class="st-cut" />
        <line x1="179" y1="295" x2="310" y2="303" class="st-vis" />
        <line x1="421" y1="295" x2="310" y2="303" class="st-vis" />
        <rect x="302" y="301" width="16" height="10" class="st-vis" />
        <text x="245" y="282" class="st-txt-ar st-txt">ميل 1% ← بالوعة</text>
      `;
      const B1 = `
        <!-- Marble Threshold 10cm + Wall tiles up to 2.10m -->
        <rect x="425" y="275" width="40" height="16" class="st-fill-poche" />
        <line x1="179" y1="110" x2="179" y2="295" class="st-vis" />
        <line x1="175" y1="110" x2="188" y2="110" class="st-thin" />
        <!-- Fixtures (thin lines): Shower head 2.00m, Mixer 1.10m, Basin 0.85m -->
        <path d="M 182 125 H 210 L 218 135" class="st-vis" />
        <rect x="182" y="210" width="12" height="14" class="st-thin" />
        <path d="M 335 232 H 395 V 248 H 355 V 295" class="st-vis" />
        <!-- Levels & Hatch -->
        <path d="M135,110 L170,130 M135,160 L170,180 M135,210 L170,230 M135,260 L170,280" class="st-hatch" />
        <text x="95" y="110" class="st-txt">+2.10</text>
        <text x="515" y="290" class="st-txt">±0.00</text>
        <text x="310" y="370" class="st-txt-ar st-txt">قطاع الحمام (1:20) — تخفيض 10 سم وعتبة رخام</text>
      `;
      let svg = ``;
      svg += wrapLayer(B0, 0, localIdx);
      svg += wrapLayer(B1, 1, localIdx);
      return svg;
    }

    function renderActiveDrawing() {
      const box = document.getElementById(`svg-stage-box`);
      const mod = MODULES.find(m => m.id === appState.activeModuleId) || MODULES[0];
      const idx = Math.min(appState.activeStageIndex, mod.stages.length - 1);
      if (!box) return;

      let inner = ``;
      if (mod.id === `floorplan`) inner = buildFloorPlanSVG(idx, false);
      else if (mod.id === `stairplan`) inner = buildStairSVG(idx);
      else if (mod.id === `section`) inner = buildSectionSVG(idx);
      else if (mod.id === `elevation`) inner = buildElevationSVG(idx);
      else if (mod.id === `details`) inner = buildDetailsSVG(idx);
      else if (mod.id === `tagging`) inner = buildFloorPlanSVG(5, true);

      const modeCls = appState.renderMode === `final` ? `arch-svg final-ink` : `arch-svg`;
      box.innerHTML = `<svg class="${modeCls}" viewBox="${mod.viewBox}" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="${mod.name} - ${mod.stages[idx].title}">${inner}</svg>`;
    }

    // =========================================================================
    // 4. UI RENDERING & INTERACTIONS
    // =========================================================================
    function renderModuleTabs() {
      const wrap = document.getElementById(`module-tabs`);
      if (!wrap) return;
      wrap.innerHTML = MODULES.map(m => {
        const activeCls = m.id === appState.activeModuleId ? `is-active` : ``;
        const doneCount = m.stages.filter((_, i) => appState.verifiedStages[`${m.id}-${i}`]).length;
        return `
          <button type="button" class="module-btn ${activeCls}" onclick="selectModule('${m.id}')">
            <span>${m.name}</span>
            <span class="module-badge">${doneCount}/${m.stages.length}</span>
          </button>
        `;
      }).join(``);
    }

    function renderSimulator() {
      const mod = MODULES.find(m => m.id === appState.activeModuleId) || MODULES[0];
      if (appState.activeStageIndex >= mod.stages.length) appState.activeStageIndex = mod.stages.length - 1;
      const idx = appState.activeStageIndex;
      const stage = mod.stages[idx];

      const elModTitle = document.getElementById(`canvas-module-title`);
      const elScale = document.getElementById(`canvas-scale-badge`);
      if (elModTitle) elModTitle.textContent = `${mod.name} — ${mod.subtitle}`;
      if (elScale) elScale.textContent = `مقياس ${mod.scale}`;

      // Stage dots
      const dotsWrap = document.getElementById(`stage-dots`);
      if (dotsWrap) {
        dotsWrap.innerHTML = mod.stages.map((_, i) => {
          const isCurr = i === idx;
          const isDone = !!appState.verifiedStages[`${mod.id}-${i}`];
          const cls = isCurr ? `is-current` : (isDone ? `is-done` : ``);
          return `<button type="button" class="stage-dot ${cls}" onclick="selectStage(${i})" aria-label="المرحلة ${i + 1}">${isDone && !isCurr ? `✓` : i + 1}</button>`;
        }).join(``);
      }

      const prevBtn = document.getElementById(`btn-prev-stage`);
      const nextBtn = document.getElementById(`btn-next-stage`);
      if (prevBtn) prevBtn.disabled = idx === 0;
      if (nextBtn) nextBtn.disabled = idx === mod.stages.length - 1;

      const setTxt = (id, val) => {
        const el = document.getElementById(id);
        if (el) el.textContent = val;
      };
      setTxt(`stage-counter`, `المرحلة ${idx + 1} من ${mod.stages.length}`);
      setTxt(`stage-title`, stage.title);
      setTxt(`stage-goal`, stage.goal);
      setTxt(`stage-golden`, stage.golden);
      setTxt(`stage-mistake`, stage.mistake);
      setTxt(`stage-tip`, stage.tip);
      setTxt(`stage-checkpoint`, stage.checkpoint);

      // Checklist
      const checkWrap = document.getElementById(`stage-checklist`);
      if (checkWrap) {
        checkWrap.innerHTML = stage.steps.map((stepTxt, sIdx) => {
          const key = `${mod.id}-${idx}-${sIdx}`;
          const checked = !!appState.checkedSteps[key];
          return `
            <label class="check-item ${checked ? `is-checked` : ``}">
              <input type="checkbox" ${checked ? `checked` : ``} onchange="toggleStepCheck('${key}', this.checked)">
              <span>${stepTxt}</span>
            </label>
          `;
        }).join(``);
      }

      const verifyBtn = document.getElementById(`btn-mark-verified`);
      const isVerified = !!appState.verifiedStages[`${mod.id}-${idx}`];
      if (verifyBtn) {
        verifyBtn.classList.toggle(`is-active`, isVerified);
        verifyBtn.textContent = isVerified ? `✓ تم تأكيد اجتياز المرحلة` : `تأكيد اجتياز هذه المرحلة`;
      }

      renderModuleTabs();
      renderActiveDrawing();
      updateOverallProgress();
    }

    function updateOverallProgress() {
      const verifiedCount = Object.values(appState.verifiedStages).filter(Boolean).length;
      const pct = Math.round((verifiedCount / TOTAL_STAGES_COUNT) * 100);
      const txtEl = document.getElementById(`overall-progress-text`);
      const fillEl = document.getElementById(`overall-progress-fill`);
      if (txtEl) txtEl.textContent = `${verifiedCount} / ${TOTAL_STAGES_COUNT} مرحلة (${pct}%)`;
      if (fillEl) fillEl.style.width = `${pct}%`;
    }

    function selectModule(modId) {
      appState.activeModuleId = modId;
      appState.activeStageIndex = 0;
      renderSimulator();
      persistState();
    }

    function selectStage(idx) {
      appState.activeStageIndex = idx;
      renderSimulator();
      persistState();
    }

    function stepStage(delta) {
      const mod = MODULES.find(m => m.id === appState.activeModuleId) || MODULES[0];
      const next = appState.activeStageIndex + delta;
      if (next >= 0 && next < mod.stages.length) {
        appState.activeStageIndex = next;
        renderSimulator();
        persistState();
      }
    }

    function setRenderMode(mode) {
      appState.renderMode = mode;
      const b1 = document.getElementById(`btn-mode-buildup`);
      const b2 = document.getElementById(`btn-mode-final`);
      if (b1) b1.classList.toggle(`is-active`, mode === `buildup`);
      if (b2) b2.classList.toggle(`is-active`, mode === `final`);
      renderActiveDrawing();
      persistState();
    }

    function toggleStepCheck(key, checked) {
      appState.checkedSteps[key] = checked;
      renderSimulator();
      persistState();
    }

    function toggleStageVerified() {
      const key = `${appState.activeModuleId}-${appState.activeStageIndex}`;
      appState.verifiedStages[key] = !appState.verifiedStages[key];
      renderSimulator();
      persistState();
    }

    // =========================================================================
    // 5. SCHEDULES, LINE WEIGHTS, CALCULATORS, GLOSSARY
    // =========================================================================
    function renderSchedules() {
      const dwBody = document.getElementById(`dw-schedule-body`);
      if (dwBody) {
        dwBody.innerHTML = DOOR_WINDOW_SCHEDULE.map((row, i) => `
          <tr class="schedule-row ${appState.selectedScheduleTag === row.code ? `is-selected` : ``}" onclick="inspectScheduleItem('dw', ${i})">
            <td><span class="code-tag">${row.code}</span></td>
            <td>${row.type}</td>
            <td style="font-family:var(--font-label);"><bdi dir="ltr">${row.size}</bdi></td>
            <td style="font-family:var(--font-label);">${row.sill}</td>
            <td style="font-family:var(--font-label);">${row.count}</td>
            <td>${row.mat}</td>
            <td>${row.swing}</td>
          </tr>
        `).join(``);
      }

      const fBody = document.getElementById(`finish-schedule-body`);
      if (fBody) {
        fBody.innerHTML = FINISH_SCHEDULE.map((row, i) => `
          <tr class="schedule-row ${appState.selectedScheduleTag === `R${row.num}` ? `is-selected` : ``}" onclick="inspectScheduleItem('finish', ${i})">
            <td><span class="code-tag">${row.num}</span></td>
            <td><strong>${row.space}</strong></td>
            <td>${row.floor}</td>
            <td>${row.skirt}</td>
            <td>${row.walls}</td>
            <td>${row.ceil}</td>
            <td>${row.notes}</td>
          </tr>
        `).join(``);
      }
    }

    function inspectScheduleItem(kind, index) {
      const box = document.getElementById(`schedule-inspector-text`);
      if (!box) return;
      if (kind === `dw`) {
        const item = DOOR_WINDOW_SCHEDULE[index];
        appState.selectedScheduleTag = item.code;
        box.textContent = `الرمز (${item.code}): ${item.type} — المقاس ${item.size} م، الجلسة: ${item.sill} م، العدد في المبنى: ${item.count}، الخامة: ${item.mat} (${item.swing}).`;
      } else {
        const item = FINISH_SCHEDULE[index];
        appState.selectedScheduleTag = `R${item.num}`;
        box.textContent = `غرفة رقم (${item.num}) — ${item.space}: الأرضية ${item.floor}، الوزرة ${item.skirt}، الحوائط (${item.walls})، السقف (${item.ceil}). ملاحظات: ${item.notes}.`;
      }
      renderSchedules();
    }

    function renderLineTypes() {
      const grid = document.getElementById(`lines-grid`);
      if (!grid) return;
      grid.innerHTML = LINE_TYPES.map(lt => `
        <div class="line-card">
          <div style="display:flex; justify-content:space-between; align-items:center; gap:var(--space-sm);">
            <strong style="font-size:0.96rem;">${lt.name}</strong>
            <span class="scale-chip">${lt.weight}</span>
          </div>
          <svg class="line-sample-svg" viewBox="0 0 260 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <line x1="6" y1="12" x2="254" y2="12" stroke="${lt.color}" stroke-width="${lt.widthPx}" ${lt.dash ? `stroke-dasharray="${lt.dash}"` : ``} stroke-linecap="round" />
          </svg>
          <span style="font-size:0.88rem; color:var(--on-surface-variant);">${lt.desc}</span>
        </div>
      `).join(``);
    }

    function updateScaleCalc() {
      const metersEl = document.getElementById(`calc-real-meters`);
      const scaleEl = document.getElementById(`calc-scale-select`);
      const outEl = document.getElementById(`scale-output-cm`);
      const noteEl = document.getElementById(`scale-formula-note`);
      if (!metersEl || !scaleEl || !outEl || !noteEl) return;

      const meters = parseFloat(metersEl.value) || 0;
      const scale = parseInt(scaleEl.value, 10) || 50;
      const factor = 100 / scale;
      const paperCm = meters * factor;

      outEl.textContent = `${paperCm.toFixed(2)} سم`;
      noteEl.textContent = `المعادلة: ${meters.toFixed(2)} م × 100 ÷ ${scale} (المعامل × ${factor}) = ${paperCm.toFixed(2)} سم على الورق`;
    }

    function loadScalePreset(meters, scale) {
      const metersEl = document.getElementById(`calc-real-meters`);
      const scaleEl = document.getElementById(`calc-scale-select`);
      if (metersEl) metersEl.value = meters;
      if (scaleEl) scaleEl.value = String(scale);
      updateScaleCalc();
    }

    function updateStairCalc() {
      const hEl = document.getElementById(`calc-floor-height`);
      const nEl = document.getElementById(`calc-risers-count`);
      const gEl = document.getElementById(`calc-going-cm`);
      const rOut = document.getElementById(`stair-riser-cm`);
      const fOut = document.getElementById(`stair-formula-val`);
      const chip = document.getElementById(`stair-comfort-chip`);
      const svg = document.getElementById(`stair-preview-svg`);
      if (!hEl || !nEl || !gEl || !rOut || !fOut || !chip || !svg) return;

      const floorM = Math.max(2.0, parseFloat(hEl.value) || 3.0);
      const count = Math.max(6, parseInt(nEl.value, 10) || 18);
      const going = Math.max(15, parseFloat(gEl.value) || 28);

      const riser = (floorM * 100) / count;
      const formula = 2 * riser + going;

      rOut.textContent = `${riser.toFixed(1)} سم`;
      fOut.textContent = `${formula.toFixed(1)} سم`;

      if (formula >= 60 && formula <= 64) {
        chip.className = `status-chip status-ok`;
        chip.textContent = `درج مريح ومتوازن (60–64 سم)`;
      } else if (formula < 60) {
        chip.className = `status-chip status-warn`;
        chip.textContent = `درج منبسط زيادة عن المعتاد (< 60 سم)`;
      } else {
        chip.className = `status-chip status-warn`;
        chip.textContent = `درج شديد الانحدار (> 64 سم)`;
      }

      // Dynamic 3-step SVG preview proportional to R and G
      const stepW = Math.min(72, Math.max(36, going * 2.1));
      const stepH = Math.min(26, Math.max(12, riser * 1.3));
      const x0 = 40;
      const y0 = 82;
      svg.innerHTML = `
        <path d="M ${x0} ${y0} V ${y0 - stepH} H ${x0 + stepW} V ${y0 - 2 * stepH} H ${x0 + 2 * stepW} V ${y0 - 3 * stepH} H ${x0 + 3 * stepW}" fill="none" stroke="var(--primary)" stroke-width="2.4" />
        <line x1="${x0 + stepW}" y1="${y0 - 2 * stepH - 12}" x2="${x0 + 2 * stepW}" y2="${y0 - 2 * stepH - 12}" stroke="var(--tertiary)" stroke-width="1.2" />
        <text x="${x0 + 1.5 * stepW}" y="${y0 - 2 * stepH - 17}" fill="var(--tertiary)" font-size="10" text-anchor="middle" font-family="var(--font-label)">G = ${going} سم</text>
        <text x="${x0 - 8}" y="${y0 - stepH * 0.5}" fill="var(--warning)" font-size="10" text-anchor="start" font-family="var(--font-label)">R=${riser.toFixed(1)}</text>
      `;
    }

    function renderFinalChecklist() {
      const box = document.getElementById(`final-checklist-box`);
      if (!box) return;
      box.innerHTML = FINAL_CHECKLIST.map((txt, i) => {
        const checked = !!appState.finalChecklist[String(i)];
        return `
          <label class="check-item ${checked ? `is-checked` : ``}">
            <input type="checkbox" ${checked ? `checked` : ``} onchange="toggleFinalCheck(${i}, this.checked)">
            <span>${txt}</span>
          </label>
        `;
      }).join(``);
    }

    function toggleFinalCheck(i, checked) {
      appState.finalChecklist[String(i)] = checked;
      renderFinalChecklist();
      persistState();
    }

    function renderGlossary(query = ``) {
      const list = document.getElementById(`glossary-list`);
      if (!list) return;
      const q = query.trim().toLowerCase();
      const filtered = GLOSSARY.filter(g => g.ar.toLowerCase().includes(q) || g.en.toLowerCase().includes(q));
      if (filtered.length === 0) {
        list.innerHTML = `<div style="color:var(--on-surface-variant); padding:var(--space-md);">لا توجد مصطلحات مطابقة لبحثك.</div>`;
        return;
      }
      list.innerHTML = filtered.map(g => `
        <div class="glossary-item">
          <strong>${g.ar}</strong>
          <span class="glossary-en">${g.en}</span>
        </div>
      `).join(``);
    }

    function filterGlossary(val) {
      renderGlossary(val);
    }

    function resetProgress(btn) {
      if (btn.dataset.armed !== `true`) {
        btn.dataset.armed = `true`;
        btn.textContent = `اضغط مرة أخرى لتأكيد المسح`;
        return;
      }
      btn.dataset.armed = `false`;
      btn.textContent = `إعادة تعيين التقدم`;
      appState.checkedSteps = {};
      appState.verifiedStages = {};
      appState.finalChecklist = {};
      renderSimulator();
      renderFinalChecklist();
      persistState();
    }

    // =========================================================================
    // 6. SPLASH SCREEN & INITIALIZATION
    // =========================================================================
    function dismissSplash() {
      const splash = document.getElementById(`splash-screen`);
      if (!splash || splash.classList.contains(`is-hidden`)) return;
      splash.classList.add(`is-docking`);
      setTimeout(() => {
        splash.classList.add(`is-hidden`);
      }, 430);
    }

    async function initApp() {
      if (window.notebookAppApi && typeof window.notebookAppApi.getAppState === `function`) {
        try {
          const saved = await window.notebookAppApi.getAppState();
          if (saved && typeof saved === `object`) {
            appState = Object.assign(appState, saved);
          }
        } catch (e) {
          // Use defaults
        }
      }

      renderSimulator();
      renderSchedules();
      renderLineTypes();
      updateScaleCalc();
      updateStairCalc();
      renderFinalChecklist();
      renderGlossary();

      if (window.lucide && typeof window.lucide.createIcons === `function`) {
        window.lucide.createIcons();
      }

      if (window.notebookAppApi && typeof window.notebookAppApi.notifyAppReady === `function`) {
        window.notebookAppApi.notifyAppReady();
      }

      setTimeout(dismissSplash, 1750);
    }

    window.addEventListener(`DOMContentLoaded`, initApp);
  </script>
</body>
</html>
