# AGENTS.md - Factu Lite Web

## Project Overview

This is an Astro-based marketing website for "Factu Lite", a sales and inventory management system for small businesses in Nicaragua. The site is primarily Spanish-language and serves as a landing page to download and promote the mobile app.

## Tech Stack

- **Framework**: Astro 6.1.3
- **Package Manager**: bun
- **Language**: TypeScript (strict mode via `astro/tsconfigs/strict`)
- **Styling**: Vanilla CSS with CSS custom properties (no Tailwind)
- **Content**: Static marketing site with no backend

## Project Structure

```
/
├── public/              # Static assets (downloads, screenshots)
├── src/
│   ├── components/      # Astro components (.astro files)
│   ├── data/           # JSON data files (config.json)
│   ├── layouts/        # Page layouts
│   ├── pages/          # Astro pages (routing)
│   └── styles/         # Global CSS
├── astro.config.mjs    # Astro configuration
├── tsconfig.json       # TypeScript configuration
└── package.json        # Dependencies and scripts
```

## Commands

### Development
```bash
bun dev              # Start dev server at localhost:4321
bun build            # Build production site to ./dist/
bun preview          # Preview production build locally
bun astro check       # Type-check Astro files
bun astro --help      # Show Astro CLI help
```

### Single Component/Page Development
```bash
# Use Astro's dev server with hot reload at localhost:4321
bun dev
```

### No Testing Framework
This project does **not** have a testing framework configured (no Vitest, Playwright, etc.).

### No Linting
This project does **not** have ESLint or Prettier configured. Code style is enforced by:
- Astro's built-in TypeScript integration
- Editor settings in `.vscode/`
- Manual code review

## Code Style Guidelines

### Astro Components (.astro files)

#### Frontmatter (JavaScript/TypeScript)
- Always include `---` fences at the top and bottom
- Import statements go inside the frontmatter
- TypeScript interfaces for Props are defined inside frontmatter
- Props destructuring with default values

```astro
---
interface Props {
  title?: string;
  description?: string;
}

const {
  title = 'Default Title',
  description = 'Default description'
} = Astro.props;
---

<!-- HTML template -->
```

#### HTML Template
- Use lowercase HTML tags
- Self-close void elements (`<img />`, `<br />`)
- Use `.astro` expression syntax for dynamic values: `{variable}`
- Conditional rendering with ternary operators or logical &&

#### Client-Side Scripts
- Scripts go in `<script>` tags at the bottom of the file
- Use standard DOM APIs (no framework)
- Always null-check DOM elements before use

```astro
<script>
  const element = document.getElementById('id');
  if (element) {
    // safe to use
  }
</script>
```

### CSS Guidelines

#### Architecture
- CSS is scoped to components via `<style>` tags
- Global styles in `src/styles/global.css`
- Use CSS custom properties (variables) for colors, spacing, typography
- Utility classes for common patterns

#### CSS Variable Naming
```css
--color-primary: #047857;
--color-primary-dark: #065F46;
--spacing-md: 1rem;
--radius-lg: 0.75rem;
--transition-fast: 150ms ease;
```

#### Utility Classes Pattern
Follow existing utility patterns:
```css
.text-center { text-align: center; }
.flex { display: flex; }
.gap-md { gap: var(--spacing-md); }
.mb-lg { margin-bottom: var(--spacing-lg); }
```

#### Responsive Design
Use mobile-first approach with these breakpoints:
```css
@media (max-width: 767px) { /* Mobile */ }
@media (min-width: 768px) and (max-width: 1023px) { /* Tablet */ }
@media (min-width: 1024px) { /* Desktop */ }
```

### TypeScript

#### Configuration
- Extends `astro/tsconfigs/strict`
- Strict null checks enabled
- Use explicit types for Props interfaces

#### Naming Conventions
- Components: PascalCase (`Header.astro`, `Pricing.astro`)
- Interfaces: PascalCase with `Props` suffix for component props
- Variables/functions: camelCase
- CSS classes: kebab-case

### Imports

#### Path Conventions
- Relative imports for sibling components: `../components/Component.astro`
- JSON data imports: `import config from '../data/config.json';`
- Use named exports where applicable

#### Import Order (recommended)
1. Astro components/layouts
2. External libraries (if any)
3. Internal components
4. Data imports
5. Types/interfaces

### File Organization

#### Component Structure
Each `.astro` component should follow this pattern:
1. Frontmatter with imports and Props interface
2. HTML template
3. Component-scoped `<style>` block
4. Client-side `<script>` block (if needed)

#### Page Structure
Pages (`src/pages/`) import and compose components:
```astro
---
import Layout from '../layouts/Layout.astro';
import Header from '../components/Header.astro';
// ... other imports
---
<Layout>
  <Header />
  <main>
    <!-- content -->
  </main>
</Layout>
```

### Error Handling

#### Null Checks
Always verify DOM elements exist before manipulation:
```javascript
const element = document.getElementById('elementId');
if (element) {
  element.addEventListener('click', handler);
}
```

#### Conditional Rendering
Use Astro's conditional expressions:
```astro
{config.app.logo ? (
  <img src={config.app.logo} alt={config.app.name} />
) : (
  <span>Default</span>
)}
```

### Data Files

#### JSON Structure
Data lives in `src/data/config.json`. When modifying:
- Maintain consistent property ordering
- Use appropriate data types (strings, numbers, arrays)
- Follow Spanish naming conventions for content
- Keep the structure flat where possible for easier parsing

### Accessibility

- Use semantic HTML elements (`<header>`, `<nav>`, `<main>`, `<section>`)
- Include `aria-label` on interactive elements without visible text
- Use `alt` attributes on images
- Ensure color contrast meets WCAG guidelines

### Git Conventions

- No specific commit message format enforced
- Keep commits focused and atomic
- Reference issues/tickets in commit messages when applicable

### Performance

- Static assets go in `public/`
- Images should be optimized
- Use lazy loading for below-fold images
- Minimize client-side JavaScript

## Important Notes

- The site is entirely Spanish-language; all content, labels, and messages should be in Spanish
- This is a marketing/landing page, not a web application
- No API routes or server-side logic (purely static)
- The actual application logic is in a separate Android/Kotlin codebase
