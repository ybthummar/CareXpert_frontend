# CareXpert Frontend

**CareXpert** is a full-featured healthcare platform that connects patients with doctors for seamless appointment booking, real-time chat, video consultations, prescription management, and more. This repository contains the frontend client built with React, TypeScript, and Vite.

> Part of the **GDG CHARUSAT Open Source Contri Sprintathon**

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Install Dependencies](#2-install-dependencies)
  - [3. Set Up Environment Variables](#3-set-up-environment-variables)
  - [4. Start the Development Server](#4-start-the-development-server)
- [Available Scripts](#available-scripts)
- [Environment Variables](#environment-variables)
- [Folder Structure](#folder-structure)
- [Contributing](#contributing)
- [Code of Conduct](#code-of-conduct)
- [License](#license)

---

## Features

- **Patient Dashboard** — View upcoming appointments, health reports, and prescriptions
- **Doctor Dashboard** — Manage appointments, pending requests, and patient records
- **Appointment Booking** — Search doctors and book appointments with ease
- **Real-Time Chat** — Socket.io–powered messaging between patients and doctors
- **Video Consultations** — In-browser video calls via VideoSDK
- **Prescription Management** — Doctors can issue prescriptions; patients can view/download them
- **Report Uploads** — Patients can upload medical reports for doctor review
- **Notifications** — Real-time notification system for appointment updates
- **Admin Panel** — Platform administration and oversight
- **Dark Mode** — Full light/dark theme support
- **Responsive Design** — Mobile-friendly UI across all pages

---

## Tech Stack

| Category            | Technology                                                  |
| ------------------- | ----------------------------------------------------------- |
| **Framework**       | [React 18](https://react.dev/) with TypeScript              |
| **Build Tool**      | [Vite 5](https://vitejs.dev/)                               |
| **Styling**         | [Tailwind CSS 3](https://tailwindcss.com/)                  |
| **UI Components**   | [shadcn/ui](https://ui.shadcn.com/) (Radix UI primitives)   |
| **Routing**         | [React Router v6](https://reactrouter.com/)                 |
| **State Management**| [Zustand](https://zustand-demo.pmnd.rs/)                    |
| **Forms**           | [React Hook Form](https://react-hook-form.com/) + [Zod](https://zod.dev/) |
| **HTTP Client**     | [Axios](https://axios-http.com/)                            |
| **Real-Time**       | [Socket.io Client](https://socket.io/)                      |
| **Video Calls**     | [VideoSDK](https://www.videosdk.live/)                       |
| **Animations**      | [Framer Motion](https://www.framer.com/motion/)             |
| **Charts**          | [Recharts](https://recharts.org/)                            |
| **Icons**           | [Lucide React](https://lucide.dev/)                          |
| **Package Manager** | [pnpm](https://pnpm.io/)                                    |

---

## Prerequisites

Ensure you have the following installed before proceeding:

- **[Node.js](https://nodejs.org/)** — v18 or higher
- **[pnpm](https://pnpm.io/installation)** — install globally via:
  ```bash
  npm install -g pnpm
  ```
- **[Git](https://git-scm.com/)**

> ⚠️ **This project uses `pnpm` exclusively.** Do not use `npm install` or `yarn`. Using the wrong package manager will generate an incorrect lockfile and your PR will be rejected.

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/gdg-charusat/CareXpert_frontend.git
cd CareXpert_frontend
```

If you are contributing, fork the repository first and clone your fork:

```bash
git clone https://github.com/<YOUR-USERNAME>/CareXpert_frontend.git
cd CareXpert_frontend
git remote add upstream https://github.com/gdg-charusat/CareXpert_frontend.git
```

### 2. Install Dependencies

```bash
pnpm install
```

### 3. Set Up Environment Variables

Create a `.env` file in the project root:

```bash
cp .env.example .env   # if an example file exists, otherwise create manually
```

Add the following variables to your `.env` file:

```env
VITE_BASE_URL=<backend-api-url>
VITE_SOCKET_URL=<socket-server-url>
```

| Variable          | Description                                           |
| ----------------- | ----------------------------------------------------- |
| `VITE_BASE_URL`   | Base URL of the CareXpert backend API (e.g. `http://localhost:5000`) |
| `VITE_SOCKET_URL` | URL of the Socket.io server for real-time features    |

> 🔐 **Need credentials?** If your assigned issue requires API keys or secrets, contact the maintainers privately — **never** commit secrets or request them in public issues/PRs. See [CONTRIBUTING.md](CONTRIBUTING.md) for contact details.

### 4. Start the Development Server

```bash
pnpm dev
```

The app will be available at **http://localhost:5173** (default Vite port).

---

## Available Scripts

| Command          | Description                              |
| ---------------- | ---------------------------------------- |
| `pnpm dev`       | Start the Vite development server        |
| `pnpm build`     | Type-check with `tsc` and build for production |
| `pnpm preview`   | Preview the production build locally     |
| `pnpm lint`      | Run ESLint on `src/` (TypeScript files)  |

---

## Environment Variables

All environment variables must be prefixed with `VITE_` to be exposed to the client (this is a [Vite requirement](https://vitejs.dev/guide/env-and-mode.html)).

Type definitions for environment variables are located in [`src/vite-env.d.ts`](src/vite-env.d.ts). When adding a new variable, update this file to maintain type safety:

```typescript
interface ImportMetaEnv {
  readonly VITE_BASE_URL: string;
  readonly VITE_SOCKET_URL: string;
  // add new variables here
}
```

---

## Folder Structure

```
CareXpert_frontend/
├── public/                  # Static assets served as-is
├── src/
│   ├── components/          # Reusable React components
│   │   ├── ui/              # shadcn/ui primitives (Button, Card, Dialog, etc.)
│   │   ├── navbar.tsx       # Top navigation bar
│   │   ├── sidebar.tsx      # Dashboard sidebar navigation
│   │   ├── footer.tsx       # Site footer
│   │   ├── layout.tsx       # Public page layout wrapper
│   │   ├── DashboardLayout.tsx  # Authenticated dashboard layout
│   │   ├── ai-chat-box.tsx  # AI-powered chat assistant widget
│   │   ├── VideoCall.tsx    # Video call component (VideoSDK)
│   │   └── theme-toggle.tsx # Dark/light mode toggle
│   ├── context/             # React context providers
│   │   ├── auth-context.tsx # Authentication context & provider
│   │   └── theme-context.tsx# Theme (dark/light) context & provider
│   ├── lib/
│   │   └── utils.ts         # Utility functions (e.g. cn() for class merging)
│   ├── pages/               # Route-level page components
│   │   ├── auth/            # Authentication pages (Login, Signup)
│   │   ├── HomePage.tsx     # Landing page
│   │   ├── PatientDashboard.tsx   # Patient dashboard
│   │   ├── DoctorDashboard.tsx    # Doctor dashboard
│   │   ├── BookAppointmentPage.tsx
│   │   ├── ChatPage.tsx     # Real-time messaging
│   │   ├── PrescriptionsPage.tsx
│   │   ├── ProfilePage.tsx
│   │   ├── AdminPage.tsx    # Admin panel
│   │   └── ...              # Other page components
│   ├── sockets/
│   │   └── socket.ts        # Socket.io client setup & event handlers
│   ├── store/
│   │   └── authstore.ts     # Zustand auth store (user state, persist)
│   ├── App.tsx              # Root component (providers + router)
│   ├── routes.tsx           # All application route definitions
│   ├── main.tsx             # App entry point (ReactDOM render)
│   └── globals.css          # Global styles & Tailwind directives
├── styles/
│   └── globals.css          # Additional global stylesheets
├── components.json          # shadcn/ui configuration
├── tailwind.config.ts       # Tailwind CSS configuration
├── tsconfig.json            # TypeScript compiler configuration
├── vite.config.ts           # Vite build configuration
├── package.json             # Dependencies & scripts
├── pnpm-lock.yaml           # pnpm lockfile (do not delete)
├── CONTRIBUTING.md          # Contribution guidelines
└── CODE_OF_CONDUCT.md       # Community code of conduct
```

### Key Architectural Decisions

- **Path alias** — `@/` maps to `src/` for clean imports (configured in `tsconfig.json` and `vite.config.ts`)
- **Component library** — UI primitives come from [shadcn/ui](https://ui.shadcn.com/) and live in `src/components/ui/`. These are copied into the project (not installed as a package) so they can be customized freely.
- **State management** — Zustand with `persist` middleware handles auth state; React Context handles theme and auth context at the provider level.
- **Routing** — React Router v6 with nested routes. Public pages use `Layout`, authenticated pages use `DashboardLayout` (includes sidebar).

---

## Contributing

We welcome contributions! Please read our **[Contributing Guide](CONTRIBUTING.md)** before getting started. Key points:

1. **Fork** the repository and create a feature branch
2. **Do not work on an issue** unless it is officially assigned to you
3. Use **`pnpm`** — PRs with `package-lock.json` or `yarn.lock` will be rejected
4. Include your **Team Number** in the PR description
5. Submit your PR within **3–5 days** of assignment

For full details on the contribution workflow, issue policies, PR guidelines, and coding standards, see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Code of Conduct

This project follows the GDG CHARUSAT community standards. Please read our [Code of Conduct](CODE_OF_CONDUCT.md) to understand the expectations for participation.

---

## License

This project is maintained by [GDG CHARUSAT](https://github.com/gdg-charusat). Please refer to the repository for license details.
