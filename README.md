# Roomify

**AI-powered Architectural Visualization SaaS**

Roomify is a cutting-edge platform that transforms 2D floor plans into photorealistic 3D renders using advanced AI models. Built for architects, interior designers, and real estate professionals, it offers a seamless workflow for visualizing spaces.

## Features

- **AI Rendering**: Generate photorealistic 3D architectural visualizations from simple inputs.
- **SaaS Platform**: Complete subscription-based service model.
- **Modern Stack**: Built with React Router v7, Tailwind CSS, and Vite for performance.
- **Containerized**: Fully dockerized for consistent deployment.

## Tech Stack

- **Frontend**: React, React Router v7, Tailwind CSS
- **Build Tool**: Vite
- **Language**: TypeScript
- **Infrastructure**: Docker

## Getting Started

### Prerequisites

- Node.js (v20+)
- Docker (optional, for containerized run)

### Installation

```bash
npm install
```

### Development

```bash
npm run dev
```

### Build

```bash
npm run build
```

### Docker

```bash
docker build -t roomify .
docker run -p 3000:3000 roomify
```
