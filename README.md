# Finite State Machine Visualizer — Fullstack FSM Simulation Platform

[![codecov](https://codecov.io/gh/leandrofahur/finite-state-machines-vizualizer/branch/main/graph/badge.svg?token=YR9K32XX5X)](https://codecov.io/gh/leandrofahur/finite-state-machines-vizualizer)
[![Python Version](https://img.shields.io/badge/python-3.12%2B-blue.svg)](https://www.python.org/downloads/)
[![Node.js Version](https://img.shields.io/badge/node.js-18%2B-green.svg)](https://nodejs.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104%2B-green.svg)](https://fastapi.tiangolo.com/)
[![Next.js](https://img.shields.io/badge/Next.js-14%2B-black.svg)](https://nextjs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> A professional, fullstack monorepo application to model, simulate, and visualize finite state machines using FastAPI and Next.js. Designed for engineering, robotics, agent logic, education, and embedded systems control.

## 🚀 Overview

**Finite State Machine Visualizer** is a modular web platform that lets you define, test, and visually explore FSMs from a Python backend in real time. Built with engineers and developers in mind, it bridges low-level state logic with modern web UIs — making FSMs both accessible and inspectable.

### ✨ Key Features

- **🎯 Core FSM Engine**: Python-based backend with flexible state and transition definitions
- **⚡ Real-Time State Updates**: Trigger events and watch transitions live via WebSocket
- **📊 Graph-Based Visualization**: Render FSMs using Mermaid.js with multiple diagram formats
- **🖥️ Interactive UI**: Modern web interface for loading, inspecting, and simulating FSMs
- **🔌 API-first Design**: FastAPI serves a structured JSON-based contract for frontend interaction
- **🛡️ Strong Type Safety**: TypeScript-based frontend with clearly typed FSM schemas
- **🧪 Comprehensive Testing**: Pytest-based backend tests with coverage reporting
- **🐳 Dockerized Dev Stack**: Seamless setup with docker-compose for easy development
- **📈 Real-time Monitoring**: Live metrics and health checks for production readiness

## 🏗️ Architecture

### Tech Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Frontend** | Next.js 14 (App Router), TailwindCSS, Shadcn/ui | Modern, responsive UI |
| **Backend API** | FastAPI, Pydantic v2, Python 3.12 | High-performance async API |
| **Testing** | Pytest, HTTPX, Coverage.py | Comprehensive test suite |
| **Dev Tools** | Docker, Docker Compose, Black, Ruff | Code quality & development |
| **Real-time** | WebSocket, FastAPI WebSocket | Live state updates |
| **Visualization** | Mermaid.js, DOT, Custom diagrams | Multiple diagram formats |
| **Deployment** | Vercel (Frontend), Railway/Fly.io (Backend) | Scalable cloud deployment |

### Monorepo Structure

```bash
finite-state-machines-vizualizer/
├── 📁 apps/
│   ├── 🎨 frontend/               # Next.js UI with TypeScript
│   │   ├── src/
│   │   │   ├── components/        # Reusable UI components
│   │   │   ├── pages/            # Next.js pages
│   │   │   ├── hooks/            # Custom React hooks
│   │   │   └── utils/            # Frontend utilities
│   │   └── public/               # Static assets
│   └── ⚙️ backend/                # FastAPI API with FSM core
│       ├── src/
│       │   ├── models/           # Pydantic data models
│       │   ├── core/             # FSM engine & validation
│       │   ├── api/              # FastAPI endpoints
│       │   └── utils/            # Visualization utilities
│       └── tests/                # Backend test suite
├── 📦 packages/
│   └── shared/                   # Shared types & constants
├── 🐳 infra/
│   └── docker-compose.yml        # Dev environment orchestration
├── 🧪 tests/
│   └── integration/              # End-to-end tests
├── 📋 .github/
│   └── workflows/                # CI/CD pipelines
├── 📚 docs/                      # Documentation
└── 📄 README.md
```

## 🚀 Quick Start

### Prerequisites

- **Python 3.12+** with UV package manager
- **Node.js 18+** with npm/yarn
- **Docker & Docker Compose** (optional)

### Development Setup

```bash
# Clone the repository
git clone https://github.com/leandrofahur/finite-state-machines-vizualizer.git
cd finite-state-machines-vizualizer

# Backend Setup
cd apps/backend
uv sync
uvicorn src.main:app --reload

# Frontend Setup (in another terminal)
cd apps/frontend
npm install
npm run dev

# Or use Docker (recommended)
docker-compose up --build
```

### API Documentation

Once running, visit:
- **Interactive API Docs**: http://localhost:8000/docs
- **Frontend Application**: http://localhost:3000
- **Backend Health**: http://localhost:8000/api/v1/fsm/health

## 🔌 API Endpoints

### Core FSM Operations

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/fsm/create` | Create new FSM definition |
| `POST` | `/api/v1/fsm/validate` | Validate FSM structure |
| `POST` | `/api/v1/fsm/visualize` | Generate diagrams |
| `POST` | `/api/v1/fsm/instance/create` | Create FSM instance |
| `GET` | `/api/v1/fsm/instance/{id}/status` | Get instance status |
| `POST` | `/api/v1/fsm/instance/{id}/trigger` | Trigger state event |
| `WS` | `/api/v1/fsm/ws/{instance_id}` | Real-time updates |

### Example Usage

```python
import requests

# Create a traffic light FSM
fsm_data = {
    "config": {"name": "Traffic Light", "version": "1.0.0"},
    "states": [
        {"name": "red", "is_initial": True},
        {"name": "yellow"},
        {"name": "green", "is_final": True}
    ],
    "transitions": [
        {"from_state": "red", "to_state": "green", "event": "timer"},
        {"from_state": "green", "to_state": "yellow", "event": "timer"},
        {"from_state": "yellow", "to_state": "red", "event": "timer"}
    ]
}

response = requests.post("http://localhost:8000/api/v1/fsm/create", json=fsm_data)
print(response.json())
```

## 🧪 Testing

### Backend Tests

```bash
cd apps/backend
make test          # Run all tests
make coverage      # Run with coverage
make ci            # Full CI pipeline
```

### Frontend Tests

```bash
cd apps/frontend
npm run test       # Run unit tests
npm run test:e2e   # Run E2E tests
npm run lint       # Run linter
```

## 📋 Git Flow & Branching Strategy

We follow a structured Git workflow to ensure clean collaboration and safe deployment practices.

### Branch Naming Convention

| Branch Type | Naming Convention | Purpose |
|-------------|------------------|---------|
| **Main** | `main` | Production-ready code only |
| **Dev** | `dev` | Staging branch for new features |
| **Feature** | `feature/<feature>` | New features (e.g., `feature/quiz-engine`) |
| **Bugfix** | `bugfix/<issue>` | Bug fixes (e.g., `bugfix/navbar-scroll`) |
| **Refactor** | `refactor/<area>` | Code refactoring (e.g., `refactor/tts-handler`) |
| **Hotfix** | `hotfix/<name>` | Emergency fixes for `main` |

### Development Workflow

```bash
# 1. Start new feature
git checkout dev
git checkout -b feature/ai-tutor-endpoint

# 2. Make changes and commit
git add .
git commit -m "feat(api): add initial AI tutor endpoint"

# 3. Push and create PR
git push origin feature/ai-tutor-endpoint

# 4. After review, merge to dev
git checkout dev
git merge feature/ai-tutor-endpoint

# 5. Release to production
git checkout main
git merge dev
git tag v1.0.0
git push origin main --tags
```

### Commit Message Convention

We use [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): description

feat(api): add FSM validation endpoint
fix(frontend): resolve state transition bug
docs(readme): update installation instructions
test(backend): add FSM engine tests
```

## 🤝 Contributing

We welcome all contributions — from code to design, to ideas and documentation!

### How to Contribute

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/amazing-feature`
3. **Make** your changes following our coding standards
4. **Test** your changes: `make ci` (backend) or `npm run test` (frontend)
5. **Commit** with conventional commit messages
6. **Push** to your branch: `git push origin feature/amazing-feature`
7. **Open** a Pull Request with detailed description

### Development Guidelines

- ✅ Follow PEP 8 (Python) and ESLint (JavaScript) standards
- ✅ Write comprehensive tests for new features
- ✅ Update documentation for API changes
- ✅ Use conventional commit messages
- ✅ Ensure all tests pass before submitting PR
- ✅ Add appropriate badges and status indicators

## 📊 Project Status

| Component | Status | Coverage | Version |
|-----------|--------|----------|---------|
| **Backend API** | ✅ Active | 95%+ | v1.0.0 |
| **Frontend UI** | 🚧 In Development | TBD | v0.1.0 |
| **Documentation** | ✅ Complete | - | v1.0.0 |
| **Testing** | ✅ Comprehensive | 95%+ | v1.0.0 |
| **Deployment** | 🚧 Setup | - | v0.1.0 |

## 📚 Documentation

- **[Backend API Docs](apps/backend/README.md)** - Complete backend documentation
- **[Frontend Docs](apps/frontend/README.md)** - Frontend development guide
- **[API Reference](http://localhost:8000/docs)** - Interactive API documentation
- **[Architecture Guide](docs/architecture.md)** - System design and patterns

## 🚀 Deployment

### Production Deployment

```bash
# Backend (Railway/Fly.io)
cd apps/backend
uv sync --frozen
uvicorn src.main:app --host 0.0.0.0 --port $PORT

# Frontend (Vercel)
cd apps/frontend
npm run build
npm start
```

### Environment Variables

```bash
# Backend
ENVIRONMENT=production
LOG_LEVEL=INFO
CORS_ORIGINS=https://your-frontend.com

# Frontend
NEXT_PUBLIC_API_URL=https://your-backend.com
NEXT_PUBLIC_WS_URL=wss://your-backend.com
```

## 👥 Contributors

We welcome all contributors! Here are our current team members:

| Avatar | Name | Role | GitHub |
|--------|------|------|--------|
| <img src="https://avatars.githubusercontent.com/u/46628080?u=7c2c2d90408b1a731118b5b3512d9da890cf2d45&v=4" width="40" /> | **Leandro Miranda Fahur Machado** | Software Engineer | [@leandrofahur](https://github.com/leandrofahur) |

### Want to Join?

We're always looking for contributors! Check out our [Contributing Guide](CONTRIBUTING.md) and [Issues](https://github.com/leandrofahur/finite-state-machines-vizualizer/issues) to get started.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **FastAPI** team for the excellent async framework
- **Next.js** team for the amazing React framework
- **Pydantic** team for the validation library
- **Mermaid.js** team for the diagram library
- **The Python & JavaScript communities** for amazing tools and libraries

---

**Made with ❤️ for the FSM community**

[![GitHub stars](https://img.shields.io/github/stars/leandrofahur/finite-state-machines-vizualizer?style=social)](https://github.com/leandrofahur/finite-state-machines-vizualizer)
[![GitHub forks](https://img.shields.io/github/forks/leandrofahur/finite-state-machines-vizualizer?style=social)](https://github.com/leandrofahur/finite-state-machines-vizualizer)
[![GitHub issues](https://img.shields.io/github/issues/leandrofahur/finite-state-machines-vizualizer)](https://github.com/leandrofahur/finite-state-machines-vizualizer/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/leandrofahur/finite-state-machines-vizualizer)](https://github.com/leandrofahur/finite-state-machines-vizualizer/pulls)
