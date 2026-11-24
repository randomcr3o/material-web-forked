# DESIGN.md

## Purpose

This file is the visual and interaction contract for AI agents building interfaces in this project. Follow it before inventing local styles or choosing components. The goal is Material 3 Expressive: familiar, usable Material patterns with a more distinctive voice through purposeful color, shape, typography, and motion. Expressiveness must never make a UI harder to understand, less accessible, or inconsistent.

This repository is Material Web (`@material/web`), a set of Material 3 web components. Its theming guides document color, typography, and shape tokens; its components provide behavior and component tokens. Do not claim that every component or token in this repo implements every newer Material 3 Expressive feature. Use the actual component and token APIs available in the installed version, and check the component documentation before writing markup or CSS.

## Priorities

When design goals conflict, use this order:

1. Correct meaning, content, and task flow
2. Accessibility, input support, and readable contrast
3. Familiar and predictable interaction
4. Responsive layout and resilience to real content
5. Brand character and expressive styling

Do not sacrifice a higher priority for a lower one. Prefer native Material Web components over hand-built lookalikes when an appropriate component exists. Keep the existing app's framework, routing, state patterns, and component conventions; this file governs design, not architecture.

## Product identity

Material 3 Expressive should feel warm, clear, confident, and human. Create personality with a considered theme and a small number of memorable moments, not decoration on every surface. Build visual hierarchy with spacing, type, color roles, and shape before adding borders, shadows, gradients, or animation.

Use a consistent theme across the whole experience. A page may emphasize one or two key actions, but should not make every element compete for attention. Keep content and controls calm enough that expressive colors and shapes remain legible.

## Theme foundation

Use Material design tokens as the source of truth. In this repository, reference tokens are `--md-ref-*`, system tokens are `--md-sys-*`, and component tokens are component-specific properties such as `--md-filled-button-container-shape`. Do not invent a `--md-comp-*` namespace. Scope component-token overrides to the relevant component or feature where practical.

### Color

Use a coherent Material color scheme, ideally generated from the product's key colors with Material Theme Builder or `@material/material-color-utilities`. Define roles, not ad hoc colors. Start with `primary`, `on-primary`, `primary-container`, `on-primary-container`, `secondary`, `tertiary`, `error`, `background`, `surface`, `surface-container*`, `on-surface`, `on-surface-variant`, `outline`, and `outline-variant` as needed.

- Use primary for the most important actions and selected emphasis, not as the background for every control.
- Use secondary and tertiary as supporting accents. Give each a clear, repeatable purpose.
- Use container roles for emphasized regions and their matching `on-*` roles for content.
- Use surface roles to create restrained elevation and grouping. Do not stack many nearly identical surface shades without a hierarchy reason.
- Use error roles for errors and destructive context, not as generic decoration.
- Ensure text and important UI boundaries meet WCAG contrast requirements. Never communicate state by color alone; pair color with text, iconography, or another clear signal.
- Do not use raw hex values in component styles when a matching theme role exists. A raw color is acceptable for an actual image or documented brand color that cannot be represented by the theme.
- Respect user-selected light and dark themes. Do not hard-code light-only text or surfaces.

Example theme values are illustrative only; establish actual brand colors from the project rather than copying these values blindly.

```css
:root {
  --md-sys-color-primary: #006a6a;
  --md-sys-color-on-primary: #ffffff;
  --md-sys-color-primary-container: #6ff7f6;
  --md-sys-color-on-primary-container: #002020;
}
```

The full token list and color scheme guidance live in [`docs/theming/color.md`](docs/theming/color.md).

### Typography

Use the Material typescale roles for hierarchy and meaning: display for rare, high-impact hero content; headline for page or section headings; title for compact headings and card titles; body for reading; label for compact UI labels. Choose a size appropriate to the content and viewport, not just because it looks expressive.

Load Roboto at weights 400, 500, and 700 if retaining the defaults. If the project has a brand typeface, set `--md-ref-typeface-brand` and `--md-ref-typeface-plain` consistently and load the required font files. Keep body text highly readable; do not use display typography for forms, dense data, or long passages. Avoid all-caps labels unless the product's established voice requires them.

Prefer `.md-typescale-*` classes and `--md-sys-typescale-*` tokens over arbitrary font sizes. Do not shrink text to force content into a layout. Allow headings, labels, and buttons to wrap when needed.

See [`docs/theming/typography.md`](docs/theming/typography.md).

### Shape

Use shape as a deliberate part of the brand voice. Let larger, more prominent surfaces use a more expressive shape and keep dense or frequently repeated controls quieter. A shared shape scale should make cards, dialogs, fields, and buttons feel related. Do not give every element the same exaggerated pill shape, mix unrelated radii, or use shape alone to indicate interaction or state.

Use the available `--md-sys-shape-corner-*` tokens and component shape tokens. This repository's shape guide notes that cut corners are not supported. Check the component docs before overriding a component token.

See [`docs/theming/shape.md`](docs/theming/shape.md).

### Spacing and layout

Use a consistent spacing rhythm based on 4px increments (commonly 4, 8, 12, 16, 24, 32, and 48px). The rhythm is a practical layout convention, not a reason to create cramped controls. Group related content closely, separate unrelated groups more clearly, and keep alignment consistent within a view.

- Use responsive layouts that adapt to available space; do not design only for one fixed viewport.
- Use readable line lengths for long-form text and avoid stretching forms across wide screens.
- Keep touch targets comfortably operable, with at least 48 by 48 CSS pixels where practical; never reduce the actual interactive target to a tiny icon.
- Use whitespace to show grouping before adding dividers or boxes.
- On small screens, prioritize the main task and preserve clear navigation; do not simply scale down a desktop layout.
- Avoid horizontal scrolling for ordinary content. For genuinely wide data, provide an intentional, accessible overflow pattern.

Spacing values are layout guidance. This repo does not define a dedicated system spacing token set; do not imply that these values are built-in Material Web tokens.

### Elevation and surfaces

Use surface roles, borders, and elevation to communicate hierarchy, not as decoration. Reserve stronger separation for overlays and important floating controls. Keep most content on a small number of related surface levels. Do not add a shadow to every card or use elevation as a substitute for clear grouping. Follow the component's built-in treatment unless there is a specific product requirement to change it.

### Motion

Motion should explain a state change, preserve continuity, or direct attention. Keep transitions brief and purposeful; avoid perpetual motion, gratuitous entrance animations, and movement that delays a task. Prefer opacity or small, meaningful movement over large spatial jumps. Do not make essential information available only through animation.

Honor `prefers-reduced-motion: reduce`: remove or substantially reduce nonessential movement and avoid disabling users' ability to understand state. This repo's theming guide says it does not currently provide `--md-sys-motion` tokens, so do not assume those tokens exist. Use the component's built-in interaction behavior where possible.

## Component rules

Select components by the user's task and the component's semantics, not by visual novelty. Use the documented `md-*` element and its documented properties/events. Do not fabricate component names, slots, CSS tokens, or behaviors. Component APIs can vary by package version; check the relevant file in [`docs/components/`](docs/components/) and the version installed in the project.

### Buttons and icon buttons

Use `md-filled-button` for the single highest-emphasis action in a local group; `md-filled-tonal-button` for a prominent but less dominant action; `md-outlined-button` for a secondary action; and `md-text-button` for a low-emphasis action. Use `md-elevated-button` only where its raised surface is useful. Avoid placing multiple equally strong filled buttons next to each other unless the actions truly have equal priority.

Use buttons to trigger actions and links to navigate. Give buttons concise action labels that say what happens. Set the correct button type in forms. Keep destructive actions visually and textually explicit; do not style an ordinary action as an error just to make it stand out.

Use `md-icon-button` for a compact, familiar action with a clear accessible name. Provide a tooltip or visible label when the icon's meaning is not obvious. Do not use icon-only controls for critical or unfamiliar actions without an accessible name and a clear way to understand them.

### FABs

Use `md-fab` or its documented variants for the primary, frequently needed action on a screen, not as generic decoration or a second competing primary action. Keep it in a stable, reachable location and ensure it does not cover content, navigation, or focused controls. Use an extended FAB only when the text label improves recognition.

### Text fields

Choose the documented filled or outlined text-field variant consistently within a form. Give every field a persistent, programmatic label; placeholders are examples or hints, never the only label. Use supporting text for brief instructions and show validation errors next to the relevant field in clear language. Preserve entered values on recoverable errors.

Use the right input type, autocomplete hints, and required/disabled/read-only state. Mark errors with text and appropriate semantics, not color alone. Do not rely on a floating label to communicate a field's meaning after entry.

### Selection controls

Use `md-checkbox` for independent, multi-select choices; `md-radio` for one choice in a mutually exclusive group; and `md-switch` for an immediate on/off setting. Group related controls under a visible label or legend. Use a switch only when changing it applies or represents a setting directly, not as a disguised submit button. Ensure each control has an associated label and clear checked/disabled states.

### Select menus and menus

Use `md-outlined-select` or the supported select variant when a user chooses one value from a known set and a native-sized list is appropriate. Keep the label visible and show a useful initial value or prompt. For a small number of choices that should always remain visible, use radio buttons or another explicit choice pattern instead.

Use `md-menu` for a temporary list of related commands or options anchored to a control. Use menu items for actions or navigation according to their documented semantics. Do not use a menu as the only way to expose critical content or hide primary navigation in a way that harms discoverability.

### Chips

Use chips for compact filters, selected values, or suggestions according to the documented chip variant. Make selection and removal states clear and operable by keyboard. Do not use chips as a replacement for ordinary navigation, a page heading, or a full-size primary action. Avoid making a long set of chips wrap into a visually noisy wall; use a clear grouping or scrolling pattern when needed.

### Tabs

Use tabs to switch between peer views of related content, not to navigate unrelated sections or conceal a required linear workflow. Keep labels short and parallel in meaning. Preserve the active state and follow the component's keyboard interaction. On narrow screens, ensure all tab labels remain reachable and the selected tab is apparent.

### Dialogs

Use `md-dialog` for a focused decision or task that genuinely needs to interrupt the current flow. Keep dialog content concise, title it clearly, and provide an obvious way to cancel or close unless the task must be completed to proceed. Put the most likely action in the clearest position and label destructive confirmation explicitly. Do not put an entire page or a long form into a dialog when an in-page flow works better.

Ensure focus enters the dialog, remains managed while it is open, and returns to the invoking control when it closes. Do not create nested dialogs. Keep essential context visible in the dialog and avoid closing it unexpectedly after validation errors.

### Lists and dividers

Use `md-list` and its documented list items for collections of related options, records, or navigation destinations. Make each row's action and selected state clear. Keep primary content aligned and avoid overloading rows with too many secondary controls. Use `md-divider` sparingly to separate groups that whitespace alone cannot distinguish; do not draw a line between every item by default.

### Progress indicators

Use `md-circular-progress` or `md-linear-progress` to represent actual ongoing work. For indeterminate work, communicate that activity is underway; for determinate work, provide accurate progress. Keep the indicator near the work it describes and provide accessible status text when progress is important. Never animate a fake progress value to suggest progress that is not known.

### Sliders

Use `md-slider` for selecting a value within a meaningful continuous or stepped range. Label the value and range, show the current value when useful, and make keyboard operation possible. Use a numeric field or explicit choices when precise entry or a small discrete set is more suitable.

### Icons, focus, and ripple

Use `md-icon` with familiar, consistent iconography and pair unclear icons with text. Do not use emoji as interface icons. Keep icons aligned and sized consistently with adjacent text.

Preserve visible keyboard focus. Never remove an outline or focus ring without supplying an equally clear replacement. Use focus indication that is visually distinct from hover, selected, and pressed states. Do not add ripple or focus-ring elements manually if the chosen Material component already provides them; check the component API first.

### Components outside this list

This repository also documents components such as `md-elevation` and other controls. Follow their own component docs and semantics. A component's presence in the package does not mean it is the right choice for every project or task. If there is no suitable Material Web component, build the smallest accessible custom component that fits the existing project and visually follows these rules.

## Interaction and accessibility

Accessibility is part of the visual design, not a cleanup step.

- Use semantic HTML and the component's native accessibility behavior. Do not add redundant ARIA that conflicts with built-in semantics.
- Every control must have a programmatic name, a visible focus state, and a keyboard-operable interaction.
- Maintain logical heading order, landmark structure, and reading order. Visual rearrangement must not make keyboard or screen-reader order confusing.
- Keep text readable and ensure contrast for text, icons, focus indicators, and important control boundaries.
- Provide clear hover, focus, pressed, selected, disabled, loading, success, and error states where relevant. Do not rely on hover because touch devices do not have it.
- Use clear, specific error messages that explain how to fix the problem. Keep error feedback close to its field or action.
- Respect zoom and text resizing. Avoid fixed heights that clip translated or enlarged content.
- Use reduced motion preferences and do not flash content.
- Test with keyboard-only interaction and at narrow and zoomed viewport sizes.

Use WCAG 2.2 AA as the baseline for new UI. Where a component or platform imposes a limitation, do not pretend it is compliant; use an accessible alternative or document the limitation.

## Content and states

Write short, plain, action-oriented labels. Keep terminology consistent across the product. Use sentence case for headings and controls by default. Avoid vague labels such as “OK” when a specific action name is possible.

Design the full state, not just the happy-path screenshot. Include useful empty, loading, success, validation, error, disabled, and offline states when relevant. Empty states should explain what is absent and offer a next step when one exists. Errors should preserve user work wherever possible. Do not fabricate realistic-looking content, data, or progress values in a production interface.

## Implementation guidance for agents

1. Inspect the existing project theme and component usage before changing the visual system.
2. Reuse the current theme and established patterns. Do not silently replace the brand palette, font, or component library.
3. For Material Web, import and use the component modules required by the app's build setup. Follow this repo's quick-start and installed-version docs; do not assume every app uses the buildless CDN example.
4. Prefer system tokens and documented component tokens. Keep overrides small, scoped, and intentional.
5. Use semantic HTML around components and keep form labels, grouping, and error associations intact.
6. Verify responsive behavior, keyboard interaction, focus visibility, theme contrast, and reduced-motion behavior before calling the design done.
7. When a requested expressive treatment conflicts with usability or accessibility, keep the usable behavior and express the brand through a safer surface, color role, shape, or illustration.
8. Do not add unsupported tokens or pretend a repo component has an API it does not. If the needed behavior is unclear, inspect the installed component docs or source before implementing it.

## Review checklist

Before finishing a UI change, check:

- Does the page have one clear primary action and a readable hierarchy?
- Are colors drawn from intentional theme roles, with appropriate matching content colors?
- Are type roles and shape choices consistent and purposeful?
- Does each control match the task and retain its expected Material behavior?
- Are labels, errors, focus, selected states, and keyboard interaction clear?
- Does the layout work on small and large screens, with real content and zoom?
- Are motion and elevation useful rather than decorative?
- Are loading, empty, error, and success states handled where applicable?
- Were only documented component names, properties, events, and tokens used?

## Repository references

- [Theming overview](docs/theming/README.md)
- [Color](docs/theming/color.md)
- [Typography](docs/theming/typography.md)
- [Shape](docs/theming/shape.md)
- [Component documentation](docs/components/)
- [Quick start](docs/quick-start.md)
- [Browser support and FAQ](docs/support.md)
