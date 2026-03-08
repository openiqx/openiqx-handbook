# How to Sync Your Fork and Keep Your Feature Branch Updated

When you’re working on a feature branch in your fork, the original project (upstream) keeps moving forward, new commits are added to `main`, other contributors merge their changes, and release branches may be updated. To avoid conflicts and keep your feature branch up to date, you need to **sync your fork** regularly and **rebase (or merge) the latest changes** into your feature branch.

This guide walks you through the entire process, from setting up the upstream remote to updating your feature branch safely.

---

## Step 0: Prerequisites – Upstream Remote Added

If you haven’t already, add the original project as a remote called `upstream`:

```bash
git remote add upstream https://github.com/original-owner/project.git
```

Verify your remotes:

```bash
git remote -v
```

You should see both `origin` (your fork) and `upstream`.

---

## Step 1: Fetch the Latest Changes from Upstream

Before updating anything, download all new commits from the original repository:

```bash
git fetch upstream
```

This fetches all branches from upstream (e.g., `upstream/main`, `upstream/release-1.2`) but does **not** change any of your local branches yet.

---

## Step 2: Update Your Local `main` Branch

Switch to your local `main` branch:

```bash
git checkout main
```

Now, update it to match the upstream `main` exactly. There are two common ways: **rebase** or **merge**. We recommend **rebase** to keep a linear history, but merging works too.

### Option A: Rebase (cleaner history)
```bash
git rebase upstream/main
```

This replays your local commits (if any) on top of the latest upstream commits. Since you probably haven’t committed directly to `main`, this simply fast‑forwards your local `main` to the same commit as `upstream/main`.

### Option B: Merge (simpler, but creates a merge commit)
```bash
git merge upstream/main
```

If there are no local commits on `main`, both commands do the same thing: fast‑forward to the latest upstream commit.

---

## Step 3: Push the Updated `main` to Your Fork

After updating your local `main`, push it to your fork (`origin`):

```bash
git push origin main
```

If your fork’s `main` has diverged (e.g., because you accidentally committed there), you may need to force‑push. But in a normal workflow where you never commit directly to `main`, a simple `git push` works.

---

## Step 4: Switch to Your Feature Branch

Now go back to the branch where you’re doing your work:

```bash
git checkout my-feature-branch
```

---

## Step 5: Update Your Feature Branch with the Latest `main`

You have two main options to bring in the new changes from `main`: **merge** or **rebase**.

### Option 1: Rebase (recommended for feature branches)

Rebasing rewrites your feature branch’s history so that it appears as if you started your work from the current `main`. This results in a clean, linear history.

```bash
git rebase main
```

If there are conflicts, Git will pause and let you resolve them.

1. Git will show which files are conflicted.
2. Edit those files to resolve conflicts (look for `<<<<<<<`, `=======`, `>>>>>>>` markers).
3. After resolving, stage the changes:

   ```bash
   git add .
   ```

4. Continue the rebase:

   ```bash
   git rebase --continue
   ```

Repeat until all commits are applied.

**After rebasing, your feature branch’s history has changed.** You will need to force‑push it to your fork because the commit SHAs are different.

```bash
git push --force-with-lease origin my-feature-branch
```

`--force-with-lease` is safer than `--force` because it checks if your remote branch has been updated by someone else (unlikely for a personal feature branch, but good practice).

### Option 2: Merge (simpler, but adds a merge commit)

If you prefer not to rewrite history, you can merge `main` into your feature branch:

```bash
git merge main
```

Resolve any conflicts, then commit the merge. Then push normally (no force needed):

```bash
git push origin my-feature-branch
```

The downside is that your feature branch’s history will include a merge commit, which can make the PR timeline a bit messier, but it’s perfectly acceptable in many projects.

---

## Step 6: Continue Working or Open a Pull Request

Your feature branch is now up to date with the latest upstream `main`. You can continue developing, or if you’re ready, open a pull request against the upstream repository.

---

## Quick Summary

```bash
# Fetch upstream changes
git fetch upstream

# Update local main
git checkout main
git rebase upstream/main
git push origin main

# Update feature branch
git checkout my-feature-branch
git rebase main                  
git push --force-with-lease origin my-feature-branch   # if rebased
```

---

## Important Tips

- **Never work directly on `main`.** Always create feature branches from an updated `main`.
- **Rebase your feature branch frequently** to minimize conflicts later.
- **Communicate with your team** if you’re force‑pushing to a shared branch (usually not an issue for personal forks).
- **Use `--force-with-lease`** instead of `--force` to avoid accidentally overwriting someone else’s changes.

By keeping your fork and feature branches in sync, you ensure a smooth integration when it’s time to open that pull request
