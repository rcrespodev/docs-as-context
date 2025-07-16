# docs-as-context
Universal Framework for AI-Assisted Programming

## Overview
docs-as-context is a comprehensive framework designed to enhance software development through AI-assisted programming. Built to be technology-agnostic, it provides a structured set of rules and tools to streamline coding, documentation, and testing processes across various stacks (e.g., MERN, Java, React, NestJS) and project types (e.g., monorepos, native apps, LLMs) following the code guidelenes of the technical team.
By leveraging tools like Cursor, this framework ensures consistency, scalability, and efficiency in development workflows.
The framework is designed to be used with Cursor, but can be used with other tools that support the same API. e.g you can use this framework with Windsurf.


## Key Features

- Document-as-Context: Each task generate and maintain your own documentation in the docs/tasks/ directory.
- Context-as-Code: Then you can use the auto-generated documentation to generate new code.
- Domain-Driven Design (DDD) Rules: Detailed guidelines for aggregates, models, business logic, edge cases, key users, and user stories to provide a clear understanding of the project domain.
- Automated Task Management: A global task-manager.mdc rule that intelligently applies relevant rules based on task type (e.g., feature, bug, deploy) and context (e.g., frontend, backend, devops).
- Structured Rule Organization: A main index.md and sub-indices (tasks-index.md, frontend-index.md, etc.) for easy navigation and scalability.
- Code Quality and Testing: Writte automated clean code with high standars of quality, testing and security. Rules for linting (linting.mdc), security(security.mdc), code review(code-review.mdc), and automated test generation (e.g., Jest .spec files) to maintain high standards.
- Temporary File Handling: Manages ephemeral files (e.g., logs, test configs) that are automatically created and deleted to keep the repository clean.
- Knowledge Base Management: knowledge-base.mdc maintains a repository of technical documentation, best practices, and code examples accessible to AI agents.
- Tech stack: Maintenaibles rules for each technology stack. e.g. mern-stack.mdc, react.mdc, nestjs.mdc, llm.mdc, mcp-agent.mdc, etc.
- Project Status Management: project-status.mdc maintains a repository of project status, progress, roadmap, backlog, sprint, sprint backlog, and sprint progress.
- Project Management: project-management.mdc maintains a repository of project management, status, progress, roadmap, backlog, sprint, sprint backlog, and sprint progress.
- Integration with github: git-commit-writer.mdc, git-issue-writer.mdc, pull-request-writer.mdc, etc.

## Base Template Structure

```yaml
root/
├── .cursor/rules/                  # All rule files
│   ├── core/               # Core rules
│   │   ├── task-manager.mdc             # Task manager rules
│   │   ├── testing.mdc                  # Testing rules
│   │   ├── code-quality.mdc            # Standards for writing quality code
│   │   ├── code-security.mdc           # Standards for writing secure code
│   │   ├── code-review.mdc             # Code review automation rules
│   │   ├── rule-writer.mdc             # Guidelines for creating new rules with consistent standards
│   │   ├── pull-request-writer.mdc     # Guidelines for writing pull request comments
│   │   ├── git-commit-writer.mdc       # Guidelines for writing git commit messages //TODO
│   │   ├── git-issue-writer.mdc        # Guidelines for writing git issues according to project templates //TODO
│   │   ├── code-linting-guidelines.mdc # Guidelines for following project linting standards
│   │   ├── documentation-guidelines.mdc # Guidelines for writing project documentation
│   │   ├── project-structure.mdc       # Rules for following project structure
│   │   ├── locale-configuration.mdc    # Rules for writing documentation and code comments in project languages
│   │   ├── development.mdc             # Guidelines for getting started with the project
│   │   ├── knowledge-base.mdc          # Knowledge base for project functionality
│   │   └── project-management.mdc      # Rules for managing project documentation
│   ├── domain/             # Domain-driven design rules
│   │   ├── user-stories-guidelines.mdc         # Guidelines for writing user stories
│   │   ├── domain-events-guidelines.mdc        # Guidelines for domain events
│   │   ├── domain-services-guidelines.mdc      # Guidelines for domain services
│   │   ├── domain-repositories-guidelines.mdc  # Guidelines for domain repositories
│   │   ├── domain-value-objects-guidelines.mdc # Guidelines for domain value objects
│   │   └── domain-entities-guidelines.mdc      # Guidelines for domain entities
│   ├── devops/             # DevOps rules
│   │   ├── ci-cd.mdc                   # CI/CD configuration guidelines
│   │   ├── monitoring.mdc              # Monitoring configuration guidelines
│   │   └── infra.mdc                   # Infrastructure configuration guidelines
│   └── stacks/             # Technology stack rules
│       ├── mern-stack-guidelines.mdc   # MERN stack configuration guidelines
│       ├── react-guidelines.mdc        # React configuration guidelines
│       ├── nestjs-guidelines.mdc       # NestJS configuration guidelines
│       ├── api-testing-guidelines.mdc  # API testing configuration guidelines
│       ├── llm-guidelines.mdc          # LLM configuration guidelines
│       ├── prisma-guidelines.mdc       # Prisma configuration guidelines
│       ├── mcp-agent-guidelines.mdc    # MCP agent configuration guidelines
│       ├── nextjs-guidelines.mdc       # NextJS configuration guidelines
│       ├── tailwind-guidelines.mdc     # Tailwind configuration guidelines
│       ├── shadcn-guidelines.mdc       # Shadcn configuration guidelines
│       ├── typescript-guidelines.mdc   # TypeScript configuration guidelines
│       ├── javascript-guidelines.mdc   # JavaScript guidelines
│       ├── python-guidelines.mdc       # Python guidelines
│       ├── java-guidelines.mdc         # Java guidelines
│       ├── csharp-guidelines.mdc       # C# guidelines
│       ├── c-guidelines.mdc            # C guidelines
│       ├── c++-guidelines.mdc          # C++ guidelines
│       ├── go-guidelines.mdc           # Go guidelines
│       ├── rust-guidelines.mdc         # Rust guidelines
│       ├── php-guidelines.mdc          # PHP guidelines
│       └── ruby-guidelines.mdc         # Ruby guidelines
│   ├── index.md                   # Index of all rules
├── docs/                   # Centralized project documentation
│   ├── tasks/              # Task files
│   │   ├── tasks-index.md             # Index of all tasks
│   │   ├── temp/                       # Temporary tasks (not committed to repository)
│   │   │   └── temporary-task.md       # Temporary task template
│   │   ├── feature/                    # Feature tasks
│   │   │   └── login-feature-task.md   # Login feature task
│   │   ├── bug/                        # Bug tasks
│   │   │   └── bug-feature-task.md     # Bug fix task
│   │   ├── deploy/                     # Deploy tasks
│   │   │   └── deploy-feature-task.md  # Deployment task
│   │   ├── refactor/                   # Refactor tasks
│   │   │   └── refactor-feature-task.md # Code refactoring task
│   │   └── chore/                      # Chore tasks
│   │       └── chore-feature-task.md   # Maintenance task
│   ├── project-status/     # Project status documentation
│   │   ├── project-progress.md         # Project progress tracking
│   │   ├── project-status.md           # Current project status
│   │   ├── project-roadmap.md          # Project roadmap
│   │   ├── project-backlog.md          # Project backlog
│   │   ├── project-sprint.md           # Sprint planning
│   │   ├── project-sprint-backlog.md   # Sprint backlog
│   │   └── project-sprint-progress.md  # Sprint progress tracking
│   └── domain/             # Domain documentation
│       ├── prd.md                      # Product requirements document
│       ├── application-flow.md         # Application flow documentation
│       ├── application-architecture.md # Application architecture
│       └── user-stories/               # User stories
│           ├── features/               # Feature user stories
│           ├── user-stories-index.md  # User stories index
│           ├── user-stories-login.mdc  # Login user story
│           ├── user-stories-register.mdc # Registration user story
│           ├── user-stories-logout.mdc # Logout user story
│           ├── user-stories-forgot-password.mdc # Password recovery user story
│           ├── user-stories-reset-password.mdc # Password reset user story
│           ├── user-stories-update-password.mdc # Password update user story
│           ├── user-stories-update-profile.mdc # Profile update user story
│           └── user-stories-delete-profile.mdc # Profile deletion user story
├── temp/                   # Temporary files (ignored in .gitignore)
└── README.md               # This file
```

## Directory Structure Explanation

### Index rules directory

The index.md file is the main index of all rules with detailed description of each rule.

```
.cursor/rules/
├── index.md                   # Index of all rules
└── ...
```

### Rules Directory (`/.cursor/rules`)
The rules directory contains all the guidelines and standards that AI agents follow when working on the project. It's organized into four main categories:

#### Core Rules (`/.cursor/rules/core`)
Essential guidelines that apply across all aspects of development:
- **task-manager.mdc**: Defines how to create, structure, update and delete tasks in the docs/tasks/ directory
- **testing.mdc**: Standards for writing high-quality, maintainable tests. Apply to all tests. Is agnostic of the technology stack.
- **code-quality.mdc**: Standards for writing high-quality, maintainable code. Apply to all code. Is agnostic of the technology stack.
- **code-security.mdc**: Security best practices and guidelines for secure code development. Apply to all code. Is agnostic of the technology stack.
- **code-review.mdc**: Automated rules for code review processes. Apply manual to review the code.
- **rule-writer.mdc**: Guidelines for creating new rules with consistent standards
- **pull-request-writer.mdc**: Standards for writing effective pull request descriptions. Based on the tasks documentation.
- **git-commit-writer.mdc**: Guidelines for writing clear and descriptive commit messages. Based on the tasks documentation.
- **git-issue-writer.mdc**: Templates and standards for creating git issues.
- **code-linting-guidelines.mdc**: Project-specific linting rules and standards.
- **documentation-guidelines.mdc**: Standards for writing project documentation
- **project-structure.mdc**: Rules for maintaining consistent project structure
- **locale-configuration.mdc**: Guidelines for internationalization and localization
- **development.mdc**: Getting started guide for new developers
- **knowledge-base.mdc**: Centralized knowledge repository for project functionality
- **project-management.mdc**: Guidelines for project management and status tracking

#### Domain Rules (`/.cursor/rules/domain`)
Domain-Driven Design (DDD) specific guidelines:
- **user-stories-guidelines.mdc**: Standards for writing user stories
- **domain-events-guidelines.mdc**: Guidelines for domain event design and implementation
- **domain-services-guidelines.mdc**: Standards for domain service development
- **domain-repositories-guidelines.mdc**: Guidelines for repository pattern implementation
- **domain-value-objects-guidelines.mdc**: Standards for value object design
- **domain-entities-guidelines.mdc**: Guidelines for entity design and management

#### DevOps Rules (`/.cursor/rules/devops`)
Infrastructure and deployment guidelines:
- **ci-cd.mdc**: Continuous Integration/Continuous Deployment configuration
- **monitoring.mdc**: Application monitoring and logging setup
- **infra.mdc**: Infrastructure as Code and deployment guidelines

#### Technology Stack Rules (`/.cursor/rules/stacks`)
Technology-specific guidelines for various frameworks and languages:
- **mern-stack-guidelines.mdc**: MongoDB, Express, React, Node.js stack guidelines
- **react-guidelines.mdc**: React.js development standards
- **nestjs-guidelines.mdc**: NestJS framework guidelines
- **api-testing-guidelines.mdc**: API testing strategies and tools
- **llm-guidelines.mdc**: Large Language Model integration guidelines
- **prisma-guidelines.mdc**: Prisma ORM usage and best practices
- **mcp-agent-guidelines.mdc**: Model Context Protocol agent configuration
- **nextjs-guidelines.mdc**: Next.js framework guidelines
- **tailwind-guidelines.mdc**: Tailwind CSS usage standards
- **shadcn-guidelines.mdc**: Shadcn/ui component library guidelines
- **typescript-guidelines.mdc**: TypeScript development standards
- **javascript-guidelines.mdc**: JavaScript development standards
- **python-guidelines.mdc**: Python development standards
- **java-guidelines.mdc**: Java development standards
- **csharp-guidelines.mdc**: C# development standards
- **c-guidelines.mdc**: C language development standards
- **c++-guidelines.mdc**: C++ development standards
- **go-guidelines.mdc**: Go language development standards
- **rust-guidelines.mdc**: Rust language development standards
- **php-guidelines.mdc**: PHP development standards
- **ruby-guidelines.mdc**: Ruby development standards

### Documentation Directory (`/docs/`)
Centralized location for all project documentation:

#### Tasks (`/docs/tasks/`)
Organized task documentation by type:
- **tasks-index.md**: Master index of all project tasks
- **temp/**: Temporary tasks that are not committed to version control
- **feature/**: New feature development tasks
- **bug/**: Bug fix and issue resolution tasks
- **deploy/**: Deployment and release tasks
- **refactor/**: Code refactoring and improvement tasks
- **chore/**: Maintenance and housekeeping tasks

#### Project Status (`/docs/project-status`)
Project management and tracking documentation:
- **project-progress.md**: Overall project progress tracking
- **project-status.md**: Current project status and health
- **project-roadmap.md**: Long-term project roadmap
- **project-backlog.md**: Product backlog management
- **project-sprint.md**: Sprint planning and management
- **project-sprint-backlog.md**: Sprint-specific backlog items
- **project-sprint-progress.md**: Sprint progress tracking

#### Domain Documentation (`/docs/domain`)
Business domain and requirements documentation:
- **prd.md**: Product Requirements Document
- **application-flow.md**: Application user flow documentation
- **application-architecture.md**: System architecture documentation
- **user-stories/**: Detailed user stories organized by feature

### Temporary Directory (`/temp`)
Contains temporary files that are automatically generated and cleaned up. This directory is ignored by version control to keep the repository clean.

## Getting Started

Clone the Repository:git clone https://github.com/<your-org>/docs-as-context.git
cd docs-as-context


### Set Up Your AI Tool:
Configure Cursor or your preferred AI-assisted programming tool.
Load the rules/ directory into the tool to enable rule-based automation.

## Configure the Rules:

- [ ] Configure the locale configuration in the rules/core/locale-configuration.mdc file.
- [ ] Configure the project structure in the rules/core/project-structure.mdc file.
- [ ] Configure the development guidelines in the rules/core/development.mdc file.
- [ ] Configure the knowledge base in the rules/core/knowledge-base.mdc file.
- [ ] Configure the project management guidelines in the rules/core/project-management.mdc file.
- [ ] Configure the code quality rules in the rules/core/code-quality.mdc file.
- [ ] Configure the code security rules in the rules/core/code-security.mdc file.
- [ ] Configure the code review rules in the rules/core/code-review.mdc file.
- [ ] Configure the code linting rules in the rules/core/code-linting-guidelines.mdc file.
- [ ] Configure the documentation rules in the rules/core/documentation-guidelines.mdc file.
- [ ] Configure the project stack rules in the rules/stacks/ directory.
- [ ] Configure the task manager rules in the rules/core/task-manager.mdc file accordion to project stacks.
- [ ] Configure the domain rules in the rules/domain/ directory.
- [ ] Configure the devops rules in the rules/devops/ directory.

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

#### Nested rules
Organize rules by placing them in .cursor/rules directories throughout your project. Nested rules automatically attach when files in their directory are referenced.

```
project/
  .cursor/rules/        # Project-wide rules
  backend/
    server/
      .cursor/rules/    # Backend-specific rules
  frontend/
    .cursor/rules/      # Frontend-specific rules
```

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
Create task files in the docs/tasks directory with metadata (e.g., type: feature, context: api). Atach the task to the appropriate folder (e.g. feature, bug, deploy, refactor, chore). The rules task-manager.mdc will apply the appropriate rules to the task.
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
- chore: A maintenance task.

#### Task Context:
- api: A API-related task. -> atach rules like .rules/stacks/api-development.mdc
- mobile: A mobile-related task. -> atach rules like .rules/stacks/mobile-development.mdc
- web: A web-related task. -> atach rules like .rules/stacks/web-development.mdc
- desktop: A desktop-related task. -> atach rules like .rules/stacks/desktop-development.mdc
- ai: A AI-related task. -> atach rules like .rules/stacks/ai-development.mdc
- mcp: A MCP-related task. -> atach rules like .rules/stacks/mcp-development.mdc
- fullstack: A fullstack-related task. -> atach multiple rules.

#### Task Hierarchy:
- major task: A major task that requires multiple sub-tasks.
- sub-task: A sub-task of a major task.
- temporary task: A temporary task that is not part of the major task. No need to be committed.

### Autodocumentation:
Each task generate and maintain your own documentation in the docs/tasks/ directory.
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
Add new rules to the appropriate subdirectory (e.g., rules/stacks/ for React-specific rules).
Update index.md or sub-indices to reflect new rules.

## Contributing
We welcome contributions to improve the framework! To contribute:

- Fork the repository.
- Create or modify rules in the rules/ directory.
- Update relevant indices (index.md, tasks-index.md, etc.).
- Submit a pull request with a detailed description (use pull-request-writer.mdc for automated PR generation).

## Future Improvements

- Expand technology-specific rules for additional stacks (e.g., Flutter, Spring Boot).
- Enhance task-manager.mdc with machine learning to improve rule selection.
- Integrate with CI/CD tools for automated rule validation.
- Implement AI-powered rule suggestions based on project context.
- Add rule effectiveness tracking and analytics.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
