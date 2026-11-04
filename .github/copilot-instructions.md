# Copilot Instructions

KitabiKeeda is a React 19 / JavaScript JSX frontend built with Vite 8. Its public catalog (`courseAPI`) and LMS marketplace (`lmsAPI`) are separate; preserve that boundary. Routes are defined in `src/routes/AppRoutes.jsx`, authentication state in `src/context/AuthContext.jsx`, and shared Axios configuration and API wrappers in `src/api/`.

- Before editing, inspect the relevant route, page, component, API service, and nearby styles. Do not infer backend contracts or features that are not in the code.
- Follow existing React Hook, component, naming, and styling patterns. Reuse shared components, layouts, `useAuth`, and the shared Axios client where appropriate.
- Keep role checks and route boundaries intact; client-side guards do not replace backend authorization.
- Preserve loading, empty, and error feedback. Never hide API failures or expose tokens, credentials, or personal data in logs or source.
- Avoid unrelated edits, new dependencies, and changes to package manifests unless the task explicitly requires them.
- Run relevant configured checks (`npm run lint`, `npm run build`). No automated test setup is currently configured; do not claim tests were run if they were not.
- Consult [AGENTS.md](../AGENTS.md) for full project rules, [PLAN.md](../PLAN.md) for verified status and proposals, [SKILLS.md](../SKILLS.md) for reusable coding practices, and [MEMORY.md](../MEMORY.md) for concise architecture and API context when relevant. Read [README.md](../README.md) for existing product documentation.
