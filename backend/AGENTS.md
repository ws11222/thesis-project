# Repository Guidelines

## Project Structure & Module Organization
This repository is a Kotlin Spring Boot backend. Application code lives under `src/main/kotlin/com/example/itda`, organized by domain (`program`, `user`, `embedding`, `feedCache`) with the usual `controller`, `service`, `persistence`, and `config` packages. Runtime config and SQL bootstrap files are in `src/main/resources` (`application.yaml`, `init_db.sql`). Tests live in `src/test/kotlin/com/example/itda`, with integration-style API tests such as `ProgramTest.kt` and `UserTest.kt`.

## Build, Test, and Development Commands
Use the Gradle wrapper from the repository root:

- `./gradlew bootRun`: start the API locally.
- `./gradlew test`: run the JUnit 5 test suite.
- `./gradlew ktlintCheck`: check Kotlin formatting and style.
- `./gradlew build`: compile, test, and package the app.
- `docker compose up`: start the containerized deployment defined in `docker-compose.yml`.

Set required database variables before local runs. `src/main/resources/application.yaml` expects `DB_URL`, `DB_USERNAME`, and `DB_PASSWORD`.

## Coding Style & Naming Conventions
Follow standard Kotlin conventions: 4-space indentation, trailing commas where already used, `UpperCamelCase` for classes, `lowerCamelCase` for functions and properties, and package names in lowercase. Keep Spring components grouped by feature rather than by technical layer across the whole repo. Run `./gradlew ktlintCheck` before opening a PR; the project uses `org.jlleitschuh.gradle.ktlint`.

## Testing Guidelines
Tests use JUnit 5, Spring Boot Test, MockMvc, MockK/Mockito, and Testcontainers with PostgreSQL/pgvector. Prefer test classes named `*Test.kt` and descriptive backtick test names that state behavior, as in the existing API tests. Add or update tests for every controller, service, or persistence change. Run `./gradlew test` locally before pushing; there is no explicit coverage threshold in the repo, so rely on meaningful behavior coverage.

## Commit & Pull Request Guidelines
Recent commits follow a lightweight conventional style such as `fix(fe) #194 : logo`. Prefer `type(scope) #issue : summary`, keeping the summary short and imperative. PRs should include a concise description, linked issue number, test evidence (`./gradlew test`, `./gradlew ktlintCheck`), and sample request/response details for API changes.

## Security & Configuration Tips
Do not commit real secrets. Keep environment values in `.env` or local shell config, and treat JWT and database credentials as local-only. Review `docker-compose.yml` carefully before changing tunnel or SSH-related settings.
