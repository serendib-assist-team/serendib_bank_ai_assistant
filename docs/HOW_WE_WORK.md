# How we work

Simple rules for everyone in the group, so that nobody changes things the others have not seen.

## 1. Talk before you change

- A new idea, a change to what the group is doing, or a bigger decision starts as an **Issue** (use the "Proposal or task" template) or a **Discussion**.
- Teammates comment. The group leader confirms the decision in the issue.
- Small fixes (a typo, a broken link) do not need an issue.

## 2. Never change `main` directly

1. Create a **branch** from `main`. Name it like `feature/short-name`, `fix/short-name` or `docs/short-name`.
2. Make your changes on that branch and commit them from your **own GitHub account**.
3. Open a **Pull Request** and fill in the template.
4. Someone **other than you** reviews it. Fix comments, then it is merged into `main`.

We do not use forks. Everyone in the organization can create branches in this repository.

## 3. Commits

- Everyone commits in their own name, with at least 3 meaningful commits each.
- Write a short message that says what changed.

## 4. Never commit

- API keys, passwords, tokens or `.env` files. Use `.env.example` for placeholders only.
- Real personal data of any kind.
- Anything we do not have permission to share. Check each source's licence before adding it.

## 5. Everyone keeps their own AI-use log

Record every use of an AI tool (date, tool, what you asked, what you used, what you changed, how you checked it). It is marked individually.

## 6. Understand everything you submit

The individual Q&A tests the whole system, not only your own part. Read each other's pull requests.
