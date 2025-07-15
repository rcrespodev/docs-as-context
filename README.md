# docs-as-context
Universal Framework for AI-Assisted Programming

## Overview
docs-as-context is a comprehensive framework designed to enhance software development through AI-assisted programming. Built to be technology-agnostic, it provides a structured set of rules and tools to streamline coding, documentation, and testing processes across various stacks (e.g., MERN, Java, React, NestJS) and project types (e.g., monorepos, native apps, LLMs) following the code guidelenes of the technical team.
By leveraging tools like Cursor, this framework ensures consistency, scalability, and efficiency in development workflows.
The framework is designed to be used with Cursor, but can be used with other tools that support the same API. e.g you can use this framework with Windsurf.


## Key Features

- Domain-Driven Design (DDD) Rules: Detailed guidelines for aggregates, models, business logic, edge cases, key users, and user stories to provide a clear understanding of the project domain.
- Automated Task Management: A global task-manager.mdc rule that intelligently applies relevant rules based on task type (e.g., feature, bug, deploy) and context (e.g., frontend, backend, devops).
- Structured Rule Organization: A main index.mdc and sub-indices (tasks-index.mdc, frontend-index.mdc, etc.) for easy navigation and scalability.
- Automatic Documentation: Generates Markdown files for tasks, features, and issues, ensuring traceability and ease of onboarding.
- Code Quality and Testing: Rules for linting (linting.mdc), security(security.mdc), code review(code-review.mdc), and automated test generation (e.g., Jest .spec files) to maintain high standards.
- Temporary File Handling: Manages ephemeral files (e.g., logs, test configs) that are automatically created and deleted to keep the repository clean.
- AI Context Enhancement: context-provider.mdc generates rich context files per task with dependencies, requirements, and objectives.
- Knowledge Base Management: knowledge-base.mdc maintains a repository of technical documentation, best practices, and code examples accessible to AI agents.


## Base Template Structure

```yaml
root/
├── rules/                  # All rule files
│   ├── universal/          # Universal rules (e.g., code-quality.mdc, testing.mdc)
│   │   ├── code-quality-guidelines.mdc # Guidelines for code quality
│   │   ├── testing-guidelines.mdc # Guidelines for testing
│   │   ├── documentation-guidelines.mdc # Guidelines for documentation
│   │   ├── security-guidelines.mdc # Universal guidelines for writing secure code
│   │   ├── code-review.mdc # Rule to review code according to the documentation guidelines
│   │   ├── linting.mdc # Rule to lint code according to the documentation guidelines
│   │   ├── performance-guidelines.mdc # Universal guidelines for writing performance code
│   │   ├── accessibility-guidelines.mdc # Universal guidelines for writing accessibile code
│   │   ├── internationalization-guidelines.mdc # Universal guidelines for writing internationalization components
│   │   ├── project-structure.mdc # Overview of the project structure and the rules that apply to it
│   │   ├── tech-stack.mdc # Overview of the tech stack and the rules that apply to it
│   │   ├── rule-writer.mdc # Guidelines for creating new rules
│   ├── domain/             # DDD-focused rules (e.g., domain-aggregates.mdc)
│   │   ├── domain-aggregates.mdc # DDD-focused rules (e.g., domain-aggregates.mdc)
│   │   ├── prd.mdc # Product Requirements Document
│   │   ├── application-flow.mdc # Application flow in user stories
│   │   ├── user-stories.mdc # Rule to write user stories according to the documentation guidelines
│   │   ├── user-stories-index.mdc # User stories index - to be used by the task-manager.mdc
│   ├── stacks/             # Technology-specific rules (e.g., mern-stack.mdc)
│   │   ├── mern-stack-guidelines.mdc # MERN stack rules (e.g., mern-stack.mdc)
│   │   ├── react-guidelines.mdc # React rules (e.g., react.mdc, nextjs.mdc)
│   │   ├── nestjs-guidelines.mdc # NestJS rules (e.g., nestjs.mdc)
│   │   ├── llm-guidelines.mdc # LLM rules (e.g., openai.mdc, anthropic.mdc)
│   │   ├── mcp-agent-guidelines.mdc # MCP agent rules (e.g., mcp-agent.mdc)
│   ├── devops/             # DevOps rules (e.g., ci-cd.mdc)
│   │   ├── ci-cd.mdc # CI/CD rules (e.g., ci-cd.mdc)
│   │   ├── monitoring.mdc # Monitoring rules (e.g., monitoring.mdc)
│   │   ├── infra.mdc # Infrastructure rules (e.g., infra.mdc)
│   │   ├── pull-request-writer.mdc # Pull request writer rules (e.g., pull-request-writer.mdc)
│   │   ├── git-commit-writer.mdc # Git commit writer rules (e.g., git-commit-writer.mdc)
│   ├── tasks/              # Task-related rules (e.g., tasks-index.mdc)
│   │   ├── tasks-manager.mdc # Task manager rules
│   │   ├── tasks-guidelines.mdc # Task guidelines rules
│   │   ├── tasks-index.mdc # Task index rules
│   └── index.mdc           # Main index of all rules
├── docs/                   # Generated documentation (e.g., task-feature-login.md)
│   ├── tasks/              # Task files (e.g., task-feature-login.md)
│   ├── features/           # Feature files (e.g., feature-login.md)
│   ├── bugs/               # Bug files (e.g., bug-login.md)
│   ├── deploys/            # Deploy files (e.g., deploy-login.md)
│   ├── refactors/          # Refactor files (e.g., refactor-login.md)
│   ├── tests/              # Test files (e.g., test-login.md)
│   ├── documentation/      # Documentation files (e.g., documentation-login.md)
├── temp/                   # Temporary files (ignored in .gitignore)
└── README.md               # This file
```

## Getting Started

Clone the Repository:git clone https://github.com/<your-org>/docs-as-context.git
cd docs-as-context


### Set Up Your AI Tool:
Configure Cursor or your preferred AI-assisted programming tool.
Load the rules/ directory into the tool to enable rule-based automation.

### Configure Glob Patterns:
Glob patterns determine which files each rule applies to. Configure them based on your project structure:

#### Understanding Glob Patterns:
- `**/*` - Applies to all files in the project
- `**/*.ts` - Applies to all TypeScript files
- `**/*.tsx` - Applies to all React TypeScript files
- `**/*.js` - Applies to all JavaScript files
- `**/*.md` - Applies to all Markdown files
- `apps/api/**/*` - Applies to all files in the API app directory
- `apps/web/**/*` - Applies to all files in the Web app directory
- `packages/**/*` - Applies to all files in packages directory

#### Project Structure Examples:

**Monorepo Structure (Turborepo/pnpm workspaces):**
```
project/
├── apps/
│   ├── api/          # Backend API
│   ├── web/          # Frontend Web
│   └── native-app/   # Mobile App
├── packages/
│   ├── database/     # Database package
│   ├── types/        # Shared types
│   └── bff/          # Backend for Frontend
└── docs/
```

**Recommended Glob Patterns for Monorepo:**
- **Backend Rules**: `apps/api/**/*` or `apps/api/**/*.ts`
- **Frontend Rules**: `apps/web/**/*` or `apps/web/**/*.{ts,tsx}`
- **Mobile Rules**: `apps/native-app/**/*` or `apps/native-app/**/*.{ts,tsx}`
- **Database Rules**: `packages/database/**/*` or `packages/database/**/*.ts`
- **Shared Types**: `packages/types/**/*` or `packages/types/**/*.ts`
- **Universal Rules**: `**/*` (applies to all files)

**Traditional Structure:**
```
project/
├── src/
│   ├── components/
│   ├── pages/
│   ├── services/
│   └── utils/
├── public/
├── tests/
└── docs/
```

**Recommended Glob Patterns for Traditional:**
- **Frontend Rules**: `src/**/*` or `src/**/*.{ts,tsx,js,jsx}`
- **Test Rules**: `tests/**/*` or `**/*.spec.{ts,js}`
- **Documentation**: `docs/**/*` or `**/*.md`

#### Configuration Best Practices:

1. **Be Specific**: Use targeted patterns rather than broad ones
   ```yaml
   # ✅ Good: Specific to API
   globs: apps/api/**/*.ts
   
   # ❌ Avoid: Too broad
   globs: **/*
   ```

2. **Consider File Types**: Different rules for different file types
   ```yaml
   # TypeScript files
   globs: **/*.ts
   
   # React components
   globs: **/*.tsx
   
   # Configuration files
   globs: **/*.config.{js,ts}
   ```

### Define Tasks:
Create task files in the docs/ directory with metadata (e.g., type: feature, context: api).
Example:
```
# Task: Implement Login Endpoint
- type: feature
- context: api
- description: Add endpoint for user authentication
```

#### Task Types:
- feature: A new feature or enhancement.
- bug: A bug fix.
- deploy: A deployment or release.
- refactor: A code refactoring.
- test: A test case.
- documentation: A documentation update.

#### Task Context:
- api: A API-related task.
- mobile: A mobile-related task.
- web: A web-related task.
- desktop: A desktop-related task.
- ai: A AI-related task.
- mcp: A MCP-related task.
- fullstack: A fullstack-related task.

#### Task Hierarchy:
- major task: A major task that requires multiple sub-tasks.
- sub-task: A sub-task of a major task.
- temporary task: A temporary task that is not part of the major task. No need to be committed.

### Autodocumentation:
Each task generate your own documentation in the docs/ directory.
- task-name: A name of the task. (e.g. task-feature-login.md)
- description: A description of the task.
- context: A context of the task.
- type: A type of the task.
- area: A area of the task.
- sub-task: A sub-task of the task.
- temporary task: A temporary task of the task.
- major task: A major task of the task.
- completed steps: A list of completed steps of the task.
- pending steps: A list of pending steps of the task.
- blocked steps: A list of blocked steps of the task.
- notes: A list of notes of the task.
- questions: A list of questions of the task.
- answers: A list of answers of the task.
- references: A list of references of the task.
- results: Documentation of the implemented code.

### Run task-manager.mdc:
The global rule will analyze task metadata and apply relevant rules (e.g., backend-feature.mdc, testing doubts).

#### Task Manager Functionality:
- **Standard Task Format**: Each task is described in a predefined format with fields like type, area, and description.
- **Automatic Analysis**: task-manager.mdc reads task metadata and selects relevant rules based on predefined criteria.
- **Rule Application**: Selected rules are automatically applied to the development context.

Example:
```
# Task: Fix UI Button Bug
- type: bug
- area: frontend
- description: Submit button not responding
```
Applied Rules: frontend-bug.mdc, testing.mdc, edge-cases.mdc, documentation.mdc, performance.mdc, accessibility.mdc, internationalization.mdc

### Contribute Rules:
Add new rules to the appropriate subdirectory (e.g., rules/frontend/ for React-specific rules).
Update index.mdc or sub-indices to reflect new rules.


## Available Rules

### Universal Rules:
- rule-writer.mdc: Guidelines for creating new rules.
- code-quality.mdc: Standards for code style and structure.
- testing.mdc: Guidelines for unit, integration, and end-to-end tests.
- documentation.mdc: Standards for Markdown documentation.
- security.mdc: Standards for security.
- code-review.mdc: Standards for code review.
- linting.mdc: Standards for linting.
- performance.mdc: Code optimization guidelines (avoid nested loops, use caches, etc.).
- accessibility.mdc: Frontend accessibility standards (WCAG compliance).
- internationalization.mdc: Multi-language support guidelines.

### Domain Rules:
- domain-aggregates.mdc: Defines aggregates and their boundaries.
- prd.mdc: Defines the product requirements document.
- application-flow.mdc: Defines the application flow in user stories.

### Task Rules:
- task-manager.mdc: Automates rule selection based on task metadata.
- tasks-index.mdc: Organizes task-related rules (features, bugs, deploys).

### AI Context Rules:
- context-provider.mdc: Generates context files per task with project dependencies, specific requirements, and task objectives.
- knowledge-base.mdc: Repository of technical documentation, best practices, and code examples accessible to AI agents.

### Technology-Specific Rules:
- mern-stack.mdc, react.mdc, nestjs.mdc, llm.mdc, mcp-agent.mdc, for stack-specific guidelines. (e.g. mern-stack.mdc for MERN stack, react.mdc for React, nestjs.mdc for NestJS. Or e.g api-development.mdc for API development, mobile-development.mdc for mobile development, etc. Or prisma-orm.mdc for Prisma ORM, etc.)

### DevOps Rules:
- ci-cd.mdc: Automates CI/CD pipeline configuration.
- monitoring.mdc: Sets up monitoring and logging.
- infra.mdc: Infrastructure rules.
- pull-request-writer.mdc: Writes pull request descriptions.
- git-commit-writer.mdc: Writes git commit messages.

## Index Structure

### Main Index Organization:
- **index.mdc**: Main entry point listing all available rules grouped by categories (domain, tasks, technology, etc.)

### Sub-indices by Context:
- **tasks-index.mdc**: Rules related to task types (features, bugs, deploys).
- **stacks-index.mdc**: Technology stack-specific rules (e.g., MERN, Spring).
- **frontend-index.mdc**: Frontend development rules (e.g., linting, testing).
- **backend-index.mdc**: Backend development rules (e.g., APIs, databases).
- **devops-index.mdc**: Deployment, CI/CD, and monitoring rules.

## Rule Organization

### Directory Structure:
- **rules/universal/**: Universal rules applicable across all projects.
- **rules/domain/**: Domain-driven design rules.
- **rules/tasks/**: Task-related rules and management.
- **rules/frontend/**: Frontend-specific rules.
- **rules/backend/**: Backend-specific rules.
- **rules/devops/**: DevOps and infrastructure rules.
- **rules/context/**: AI context and knowledge base rules.

### Documentation and Versioning:
- **rules-index.md**: Centralized documentation listing all rules and their purposes.
- **Version Control**: Track rule changes with versioning (e.g., rule-writer-v1.mdc, rule-writer-v2.mdc).
- **Feedback Loop**: Process for developers to suggest rule improvements after usage.

## Contributing
We welcome contributions to improve the framework! To contribute:

- Fork the repository.
- Create or modify rules in the rules/ directory.
- Update relevant indices (index.mdc, tasks-index.mdc, etc.).
- Submit a pull request with a detailed description (use pull-request-writer.mdc for automated PR generation).

## Future Improvements

-  Expand technology-specific rules for additional stacks (e.g., Flutter, Spring Boot).
- Enhance task-manager.mdc with machine learning to improve rule selection.
- Integrate with CI/CD tools for automated rule validation.
- Implement AI-powered rule suggestions based on project context.
- Add rule effectiveness tracking and analytics.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
