# AGENTS.md - Phone Store Angular Project

## Build/Lint/Test Commands

```bash
# Development server (http://localhost:4200/)
npm start
# or
ng serve

# Production build
npm run build
# or
ng build

# Development build with watch
npm run watch
# or
ng build --watch --configuration development

# Run all tests
npm test
# or
ng test

# Run a single test file
ng test --include src/app/my-component.spec.ts

# Run tests in watch mode
ng test --watch

# Generate new component
ng generate component component-name
ng g c component-name

# See all available schematics
ng generate --help
```

**Note:** There is no explicit lint command configured. TypeScript strict mode and Angular compiler provide type checking.

## Code Style Guidelines

### Formatting
- **Indentation:** 2 spaces (no tabs)
- **Quotes:** Single quotes for TypeScript (`'string'`)
- **Print width:** 100 characters
- **Trailing whitespace:** Trimmed automatically
- **Final newline:** Required at end of files
- **Formatter:** Prettier (configured in package.json)

### TypeScript Configuration
- **Target:** ES2022
- **Strict mode:** Enabled (all strict flags on)
- **Module:** preserve
- **Decorators:** Experimental decorators enabled
- **Import helpers:** Enabled
- **Skip lib check:** Enabled

### Angular Standards

#### Component Structure
```typescript
import { Component, signal } from '@angular/core';

@Component({
  selector: 'app-component-name',  // Prefix: app-
  imports: [/* standalone imports */],
  templateUrl: './component-name.html',
  styleUrl: './component-name.css'   // Note: singular 'styleUrl'
})
export class ComponentName {
  // Use signals for state
  protected readonly state = signal(initialValue);
}
```

#### Naming Conventions
- **Components:** PascalCase (e.g., `ProductList`, `App`)
- **Files:** kebab-case (e.g., `product-list.ts`, `app.html`)
- **Selectors:** app- prefix + kebab-case (e.g., `app-product-list`)
- **Signals:** Use `signal()` for reactive state
- **Protected:** Mark component properties as `protected readonly` when appropriate

#### Imports Order
1. Angular core imports
2. Angular router/common imports
3. Third-party imports (rxjs, etc.)
4. Local imports (absolute paths preferred)

### Error Handling
- Use `provideBrowserGlobalErrorListeners()` in app config
- Handle bootstrap errors with `.catch((err) => console.error(err))`
- TypeScript strict mode catches most errors at compile time

### Styling (Tailwind CSS v4)
- Import in `src/styles.css`: `@import "tailwindcss";`
- PostCSS configuration in `.postcssrc.json`
- Component styles use CSS (not SCSS)

### Testing (Vitest)
- Test files: `*.spec.ts` pattern
- Located alongside components (same directory)
- Uses jsdom environment
- Configuration via Angular CLI builder

### Project Structure
```
src/
  app/
    app.ts              # Root component (standalone)
    app.html            # Root template
    app.css             # Root styles
    app.config.ts       # App configuration
    app.routes.ts       # Route definitions
  main.ts               # Bootstrap entry
  styles.css            # Global styles + Tailwind
public/                 # Static assets
```

### GitHub Deployment
- Base HREF: `/phone-store/`
- Deployed via GitHub Actions (`.github/workflows/deploy.yml`)

### VS Code
- Recommended extension: `angular.ng-template`
- Pre-configured tasks for start and test

## Key Dependencies
- Angular 21.1.x (latest)
- TypeScript 5.9.x
- Tailwind CSS 4.1.x
- Vitest 4.0.x (testing)
- RxJS 7.8.x
