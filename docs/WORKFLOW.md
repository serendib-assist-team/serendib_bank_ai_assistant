# Team Collaboration Workflow

This document defines how the seven project members collaborate on the **Serendib Bank AI Assistant** repository.

## 1. Core principles

- Keep the `main` branch stable and suitable for demonstration.
- Do not commit or push directly to `main`.
- Use GitHub Issues to define, discuss, assign, and track work.
- Use feature branches and pull requests for all code and documentation changes.
- Keep changes focused, reviewable, and connected to an issue whenever practical.
- Communicate early about blockers, design changes, and work that affects another member.

## 2. Before starting work

1. Check the project plan and existing Issues before creating duplicate work.
2. Open or update an Issue describing the task, its context, and acceptance criteria.
3. Discuss major architecture, data-source, model, or interface decisions with the team before implementation.
4. Agree on ownership and identify dependencies.
5. Keep the agreed project constraints in mind:
   - Use public, appropriate banking and financial information sources.
   - Do not use real customer records, credentials, or confidential bank information.
   - Keep the prototype within the project's zero-cost/open-source constraint.
   - Ground generated answers in retrieved evidence and provide source citations.
   - Require human confirmation for actions that should not be executed autonomously.

Use GitHub Discussions, if enabled for this repository, for broad questions and open-ended design conversations. Use Issues for work that needs an owner and a trackable outcome.

## 3. Branch naming

Create a branch from the latest `main` branch for each independent task.

Use one of these prefixes:

| Prefix | Purpose | Example |
|---|---|---|
| `feature/` | New functionality | `feature/document-ingestion` |
| `fix/` | Bug fixes | `fix/retrieval-filtering` |
| `docs/` | Documentation | `docs/setup-guide` |
| `test/` | Tests and evaluation | `test/rag-evaluation` |
| `chore/` | Maintenance and configuration | `chore/dependency-update` |

Keep branch names short and descriptive. Avoid spaces.

## 4. Recommended Git workflow

Start by updating your local `main` branch:

```bash
git switch main
git pull origin main
```

Create a branch for your Issue:

```bash
git switch -c feature/short-task-name
```

Make focused changes and commit them with meaningful messages:

```bash
git add .
git commit -m "Add document metadata extraction"
git push -u origin feature/short-task-name
```

Open a pull request on GitHub with:

- Base branch: `main`
- Compare branch: your task branch
- A clear summary of the changes
- A link to the related Issue
- Testing or verification notes

Do not merge your own pull request unless the lecturer or team has explicitly agreed to an exception. Wait for review and approval.

## 5. Pull request review

- Every pull request should be reviewed by at least one other team member before merging.
- The author should not approve their own pull request.
- Reviewers should check correctness, clarity, maintainability, project constraints, and relevant tests.
- Ask questions or request changes when something is unclear or incomplete.
- Resolve review conversations and update the branch before merging.
- Prefer small pull requests that are easy to understand and verify.

## 6. Commit and individual contribution

- Each member must work using their own GitHub account.
- Commit messages should describe the actual change, for example:
  - `Add PDF text extraction utility`
  - `Create retrieval evaluation tests`
  - `Document API configuration`
- Avoid empty, misleading, or unrelated commits.
- The project brief requires at least **three meaningful commits per member**. Plan work so each member contributes genuine, reviewable changes.
- Keep Issues, pull requests, and commit history aligned with the work completed.

## 7. AI-assisted development

AI tools may be used as development support, but each contributor is responsible for the work they submit.

- Understand, inspect, and test AI-generated code before committing it.
- Do not submit code that you cannot explain.
- Verify factual claims, citations, dependencies, and generated configuration.
- Record AI assistance in the project's AI-use log when required by the coursework.
- Never paste credentials, private documents, customer data, or confidential information into AI tools.

## 8. Security, privacy, and project constraints

- Never commit API keys, passwords, access tokens, private keys, or local secret files.
- Keep a safe `.env.example` containing placeholder values only; do not commit a real `.env` file.
- Do not include real customer data or confidential banking information.
- Check the licence and terms of public datasets and documents before using them.
- Do not add paid APIs, paid hosting, or other paid dependencies without explicit team and lecturer approval.
- Keep human confirmation in the loop for consequential agent actions.
- Report accidental exposure of a secret immediately and rotate the affected credential.

## 9. Keeping the repository healthy

- Update documentation when setup steps, interfaces, or behaviour change.
- Keep dependencies necessary and explain significant additions.
- Add or update tests for changed behaviour where practical.
- Avoid committing generated files, caches, virtual environments, and large unrelated files.
- Communicate breaking changes before merging them.

## 10. Suggested repository settings

An organization owner or repository administrator should configure a branch ruleset for `main` where the GitHub plan and repository settings allow it.

Recommended protections:

- Require pull requests before merging.
- Require at least one approving review.
- Dismiss stale approvals when new commits are pushed.
- Require conversation resolution before merging.
- Block force pushes.
- Block branch deletion.
- Do not allow routine team work to bypass the ruleset.

The team should also enable GitHub Issues and, if useful, GitHub Discussions in repository settings.

## 11. Definition of done

A task is ready to close when:

- Its acceptance criteria are met.
- Relevant tests or checks have been completed and reported.
- Documentation has been updated where needed.
- The pull request has received the required review and has been merged.
- No secrets, private data, or unapproved paid services have been introduced.
- The related Issue has been closed or updated.
