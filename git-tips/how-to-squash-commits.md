# How to Squash Commits

Many open-source maintainers prefer pull requests to contain **a single clean commit**, even if you made many commits while developing.

Squashing combines multiple commits into **one final commit** before merging.

This keeps the project history clean and easier to read.

---

## When Squashing Is Useful

You may have commits like:

```
fix bug
fix typo
update test
address review comments
final fix
```

Maintainers usually prefer something like:

```
Fix scheduler cache invalidation
```

Squashing helps convert messy development history into a **clean final change**.

---

## Use Interactive Rebase (Recommended)

Run:

```
git rebase -i HEAD~3
```

Replace `3` with the number of commits you want to squash.

Git will open an editor like this:

```
pick a1b2c3 first commit
pick d4e5f6 second commit
pick g7h8i9 third commit
```

Change every commit after the first to `squash` or `s`:

```
pick a1b2c3 first commit
squash d4e5f6 second commit
squash g7h8i9 third commit
```

Save and exit.

Git will then allow you to edit the **final commit message**.

---

## Push the Updated Commit

After squashing, you must force push:

```
git push --force
```

Your pull request will update automatically.

---

## Important Note

Force pushing **only affects your branch**, not the main repository.

It is safe when working on your own PR branch.

---

## Quick Summary

```
git rebase -i HEAD~N
# change "pick" to "squash"
git push --force
```

Squashing makes your contribution **cleaner and easier for maintainers to review**.
