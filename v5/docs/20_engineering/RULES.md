# Engineering Rules

## 1) Scope Control
- Do not invent features.
- Implement only what PRD/SPEC/TASKS specify.

## 2) PRD Immutability
- Never edit docs/00_context/PRD.md.
- Questions/suggestions only in PRD_NOTES.md.

## 3) Coding Standards
- Formatting:
- Linting:
- Naming conventions:

## 4) Testing
- Unit tests required where specified.
- Verification commands must be recorded in CHANGELOG.

## 5) Security
- No secrets in code.
- Env vars for config.
- Validate inputs; sanitize outputs.

## 6) OpenAPI Contract
- OPENAPI.yaml is the contract.
- Implementation must conform to spec-first.

## 7) Change Management
- Every task must update docs/90_ops/CHANGELOG.md.
- No silent breaking changes.
