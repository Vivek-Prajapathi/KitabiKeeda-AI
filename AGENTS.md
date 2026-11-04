# KitabiKeeda Agent Instructions

## Project Overview

KitabiKeeda is a browser-based learning platform frontend. It has a public site and course catalog, a separate LMS marketplace, authenticated learner pages, an instructor workspace, and role-protected administration pages. This repository contains the Vite frontend; backend behavior depends on an external API.

For the product description and route overview, see [README.md](./README.md). Treat the source code as authoritative when it differs from documentation.

## Technology Stack

- React 19 and JavaScript with JSX; there are no application TypeScript source files.
- Vite 8, React Router 7, and Axios.
- React Context API for authentication state.
- Tailwind CSS 4 and custom CSS.
- Lucide React, Sonner, and Recharts.
- Oxlint is the configured linter.

The exact dependencies and available scripts are in [package.json](./package.json).

## Architecture and Entry Points

- `index.html` loads [`src/main.jsx`](./src/main.jsx), which mounts [`src/App.jsx`](./src/App.jsx).
- [`src/routes/AppRoutes.jsx`](./src/routes/AppRoutes.jsx) defines public, learner, instructor, marketplace, and admin routes. It wraps the routes with `BrowserRouter` and `AuthProvider`; some pages are lazy-loaded.
- `src/layouts/` contains public, user, and admin route layouts. Shared UI components are in `src/components/`.
- `src/pages/` contains public, account, course, marketplace, and instructor pages. Learner profile pages are in `src/profile/`; admin pages are in `src/admin/pages/`.
- `src/context/AuthContext.jsx` owns authentication state and actions. `src/hooks/useAuth.js` re-exports its hook, and `src/components/ProtectedRoute.jsx` enforces client-side route gates.
- `src/api/axios.js` configures the shared Axios client. Feature API wrappers are in the other `src/api/*.js` modules.
- `src/index.css` is the global stylesheet. Page and component styling uses utility classes and custom CSS; follow the nearby feature's approach.
- `src/admin/components/`, `src/admin/styles/`, and `src/styles/` currently contain no source files.

The regular catalog (`/courses`) and LMS marketplace (`/marketplace`) use different API services (`courseAPI` and `lmsAPI`). Keep those feature boundaries intact unless a request explicitly changes them.

## Coding and Naming Conventions

- Follow the neighboring file's formatting and import style; the existing files are not perfectly uniform.
- Components and pages use descriptive PascalCase filenames and component names, commonly declared as functions or arrow functions and default-exported.
- Hooks use the `use` prefix. API wrapper objects and methods use descriptive camelCase names.
- Keep feature-specific pages and API calls in their existing folders rather than introducing a new architectural layer without need.
- Reuse existing dependencies and helpers. Do not add a dependency or change package manifests unless the task explicitly requires it.

## Component and Hook Guidelines

- Before adding a component, search `src/components/` and the relevant feature folder for an existing implementation to reuse.
- Keep components focused on the UI or feature responsibility that matches their current folder. Use React Router links for in-app navigation.
- Use React Hooks only in components or custom hooks and follow the existing state ownership pattern: page-local state for page behavior, `AuthContext` for shared authentication.
- Keep effect dependencies correct and clean up subscriptions or asynchronous work when a component unmounts.
- Preserve existing loading, empty, and error states when changing data-driven screens.

## Routing, State, and Authentication

- Add or change route definitions in `src/routes/AppRoutes.jsx` and use the existing layouts and `ProtectedRoute` wrapper.
- Do not treat client-side route protection as a security boundary. Authorization must be enforced by the backend as well.
- Use `useAuth` for the established authentication interface; do not create a second global authentication store.
- `AuthContext` persists the current user and access token in browser `localStorage`; do not log or expose their values.

## API Integration and Error Handling

- Use the existing service module under `src/api/` and the shared `axiosInstance` rather than creating an unrelated HTTP client.
- Read the actual request shape, response handling, and callers before changing or adding an endpoint. Do not infer backend contracts from UI labels or invent routes.
- The configured base URL is `VITE_API_BASE_URL`, falling back in `src/api/axios.js` to `https://mockapi-mauve.vercel.app/api/v1`.
- Preserve the established user feedback patterns: inline page errors and loading states, `console.error` for caught operational failures, and Sonner toast notifications where used.
- Do not hide failures behind success-shaped defaults. Handle rejected requests and unsuccessful API response payloads consistently with the surrounding feature.

## Security

- Never place credentials, access tokens, private keys, or personal data in source, documentation, logs, or commits.
- Treat all `VITE_` variables as browser-visible; never put secrets in them.
- Do not weaken role checks, bypass backend authorization, or assume values from `localStorage` are trustworthy.
- Avoid logging full request/response payloads that may contain personal or authentication data.

## Testing and Validation

- `package.json` currently provides `npm run lint` and `npm run build`; it has no test script, and no application test files or test framework were found.
- Run the smallest relevant existing validation for code changes. Do not claim tests passed unless they were actually run.
- Do not introduce a test framework or other dependency without approval; document when behavior cannot be covered by the current setup.

## Before Making Changes

1. Read the relevant parts of `README.md` and inspect the route, page, API service, and shared component involved.
2. Verify that a proposed endpoint, feature, dependency, or convention exists before relying on it.
3. Keep the change limited to the requested behavior and preserve existing route, authentication, and catalog/marketplace behavior.
4. Update relevant documentation when an implementation change makes it inaccurate.
5. Do not overwrite existing documentation; read and extend it carefully.

For this documentation set, see [PLAN.md](./PLAN.md) for verified status and proposals, [SKILLS.md](./SKILLS.md) for reusable guidance, and [MEMORY.md](./MEMORY.md) for compact implementation context.
