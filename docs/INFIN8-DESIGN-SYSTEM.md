# Infin8 Apps and Website Design System

Version: 2026.08  
Authority: Infin8 Apps design source of truth  
Canonical source: `E:\Infin8-Apps\docs\INFIN8-DESIGN-SYSTEM.md`

This contract applies to every Infin8 application, website, game, audio product, installer-facing screen, promotional capture, and customer-facing support surface. It is provider-neutral: Codex, Claude, Gemini, Copilot, local Ollama models, terminal agents, human developers, and future automation must follow the same rules.

Repository-specific build, security, deployment, DSP, and release instructions remain authoritative within their scope. This design contract adds mandatory visual, interaction, accessibility, dependency, synchronization, and evidence rules; it does not replace stricter local rules.

## 1. Non-negotiable product principles

1. **Infin8 owns the experience.** Product layout, information hierarchy, interaction design, artwork, copy, and final presentation must be recognizably Infin8. Do not ship an unchanged framework demo, dashboard template, generated mockup, or third-party design system skin.
2. **The interface explains itself.** A user should understand what the product sees, what an action changes, why a warning exists, and how to recover without specialist knowledge.
3. **Transparency means visibility and honesty.** Use translucent surfaces where they improve the visual hierarchy, and provide operational transparency through status, evidence, progress, logs, undo/recovery, and explicit safety boundaries.
4. **Local-first is visible.** Clearly distinguish local processing, loopback services, external requests, protected routes, customer data, credentials, and publication actions.
5. **One product, one source of truth.** Shared tokens and reusable components are centralized. Product-specific copies required for standalone packaging must be synchronized and validated.
6. **Customer releases are evidence-backed.** Source inspection, validation, packaged runtime proof, screenshot proof, publication proof, and hosted proof are separate claims.
7. **Development is not a release.** Do not create ZIPs, installers, portable packages, release directories, or other distribution artifacts unless the user explicitly requests a release and confirms the product is finished for that release.

## 2. Free UI technology and commercial-release gate

Infin8 interfaces may use first-party code, operating-system primitives, standard-library UI runtimes, or third-party/open-source frameworks when all of the following are true:

- no purchase, subscription, per-seat fee, runtime fee, royalty, paid designer, paid theme, paid component pack, or paid commercial license is required to build, maintain, package, or commercially release the interface;
- the complete UI dependency remains usable for commercial Infin8 releases on its free/open-source license, without a trial, watermark, revenue cap, feature lock, hosted account, or forced paid upgrade;
- the framework and every shipped module are permitted for the intended commercial distribution model;
- applicable copyright notices, license texts, attribution, relinking/source obligations, and third-party notices are recorded and packaged as required;
- the dependency does not claim ownership of Infin8 product assets or force unrelated Infin8 source disclosure;
- the product can be built and packaged repeatably without a paid or unlicensed designer template, hosted UI service, activation server, or private runtime dependency;
- security and update support are acceptable for the product lifetime;
- the resulting interface is custom-designed to this contract rather than visually inherited from the framework defaults.

Qt, Qt for Python/PySide, Tauri, Electron, React, standard HTML/CSS, iPlug2 WebViews, and operating-system APIs are implementation technologies, not visual identities. Their use requires a repository-level dependency/license review. Community Qt/PySide may be used only through a no-cost open-source license route whose obligations the product can satisfy; a paid Qt commercial license is not an approved dependency. This document is an engineering gate, not legal advice.

Every customer release must include or generate:

- `THIRD-PARTY-NOTICES.txt` or an equivalent packaged notice catalogue;
- an auditable dependency/lockfile inventory;
- the product and dependency versions used to build it;
- a validation check that paid, forbidden, or unreviewed UI packages are not shipped.

If a dependency later changes its terms, introduces a commercial-use fee, or cannot be redistributed while keeping the Infin8 application closed-source where required, agents must stop adopting or upgrading it and propose a free replacement. Only the user can explicitly change this no-paid-UI rule.

## 3. Core visual language

### 3.1 Desktop and control surfaces

| Token | Canonical value | Use |
| --- | --- | --- |
| `base` | `#090b13` | Application background and darkest scrim |
| `panel` | `#111522` | Main translucent panel source color |
| `panel-alt` | `#151a2a` | Raised rows, controls, and secondary surfaces |
| `border` | `#242b42` | Hairline structure and separators |
| `cyan` | `#4de8ff` | Primary action, focus, live data, active navigation |
| `cyan-bright` | `#7ff0ff` | Hover/highlight only |
| `purple` | `#9b6dff` | Brand accent, secondary data, creative context |
| `text` | `#edf2ff` | Primary text |
| `text-soft` | `#d6dced` | Supporting readable text |
| `muted` | `#929bb3` | Metadata and secondary labels |
| `success` | `#5ce6a5` | Healthy, complete, active |
| `warning` | `#ffd479` | Review, incomplete, degraded |
| `danger` | `#ff708b` | Failed, critical, destructive boundary |

### 3.2 Website profile

The public site keeps its existing web-calibrated tokens in `assets/style.css`: `#070910`, `#0d111c`, translucent `rgba(17,22,36,.82)`, `#8b5cf6`, `#39d7ee`, and `#39dfa0`. These are an approved profile of the same identity. New site UI must reuse the tokens and shared `.button`, navigation, card, focus, container, and responsive rules instead of recreating nearby colors.

Canonical site source and the active `htdocs` deployment mirror must remain aligned through the repository-supported sync/deploy flow.

### 3.3 Audio/iPlug2 WebView profile

`E:\Infin8-Audio\docs\ui-system.md`, `plugins/SharedUI/suite-ui.css`, `suite-ui.js`, `big_knob.png`, and `tools/verify-ui-system.ps1` are the executable Audio UI contract.

- Shared VST WebView CSS/JS copies remain byte-identical and self-contained.
- Knob cards, knob stages, and principal work sections stay transparent enough for the suite texture to remain visible.
- Borders, dividers, focus states, live announcements, preset/license workflow, keyboard behavior, telemetry, and shared shell chrome remain synchronized.
- Effects, Synth, and Vox keep the shared shell; product configuration changes workflow and parameters, not the interaction contract.
- Product releases may not reintroduce legacy native panels, duplicate filmstrips, raster control chrome, unused artwork, or unreferenced WebView assets.
- `tools/verify-ui-system.ps1` must pass before an Audio suite release.

The Audio palette uses the approved brighter WebView profile (`#42e0ff`, `#bc62ff`) because it is calibrated for plugin-scale controls and raster texture. Do not silently replace it with the desktop profile.

## 4. Texture and transparency

The Infin8 galaxy texture is a persistent brand surface, not decoration pasted into isolated headers.

- Paint it cover-scaled and centered without distortion.
- Apply a dark top-to-bottom scrim before placing content.
- Principal workspace panels should use translucent fills so the texture remains perceptible without reducing readability.
- Use stronger opacity for tables, code, forms, dense diagnostics, and modal dialogs.
- Avoid blur when it makes text less crisp, increases GPU load unnecessarily, or is not consistently supported. Alpha-composited panels are the baseline.
- Never place body text directly on a bright texture region without a readable surface or scrim.
- Do not stack many semi-transparent layers until the texture disappears or contrast becomes unpredictable.

Desktop reference:

```text
Backdrop: texture + rgba(7, 10, 19, 0.50 -> 0.66) vertical scrim
Primary panel: rgba(17, 21, 34, 0.82 to 0.90)
Raised row: rgba(21, 26, 42, 0.80 to 0.92)
Sidebar: rgba(9, 12, 22, 0.93 to 0.97)
Border: rgba(76, 86, 118, 0.45 to 0.65)
```

## 5. Shape, spacing, and typography

- Segoe UI is the Windows default; Inter/system sans is the web default. Product media may use an approved display face, but controls and dense data remain highly readable.
- Page titles: 25–32 px equivalent, 700–800 weight.
- Section titles: 15–20 px equivalent, 700–800 weight.
- Body and table text: never below a readable 12 px equivalent at 100% scale.
- Metadata: 11–13 px equivalent with adequate contrast.
- Main panel radius: 13–16 px desktop, up to 22 px marketing/web cards.
- Control radius: 8–10 px. Compact chips: 7–9 px.
- Base spacing unit: 4 px; preferred gaps are 8, 12, 16, 24, and 32 px.
- Do not create arbitrary one-off radii, colors, shadow recipes, or spacing values when a token fits.

## 6. Application shell and navigation

- Use a stable left rail for five or more primary workspaces; use tabs only for closely related views within one workspace.
- Brand lockup stays at the top; settings, legal, and infrequent controls stay at the bottom or in a deliberate utility area.
- Active navigation uses cyan text plus a subtle cyan translucent fill and border. Color alone is not the only state signal.
- The top workspace header contains the page title and only global, high-value actions.
- Monitoring, rendering, scanning, publishing, or long-running operations expose live/paused/running/failed states persistently.
- At common laptop and desktop sizes, primary actions and current status must not be clipped or require horizontal scrolling.

## 7. Components and data presentation

- Metric cards contain one label, one main value, and at most one short context line.
- Tables support readable headings, row selection, tooltips/details for truncated values, useful filtering, and a strong empty state.
- Severity order is critical, warning, notice, information. Pair color with words/icons and evidence.
- Charts include labels/legends and do not imply accuracy the source data cannot support.
- Primary actions use cyan-to-periwinkle treatment or solid cyan. Destructive actions never use the primary style.
- Forms explain validation beside the field and preserve entered data after recoverable errors.
- Empty states tell the user whether a service is inactive, no data was observed, permission is missing, or a check has not run.

## 8. Operational transparency and safety copy

Every diagnostic, AI, security, deployment, optimization, licensing, or account workflow must show:

- what was observed or requested;
- the source and timestamp when meaningful;
- what is local and what is external;
- evidence behind warnings or recommendations;
- what the next action changes;
- whether administrator rights, network access, credentials, or publication are involved;
- success, partial success, failure, cancellation, and recovery state;
- the boundary between a heuristic signal and proven malicious/failed behavior.

Raw identifiers remain internal when a correlated human-readable name is available. Logs, prompts, UI, and exports display names or neutral labels while retaining identifiers only where authorization/audit requires them.

## 9. Accessibility and input

- Minimum normal-text contrast is WCAG AA; do not rely on texture, glow, or color alone.
- All interactive controls expose accessible names, keyboard focus, visible focus rings, and logical tab order.
- Respect reduced-motion preferences. Animation is functional and interruptible, never required to understand state.
- Support Windows display scaling and text scaling. Avoid fixed pixel layouts that clip at 125%, 150%, or 200%.
- Pointer targets should be at least 36 px desktop-equivalent; primary touch targets should be at least 44 px.
- Data tables and canvases need keyboard or semantic alternatives for important actions.
- Audio controls retain keyboard adjustment and live announcements required by the Audio contract.

## 10. Responsive behavior

- Validate at minimum: 1280×720, 1440×900, 1920×1080, and one high-DPI configuration for desktop; 360, 768, 1024, and 1440 CSS pixels for websites.
- Cards reflow before text truncates. Dense tables may scroll inside their panel, but the entire application should not develop an uncontrolled horizontal scrollbar.
- Sidebars may compact on smaller widths but must retain understandable navigation and a visible active state.
- Preserve the product's intentional stage/canvas/timeline priority instead of stacking every panel equally.

## 11. Product profiles

### Operational desktop products

Control Panel, Optimizer, Sentinel, and management utilities use the desktop palette, texture/scrim, translucent shell, strong table surfaces, left navigation, visible runtime status, and evidence-first diagnostics.

### Creative desktop products

Editor and Website Editor may use denser canvases, timelines, inspectors, and device previews. Preserve content area priority, undo/redo visibility, selected-object context, and safe-source boundaries.

### Public website and Arcade

Reuse `assets/style.css` tokens and components. Keep navigation, buttons, support/legal access, responsive containers, and product imagery consistent. Game UI may adopt its game context but must retain readable Infin8 promotion and site controls without covering active play, HUD, or touch controls.

### Audio products

Follow the exact Audio profile in section 3.3 and the repository verifier. DSP safety and parameter stability override decorative UI changes.

## 12. Images, screenshots, and README presentation

- Product imagery must come from a validated real interface unless explicitly labelled concept art.
- Use the repository screenshot updater to launch, position, capture, validate, and close packaged applications.
- Never refresh a product image before its current UI and customer-facing data are established.
- Do not expose tokens, private endpoints, personal paths, private messages, customer records, or unrelated windows.
- README claims must match the pictured build and current source. Website and app pictures are updated independently.

## 13. Required development workflow

Before implementation:

1. Read this guide and the repository's `AGENTS.md`/provider instructions.
2. Identify the applicable product profile and existing canonical components/assets.
3. Inspect the real product and current screenshot; do not design from assumptions.
4. Record any new dependency, its no-cost license, and its commercial-release basis before adopting it. Reject dependencies that require payment for UI development or release.

During implementation:

1. Use existing tokens/components first.
2. Keep source, packaged-resource copies, and active website/runtime mirrors aligned.
3. Preserve unrelated work and existing safety/release rails.
4. Implement loading, empty, success, warning, failure, cancellation, and reduced-permission states.

Before completion:

1. Run the repository's design-system sync check.
2. Run source tests, accessibility checks, responsive checks, and the product build.
3. Inspect the packaged runtime visually at required sizes.
4. Run product-specific gates such as Audio `verify-ui-system.ps1` or website AgentCheck.
5. Update product imagery only after the UI proof passes.
6. Report source proof, packaged proof, screenshot proof, and deployment proof separately.

## 14. Agent and provider enforcement

Every provider entry file must direct the model to this synchronized guide. If an agent cannot read the guide, it must stop before customer-facing UI changes. A provider may propose a deviation only when it documents:

- why the existing profile cannot satisfy the product requirement;
- the precise token/component/dependency change;
- accessibility, no-paid-UI compliance, and commercial-release impact;
- synchronization and migration plan;
- validation evidence.

Silent drift is forbidden. Repository-specific exceptions must be explicit, narrow, documented, and validated.
