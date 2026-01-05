# Python Project CLAUDE.md Template

Add these sections to your Python project's CLAUDE.md alongside the general rules.

---

## Commands

```bash
# Development
python -m venv venv
source venv/bin/activate  # or `venv\Scripts\activate` on Windows
pip install -e ".[dev]"

# Testing
pytest                           # Run all tests
pytest tests/unit/               # Run unit tests only
pytest -x                        # Stop on first failure
pytest --cov=src                 # With coverage

# Linting & Formatting
ruff check .                     # Lint
ruff format .                    # Format
mypy src/                        # Type checking

# Build
python -m build
```

## Standards

- Python 3.11+ with type hints on all public functions
- Ruff for linting and formatting
- pytest for testing with pytest-cov for coverage
- mypy for type checking (strict mode)

## Directory Structure

```
project/
├── src/
│   └── package_name/
│       ├── __init__.py
│       ├── module.py
│       └── py.typed          # PEP 561 marker
├── tests/
│   ├── unit/
│   ├── integration/
│   └── conftest.py           # Shared fixtures
├── pyproject.toml
└── CLAUDE.md
```

## Testing Requirements

- Unit tests in `tests/unit/`, integration in `tests/integration/`
- Use fixtures from `conftest.py` for common setup
- Avoid mocks unless testing external services
- Target 80%+ coverage on new code

## Code Patterns

### Error Handling
```python
# Use specific exceptions, not bare except
try:
    result = risky_operation()
except SpecificError as e:
    logger.error("Operation failed", exc_info=e)
    raise
```

### Type Hints
```python
from typing import Optional, List

def process_items(items: List[str], limit: Optional[int] = None) -> dict[str, int]:
    ...
```

### Async Patterns (if applicable)
```python
import asyncio
from typing import AsyncIterator

async def fetch_all(urls: list[str]) -> AsyncIterator[Response]:
    async with aiohttp.ClientSession() as session:
        for url in urls:
            yield await session.get(url)
```

## Dependencies

Manage in `pyproject.toml`:
```toml
[project]
dependencies = [
    "httpx>=0.25",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0",
    "ruff>=0.1",
    "mypy>=1.0",
]
```

## Notes

- Use `python -m module` over `python module.py` for proper imports
- Prefer pathlib over os.path
- Use dataclasses or Pydantic for data structures
