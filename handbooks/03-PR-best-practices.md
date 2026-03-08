# Writing Effective Pull Requests

After working on an issue and implementing a solution, the next step is to submit a **Pull Request (PR)**.

A pull request is how contributors propose changes to a repository and collaborate with maintainers during the review process.

Learning how to write **clear, focused, and well-structured pull requests** greatly increases the chances that your contribution will be accepted.

---

## What a Pull Request Is

A **Pull Request (PR)** is a request to merge your code changes into the main project repository.

It allows maintainers to:

* review your code
* suggest improvements
* ask questions
* request modifications
* eventually merge the change into the project

Pull requests are a **collaborative discussion around code**.

---

## The Typical Contribution Flow

A common open-source workflow looks like this:

1. Fork the repository
2. Clone your fork locally
3. Create a new branch
4. Make your changes
5. Commit your changes
6. Push the branch to your fork
7. Open a Pull Request

Example branch naming:

```
fix-login-bug
add-missing-tests
improve-error-handling
```

Use **descriptive branch names** that explain the purpose of the change.

---

## Keep Pull Requests Small

One of the most important best practices is:

**Keep pull requests small and focused.**

Avoid:

* fixing multiple unrelated issues in one PR
* large refactors mixed with bug fixes
* formatting changes mixed with logic changes

Good pull requests usually:

* solve **one specific issue**
* change **a small number of files**
* are easy for maintainers to review

Small PRs get merged **much faster**.

---

## Write a Clear Pull Request Title

Your title should clearly summarize the change.

Examples:

Good titles:

```
Fix incorrect cache invalidation in scheduler
Add missing unit tests for authentication service
Improve error handling in API request parser
```

Avoid vague titles like:

```
Update code
Fix stuff
Changes
```

A clear title helps maintainers quickly understand the purpose of the PR.

---

## Write a Helpful Pull Request Description

Your PR description should explain:

* what problem this change solves
* how the solution works
* any important implementation details

A simple format works well:

```
Problem:
Describe the issue this PR fixes.

Solution:
Explain how the problem was solved.

Testing:
Describe how the change was tested.
```

This context helps reviewers understand the reasoning behind your changes.

---

## Link the Related Issue

If your pull request fixes an issue, link it in the description.

Example:

```
Fixes #42
```

This automatically connects the PR to the issue and closes the issue when the PR is merged.

---

## Follow Project Conventions

Before submitting a PR, check the repository for:

* coding style guidelines
* commit message conventions
* formatting rules
* testing requirements

These are often described in:

```
CONTRIBUTING.md
```

or in the project's documentation.

Following these conventions makes review easier.

---

## Add Tests When Possible

Good pull requests often include **tests**.

For example:

* adding tests for new features
* adding tests that reproduce a bug
* improving coverage for existing code

Tests show maintainers that:

* the behavior is verified
* the change will not break other parts of the system

Even small test additions can significantly improve a contribution.

---

## Run Tests Before Submitting

Before opening a pull request, ensure that:

* all tests pass
* the project builds successfully
* no linting or formatting errors remain

Submitting a PR with failing tests slows down the review process.

---

## Be Open to Feedback

Maintainers may request changes during review.

Common feedback includes:

* improving code clarity
* adjusting implementation details
* adding tests
* following project conventions

This feedback is normal and part of the collaboration process.

Respond politely and make the requested updates when possible.

---

## Updating Your Pull Request

If reviewers request changes:

1. Make the updates locally
2. Commit the changes
3. Push the updated branch

Your pull request will automatically update.

You do **not** need to create a new PR.

---

## Avoid These Common Mistakes

New contributors sometimes:

* submit very large pull requests
* mix multiple changes together
* ignore project conventions
* fail to explain their changes
* submit PRs with failing tests

Avoiding these mistakes will make your contributions smoother.

---

## Final Advice

A good pull request is:

* focused
* clearly explained
* well-tested
* easy to review

Maintainers review many contributions, so making your PR **clear and organized** shows respect for their time and increases the likelihood that your work will be merged.

Learning to write great pull requests is one of the most valuable skills in open-source development.
