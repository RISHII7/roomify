# Changelog

All notable changes to the Roomify project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased] - feat/upload-files

### Added
- **Interactive Drag-and-Drop Uploader**: Created a robust `Upload` component (`components/upload/index.tsx`) using React hooks (`useCallback`, `useEffect`, `useRef`, `useState`) and Tailwind CSS.
- **File Validation & Reading**: Supports JPG, JPEG, PNG, and WEBP formats up to 50MB. Reads files as Base64 strings.
- **Simulated File Analysis Progress**: Built an animated progress bar indicating analysis status ("Analyzing Floor Plan..." and "Redirecting...") before triggering the success state.
- **Dynamic Auth Verification**: Integrates with `AuthContext` to restrict uploads to authenticated users (displays "Sign in or sign up with Puter to upload" for guest users).
- **Client-Side Routing to Visualizer**: Handled navigation to the dynamic visualizer page (`/visualizer/:id`) after successful file upload completion.
- **Visualizer Layout Placeholder**: Created a route parameter page `visualizer.$id.tsx` to handle the rendering of uploaded floor plans and AI visualizations.
- **Configuration & Timing Constants**: Centralized constants (`lib/constants/index.ts`) for timeouts, intervals, sizes, and the highly-detailed AI render prompt (`ROOMIFY_RENDER_PROMPT`).

### Changed
- **Homepage Integration**: Replaced the static placeholder with the interactive `Upload` component on the landing page (`app/routes/home.tsx`).
- **Route Configuration**: Configured the dynamic `:id` route parameter for `/visualizer/:id` in `app/routes.ts`.

---

## [0.2.0] - feat/homepage

### Added
- **Modern Landing Page**: Overhauled `app/routes/home.tsx` to display a sleek hero section, dynamic branding, announcement badges, and CTA triggers.
- **Community Projects Grid**: Built a visual grid showing mock-up architectural rendering items with metadata and badges.

---

## [0.1.1] - feat/authentication

### Added
- **Puter.js Integration**: Added `@heyputer/puter.js` as a dependency.
- **Modular Auth Actions**: Created `lib/puter.action.ts` wrapper actions for `signIn`, `signOut`, and `getCurrentUser`.
- **Global Auth State**: Configured root React Context (`app/root.tsx`) to manage and propagate authentication state globally.
- **Auth UI Integration**: Dynamic login/logout buttons and user greeting badges in the Navbar component.

---

## [0.1.0] - 2026-02-19

### Added
- **Project Scaffold**: Initialized React Router v7 project with Tailwind CSS, TypeScript, and Vite.
- **Infrastructure**: Containerized the application using a multi-stage `Dockerfile` and `.dockerignore`.
- **CI/CD Pipelines**:
  - `ci.yml`: Automated compilation and type-checking on pull requests to `main`.
  - `release.yml`: Automated GitHub release generation and Docker Hub/GHCR packaging.
