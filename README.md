# Finite State Machine Visualizer — Fullstack FSM Simulation Platform

> A professional, fullstack monorepo application to model, simulate, and visualize finite state machines using FastAPI and Next.js. Designed for engineering, robotics, agent logic, education, and embedded systems control.

## Overview
**Finite State Machine Visualizer** is a modular web platform that lets you define, test, and visually explore FSMs from a Python backend in real time. Built with engineers and developers in mind, it bridges low-level state logic with modern web UIs — making FSMs both accessible and inspectable.

### Key Features

- **Core FSM Engine**: Python-based backend with flexible state and transition definitions.
- **Real-Time State Updates**: Trigger events and watch transitions live.
- **Graph-Based Visualization**: Render FSMs using Mermaid.js.
- **Interactive UI**: Web interface for loading, inspecting, and simulating FSMs.
- **API-first Design**: FastAPI serves a structured JSON-based contract for frontend interaction.
- **Strong Type Safety**: TypeScript-based frontend with clearly typed FSM schemas.
- **Test Coverage**: Pytest-based backend tests for FSM logic and API behavior.
- **Dockerized Dev Stack**: Seamless setup with docker-compose.



## Tech Stack

| Layer        | Tech                                               |
|--------------|----------------------------------------------------|
| Frontend     | Next.js (App Router), TailwindCSS, Shadcn/ui       |
| Backend API  | FastAPI, Pydantic, Python 3.11                     |
| Testing      | Pytest, HTTPX                                      |
| Dev Tools	   | Docker, Docker Compose, Black, Ruff                |
| Realtime DB  | Supabase                                           |
| Vizualization| Mermaid.js (state diagrams)                        |
| Deployment   | Vercel (Frontend), Railway/Fly.io (Backend)        |



## Monorepo Structure
```bash
finite-state-machine-vizualizer/
├── apps/
│   ├── frontend/               # Next.js UI
│   └── backend/                # FastAPI API with FSM core
├── packages/
│   └── shared/                 # Shared types/constants
├── infra/
│   └── docker-compose.yml      # Dev environment orchestration
├── tests/
│   └── test_fsm.py             # Backend unit & integration tests
├── .github/
│   └── workflows/              # CI/CD pipelines
├── CODE_OF_CONDUCT.md
└── README.md
```



## Git Flow & Branching Strategy
We follow a structured Git workflow to ensure clean collaboration and safe deployment practices.

### Branch Naming

| Branch Type | Naming Convention   | Purpose |
|-------------|---------------------|---------|
| Main        | `main`              | Production-ready code only                        |
| Dev         | `dev`               | Staging branch for new features                   |
| Feature     | `feature/<feature>` | New features (e.g., `feature/quiz-engine`)        |
| Bugfix      | `bugfix/<issue>`    | Bug fixes (e.g., `bugfix/navbar-scroll`)          |
| Refactor    | `refactor/<area>`   | Code refactoring (e.g., `refactor/tts-handler`)   |
| Hotfix      | `hotfix/<name>`     | Emergency fixes for `main`                        |



### Git Flow Process

1. **Start New Work**
```bash
$ git checkout dev
$ git checkout -b feat/my-new-feature
```

2. **Push & Open PR**
- Push your branch:

```bash
$ git push origin feat/my-new-feature
```

- Open a Pull Request into `dev`.
- Get at least 1 approval before merging.

3. **Merging**
- Only maintainers merge into main (via `dev`).
- Use squash merge unless otherwise needed.

4. **Release to Production**

```bash
$ git checkout main
$ git merge dev
$ git tag vX.X.X
$ git push origin main --tags
```

### Example Workflow
```bash
# Start working on a feature
git checkout dev
git checkout -b feature/ai-tutor-endpoint

# Make changes
git add .
git commit -m "feature(api): add initial AI tutor endpoint"
git push origin feature/ai-tutor-endpoint

# Open PR → review → merge into dev
```



## Contributors
We welcome all contributions — from code to design, to ideas and documentation!

| Avatar | Name | Role | GitHub |
|--------|------|------|--------|
| <img src="https://avatars.githubusercontent.com/u/46628080?u=7c2c2d90408b1a731118b5b3512d9da890cf2d45&v=4" width="40" /> | **Leandro Miranda Fahur Machado** | Software Enginner | [@leandrofahur](https://github.com/leandrofahur) |
