# How to Backport a Fix to Another Version

Sometimes a fix is merged into the **main branch** of an open source project, but it also needs to be applied to an **older release branch** (e.g., `release-1.2`). Applying the same change to another branch is called **backporting**.

Git makes this easy using `cherry-pick`. However, when you’re working from a **fork**, you need to set up your local repository correctly to have access to all the upstream branches.

This guide assumes you have already forked the project on GitHub and cloned your fork locally.

---

## Step 0: Set Up Your Local Repository with All Branches

Your fork (called `origin`) usually contains only the default branch (e.g., `main`). The original project (called `upstream`) has all the release branches. To get them locally, you need to add the upstream remote and fetch from it.

### 0.1 Add the upstream remote (if you haven’t already)

```bash
git remote add upstream https://github.com/original-owner/project.git
```

### 0.2 Fetch all branches from upstream

```bash
git fetch upstream
```

Now you have all upstream branches available locally as remote-tracking branches (e.g., `upstream/main`, `upstream/release-1.2`). You can list them with:

```bash
git branch -r
```

You’ll see both `origin/*` (your fork) and `upstream/*` (the original project).

### 0.3 Create a local branch for the target release (if you don’t have one)

If you want to backport to `release-1.2`, create a local branch that tracks the upstream release branch:

```bash
git checkout -b release-1.2 upstream/release-1.2
```

This gives you a local branch `release-1.2` that is exactly in sync with the upstream release branch. You’ll use this branch to apply the backport.

---

## Step 1: Find the Commit Hash

View the commit history in the branch where the fix was originally merged (usually `upstream/main` or `main` on your fork). You can do this without switching branches:

```bash
git log upstream/main
```

Find the commit that contains the fix. Example output:

```
commit a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0
Author: Your Name <you@example.com>
Date:   Mon Mar 8 12:00:00 2025 -0500

    Fix authentication timeout bug
```

Copy the commit hash (`a1b2c3d...`).

---

## Step 2: Switch to the Target Release Branch

```bash
git checkout release-1.2
```

Make sure your local branch is up to date with upstream (in case new changes were added after you created it):

```bash
git pull upstream release-1.2
```

---

## Step 3: Apply the Commit with Cherry‑pick

```bash
git cherry-pick a1b2c3d
```

Git will apply the changes from that commit onto your current branch. If the commit introduced changes that depend on other commits, you may need to cherry‑pick a range or additional commits, but for a single fix, this is usually enough.

---

## Step 4: Resolve Conflicts (If Any)

Sometimes the code in the older branch has diverged, causing conflicts. If `cherry-pick` reports conflicts:

1. Open the conflicting files and resolve the differences.
2. After resolving, stage the changes:

   ```bash
   git add .
   ```

3. Continue the cherry‑pick:

   ```bash
   git cherry-pick --continue
   ```

(If you ever want to abort the cherry‑pick, use `git cherry-pick --abort`.)

---

## Step 5: Push the Backport to Your Fork

Now that the fix is applied to your local `release-1.2` branch, push it to your fork (`origin`):

```bash
git push origin release-1.2
```

---

## Step 6: Open a Pull Request

Go to your fork on GitHub. You’ll likely see a prompt to create a pull request for the recently pushed branch. If not, navigate to the “Pull requests” tab and click “New pull request.”

- **Base repository:** The original project’s `release-1.2` branch.
- **Head repository:** Your fork’s `release-1.2` branch.

Create the pull request with a clear description that this is a backport of the original fix (include the original commit hash or PR number).

---

## Quick Summary

```bash
# Add upstream and fetch all branches
git remote add upstream <original-repo-url>
git fetch upstream

# Create local branch for the target release
git checkout -b release-1.2 upstream/release-1.2

# Cherry‑pick the fix
git cherry-pick <commit-hash>

# Push to your fork and open a PR
git push origin release-1.2
```

Backporting ensures that important fixes reach **all supported versions** of a project, keeping users on older releases secure and stable.
