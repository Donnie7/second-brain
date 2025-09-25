# Second Brain

This repository works as my **second brain**, where I organize ideas, notes, and knowledge in a structured way.  
The goal is to have a single place where ideas can be worked on daily and then integrated through **automatic Pull Requests**.

---

## 🚀 Workflow

1. Ideas and notes are discussed and organized.
2. Each set of changes is saved in files (e.g., `daily_notes/2025-09-25.md`).
3. These changes are pushed into a branch with the prefix `auto-pr/`.
4. GitHub Actions detects the push and automatically opens a **Pull Request** against the main branch (`main`).
5. I just need to review and merge the PR.

---

## ⚙️ Auto PR Configuration

The repository contains a GitHub Actions workflow at:

```
.github/workflows/auto-pr.yml
```

### Workflow content

```yaml
name: Auto Pull Request

on:
  workflow_dispatch:
  push:
    branches:
      - "auto-pr/**"

jobs:
  create-pr:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v4

      - name: Create Pull Request
        uses: peter-evans/create-pull-request@v6
        with:
          commit-message: "Auto PR update"
          branch: "auto-pr-generated"
          delete-branch: true
          title: "Auto PR from ChatGPT"
          body: "This PR contains the latest organized notes/ideas."
```

---

## 📝 Daily usage

1. Create a new branch:
   ```bash
   git checkout -b auto-pr/2025-09-25
   ```
2. Add the day’s notes:
   ```bash
   echo "Notes from 25-09-2025" > daily_notes/2025-09-25.md
   git add daily_notes/2025-09-25.md
