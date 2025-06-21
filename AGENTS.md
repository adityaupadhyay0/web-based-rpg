# Agent Guidelines

This file provides general guidelines for AI agents working on this codebase.

## General Principles

- **Modularity:** Strive to keep components small, focused, and reusable.
- **Clarity:** Write code that is easy to understand and maintain. Add comments where necessary to explain complex logic.
- **Testing:** Write unit tests for new functionality and bug fixes. Ensure all tests pass before submitting changes.
- **Consistency:** Follow existing coding styles and conventions.
- **Layered Architecture (Backend):** Adhere to the established layered architecture for the backend:
    - **interfaces:** Handles HTTP requests, data validation, and serialization. Calls application services.
    - **app:** Orchestrates use cases. Contains application services that use domain objects and repositories.
    - **domain:** Contains business logic, entities, value objects, and domain services. Should be independent of infrastructure concerns.
    - **infrastructure:** Implements interfaces defined in the domain or application layers (e.g., repositories, external service clients).
- **Commit Messages:** Write clear and concise commit messages. Follow the convention of a short subject line (max 50 chars), a blank line, and a more detailed body if needed.

## Specific Instructions

- (Add any project-specific instructions here as the project evolves)

## Running Checks

- (Add any programmatic checks here, e.g., linters, test commands)
- Ensure all tests pass: `[your_test_command_here]` (replace with actual command once test runner is set up)
- Ensure linter passes: `[your_lint_command_here]` (replace with actual command once linter is set up)
