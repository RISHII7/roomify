# Changelog

All notable changes to the Roomify project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0-lts] - 2026-06-01

### Added
- **Puter.js Cloud Worker Script**: Created the router script (`lib/puter.worker.js`) executing on the Puter.js cloud execution service, implementing:
  - `POST /api/projects/save`: Saves projects by UUID with verification, using Puter's KV database.
  - `GET /api/projects/list`: Queries and lists all stored user projects prefixed with `roomify_project_`.
  - `GET /api/projects/get`: Queries and retrieves a single project item details using the project ID.
- **AI 3D Image Generation**: Integrated Puter's `puter.ai.txt2img` using the `gemini-2.5-flash-image-preview` model and the custom detailed prompt (`ROOMIFY_RENDER_PROMPT`) to generate top-down 3D architectural renders (`lib/ai.action.ts`).
- **Before-and-After Slider**: Incorporated `react-compare-slider` in the Editor/Visualizer view to enable interactive comparison between original and rendered floor plans.
- **Dynamic Image Export**: Added export download functionality in the Visualizer page to download generated renders as PNG files.
- **Project Creation & Database Save**: Implemented `createProject` in `lib/puter.action.ts` to host project assets (source and rendered images) via Puter hosting and save project entries to the Puter worker database.
- **Project History Listing**: Integrated `getProjects` and `getProjectById` to pull all designs or fetch a specific project entry from the worker database.
- **Dynamic Visualizer Rendering**: Updated the `visualizer.$id` route (`app/routes/visualizer.$id.tsx`) to pull source image and name details from location router state.
- **Homepage Integration**: Configured `app/routes/home.tsx` to handle full project creation workflow, store new projects locally, and navigate users to their visualizer layout.
- **Puter.js Site Hosting Integration**: Implemented hosting configurations via `puter.hosting.create` dynamically linked to user subdomain naming and persisted in Puter's key-value store.
- **Image Hosting Pipeline**: Added an asset pipeline (`lib/puter.hosting.ts`) to dynamically fetch, convert, and host source/rendered image assets directly on the user's hosted domain.
- **File System & Blob Utilities**: Created helpers (`lib/utils/index.ts`) for canvas-to-blob transformation, Base64 data URL parser, content-type mapping, and image file extension retrieval.
- **Extended Type Definitions**: Expanded `types.d.ts` to support project assets, layout props, material catalogs, and hosting configurations.
- **Environment Template**: Created `.env.example` to document the required environment variables (`VITE_PUTER_WORKER_URL`).

### Fixed
- **TypeScript & Dependency Resolution**: Installed missing `react-compare-slider` package and resolved a type safety assignment error (`TS2322`) in the comparison slider component inside `app/routes/visualizer.$id.tsx`.
- **TypeScript Deprecation**: Migrated `tsconfig.json` from the deprecated `baseUrl` option to explicit path mapping configurations to resolve TS 7.0 compatibility warnings.
- **CI/CD Lockfile Alignment**: Resolved a pipeline deployment error by synchronizing `package-lock.json` with `package.json` to allow clean installations (`npm ci`) in GitHub Actions and Docker build environments.
- **Mermaid Diagram Syntax**: Fixed a syntax parse error in the `README.md` architectural flow diagram by quoting the subgraph name.

---

## [0.2.0] - 2026-05-29

### Added
- **Interactive Drag-and-Drop Uploader**: Created a robust `Upload` component (`components/upload/index.tsx`) using React hooks (`useCallback`, `useEffect`, `useRef`, `useState`) and Tailwind CSS.
- **File Validation & Reading**: Supports JPG, JPEG, PNG, and WEBP formats up to 50MB. Reads files as Base64 strings.
- **Simulated File Analysis Progress**: Built an animated progress bar indicating analysis status ("Analyzing Floor Plan..." and "Redirecting...") before triggering the success state.
- **Dynamic Auth Verification**: Integrates with `AuthContext` to restrict uploads to authenticated users (displays "Sign in or sign up with Puter to upload" for guest users).
- **Client-Side Routing to Visualizer**: Handled navigation to the dynamic visualizer page (`/visualizer/:id`) after successful file upload completion.
- **Visualizer Layout Placeholder**: Created a route parameter page `visualizer.$id.tsx` to handle the rendering of uploaded floor plans and AI visualizations.
- **Configuration & Timing Constants**: Centralized constants (`lib/constants/index.ts`) for timeouts, intervals, sizes, and the highly-detailed AI render prompt (`ROOMIFY_RENDER_PROMPT`).
- **Modern Landing Page**: Overhauled `app/routes/home.tsx` to display a sleek hero section, dynamic branding, announcement badges, and CTA triggers.
- **Community Projects Grid**: Built a visual grid showing mock-up architectural rendering items with metadata and badges.
- **Puter.js Integration**: Added `@heyputer/puter.js` as a dependency.
- **Modular Auth Actions**: Created `lib/puter.action.ts` wrapper actions for `signIn`, `signOut`, and `getCurrentUser`.
- **Global Auth State**: Configured root React Context (`app/root.tsx`) to manage and propagate authentication state globally.
- **Auth UI Integration**: Dynamic login/logout buttons and user greeting badges in the Navbar component.

### Changed
- **Homepage Integration**: Replaced the static placeholder with the interactive `Upload` component on the landing page (`app/routes/home.tsx`).
- **Route Configuration**: Configured the dynamic `:id` route parameter for `/visualizer/:id` in `app/routes.ts`.

### Fixed
- **DevTools Route Matching Noise**: Added a dummy `com.chrome.devtools.json` static asset to suppress DevTools console query errors in development.

---

## [0.1.0] - 2026-02-19

### Added
- **Project Scaffold**: Initialized React Router v7 project with Tailwind CSS, TypeScript, and Vite.
- **Infrastructure**: Containerized the application using a multi-stage `Dockerfile` and `.dockerignore`.
- **CI/CD Pipelines**:
  - `ci.yml`: Automated compilation and type-checking on pull requests to `main`.
  - `release.yml`: Automated GitHub release generation and Docker Hub/GHCR packaging.
