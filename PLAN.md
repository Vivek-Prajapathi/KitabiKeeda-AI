# KitabiKeeda Project Plan

## Objective

Provide a frontend for discovering courses and supporting learner, instructor, and administrator workflows through a shared learning platform. The repository is the React/Vite frontend; backend services are external.

## Verified Current Status

The following are present in the checked-in frontend code. Their presence does not verify that an external backend is available or that every workflow succeeds end to end.

### Implemented frontend surfaces

- **Public site and account access:** homepage, public course catalog and course detail routes, registration, login, account activation, forgot-password, and reset-password routes.
- **LMS marketplace:** separate marketplace and detail routes, course/category/search API methods, and wishlist-related API methods.
- **Learner area:** authenticated dashboard, profile, profile settings, learning, and order routes.
- **Instructor area:** instructor-protected workspace route and API methods for courses, draft creation, updates, lectures, course submission, students, revenue, and analytics.
- **Administration:** admin-protected routes and pages for overview, analytics, users, courses, LMS marketplace, LMS administration, coupons, orders, notifications, and site layout.
- **Authentication and access gates:** `AuthContext`, `useAuth`, and `ProtectedRoute`, with user, instructor, and administrator checks on the client.
- **API organization:** shared Axios configuration and feature wrappers in `src/api/`.
- **Build and lint commands:** Vite build and Oxlint scripts are declared in `package.json`.

### Not verified or not configured

- No automated test script, test framework, or application test files were found.
- Backend availability, response contracts, CORS, and end-to-end behavior were not tested in this repository review.
- Payment API wrappers exist, but that alone does not establish a configured payment provider or a complete checkout workflow.
- The README documents checkout, instructor image upload, and instructor publishing limitations; confirm these against the current backend and UI before treating them as current runtime defects.

## Architecture

`index.html` loads `src/main.jsx`, which mounts `src/App.jsx`. `src/routes/AppRoutes.jsx` owns the route tree and places it inside `BrowserRouter` and `AuthProvider`. Routes compose the public, user, and admin layouts; selected page routes are lazy-loaded. UI is grouped into shared components, public pages, learner profile pages, and admin pages. API calls use the shared Axios instance and service modules in `src/api/`.

The public catalog uses `courseAPI`; the distinct LMS marketplace and learning workflows use `lmsAPI`. Authentication state is shared through React Context.

## Functional Requirements Reflected in Current Code

- Render public learning and catalog routes without requiring authentication.
- Keep learner, instructor, and administrator route access aligned with the route guards and roles in `AppRoutes.jsx` and `ProtectedRoute.jsx`.
- Route catalog and LMS marketplace requests through their existing API services.
- Preserve account, profile, learning, instructor, and admin surfaces already represented in the route tree.
- Show appropriate loading, success, and error feedback for asynchronous operations, consistent with the relevant page.

These describe current frontend responsibilities; server-side authorization and business rules remain backend responsibilities.

## Non-Functional Requirements for Changes

- Preserve the existing React/Vite application structure and the separation between regular catalog and LMS marketplace.
- Keep changes focused, use existing dependencies, and avoid exposing secrets or personal data.
- Maintain keyboard-accessible controls and responsive behavior when changing UI.
- Treat backend contracts as unverified until confirmed from implementation or an authoritative API source.
- Do not represent a frontend role check as sufficient authorization.

## Roadmap

There is no product backlog or approved feature roadmap recorded in the repository. The following are maintenance and verification proposals, not committed product features.

### Completed (verified in code)

1. **Frontend route and feature surfaces** — public, learner, instructor, marketplace, and administration routes are defined in `src/routes/AppRoutes.jsx`.
2. **Centralized API layer** — Axios configuration and service modules are present in `src/api/`.
3. **Shared authentication state and route guards** — implemented in `src/context/AuthContext.jsx` and `src/components/ProtectedRoute.jsx`.
4. **Build and lint entry points** — `npm run build` and `npm run lint` are declared in `package.json`.

### Pending / proposed

1. **Confirm backend/API contracts and runtime integration** — compare each used endpoint and response shape with the maintained backend specification and verify against an approved non-production environment. This requires authoritative backend access; it has not been validated here.
2. **Decide on an automated test strategy** — first identify the desired coverage and obtain approval for any required tooling; then add tests for the agreed behaviors. No test runner is currently configured.
3. **Prioritize future product work** — obtain explicit product requirements before adding features. No additional feature work is inferred from this plan.

### Dependencies

- Backend integration verification depends on an authoritative API contract and an authorized test environment.
- Automated test implementation depends on an approved test scope and (if needed) an approved test-tooling decision.
- Product implementation depends on a user-approved feature requirement; there is no inferred feature dependency graph.

## Implementation Steps for Future Changes

1. Identify the affected route, page, shared component, state owner, and API wrapper.
2. Confirm any backend request/response contract before changing API behavior.
3. Implement within the existing feature boundaries and preserve authentication and error/loading behavior.
4. Run relevant available checks (`npm run lint`, `npm run build`) and exercise affected flows where an authorized environment is available.
5. Update the README or AI-agent docs only when verified project behavior or decisions change.

## Validation Strategy

- Run `npm run lint` for configured lint rules.
- Run `npm run build` to validate the production bundle.
- There is no configured automated test command. Do not report automated test coverage until a test setup exists and tests have been run.
- Validate API-dependent flows only with a configured, authorized backend; do not infer success from a successful frontend build.
