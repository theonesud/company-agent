---
name: code-fe
description: Coding Standards for Frontend Development
---

Here are the coding standards that everyone developing the frontend should follow (Deviations from these standards can be made but they should be minimal, and should be verified by the user):

## Frontend Code Structure
frontend/ (Root folder: all imports in the code should be absolute and relative to this folder)
├── public/
│   ├── images/
│   ├── ...
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── loading.tsx
│   │   ├── error.tsx
│   │   ├── not-found.tsx
│   │   ├── globals.css
│   │   ├── (auth)/
│   │   │   ├── login/
│   │   │   │   ├── page.tsx
│   │   │   │   └── ...
│   │   │   └── ...
│   │   ├── dashboard/
│   │   │   ├── page.tsx
│   │   │   └── ...
│   │   └── ...
│   ├── components/
│   │   ├── ui/
│   │   │   ├── button.tsx
│   │   │   ├── ...
│   │   ├── features/
│   │   │   ├── user-profile.tsx
│   │   │   ├── ...
│   ├── lib/
│   │   ├── utils.ts
│   │   ├── constants.ts
│   │   ├── logger.ts
│   │   ├── env.ts
│   │   ├── ...
│   ├── types/
│   │   ├── index.ts
│   │   ├── ...
│   ├── styles/
│   │   ├── ...
│   ├── tests/
│   │   ├── e2e/
│   │   │   ├── example.spec.ts
│   │   │   ├── ...
│   │   ├── unit/
│   │   │   ├── example.test.ts
│   │   │   ├── ...
├── .env
├── .env.local
├── .gitignore
├── biome.json
├── middleware.ts
├── next.config.ts
├── package.json
├── tsconfig.json

## Ignored Files
- Apart from the standard js stuff, node_modules/, .next/, .env and .DS_Store should be ignored in .gitignore.

## Package Management
- The environment should be managed by npm. Use `npm install` to install dependencies.
- The dependencies in package.json should be fixed to a specific version. Before using any package in the codebase, check if it is available in package.json. If not, run `npm install <package-name>` to install it.

## Formatting & Linting
- Use Biome to format and lint the code.
- The configuration in biome.json should be strict.

## Configs & Environment
- `src/lib/env.ts` should be used to validate and export environment variables (using Zod).
- Do not use `process.env` directly in components. Use the exported variables from `src/lib/env.ts`.
- Do not hardcode strings in the code. Move them to `src/lib/constants.ts` or a specific config file.

## Logging
- `src/lib/logger.ts` should export a structured logger (or a wrapper around console).
- Use this logger to log important user actions or errors.
- Do not use raw `console.log` in production code; use the logger.

## App Structure
- `app/layout.tsx` should only contain the global html/body structure, fonts, and global providers.
- `middleware.ts` should be used for authentication checks and global request logging.
- `app/error.tsx` (and `global-error.tsx`) must be used to catch and handle errors gracefully at the route level.

## Styling
- Use CSS Modules for component-level styling (file.module.css).
- Define global design tokens (colors, spacing) as CSS variables in src/app/globals.css.
- Do not use hardcoded hex values or pixels in components. Use CSS variables instead.
- Use modern CSS Grid and Flexbox for layouts.

## Components
- Place generic components in `src/components/ui`. Place domain-specific components in `src/components/features`.
- Define helper functions or types used only by a single component in the same file as the component.
- Do not split files unnecessarily. Keep related code in the same file.
- Use named exports. Do not use default exports.
- Add "use client" directive only when necessary (e.g., usage of hooks, event listeners).
- Make leaf components Client Components where possible. Keep Page components as Server Components.

## Data Fetching & State
- Fetch initial data in Server Components (page.tsx) and pass it as props.
- Prefer Server Actions for data mutations and form submissions.
- Do not use client-side data fetching (useEffect) for initial data load unless absolutely necessary (e.g. strict requirement for live data).
- Use URL Search Params for persistable state (filters, tabs, pagination).
- Avoid global state managers (like Zustand/Redux). Use them only if the state is complex, client-side only, and shared across many disparate components.
- Handle loading and error states using `loading.tsx` and `error.tsx` files.

## Tests
- End-to-end tests for user flows and page interactions should be defined in `src/tests/e2e/`. Use Playwright. Prefer testing by user-visible locators (roles, text) rather than CSS classes.
- Unit tests for pure logic functions, hooks, and utilities should be defined in `src/tests/unit/`. Use Vitest.

## General Coding Guidelines
- Do not create a variable if it is used only once, do the functionality inline.
- Do not create a function if its code is used only in one place, write the code in the same place. If the same/similar code is used in multiple places, create a function.
- Simple code is better than complex. Complex is better than complicated.
- Flat structure is better than nested. Do not nest clean components deeply.
- Error handling should be done primarily via Error Boundaries (`error.tsx`). Avoid extensive manual `try/catch` blocks in components unless handling specific user feedback from Server Actions.
- There should be one, and preferably only one obvious way to do something.
- Avoid code comments until absolutely necessary. A user reading the code should be able to understand the code in itself.
- Do not use `any` types. Define rigid interfaces in src/types/ or inline.

## DevOps: Build and Deployment
- Building, deploying the app using docker and github actions will be mentioned in a separate skill.

## Deviations from the Coding Standards
- You can create a reusable hook in src/lib/hooks/ if the logic is used in more than 3 distinct components.
