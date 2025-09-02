### I. Basic Git Concepts

1.  **What is Git?**
    *   *Hint: Distributed Version Control System (DVCS), tracking changes, collaboration.*
2.  **What is the difference between Git and GitHub?**
    *   *Hint: Git is the tool, GitHub is a hosting service for Git repositories.*
3.  **What is a repository in Git?**
    *   *Hint: Project folder, `.git` directory, history.*
4.  **Explain the three states of Git (working directory, staging area, local repository).**
    *   *Hint: Modified, Staged, Committed.*
5.  **What is a commit? What does a commit object contain?**
    *   *Hint: Snapshot, metadata (author, date, message), pointer to parent commit.*
6.  **What is the purpose of the `.git` directory?**
    *   *Hint: Stores all Git's metadata for the repository.*
7.  **What is a "head" in Git?**
    *   *Hint: Pointer to the tip of the current branch.*

### II. Common Git Commands

1.  **How do you initialize a new Git repository?**
    *   *Command: `git init`*
2.  **How do you add files to the staging area?**
    *   *Command: `git add <file>` or `git add .`*
3.  **How do you commit changes? What makes a good commit message?**
    *   *Command: `git commit -m "message"` or `git commit`*
    *   *Hint: Concise subject line, detailed body, imperative mood.*
4.  **How do you check the status of your working directory and staging area?**
    *   *Command: `git status`*
5.  **How do you view the commit history?**
    *   *Command: `git log` (and its various options like `--oneline`, `--graph`, `--all`)*
6.  **How do you view the differences between your working directory and the staging area?**
    *   *Command: `git diff`*
7.  **How do you view the differences between the staging area and the last commit?**
    *   *Command: `git diff --staged` or `git diff --cached`*
8.  **How do you view the differences between two commits?**
    *   *Command: `git diff <commit1> <commit2>`*
9.  **How do you clone a repository?**
    *   *Command: `git clone <URL>`*

### III. Branching and Merging

1.  **What is a branch in Git? Why are branches useful?**
    *   *Hint: Independent line of development, isolation, feature development.*
2.  **How do you create a new branch?**
    *   *Command: `git branch <branch-name>`*
3.  **How do you switch between branches?**
    *   *Command: `git checkout <branch-name>` or `git switch <branch-name>` (newer)*
4.  **How do you create a new branch and switch to it immediately?**
    *   *Command: `git checkout -b <branch-name>` or `git switch -c <branch-name>`*
5.  **How do you list all branches?**
    *   *Command: `git branch` (local), `git branch -r` (remote), `git branch -a` (all)*
6.  **What are the two main ways to integrate changes from one branch into another? Explain the difference.**
    *   *Hint: `git merge` vs. `git rebase`.*
7.  **Explain a "fast-forward" merge.**
    *   *Hint: No new merge commit, linear history.*
8.  **Explain a "three-way" merge (recursive merge).**
    *   *Hint: Common ancestor, new merge commit.*
9.  **What is a merge conflict? How do you resolve one?**
    *   *Hint: When Git can't automatically combine changes, manual editing, `git add`, `git commit`.*
10. **When would you use `git merge --no-ff`?**
    *   *Hint: To always create a merge commit, even for fast-forwardable merges, to preserve branch history.*
11. **How do you delete a local branch? How do you delete a remote branch?**
    *   *Command: `git branch -d <branch-name>`, `git push origin --delete <branch-name>`*

### IV. Remote Repositories

1.  **What is a remote repository?**
    *   *Hint: Version of your project hosted on the internet or network, collaboration.*
2.  **How do you add a remote repository?**
    *   *Command: `git remote add <name> <URL>`*
3.  **What is the default name for the main remote repository?**
    *   *Answer: `origin`*
4.  **How do you push your local commits to a remote repository?**
    *   *Command: `git push <remote-name> <branch-name>`*
5.  **How do you fetch changes from a remote repository without merging them?**
    *   *Command: `git fetch`*
6.  **How do you fetch changes from a remote repository and merge them into your current branch?**
    *   *Command: `git pull` (which is `git fetch` + `git merge`)*
7.  **What is the difference between `git fetch` and `git pull`?**
    *   *Hint: `fetch` only downloads, `pull` downloads and integrates.*

### V. Undoing Changes / History Rewriting

1.  **How do you undo uncommitted changes in your working directory?**
    *   *Command: `git restore <file>` or `git checkout -- <file>`*
2.  **How do you unstage a file?**
    *   *Command: `git restore --staged <file>` or `git reset HEAD <file>`*
3.  **What is `git revert`? When would you use it?**
    *   *Hint: Creates a new commit that undoes the changes of a previous commit, safe for shared history.*
4.  **What is `git reset`? Explain the different modes (`--soft`, `--mixed`, `--hard`).**
    *   *Hint: Moves `HEAD` and optionally the index/working directory. `--soft` (moves HEAD), `--mixed` (moves HEAD and unstages), `--hard` (moves HEAD, unstages, and discards working directory changes). Use with caution on shared history.*
5.  **When would you use `git reset --hard`? What are the risks?**
    *   *Hint: To completely discard all local changes and commits, dangerous as it's destructive.*
6.  **What is `git stash`? When is it useful?**
    *   *Hint: Temporarily saves changes that are not ready to be committed, useful for context switching.*
7.  **How do you apply a stashed change?**
    *   *Command: `git stash apply` or `git stash pop`*
8.  **What is `git rebase -i` (interactive rebase)? What can you do with it?**
    *   *Hint: Rewriting history, squashing commits, reordering commits, editing commit messages.*
9.  **When should you avoid rebasing?**
    *   *Hint: On branches that have been pushed to a shared remote repository.*

### VI. Advanced Concepts / Best Practices

1.  **Explain Git flow or GitHub flow.**
    *   *Hint: Common branching strategies for managing releases and features.*
2.  **What is a "detached HEAD" state? How do you get out of it?**
    *   *Hint: When `HEAD` points directly to a commit instead of a branch. Create a new branch or checkout an existing one.*
3.  **What is a Git hook? Give an example.**
    *   *Hint: Scripts that Git executes before or after events (e.g., `pre-commit`, `post-merge`).*
4.  **What is `git reflog`? When would you use it?**
    *   *Hint: Records all changes to `HEAD`, useful for recovering lost commits or branches.*
5.  **How do you squash multiple commits into a single commit?**
    *   *Hint: Using `git rebase -i`.*
6.  **What is the purpose of `.gitignore`?**
    *   *Hint: Specifies untracked files that Git should ignore (e.g., compiled code, logs, `.env` files).*
7.  **How do you handle large binary files in Git?**
    *   *Hint: Git LFS (Large File Storage).*
8.  **What is a submodule in Git? When would you use it?**
    *   *Hint: Embedding one Git repository inside another as a subdirectory, for managing external dependencies.*
9.  **Explain the difference between `git cherry-pick` and `git revert`.**
    *   *Hint: `cherry-pick` applies a specific commit from one branch to another, `revert` creates an inverse commit.*
10. **Describe your typical Git workflow for contributing to a project.**
    *   *Hint: Clone, create feature branch, commit, rebase/merge with `main`/`develop`, push, pull request.*

### VII. Scenario-Based Questions

1.  **You've accidentally committed sensitive information (e.g., API keys) and pushed it to a public repository. What do you do?**
    *   *Hint: `git filter-repo` (recommended) or `git rebase -i` (if not pushed), then notify, invalidate credentials.*
2.  **You're working on a feature branch, and suddenly an urgent bug fix is required on `main`. What's your approach?**
    *   *Hint: `git stash`, switch to `main`, fix bug, commit, switch back, `git stash pop`.*
3.  **You made several commits on your feature branch, but your team lead wants you to combine them into a single, clean commit before merging. How would you do this?**
    *   *Hint: `git rebase -i HEAD~<number of commits>` and use the `squash` command.*
4.  **Your colleague pushed some changes to a shared branch, and you pulled them. Now you realize their changes introduced a bug. How would you fix this collaboratively?**
    *   *Hint: Discuss, then potentially `git revert` their problematic commit, or collaboratively fix and commit new changes.*
5.  **You have a local commit that you haven't pushed yet, but you realize you want to amend its message or add more files to it. How would you do that?**
    *   *Hint: Stage additional files, then `git commit --amend`.*
