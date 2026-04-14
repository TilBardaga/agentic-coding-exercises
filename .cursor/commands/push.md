---
description: Push already-committed work to the remote (push-only; no add/commit)
---

# Push (`/push`)

Transmit **commits that already exist locally** to **`origin`**. This command is **push-only**: no staging, no new commits.

If the working tree is **not clean**, stop and send the user to **`/finish`** first.

## Process

### 1. Preconditions

- Run: `git status --porcelain`
- **If not empty:** STOP. Tell the user: *You have uncommitted changes. Run **`/finish`** (or commit manually), then run **`/push`** again.*

- Run: `git rev-parse --abbrev-ref HEAD` → note **current branch**.
- Run: `git fetch origin` (or `git remote update` if `fetch` is unavailable—prefer `git fetch origin`).

- **Commits to push:** compare local branch to its upstream when set:

  ```bash
  git rev-list --count @{u}..HEAD
  ```

  If upstream is **not** configured, use the current branch name from step 1:

  ```bash
  git rev-list --count origin/<branch>..HEAD
  ```

  (replace `<branch>` with the current branch name).

- **If count is 0** (or no commits ahead): STOP. *Nothing local to push, or branch has no upstream—set upstream after first push if needed.*

### 2. Branch safety

- If current branch is **`main`** or **`master`**: **warn** that this pushes directly to the default branch; confirm it matches team practice.

### 3. Remote freshness

- After `fetch`, check if local is **behind** remote:

  ```bash
  git rev-list --count HEAD..origin/<branch>
  ```

- **If the count is greater than zero:** STOP. *Local branch is behind **`origin/<branch>`**. Pull/rebase or merge, resolve, then retry.*

### 4. Target check

- Run: `git remote -v`
- Confirm **`origin`** points at the repository you intend (not a wrong fork or template), unless the user said otherwise.

### 5. User confirmation

Show a short checklist:

- Branch name  
- Commits ahead (count)  
- Clean working tree  
- Not behind remote  

Ask explicitly: *Ready to push these commits to **`origin`**?* Wait for clear approval (e.g. yes / go / push it).

### 6. Push

Only after approval:

```bash
git push -u origin HEAD
```

Use `-u` so the upstream is set when missing. If upstream already exists, `git push` is enough—you may use either per local git defaults.

## Hard restrictions

- **Never** `git add` or `git commit` in this workflow.
- **Never** amend or rebase unless the user explicitly asks in this session for a different workflow.
- Uncommitted changes → always redirect to **`/finish`**.
