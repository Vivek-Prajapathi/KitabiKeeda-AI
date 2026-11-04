# KitabiKeeda Project Memory

Concise, code-grounded context for future agents. Update only when a significant implementation decision or project change is verified. Never add personal data, credentials, tokens, or secret values.

## Purpose and Stack

- React 19 / JavaScript JSX frontend for KitabiKeeda's public course catalog, LMS marketplace, learner area, instructor workspace, and admin UI.
- Vite 8, React Router 7, Axios, React Context, Tailwind CSS 4/custom CSS, Lucide React, Sonner, Recharts, and Oxlint.
- The backend is external. `src/api/axios.js` reads `VITE_API_BASE_URL`; its fallback is `https://mockapi-mauve.vercel.app/api/v1`.

## Architecture and Existing Patterns

- `index.html` → `src/main.jsx` → `src/App.jsx` → `src/routes/AppRoutes.jsx`.
- `AppRoutes` wraps the route tree in `BrowserRouter` and `AuthProvider`; shared layouts are under `src/layouts/`, reusable UI under `src/components/`.
- Public and account pages are in `src/pages/`; learner profile pages are in `src/profile/`; admin pages are in `src/admin/pages/`.
- `src/context/AuthContext.jsx` owns auth state and methods; `src/hooks/useAuth.js` re-exports the hook. `ProtectedRoute` gates learner, instructor, and admin routes on the client.
- Shared requests use `src/api/axios.js`; API wrappers are separated by auth, regular course, LMS, admin, analytics, and notification responsibility.
- The `/courses` catalog uses `courseAPI`; `/marketplace` and LMS learning workflows use `lmsAPI`. Keep this distinction.
- UI code is JavaScript/JSX with function components, React Hooks, Tailwind utility classes, and custom CSS.

## API Endpoints Present in Source

These are frontend request paths, not a verified backend contract. The base URL is configured separately as described above; dynamic path segments are shown with `:id`-style placeholders.

- **Auth (`src/api/auth.js`):** `POST /auth/register`, `/auth/activate-user`, `/auth/login`, `/auth/social-auth`, `/auth/forgot-password`, `/auth/reset-password`; `GET /auth/logout`, `/auth/me`, `/auth/get-all-user-dashboard`; `PUT /auth/update-user-info`, `/auth/update-user-password`, `/auth/update-user-profile-picture`, `/auth/update-user-roles`; `DELETE /auth/delete-user/:id`. The Axios refresh interceptor calls `GET /auth/refreshtoken`.
- **Regular courses (`src/api/course.js`):** `POST /course/create-course`; `PUT /course/edit-course/:id`, `/course/add-question`, `/course/add-answer`, `/course/add-review/:id`, `/course/add-replay`; `GET /course/get-course/:id`, `/course/get-courses`, `/course/get-course-content/:id`, `/course/get-all-course-dashboard`; `DELETE /course/delete-course/:id`.
- **LMS public/learner (`src/api/lms.js`):** `GET /lms/courses`, `/lms/my-learning`, `/lms/categories`, `/lms/search`, `/lms/home`, `/lms/courses/:courseId`, `/lms/courses/:courseId/curriculum`, `/lms/courses/:courseId/sections`, `/lms/sections/:sectionId`, `/lms/sections/:sectionId/lectures`, `/lms/lectures/:lectureId`, `/lms/lectures/:lectureId/access`, `/lms/purchases`, `/lms/orders`, `/lms/orders/:orderId`, `/lms/enrollments`, `/lms/enrollments/:enrollmentId`, `/lms/wishlist`, `/lms/reviews/:courseId`, `/lms/certificates`, `/lms/certificates/:certificateId`, `/lms/certificates/:certificateId/download`; `POST /lms/payments/create`, `/lms/payments/verify`, `/lms/lectures/:lectureId/progress`, `/lms/lectures/:lectureId/complete`, `/lms/wishlist/toggle`, `/lms/reviews/:courseId`, `/lms/coupons/validate`, `/lms/payments/refund`; search passes query parameter `q`.
- **LMS categories (`src/api/lms.js`):** `POST /lms/categories`; `GET /lms/categories/all`; `PUT /lms/categories/:categoryId`; `DELETE /lms/categories/:categoryId`.
- **Instructor (`src/api/lms.js`):** `GET /lms/instructor/courses`, `/lms/instructor/students`, `/lms/instructor/revenue`, `/lms/instructor/analytics`; `POST /lms/instructor/courses`, `/lms/instructor/courses/:courseId/lectures`, `/lms/instructor/courses/:courseId/submit`; `PUT /lms/instructor/courses/:courseId`.
- **LMS admin (`src/api/lms.js`):** `GET /lms/admin/courses`, `/lms/admin/instructors`, `/lms/admin/orders`, `/lms/admin/enrollments`, `/lms/admin/analytics`, `/lms/admin/enrollments/export`, `/lms/progress-analytics`; `PUT /lms/admin/courses/:courseId/status`; `POST /lms/courses/clone`.
- **Other admin services:** `src/api/admin.js` also defines `GET /order/get-all-order-dashboard`, `/notifications/get-all-notification`, `/analytics/get-users-analytics`, `/analytics/get-course-analytics`, `/analytics/get-order-analytics`, `/layout/get-layout?type=...`; `PUT /notifications/update-notification-status/:id`, `/layout/update-layout`; `POST /layout/create-layout`. `src/api/analytics.js` and `src/api/notification.js` expose subsets of those analytics and notification paths.

## Authentication Flow

`AuthContext` initializes from `localStorage` and verifies an existing session using `authAPI.getMe()`. Login stores the returned user and access token. Logout calls the API and clears local state/storage. The shared Axios client attaches the stored access token and has a refresh-token retry path. Do not treat browser-stored role/user data or client-side guards as server authorization.

## Known Gaps and Pending Verification

- `package.json` has `dev`, `build`, `lint`, and `preview` scripts; no test script, test framework, or application test files were found.
- Backend endpoint contracts and live integration have not been independently verified.
- Payment request methods exist, but they do not prove a complete checkout or payment-provider integration.
- `README.md` documents checkout, instructor image upload, and direct instructor publishing limitations. Recheck the live integration before relying on these notes.
- No product backlog or additional implementation decisions were found in the repository review.

## Update Policy

Change this document only after a significant project decision or implementation change has been verified in source. Keep endpoint information synchronized with `src/api/` and never add secrets from local environment files.
