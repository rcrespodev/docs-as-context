Guidelines=Template

rules/
	core/ #Core rules
		tasks-guidelines.mdc		#Guidelines for the tasks -> regla para crear tareas en docs/tasks/
        code-quality.mdc		#Standards for writing code according to technical guidelines -> regla para que los agentes escriban codigo de calidad
        code-security.mdc #Standards for writing secure code according to technical guidelines -> regla para que los agentes escriban codigo seguro
        code-review.mdc #Code review automation rules -> regla para que los agentes revisen el codigo que ellos mismos escribieron
        rule-writer.mdc #New rules written guidelines -> regla para que los agentes escriban nuevas reglas con estandares consistentes.
        pull-request-writer.mdc #Pull request writer guidelines -> regla para que los agentes escriban los comentarios de los pull requests a partir de documentacion generada por los agentes en docs/tasks.
		git-commit-writer.mdc #Git commit writer guidelines -> regla para que los agentes escriban mensajes de commit.
        git-issue-writer.mdc #Git issue writer guidelines -> regla para que los agentes escriban issues acorde a los templates del proyecto.
        code-linting-guidelines.mdc #Code linting guidelines -> regla para que los agentes escriban codigo siguiendo los estandares de linting del proyecto.
        documentation-guidelines.mdc #Documentation guidelines -> regla para que los agentes escriban la documentacion del proyecto (prd y application-flow).
        project-structure.mdc #Project structure rules -> regla para que los agentes escriban codigo siguiendo la estructura del proyecto (project-structure.md).
        locale-configuration.mdc #Locale configuration rules -> regla para que los agentes escriban documentacion y comentarios de codigo siguiendo la configuracion de idiomas del proyecto.
        development.mdc # Getting started with the project -> regla para que los agentes escriban la documentacion de como empezar a trabajar en el proyecto.
        knowledge-base.mdc #Knowledge base for the project -> regla para que los agentes escriban la documentacion de como funciona el proyecto.
        project-management.mdc #Project management rules -> regla para que los agentes escriban la documentacion de como gestionar el proyecto en la folder docs/project-status.
	domain/ #Domain-driven design rules
        user-stories-guidelines.mdc		#Guidelines for the user stories -> regla para que los agentes escriban user stories acorde a los templates del proyecto.
        domain-events-guidelines.mdc #Domain events guidelines -> regla para que los agentes escriban eventos de dominio acorde a la definicion tecnica del proyecto.
        domain-services-guidelines.mdc #Domain services guidelines -> regla para que los agentes escriban servicios de dominio acorde a la definicion tecnica del proyecto.
        domain-repositories-guidelines.mdc #Domain repositories guidelines -> regla para que los agentes escriban repositorios de dominio acorde a la definicion tecnica del proyecto.
        domain-value-objects-guidelines.mdc #Domain value objects guidelines -> regla para que los agentes escriban objetos de valor de dominio acorde a la definicion tecnica del proyecto.
        domain-entities-guidelines.mdc #Domain entities guidelines -> regla para que los agentes escriban entidades de dominio acorde a la definicion tecnica del proyecto.
    devops/ #Devops rules
		ci-cd.mdc #CI/CD guidelines -> regla para que los agentes escriban la documentacion de como configurar el CI/CD del proyecto.
		monitoring.mdc #Monitoring guidelines -> regla para que los agentes escriban la documentacion de como configurar el monitoring del proyecto.
		infra.mdc #Infrastructure guidelines -> regla para que los agentes escriban la documentacion de como configurar la infraestructura del proyecto.
	stacks/ #Stacks rules
		mern-stack-guidelines.mdc #MERN stack guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con el stack MERN. 
		react-guidelines.mdc #React guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con React.
		nestjs-guidelines.mdc #NestJS guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con NestJS.
        api-testing-guidelines.mdc #API testing guidelines -> regla para que los agentes escriban la documentacion de como configurar el testing de la API del proyecto.
        llm-guidelines.mdc #LLM guidelines -> regla para que los agentes escriban la documentacion de como configurar el LLM del proyecto.
        prisma-guidelines.mdc #Prisma guidelines -> regla para que los agentes escriban la documentacion de como configurar el Prisma del proyecto.
        mcp-agent-guidelines.mdc #MCP agent guidelines -> regla para que los agentes escriban la documentacion de como configurar el MCP agent del proyecto.
        nextjs-guidelines.mdc #NextJS guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con NextJS.
        tailwind-guidelines.mdc #Tailwind guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con Tailwind.
        shadcn-guidelines.mdc #Shadcn guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con Shadcn.
        typescript-guidelines.mdc #Typescript guidelines -> regla para que los agentes escriban la documentacion de como configurar el proyecto con Typescript.
        javascript-guidelines.mdc #Javascript guidelines
        python-guidelines.mdc #Python guidelines
        java-guidelines.mdc #Java guidelines
        csharp-guidelines.mdc #C# guidelines
        c-guidelines.mdc #C guidelines
        c++-guidelines.mdc #C++ guidelines
        go-guidelines.mdc #Go guidelines
        rust-guidelines.mdc #Rust guidelines
        php-guidelines.mdc #PHP guidelines
        ruby-guidelines.mdc #Ruby guidelines
docs/ #Centralize the Documentation of the project 
		tasks/
            tasks-index.md #Index of the tasks
            temp/
                temporary-task.md #Temporary task (not committed to the repository)
			feature/
				login-feature-task.md #Task for the login feature
			bug/
				bug-feature-task.md #Task for the bug feature
			deploy/
				deploy-feature-task.md #Task for the deploy feature
			refactor/
				refactor-feature-task.md #Task for the refactor feature
			chore/
				chore-feature-task.md #Task for the chore feature
		project-status/
            project-progress.md #Project progress
            project-status.md #Project status
            project-roadmap.md #Project roadmap
            project-backlog.md #Project backlog
            project-sprint.md #Project sprint
            project-sprint-backlog.md #Project sprint backlog
            project-sprint-progress.md #Project sprint progress
        domain/
			prd.md #Product requirements document
            application-flow.md #Application flow
            application-architecture.md #Application architecture
            user-stories/
                features/
                user-stories-index.md #Index of the user stories
                user-stories-login.mdc #User story for the login feature
                user-stories-register.mdc #User story for the register feature
                user-stories-logout.mdc #User story for the logout feature
                user-stories-forgot-password.mdc #User story for the forgot password feature
                user-stories-reset-password.mdc #User story for the reset password feature
                user-stories-update-password.mdc #User story for the update password feature
                user-stories-update-profile.mdc #User story for the update profile feature
                user-stories-delete-profile.mdc #User story for the delete profile feature