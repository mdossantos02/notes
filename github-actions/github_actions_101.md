# GitHub Actions 101: A Beginner's Tutorial

GitHub Actions enables you to automate, customize, and execute your software development workflows right in your GitHub repository.

---

## 📘 What is GitHub Actions?

GitHub Actions is a CI/CD platform that allows you to automate your build, test, and deployment pipeline. You define workflows in YAML files stored in your GitHub repository.

---

## 🚀 Key Concepts

### 1. **Workflow**
A workflow is an automated process defined in `.github/workflows/*.yml`.

### 2. **Job**
A job is a set of steps that run in the same runner environment.

### 3. **Step**
A step is an individual task, either a shell command or an action.

### 4. **Runner**
A server that runs your workflows.

### 5. **Action**
Reusable extensions that perform a job (e.g., setup Node.js, deploy to AWS, etc.).

---

## 📁 File Structure

Your workflows go inside the `.github/workflows/` directory of your repo.

Example:
```
.github/
└── workflows/
    └── ci.yml
```

---

## ✏️ Creating Your First GitHub Action Workflow

Create a file: `.github/workflows/ci.yml`

```yaml
name: CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

---

## ⚙️ Trigger Types

- `push`: Triggered on a push to branches.
- `pull_request`: Triggered when a PR is opened.
- `schedule`: Runs at scheduled intervals (cron).
- `workflow_dispatch`: Manual trigger.

---

## 🧪 Using Actions

Actions are defined in the `uses` field. Examples:
- `actions/checkout@v3`: Checks out your repo.
- `actions/setup-node@v4`: Sets up Node.js.

You can find thousands of actions on the [GitHub Marketplace](https://github.com/marketplace?type=actions).

---

## 🛠 Debugging Workflows

- Visit the **Actions** tab in your repo.
- Select a workflow run to see logs.
- Add `run: echo "Debug info"` to inspect values.

---

## 📦 Caching Dependencies

Speed up builds with caching:

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-npm-
```

---

## ✅ Best Practices

- Use small, reusable steps.
- Use secrets for sensitive data (Settings → Secrets).
- Test workflows in branches before merging to `main`.

---

## 📚 Further Reading

- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [Workflow Syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [Action Marketplace](https://github.com/marketplace?type=actions)

---

Happy automating! 🚀
