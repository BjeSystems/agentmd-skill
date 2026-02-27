# Project Scan Analyzer

Detection algorithms for /AgentCheck command.

## Language Detection

### JavaScript/TypeScript
```bash
Indicators:
- package.json
- tsconfig.json
- *.js, *.ts, *.jsx, *.tsx files

Conventions:
- npm/yarn/pnpm package manager
- node_modules in .gitignore
- src/ or lib/ directory structure
```

### Python
```bash
Indicators:
- pyproject.toml (modern)
- requirements.txt (legacy)
- setup.py or setup.cfg
- *.py files

Conventions:
- venv/ or .venv/ virtual environment
- __pycache__ in .gitignore
- src/ or package_name/ directory
```

### Go
```bash
Indicators:
- go.mod
- go.sum
- *.go files

Conventions:
- vendor/ directory (optional)
- cmd/ and pkg/ structure
```

### Rust
```bash
Indicators:
- Cargo.toml
- Cargo.lock
- src/main.rs or src/lib.rs

Conventions:
- target/ build directory
- Cargo workspace for multi-crate
```

### Ruby
```bash
Indicators:
- Gemfile
- Gemfile.lock
- *.rb files

Conventions:
- bundle exec for commands
- spec/ or test/ directories
```

## Framework Detection

### Next.js
```bash
Indicators:
- node_modules/next
- app/ directory (App Router)
- pages/ directory (Pages Router)

Rules to add:
- Server/Client component separation
- API routes conventions
- Image optimization
```

### React (non-Next)
```bash
Indicators:
- node_modules/react
- src/App.js or src/App.tsx
- No next dependency

Rules to add:
- Component composition patterns
- Hooks usage guidelines
```

### Django
```bash
Indicators:
- manage.py
- settings.py
- apps/ directory structure

Rules to add:
- Model-View-Template separation
- Migration workflow
- Admin customization
```

### FastAPI
```bash
Indicators:
- main.py with FastAPI import
- pydantic models
- routers/ directory

Rules to add:
- Pydantic validation
- Dependency injection
- Async route handlers
```

## Tooling Detection

### Docker
```bash
Indicators:
- Dockerfile
- docker-compose.yml
- .dockerignore

Rules to add:
- Multi-stage builds
- Layer caching
- Health checks
```

### CI/CD (GitHub Actions)
```bash
Indicators:
- .github/workflows/*.yml

Rules to add:
- Test before build
- Secret management
- Deployment environments
```

### Linters
```bash
Indicators:
- .eslintrc (JavaScript)
- .pylintrc (Python)
- golangci-lint.yml (Go)

Rules to add:
- Pre-commit checks
- CI lint gate
- Auto-fix commands
```

## Architecture Patterns

### Monorepo
```bash
Indicators:
- Multiple package.json or pyproject.toml
- packages/ or apps/ directories
- Lerna, Nx, or Turborepo config

Rules to add:
- Workspace dependency management
- Cross-package imports
- Unified build commands
```

### Microservices
```bash
Indicators:
- Multiple service directories
- docker-compose with multiple services
- API gateway references

Rules to add:
- Service boundaries
- Inter-service communication
- Shared library versioning
```

## Documentation Detection

```bash
High quality:
- README.md with badges
- docs/ directory with structure
- CONTRIBUTING.md
- API documentation files

Medium quality:
- README.md basic only
- Code comments present
- No structured docs

Low quality:
- Minimal README
- Sparse comments
- Suggest improvement
```

## Confidence Scoring

Assign confidence to detections:

```
High (90%+):
- Multiple indicators match
- Clear configuration files
- Standard directory structure

Medium (70-89%):
- Some indicators present
- Non-standard structure
- Multiple possibilities

Low (<70%):
- Single indicator
- Ambiguous patterns
- Default to generic rules
```

## Detection Output Format

```json
{
  "language": {
    "primary": "typescript",
    "confidence": 95,
    "secondary": ["javascript"]
  },
  "framework": {
    "detected": "nextjs",
    "version": "14.x",
    "confidence": 98,
    "router": "app"
  },
  "tooling": {
    "docker": true,
    "ci_cd": "github-actions",
    "linter": "eslint",
    "test": "jest"
  },
  "architecture": {
    "pattern": "monorepo",
    "confidence": 85
  },
  "documentation": {
    "readme_quality": "high",
    "has_api_docs": true,
    "has_contributing": true
  }
}
```
