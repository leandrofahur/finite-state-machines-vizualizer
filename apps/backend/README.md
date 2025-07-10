# Finite State Machine Visualizer API

[![codecov](https://codecov.io/gh/leandrofahur/finite-state-machines-vizualizer/branch/main/graph/badge.svg?token=YR9K32XX5X)](https://codecov.io/gh/leandrofahur/finite-state-machines-vizualizer)
[![Python Version](https://img.shields.io/badge/python-3.12%2B-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104%2B-green.svg)](https://fastapi.tiangolo.com/)
[![Pydantic](https://img.shields.io/badge/Pydantic-2.0%2B-orange.svg)](https://pydantic.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A professional FastAPI backend for defining, simulating, and visualizing finite state machines with real-time WebSocket support.

## 🚀 Features

- **Core FSM Engine**: Robust state machine execution with validation
- **Real-time Updates**: WebSocket support for live state transitions
- **Multiple Visualizations**: Mermaid.js, DOT, and text-based diagrams
- **Comprehensive Validation**: Graph structure and reachability analysis
- **Type Safety**: Full Pydantic model validation
- **RESTful API**: Clean, documented endpoints with OpenAPI
- **Test Coverage**: Comprehensive test suite with coverage reporting

## 🏗️ Architecture

```
src/
├── models/          # Pydantic data models
│   ├── state.py     # State and Transition models
│   └── fsm.py       # FSM configuration models
├── core/            # Business logic
│   ├── engine.py    # FSM execution engine
│   └── validator.py # Validation logic
├── api/             # FastAPI endpoints
│   ├── routes.py    # API routes
│   └── schemas.py   # Request/response schemas
├── utils/           # Utilities
│   └── visualization.py # Diagram generation
└── main.py          # FastAPI application
```

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Framework** | FastAPI | High-performance async API |
| **Validation** | Pydantic v2 | Data validation & serialization |
| **Testing** | Pytest | Test framework |
| **Linting** | Ruff | Fast Python linter |
| **Formatting** | Black | Code formatter |
| **Coverage** | Coverage.py | Test coverage reporting |
| **Package Manager** | UV | Fast Python package manager |

## 📦 Installation

### Prerequisites

- Python 3.12+
- UV package manager

### Setup

```bash
# Clone the repository
git clone https://github.com/leandrofahur/finite-state-machines-vizualizer.git
cd finite-state-machines-vizualizer/apps/backend

# Install dependencies
uv sync

# Activate virtual environment
source .venv/bin/activate  # On Unix/macOS
# or
.venv\Scripts\activate     # On Windows
```

## 🚀 Development

### Available Commands

```bash
# Code Quality
make lint          # Run ruff linter with auto-fix
make format        # Run black formatter
make lint-fix      # Run both format and lint

# Testing
make test          # Run pytest with verbose output
make coverage      # Run tests with coverage reporting
make ci            # Run full CI pipeline

# Server
uvicorn src.main:app --reload  # Development server
```

### Running the Server

```bash
# Development mode
uvicorn src.main:app --reload --host 0.0.0.0 --port 8000

# Production mode
uvicorn src.main:app --host 0.0.0.0 --port 8000
```

## 📚 API Documentation

Once the server is running, visit:

- **Interactive API Docs**: http://localhost:8000/docs
- **ReDoc Documentation**: http://localhost:8000/redoc
- **OpenAPI Schema**: http://localhost:8000/openapi.json

## 🔌 API Endpoints

### FSM Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/fsm/create` | Create a new FSM definition |
| `POST` | `/api/v1/fsm/validate` | Validate an FSM definition |
| `POST` | `/api/v1/fsm/visualize` | Generate FSM visualizations |

### Instance Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/v1/fsm/instance/create` | Create FSM instance |
| `GET` | `/api/v1/fsm/instance/{id}/status` | Get instance status |
| `POST` | `/api/v1/fsm/instance/{id}/trigger` | Trigger event |
| `GET` | `/api/v1/fsm/instance/list` | List all instances |
| `DELETE` | `/api/v1/fsm/instance/{id}` | Destroy instance |

### Real-time Updates

| Method | Endpoint | Description |
|--------|----------|-------------|
| `WS` | `/api/v1/fsm/ws/{instance_id}` | WebSocket for real-time updates |

### Health & Monitoring

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/fsm/health` | Health check |
| `GET` | `/` | API information |

## 📊 Example Usage

### Creating an FSM

```python
import requests

fsm_data = {
    "config": {
        "name": "Traffic Light",
        "description": "Simple traffic light FSM",
        "version": "1.0.0"
    },
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

### WebSocket Connection

```javascript
const ws = new WebSocket('ws://localhost:8000/api/v1/fsm/ws/instance-1');

ws.onmessage = function(event) {
    const data = JSON.parse(event.data);
    if (data.type === 'state_update') {
        console.log(`State changed: ${data.data.previous_state} -> ${data.data.current_state}`);
    }
};

// Trigger an event
ws.send(JSON.stringify({
    type: 'trigger_event',
    data: { event: 'timer' }
}));
```

## 🧪 Testing

### Running Tests

```bash
# Run all tests
make test

# Run with coverage
make coverage

# Run specific test file
python -m pytest tests/test_fsm_models.py -v

# Run with specific markers
python -m pytest -m "slow" -v
```

### Test Structure

```
tests/
├── test_fsm_models.py    # Model validation tests
├── test_engine.py        # FSM engine tests
├── test_api.py          # API endpoint tests
└── test_visualization.py # Visualization tests
```

## 🔧 Configuration

### Environment Variables

```bash
# Development
export ENVIRONMENT=development
export LOG_LEVEL=DEBUG

# Production
export ENVIRONMENT=production
export LOG_LEVEL=INFO
```

### Pytest Configuration

See `pyproject.toml` for full pytest configuration:

```toml
[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
addopts = [
    "--strict-markers",
    "--strict-config",
    "--cov=src",
    "--cov=tests",
    "--cov-report=term-missing",
    "--cov-report=html",
    "--cov-report=xml",
]
```

## 📈 Monitoring

### Health Check

```bash
curl http://localhost:8000/api/v1/fsm/health
```

Response:
```json
{
    "status": "healthy",
    "engine_instances": 5,
    "uptime": "2h 15m 30s"
}
```

### Metrics

- Active FSM instances
- API response times
- Error rates
- WebSocket connections

## 🚀 Deployment

### Docker

```dockerfile
FROM python:3.12-slim

WORKDIR /app
COPY . .

RUN pip install uv
RUN uv sync --frozen

EXPOSE 8000
CMD ["uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Environment Variables

```bash
# Required
ENVIRONMENT=production
LOG_LEVEL=INFO

# Optional
CORS_ORIGINS=https://your-frontend.com
API_KEY=your-secret-key
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Run tests: `make ci`
5. Commit your changes: `git commit -m 'feat: add amazing feature'`
6. Push to the branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guidelines
- Write comprehensive tests
- Update documentation
- Use conventional commit messages
- Ensure all tests pass before submitting PR

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](../LICENSE) file for details.

## 👥 Authors

- **Leandro Miranda Fahur Machado** - *Initial work* - [@leandrofahur](https://github.com/leandrofahur)

## 🙏 Acknowledgments

- FastAPI team for the excellent framework
- Pydantic team for the validation library
- The Python community for amazing tools and libraries

---

**Made with ❤️ for the FSM community** 