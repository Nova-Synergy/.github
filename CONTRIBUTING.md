# Contributing to Travel Bridge Platform

Thank you for contributing to **Travel Bridge Platform**, developed by the **Nova-Synergy** team.

This document defines the development workflow, branch strategy, pull request process, commit conventions, and collaboration rules that all team members should follow.

---

## 1. Team Structure

Travel Bridge is developed by a collaborative team where all members may contribute to both **Frontend and Backend** development.

### Repository Roles

- **Team Leader:** Responsible for project management, Pull Request review, approval, and merging into `main`.
- **Team Members:** Responsible for implementing assigned tasks, creating branches, pushing code, and opening Pull Requests.

Team members should not merge directly into `main`.

---

## 2. Main Branch

The `main` branch represents the stable version of the project.

### Rules

- Do not push directly to `main`.
- Do not force-push to `main`.
- Do not delete `main`.
- All changes must go through a Pull Request.
- Pull Requests require approval from the Team Leader.
- The Team Leader is responsible for the final merge.

---

## 3. Branch Strategy

We use short-lived branches for features, fixes, and other development tasks.

### Branch Naming

Use the following format:

```text
feature/<feature-name>
bugfix/<bug-name>
hotfix/<issue-name>
refactor/<area-name>
docs/<document-name>
test/<test-name>
```

### Examples

```text
feature/user-authentication
feature/trip-planning
feature/tour-guide-profile
feature/place-reviews

bugfix/login-validation
bugfix/booking-error

refactor/search-module

docs/update-api-documentation

test/trip-planning-tests
```

Keep branch names:

- Short
- Descriptive
- Written in English
- Related to the actual task

---

## 4. Starting a New Task

Before starting any task, make sure your local `main` branch is up to date.

```bash
git checkout main
git pull origin main
```

Create a new branch:

```bash
git checkout -b feature/your-feature-name
```

Example:

```bash
git checkout -b feature/trip-planning
```

---

## 5. Development Rules

While working on a task:

- Work only on your assigned branch.
- Do not modify unrelated parts of the project.
- Keep changes focused on the assigned task.
- Follow the existing project architecture and coding conventions.
- Avoid unnecessary refactoring.
- Do not commit passwords, API keys, connection strings, tokens, or other secrets.
- Test your changes before creating a Pull Request.
- Update documentation when your changes affect documented behavior.

---

## 6. Commit Messages

Commit messages should clearly describe what was changed.

### Recommended Format

```text
<type>: <short description>
```

### Common Types

| Type | Purpose |
|---|---|
| `feat` | Add a new feature |
| `fix` | Fix a bug |
| `refactor` | Improve code without changing behavior |
| `docs` | Documentation changes |
| `test` | Add or modify tests |
| `chore` | Maintenance or configuration |
| `style` | Formatting/style changes |

### Examples

```text
feat: add trip planning endpoint
fix: resolve review validation issue
docs: update project architecture
test: add trip planning tests
refactor: improve destination service
chore: update project dependencies
```

Keep commits small and meaningful.

Avoid messages such as:

```text
update
changes
final
test
new code
```

---

## 7. Pull Request Process

When your task is complete, push your branch:

```bash
git push -u origin feature/your-feature-name
```

Then create a Pull Request:

```text
Your Branch → main
```

### Pull Request Title

Use a clear title.

Examples:

```text
Add trip planning feature
Fix destination search validation
Implement tour guide availability
Add review management
```

### Pull Request Description

Every Pull Request should explain:

#### What was changed?

Describe the implemented functionality or fix.

#### Why was it changed?

Explain the problem or requirement being addressed.

#### Testing

Explain how the changes were tested.

Example:

```text
## What Changed
- Added trip creation endpoint
- Added trip validation
- Added database entities

## Why
Implemented the trip planning requirement.

## Testing
- Tested API endpoints using Swagger
- Added unit tests for validation
```

---

## 8. Pull Request Review

All Pull Requests targeting `main` must be reviewed by the **Team Leader**.

The Team Leader may:

- Approve the Pull Request
- Request changes
- Add comments
- Ask for additional tests
- Request architectural changes
- Merge the Pull Request

Team members can discuss and respond to review comments, but they should not approve or merge their own Pull Requests.

---

## 9. Updating a Pull Request

If changes are requested during review:

1. Stay on the same feature branch.
2. Make the requested changes.
3. Test the changes.
4. Commit and push again.

Example:

```bash
git add .
git commit -m "fix: address review comments"
git push
```

The existing Pull Request will automatically be updated.

---

## 10. Keeping Your Branch Updated

Before creating a Pull Request, make sure your branch is based on the latest `main`.

A simple approach:

```bash
git checkout main
git pull origin main
git checkout your-branch
git merge main
```

Resolve any conflicts locally, then test the project before pushing.

---

## 11. Merge Strategy

The project uses **Squash and Merge**.

This means multiple development commits from a Pull Request are combined into one clean commit on `main`.

Example:

```text
feature/trip-planning
    ├── feat: create trip entity
    ├── feat: add trip service
    ├── fix: validation
    └── test: trip service

                ↓ Squash & Merge

main
    └── feat: implement trip planning
```

This keeps the `main` branch history clean and easier to understand.

---

## 12. Code Quality

All contributors should follow these principles:

- Keep code readable and maintainable.
- Use meaningful names for classes, methods, variables, and files.
- Follow the project's architecture.
- Avoid duplicated code where practical.
- Handle errors properly.
- Validate user input.
- Write tests for important business logic.
- Keep methods and classes focused.
- Avoid introducing unnecessary dependencies.

---

## 13. Architecture Rules

Travel Bridge follows a **Modular Monolith** architecture.

The main modules include:

- Identity
- Catalog
- Search
- Community
- Planning
- AI Assistant
- Recommendations
- Guides
- Local Information
- Moderation
- Notifications
- Administration

### Important Rules

Modules should communicate through defined contracts and domain events where appropriate.

Avoid directly accessing another module's internal database tables or implementation details.

Each module should maintain clear boundaries between:

```text
API
 ↓
Application
 ↓
Domain
 ↓
Infrastructure
```

Infrastructure implementations should not leak into the Domain layer.

---

## 14. Database Changes

When modifying the database:

- Clearly document the change.
- Create the appropriate EF Core migration.
- Test the migration locally.
- Make sure existing functionality is not broken.
- Do not manually modify production databases without authorization.

Never commit sensitive database credentials.

---

## 15. API Development

For API changes:

- Follow RESTful conventions.
- Use appropriate HTTP methods and status codes.
- Validate incoming requests.
- Return consistent responses.
- Document new endpoints.
- Test endpoints using Swagger or an appropriate API testing tool.

For example:

```text
GET    /api/destinations
GET    /api/destinations/{id}
POST   /api/destinations
PUT    /api/destinations/{id}
DELETE /api/destinations/{id}
```

---

## 16. AI Integration

AI functionality is isolated behind an abstraction such as:

```text
IAiProvider
```

AI-generated suggestions must not directly modify critical domain data without proper validation.

AI-related features should consider:

- Input validation
- Rate limiting
- Usage tracking
- Error handling
- Provider independence
- Domain-level validation

API keys and AI provider credentials must never be committed to GitHub.

---

## 17. Testing

Before opening a Pull Request, run the relevant tests.

For .NET projects:

```bash
dotnet build
dotnet test
```

Contributors should test:

- New functionality
- Modified functionality
- Validation rules
- Important business logic
- API behavior where applicable

A Pull Request should not be opened if known build or test failures are introduced without documenting them.

---

## 18. Documentation

Documentation is part of the project.

When introducing a significant feature, update the relevant documentation.

Project documentation is located under:

```text
docs/
```

Important documents include:

```text
docs/
├── requirements-specification.md
├── uml-design.md
└── diagrams/
```

If your implementation changes an existing requirement or design decision, discuss it with the Team Leader before modifying the documentation.

---

## 19. Issue and Task Workflow

Before starting development:

1. Check the assigned task or issue.
2. Understand the requirements.
3. Ask questions if something is unclear.
4. Create a branch for the task.
5. Implement the solution.
6. Test it.
7. Create a Pull Request.
8. Address review feedback.
9. Wait for approval.
10. The Team Leader merges the Pull Request.

---

## 20. Conflict Resolution

If your branch has conflicts with `main`:

1. Update your local `main`.
2. Merge the latest `main` into your branch.
3. Resolve conflicts carefully.
4. Test the application.
5. Push the updated branch.

Never overwrite another developer's work without understanding the conflict.

---

## 21. Security

Never commit:

```text
API Keys
Passwords
JWT Secrets
Connection Strings
Access Tokens
Private Keys
Environment Secrets
```

Use appropriate local configuration mechanisms such as:

- Environment variables
- .NET User Secrets
- Local configuration files excluded by `.gitignore`
- Secret management services when required

If a secret is accidentally committed, report it immediately to the Team Leader.

---

## 22. General Team Rules

### Do

- Communicate before making major architectural changes.
- Keep Pull Requests focused.
- Review your own changes before submitting a PR.
- Test your code.
- Keep documentation updated.
- Respect other contributors.
- Ask for clarification when requirements are unclear.

### Don't

- Push directly to `main`.
- Merge your own Pull Request.
- Force-push shared branches without agreement.
- Commit secrets.
- Make large unrelated changes in a feature branch.
- Delete another contributor's work.
- Introduce major architectural changes without discussion.

---

## 23. Standard Workflow

The complete workflow is:

```text
Task / Issue
     ↓
Create Branch
     ↓
Develop
     ↓
Test
     ↓
Commit
     ↓
Push Branch
     ↓
Create Pull Request
     ↓
Team Leader Review
     ↓
Changes Requested?
   ↙          ↘
 Yes           No
  ↓             ↓
Fix & Push    Approve
  ↓             ↓
Review Again   Squash & Merge
                  ↓
                main
```

---

## 24. Final Rule

The goal of this workflow is not to make development complicated.

It exists to keep **Travel Bridge Platform**:

- Organized
- Stable
- Maintainable
- Easy to collaborate on
- Easy to review
- Safe to evolve

Every contributor is responsible for maintaining the quality of the project and respecting the team's development workflow.

---

**Travel Bridge Platform**  
**Nova-Synergy**  
*Building a scalable tourism platform for the future.*
