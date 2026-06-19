# ARCH-frontend.md — [PROJECT NAME]
# Load this file for: UI components, routing, state, styling, forms, client-side logic.
# Read rule: read Summary first. Load the rest only if Summary doesn't answer the question.
# Update rule: replace/update existing entries when things change. Do not append stale info.
# Last updated: [date]

## Summary
<!-- 5 lines max. One sentence per major component. Claude reads this first. -->
- Framework: [e.g. "React 18 + Vite, TypeScript strict mode"]
- Routing: [e.g. "React Router v6, all routes defined in src/routes/index.tsx"]
- State: [e.g. "Zustand for global state, React Query for server state — no Redux"]
- Styling: [e.g. "CSS variables only — color palette in CLAUDE.md, no Tailwind"]
- Forms: [e.g. "React Hook Form + Zod validation throughout"]

---

## Stack
- Framework: [e.g. React 18]
- Build tool: [e.g. Vite 5]
- Language: [e.g. TypeScript 5, strict mode]
- Routing: [e.g. React Router v6]
- State: [e.g. Zustand + React Query]
- Forms: [e.g. React Hook Form + Zod]
- Styling: [e.g. CSS custom properties — see CLAUDE.md for palette]
- Key deps: [anything non-obvious]

## Folder Structure
```
[paste your actual frontend folder tree here]
e.g.
src/
├── components/    ← Reusable UI components
├── pages/         ← Route-level page components
├── hooks/         ← Custom React hooks
├── store/         ← Zustand stores
├── api/           ← API client functions (React Query hooks)
├── types/         ← Shared TypeScript types
└── utils/         ← Helpers, formatters
```

## Routing
<!-- Key routes only -->
| Path | Component | Auth required |
|---|---|---|
| / | pages/Home.tsx | No |
| /dashboard | pages/Dashboard.tsx | Yes |
| /[route] | pages/[Component].tsx | [yes/no] |

## State Architecture
- Global state: [e.g. "Zustand — one store per domain in src/store/"]
- Server state: [e.g. "React Query — all API calls go through hooks in src/api/"]
- Local state: [e.g. "useState for component-scoped UI state only"]
- Rule: [e.g. "Never fetch data directly in components — always use a custom hook"]

## Component Conventions
- [e.g. "Page components in src/pages/, never import pages from other pages"]
- [e.g. "No inline styles — CSS custom properties only"]
- [e.g. "Every form uses React Hook Form — no uncontrolled inputs"]
- [e.g. "Error boundaries wrap every page-level component"]

## API Integration
- Client: [e.g. "axios instance in src/api/client.ts — all requests go through it"]
- Auth headers: [e.g. "JWT attached via axios interceptor — never manually"]
- Error handling: [e.g. "401 interceptor auto-refreshes token, 403 redirects to /login"]

## Constraints
<!-- Firewall. Claude must not violate without explicit user approval. -->
- [e.g. "No direct fetch() calls — always use the API client in src/api/"]
- [e.g. "No Tailwind — CSS custom properties only, palette from CLAUDE.md"]
- [e.g. "No class components — functional components and hooks only"]
- [e.g. "TypeScript strict — no 'any' types without a comment explaining why"]

## Testing
**Runner:** [e.g. Vitest + React Testing Library]
**Command:** [e.g. `npm run test`]
**E2E:** [e.g. Playwright — `npm run test:e2e`]

What is tested:
- Unit: [e.g. "utility functions, custom hooks"]
- Component: [e.g. "critical UI components via RTL"]
- E2E: [e.g. "auth flow, core user journeys via Playwright"]

Coverage gaps: [things you know are untested]
Skipped tests: [intentionally skipped + reason]
Flaky tests: [intermittent failures + root cause]

## Known Gotchas
<!-- Non-obvious things that cost time -->
- [e.g. "React Query cache is shared — invalidate carefully or stale data leaks across users"]
- [e.g. "Vite HMR drops Zustand state on store file changes — full reload needed"]
