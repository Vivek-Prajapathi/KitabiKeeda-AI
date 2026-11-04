# Reusable Coding Skills for KitabiKeeda

This guide separates observed project patterns from recommendations. General recommendations below are guidance, not claims that a tool or feature is already configured.

## React Development

- **When to use:** Any work that changes the UI, data flow, or rendered behavior.
- **Project-specific:** The app uses React 19 function components and JSX. The route tree is in `src/routes/AppRoutes.jsx`; reusable UI is in `src/components/` and feature folders.
- **Recommended approach:** Trace the current component and its callers before changing it. Keep state near its consumers unless it is shared application state.
- **Coding standards:** Follow the neighboring component's imports, formatting, and export style; use descriptive component names.
- **Common mistakes:** Duplicating an existing component, moving unrelated behavior into a shared component, or changing the catalog and marketplace as though they were one feature.
- **Best practices:** Keep rendering declarative, preserve loading/empty/error states, and use existing shared layouts and components where appropriate.

## JavaScript and TypeScript

- **When to use:** Any application logic or API contract work.
- **Project-specific:** Application code is JavaScript (`.js`/`.jsx`); no TypeScript application source was found. Type declaration packages in dependencies do not mean app code is TypeScript.
- **Recommended approach:** Preserve the existing JavaScript codebase unless a task explicitly calls for a migration.
- **Coding standards:** Use clear camelCase identifiers for values and functions; inspect the local file for semicolon and formatting style.
- **Common mistakes:** Assuming TypeScript types or interfaces exist, or adding a TypeScript configuration as an incidental change.
- **Best practices:** Validate untrusted API data at use sites and handle optional response fields explicitly.
- **General recommendation:** Prefer small, readable functions and avoid implicit coercions when handling API data.

## Component Development

- **When to use:** Adding or changing UI elements or pages.
- **Project-specific:** Shared UI lives in `src/components/`; public pages in `src/pages/`; learner pages in `src/profile/`; admin pages in `src/admin/pages/`.
- **Recommended approach:** Search for an existing component and its styles first. Use React Router navigation for internal links.
- **Coding standards:** Keep filenames and component names descriptive and PascalCase; use semantic HTML and accessible names for interactive controls.
- **Common mistakes:** Duplicating cards/navigation, using plain anchors for app-local routes, or introducing a new component layer without need.
- **Best practices:** Keep components focused, preserve existing responsive behavior, and provide useful loading, empty, and failure states.

## React Hooks

- **When to use:** Local state, lifecycle synchronization, memoization, or reusable stateful logic.
- **Project-specific:** Pages use `useState`, `useEffect`, and, where useful, `useMemo`/`useCallback`; authentication is accessed through `useAuth`.
- **Recommended approach:** Follow the existing page's approach and keep effect dependencies accurate.
- **Coding standards:** Call hooks at the top level of function components or custom hooks. Name custom hooks with the `use` prefix.
- **Common mistakes:** Conditional hook calls, stale effect dependencies, or starting asynchronous work without considering unmount cleanup.
- **Best practices:** Cancel or ignore obsolete requests where the surrounding code does so; avoid memoization unless it improves a measured or clear repeated computation.

## Routing

- **When to use:** Adding or changing a navigable screen or access rule.
- **Project-specific:** `src/routes/AppRoutes.jsx` uses React Router 7, nested layouts, `Suspense` for selected lazy routes, and `ProtectedRoute` for learner, instructor, and admin access.
- **Recommended approach:** Add routes to the existing tree and retain the correct layout and guard.
- **Coding standards:** Use `Link`/`Navigate` and route parameters as the existing route structure does.
- **Common mistakes:** Adding a route outside the intended layout, weakening a role guard, or confusing `/courses` with `/marketplace`.
- **Best practices:** Check direct navigation, refresh behavior, access-denied behavior, and fallback rendering when validating route changes.

## State Management

- **When to use:** Choosing where new UI or shared data state belongs.
- **Project-specific:** `AuthContext` is the shared authentication state. Feature and page data generally use local React state.
- **Recommended approach:** Use local state for page-specific concerns and `useAuth` for the established authentication interface.
- **Coding standards:** Keep state updates predictable and preserve existing response/loading state patterns.
- **Common mistakes:** Creating a parallel global store, putting unrelated page state into authentication context, or assuming cached user data is authoritative.
- **Best practices:** Treat server data as asynchronous and potentially absent or stale; let the backend remain authoritative for permissions.

## API Integration with Axios

- **When to use:** Reading or changing data served by the backend.
- **Project-specific:** Use `src/api/axios.js` and the relevant wrapper: `auth.js`, `course.js`, `lms.js`, `admin.js`, `analytics.js`, or `notification.js`. The base URL comes from `VITE_API_BASE_URL` or the fallback configured in `axios.js`.
- **Recommended approach:** Inspect both the service method and its call site before changing a request or interpreting its response.
- **Coding standards:** Keep request methods in the relevant API service and use the shared Axios instance.
- **Common mistakes:** Inventing an endpoint, bypassing interceptors with a new client, or treating an API wrapper as proof that the server workflow is live.
- **Best practices:** Handle rejected requests and unsuccessful response payloads; do not silently replace failures with apparently valid data.

## Authentication and Authorization

- **When to use:** Login, account state, or protected-page work.
- **Project-specific:** `AuthContext` exposes login, registration, activation, logout, and user update operations. `ProtectedRoute` checks authentication and instructor/admin role flags. Axios adds the stored access token and attempts refresh handling.
- **Recommended approach:** Reuse `useAuth`, the existing auth API service, and the route guard.
- **Coding standards:** Never print or embed tokens. Keep client-side redirects consistent with existing role behavior.
- **Common mistakes:** Treating local storage or a client-side route guard as secure authorization, or adding a second token store.
- **Best practices:** Enforce permissions on the backend, use only approved API environments, and handle expired-session behavior without exposing credentials.

## Form Handling and Validation

- **When to use:** Account, course, category, or settings forms.
- **Project-specific:** Forms currently use React-controlled inputs and local component state; no form library is configured.
- **Recommended approach:** Follow the form in the same feature and validate required fields before sending the request.
- **Coding standards:** Use labels associated with controls, appropriate input types, and visible loading/error feedback.
- **Common mistakes:** Adding a form dependency without need, relying only on browser validation, or assuming client validation replaces backend validation.
- **Best practices:** Preserve entered values on recoverable errors and prevent duplicate submissions while requests are in progress.

## Error Handling

- **When to use:** Any asynchronous API interaction or user-submitted operation.
- **Project-specific:** Pages use a mix of inline error states, Sonner toasts, and `console.error` in caught failures.
- **Recommended approach:** Match the relevant feature's existing feedback pattern and distinguish loading, success, empty, and failed states.
- **Coding standards:** Show a useful user-facing message and retain enough contextual logging for diagnosis without logging sensitive payloads.
- **Common mistakes:** Swallowing errors, reporting success after a failed request, or displaying raw internal details to users.
- **Best practices:** Handle both rejected HTTP requests and error-shaped API responses when the service uses both.

## CSS and Responsive Design

- **When to use:** Any visual or layout change.
- **Project-specific:** The project combines Tailwind utility classes and custom CSS; global styles are in `src/index.css`, and feature pages may use their own class names.
- **Recommended approach:** Inspect the closest existing styles and preserve their responsive and visual behavior.
- **Coding standards:** Reuse existing design tokens/classes where present and keep selectors scoped to the feature.
- **Common mistakes:** Adding a new styling framework, using global selectors that affect unrelated pages, or assuming an empty `src/styles/` folder contains an established system.
- **Best practices:** Check narrow and wide layouts, focus visibility, semantic structure, and accessible contrast when changing UI.

## Debugging

- **When to use:** Unexpected rendering, routing, state, or API behavior.
- **Project-specific:** Start with the route in `src/routes/AppRoutes.jsx`, the consuming page, and the relevant service in `src/api/`; inspect `AuthContext` when auth state is involved.
- **Recommended approach:** Reproduce the behavior, follow the request/state path, and verify response assumptions against actual code or an authoritative backend contract.
- **Coding standards:** Keep diagnostic logging temporary and avoid logging credentials or personal data.
- **Common mistakes:** Guessing at backend behavior from UI copy, or fixing symptoms without tracing the request and state owner.
- **Best practices:** Validate the smallest relevant change with the available lint/build scripts and a permitted runtime environment.

## Testing

- **When to use:** Verifying a code change or a reported defect.
- **Project-specific:** `npm run lint` and `npm run build` are configured. No automated test runner, test script, or application test files were found.
- **Recommended approach:** Run the relevant configured checks; manually verify affected flows when an authorized backend/environment is available.
- **Coding standards:** Report exactly which checks were run and their outcomes.
- **Common mistakes:** Claiming automated tests passed when no test command ran, or treating a successful build as proof of API behavior.
- **Best practices:** Propose test tooling only when needed and obtain approval before adding dependencies or configuration.

## Git and Version Control

- **When to use:** Preparing or reviewing repository changes.
- **Project-specific:** No project-specific branch, commit-message, or release convention was found during this review.
- **Recommended approach:** Inspect the worktree before editing and review the diff afterward; stage only task-related files.
- **Coding standards:** Keep commits and changes focused; do not rewrite history or discard unrelated work.
- **Common mistakes:** Including `.env` or generated output, or assuming a commit convention not documented in this repository.
- **Best practices:** Keep secrets out of Git, check `.gitignore`, and make the scope of each change clear.
- **General recommendation:** Use a feature branch and a descriptive commit message when that matches the contributor's workflow.
