---
name: vercel-react-best-practices
description: Best practices for React 18+ and Next.js (App router, Server/Client components, Suspense). Use when writing or reviewing React code.
---

# Vercel & React Best Practices

You are enforcing modern, highly-performant React and Next.js standards.

## Core Directives
1. **Component Boundaries:** Strictly separate Server Components from Client Components. Default to Server Components; only use `"use client"` when state, effects, or DOM events are required.
2. **Data Fetching:** Fetch data on the server when possible. Use React Suspense boundaries for loading states instead of manual `isLoading` boolean checks.
3. **State Management:** Keep state as local as possible. Do not lift state unnecessarily. Prefer URL search params for shareable state.
4. **Performance:** Memoize expensive calculations. Ensure image optimization (using `<Image>`) and dynamic imports for heavy client libraries.

## Workflow
1. Review the component structure.
2. Ensure proper use of `"use client"` and `"use server"`.
3. Refactor any outdated hooks or state patterns to modern React 18+ equivalents.
