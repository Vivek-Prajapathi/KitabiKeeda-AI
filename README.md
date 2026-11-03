# 📚 KitabiKeeda – Online Learning Management Platform

A modern, responsive Learning Management System (LMS) built with **React 19**, designed to connect students, instructors, and administrators through a unified learning ecosystem.

🌐 **Live Demo:** https://kitabi-keeda-frontend-using-ai-8yej.vercel.app/

📂 **GitHub Repository:** https://github.com/Vivek-Prajapathi/KitabiKeeda-Frontend-using-AI

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Platform Modules](#-platform-modules)
- [Technology Stack](#-technology-stack)
- [Application Architecture](#-application-architecture)
- [Getting Started](#-getting-started)
- [Environment Configuration](#-environment-configuration)
- [Available Scripts](#-available-scripts)
- [Application Routes](#-application-routes)
- [API Integration](#-api-integration)
- [Authentication and Authorization](#-authentication-and-authorization)
- [Design System](#-design-system)
- [Deployment](#-deployment)
- [AI-Assisted Development](#-ai-assisted-development)
- [Known Limitations](#-known-limitations)
- [Contributing](#-contributing)
- [Developer](#-developer)

---

## 🚀 Overview

KitabiKeeda is an educational platform that provides different experiences based on user roles and learning requirements.

The platform combines:

- A public educational website.
- An online course catalog.
- A dedicated LMS Marketplace.
- Student learning dashboards.
- Instructor workspace.
- Administrative management tools.

The frontend communicates with the KitabiKeeda backend through centralized Axios services, supporting authentication, course management, learning activities, and role-based access control.

---

## ✨ Key Features

### 🌐 Public Website

- Responsive homepage with featured courses.
- Course discovery and category-based filtering.
- Public course catalog and detailed course information.
- Course pricing, curriculum, and tags.
- User registration and login.
- Account activation.
- Forgot password and password reset functionality.
- Responsive navigation and account controls.

### 🎓 Student Dashboard

- Protected student dashboard.
- Student profile and account settings.
- My Learning section.
- Course progress tracking.
- Certificate viewing and downloading.
- Purchase history.
- Order management.
- Wishlist viewing and management.

### 🛍️ LMS Marketplace

- Dedicated LMS course marketplace.
- API-driven course listings.
- Course search and category filtering.
- Individual LMS course details.
- Wishlist functionality.
- Role-based navigation.
- Separate LMS layouts and routes.
- Navigation between the main website and LMS Marketplace.

### 👨‍🏫 Instructor Workspace

- Protected instructor dashboard.
- Draft course creation and editing.
- Lesson creation and management.
- Course submission for review.
- Student enrollment information.
- Analytics and revenue information.

### 🛡️ Admin Dashboard

- Administrative overview and analytics.
- User management.
- Regular course management.
- LMS course lifecycle management.
- Instructor and enrollment management.
- Order management.
- Coupon management.
- Notification management.
- Site content management.
- CSV export for supported LMS data.
- Role-based access protection.

---

## 🧩 Platform Modules

KitabiKeeda provides two separate course experiences.

| Feature | Public Course Catalog | LMS Marketplace |
|---|---|---|
| Route | `/courses` | `/marketplace` |
| API Service | `courseAPI` | `lmsAPI` |
| Course Details | `/courses/:id` | `/marketplace/:id` |
| Purpose | Regular public courses | LMS-based learning marketplace |

**Important:** The Public Course Catalog and LMS Marketplace are independent features with separate routes, API services, and layouts.

- Use **Courses** to access the regular course catalog.
- Use **LMS Marketplace** to explore LMS courses.
- Use **Back to Site Home** to return to the main website.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| React 19 | Component-based UI development |
| JavaScript | Application logic |
| Vite 8 | Development server and build tooling |
| React Router 7 | Client-side routing |
| Axios | HTTP requests and API communication |
| Context API | Global authentication state |
| Tailwind CSS 4 | Utility-first styling |
| Custom CSS | Component and page styling |
| Lucide React | Icons |
| Sonner | Toast notifications |
| Recharts | Analytics visualizations |
| Oxlint | Code linting |

---

## 🏗️ Application Architecture

The application follows a modular frontend architecture that separates components, layouts, routing, authentication, API services, and feature-specific pages.

### Project Structure

```text
KitabiKeeda/
│
├── public/
│   └── Static files and public assets
│
├── src/
│   │
│   ├── admin/
│   │   └── pages/
│   │       └── Admin dashboard and management pages
│   │
│   ├── api/
│   │   ├── axios.js
│   │   ├── auth.js
│   │   ├── course.js
│   │   ├── lms.js
│   │   ├── admin.js
│   │   ├── analytics.js
│   │   └── notification.js
│   │
│   ├── assets/
│   │
│   ├── components/
│   │   └── Shared UI and route protection
│   │
│   ├── context/
│   │   └── Authentication context
│   │
│   ├── hooks/
│   │
│   ├── layouts/
│   │   └── Public, student and admin layouts
│   │
│   ├── pages/
│   │   └── Public pages, Marketplace and instructor workspace
│   │
│   ├── profile/
│   │   └── Student profile, orders and My Learning
│   │
│   ├── routes/
│   │   └── React Router configuration
│   │
│   ├── styles/
│   │
│   ├── App.jsx
│   ├── index.css
│   └── main.jsx
│
├── .env.example
├── index.html
├── package.json
├── postcss.config.js
├── tailwind.config.js
└── vite.config.js
```

### API Service Organization

API communication is centralized inside `src/api/`.

| File | Responsibility |
|---|---|
| `axios.js` | Shared Axios instance, base URL, authentication headers and refresh-token handling |
| `auth.js` | Authentication and account operations |
| `course.js` | Public and admin course operations |
| `lms.js` | LMS Marketplace, student learning and instructor operations |
| `admin.js` | Administrative API operations |
| `analytics.js` | Analytics-related operations |
| `notification.js` | Notification-related operations |

This separation keeps network requests organized and improves application maintainability.

---

## ⚙️ Getting Started

Follow these instructions to run KitabiKeeda locally.

### Prerequisites

Make sure you have installed:

- Node.js `20.19+` or `22.12+`
- npm
- Git
- Access to a compatible KitabiKeeda backend API

### 1. Clone the Repository

```bash
git clone https://github.com/Vivek-Prajapathi/KitabiKeeda-Frontend-using-AI.git
```

### 2. Navigate to the Project

```bash
cd KitabiKeeda-Frontend-using-AI
```

### 3. Install Dependencies

```bash
npm install
```

### 4. Configure Environment Variables

```bash
cp .env.example .env
```

Add your backend API URL to the `.env` file.

### 5. Start the Development Server

```bash
npm run dev
```

### 6. Open the Application

Visit:

```text
http://localhost:5173
```

The application will now be available in your browser.

---

## 🔐 Environment Configuration

The application uses environment variables to configure backend communication.

Create a `.env` file in the project root.

| Variable | Required | Description |
|---|---|---|
| `VITE_API_BASE_URL` | No | Backend API base URL, including the API path prefix |

Example:

```env
VITE_API_BASE_URL=https://your-backend-api.example.com/api/v1
```

If this variable is not configured, the application uses the following default API endpoint:

```text
https://mockapi-mauve.vercel.app/api/v1
```

**Security Notes:**

- Never commit your `.env` file.
- Never expose private API credentials or secrets.
- Vite exposes `VITE_` environment variables to browser-side code.
- Ensure that the backend allows requests from your frontend origin through its CORS configuration.

---

## 📜 Available Scripts

Run the following commands from the project directory.

| Command | Description |
|---|---|
| `npm run dev` | Starts the development server |
| `npm run build` | Generates the production build |
| `npm run preview` | Previews the production build locally |
| `npm run lint` | Runs Oxlint to check the code |

Build the application:

```bash
npm run build
```

The optimized production files are generated inside the `dist/` directory.

**Note:** A test script is not currently configured in `package.json`.

---

## 🛣️ Application Routes

The application uses React Router 7 for client-side navigation and protected routes.

### Public Routes

| Route | Description |
|---|---|
| `/` | Main homepage |
| `/courses` | Public course catalog |
| `/courses/:id` | Public course details |
| `/login` | User login |
| `/register` | User registration |
| `/activate-account` | Account activation |
| `/forgot-password` | Password recovery request |
| `/reset-password` | Password reset |
| `/reset-password/:token` | Token-based password reset |

### Student Routes

These routes require authentication.

| Route | Description |
|---|---|
| `/dashboard` | Student dashboard |
| `/dashboard/profile` | Student profile |
| `/dashboard/profile/settings` | Profile settings |
| `/dashboard/profile/my-learning` | My Learning |
| `/dashboard/orders` | Order history |

My Learning supports the following query parameters:

```text
?tab=courses
?tab=progress
?tab=certificates
?tab=purchases
?tab=wishlist
```

### LMS and Instructor Routes

| Route | Description | Access |
|---|---|---|
| `/marketplace` | LMS Marketplace | Public |
| `/marketplace/:id` | LMS course details | Public |
| `/instructor` | Instructor workspace | Instructor / Admin |

### Admin Routes

All the following routes require administrator access.

| Route | Description |
|---|---|
| `/admin` | Admin overview |
| `/admin/analytics` | Admin analytics |
| `/admin/users` | User management |
| `/admin/courses` | Course management |
| `/admin/courses/create` | Create a course |
| `/admin/courses/edit/:id` | Edit a course |
| `/admin/marketplace` | LMS course lifecycle management |
| `/admin/lms-admin` | LMS administration |
| `/admin/coupons` | Coupon management |
| `/admin/orders` | Order management |
| `/admin/notifications` | Notification management |
| `/admin/layout` | Site content management |

---

## 🔒 Authentication and Authorization

KitabiKeeda implements authentication and role-based authorization to control access to protected pages.

The application uses:

- React Context API for shared authentication state.
- Axios for backend communication.
- Centralized API services.
- Protected routes.
- Role-based route authorization.
- Authentication-aware navigation.

### Access Control

| User Role | Access |
|---|---|
| Public User | Public website and course catalogs |
| Student | Student dashboard and learning features |
| Instructor | Instructor workspace |
| Admin | Administration modules and authorized instructor features |

Unauthenticated users are redirected to the login page when accessing protected routes.

Users without the required role are redirected to the student dashboard.

---

## 🎨 Design System

KitabiKeeda uses a consistent visual identity built around violet, navy, and neutral colors.

Shared design tokens are maintained in `src/index.css`.

| Color | Hex Code | Usage |
|---|---|---|
| Primary Violet | `#6d5ce7` | Primary actions and highlights |
| Deep Navy | `#172554` | Headings and navigation |
| Light Violet | `#eeeafe` | Highlighted surfaces |
| Background | `#f7f8fc` | Page backgrounds |
| Main Text | `#172033` | Primary content |
| Muted Text | `#667085` | Secondary content |
| Border | `#e5e7eb` | Dividers and borders |

The LMS uses scoped styling to avoid unintended changes to public website and administration components.

---

## 🚀 Deployment

KitabiKeeda is deployed using **Vercel**.

### Live Deployment

**Production URL:**

https://kitabi-keeda-frontend-using-ai-8yej.vercel.app/

### Deployment Configuration

| Setting | Value |
|---|---|
| Hosting Platform | Vercel |
| Framework | Vite |
| Build Command | `npm run build` |
| Output Directory | `dist` |
| Install Command | `npm install` |

### Deploy Your Own Version

1. Push the project to GitHub.
2. Log in to Vercel using your GitHub account.
3. Import the project repository.
4. Select Vite as the framework preset.
5. Configure the required environment variables.
6. Configure the production build settings.
7. Click Deploy.

### React Router Configuration

For client-side routing, add a `vercel.json` file in the project root:

```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

This allows React Router to handle application routes when users directly open or refresh a page.

### Continuous Deployment

Vercel can automatically redeploy the application when new changes are pushed to the connected GitHub repository.

For production deployments, ensure that:

- The correct production API URL is configured.
- Backend CORS allows the deployed frontend domain.
- The application builds successfully.
- Protected routes and authentication work correctly.
- The application is served over HTTPS.

**Important:** This repository contains the frontend. The backend API must be hosted and accessible separately.

---

## 🤖 AI-Assisted Development

KitabiKeeda was developed with assistance from modern AI-powered development tools.

### Devin AI

Used to assist with larger implementation tasks, exploring the existing application, frontend redesign requirements, and refining features across the public website and LMS.

### GitHub Copilot

Used for code suggestions, component development, styling improvements, and documentation assistance.

AI-generated suggestions and code were reviewed, tested, and integrated as part of the development process.

AI tools assisted with development; they do not replace project authorship, review, or responsibility for the final implementation.

---

## ⚠️ Known Limitations

The following limitations depend on the current frontend and backend integration:

1. **Checkout:** The course details interface currently reports that checkout is unavailable. Having payment-related API methods does not automatically configure a payment provider or complete the checkout workflow.

2. **Instructor Image Upload:** Instructor course image upload is not exposed as a supported workflow in the current integration.

3. **Course Publishing:** The instructor workflow supports draft creation, editing, lesson creation, and submission for review. Direct publishing is not exposed as a supported instructor workflow.

4. **Incomplete Backend Data:** Some purchase and order amounts or statuses may not be returned by the backend. The frontend does not fabricate missing information.

5. **Backend Dependencies:** LMS analytics, course information, and administrative data depend on backend availability and the permissions of the authenticated user.

---

## 🤝 Contributing

Contributions and improvements are welcome.

Follow these steps when working on the project:

1. Create a feature branch.
2. Keep changes focused on the requested functionality.
3. Follow the existing component, API, routing, and CSS conventions.
4. Preserve backend API contracts and authorization checks.
5. Maintain the separation between the public course catalog and LMS Marketplace.
6. Run the available checks before submitting changes.

```bash
npm run lint
npm run build
```

7. Include a clear description of the changes in your pull request.
8. Add screenshots for significant UI changes where useful.

---

## 👨‍💻 Developer

**Vivek Prajapathi**

- GitHub: [@Vivek-Prajapathi](https://github.com/Vivek-Prajapathi)
- Repository: [KitabiKeeda – Frontend](https://github.com/Vivek-Prajapathi/KitabiKeeda-Frontend-using-AI)
- Live Application: [KitabiKeeda](https://kitabi-keeda-frontend-using-ai-8yej.vercel.app/)

---

**📚 KitabiKeeda – Making Learning More Accessible.**