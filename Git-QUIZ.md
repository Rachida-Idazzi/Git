<div align="center">

<h1>
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=30&pause=1000&color=0B5ED7&center=true&vCenter=true&width=650&lines=Git+Concepts+Quiz;Fetch+%7C+Rebase+%7C+Revert;Think+first.+Toggle+to+reveal." alt="Git Concepts Quiz" />
</h1>

<p><b>One scenario quiz. No coding required. Click a question to reveal the answer.</b></p>

</div>

---

### 🌿 Scenario Quiz — Git

*Branches, remotes, reset vs revert, rebase, detached HEAD, and the everyday traps.*

<details>
<summary><b>1.</b> What's the difference between <code>git fetch</code> and <code>git pull</code>?</summary>

`fetch` downloads new commits from the remote into your local refs but leaves your working branch untouched. `pull` = `fetch` + `merge` (or `rebase`, if configured) — it also updates your current branch.
</details>

<details>
<summary><b>2.</b> What does <code>git status</code> tell you that <code>git log</code> doesn't?</summary>

The state of your **working tree and index**: what's modified, staged, untracked, or conflicted right now. `log` only shows commits already recorded in history.
</details>

<details>
<summary><b>3.</b> What's the difference between a <b>branch</b> and a <b>tag</b>? When do you use each?</summary>

A branch is a **moving pointer** that advances as you commit — used for ongoing work. A tag is a **fixed pointer** to one specific commit — used to mark releases (`v1.0`).
</details>

<details>
<summary><b>4.</b> You committed to <code>main</code> by mistake. How do you move that commit to a new branch and reset <code>main</code>?</summary>

`git branch new-branch` (points new branch at current commit), then `git reset --hard HEAD~1` on `main`. Switch with `git checkout new-branch` and keep working there.
</details>

<details>
<summary><b>5.</b> What does <code>git reset --soft HEAD~1</code> do vs <code>git reset --hard HEAD~1</code>?</summary>

`--soft` moves HEAD back one commit but **keeps changes staged**. `--hard` moves HEAD back and **discards** both the commit and your working-tree changes — destructive.
</details>

<details>
<summary><b>6.</b> What is <code>git revert</code> and how does it differ from <code>git reset</code>?</summary>

`revert` creates a **new commit** that undoes an earlier one — history is preserved, safe for shared branches. `reset` rewrites history by moving the branch pointer — dangerous if already pushed.
</details>

<details>
<summary><b>7.</b> What's the difference between <code>git merge</code> and <code>git rebase</code>? When is each appropriate?</summary>

`merge` joins branches with a merge commit — preserves history, safe on shared branches. `rebase` replays your commits on top of another branch — linear history, good for local cleanup before pushing.
</details>

<details>
<summary><b>8.</b> What is a <b>detached HEAD</b> and why is it dangerous?</summary>

HEAD points at a commit instead of a branch (e.g. after `checkout <sha>`). New commits aren't attached to any branch, so they become unreachable and can be lost by garbage collection.
</details>

<details>
<summary><b>9.</b> What does <code>.gitignore</code> do? Does it affect already-tracked files?</summary>

Tells Git which untracked paths to ignore. It does **not** affect files already tracked — you must `git rm --cached` them first for the rule to apply.
</details>

<details>
<summary><b>10.</b> What's the difference between <code>git remote add</code> and <code>git clone</code>?</summary>

`clone` copies a remote repo locally and sets `origin` automatically. `remote add` just registers a remote in an **existing** local repo — no copy, no fetch.
</details>

<details>
<summary><b>11.</b> What is a pull request (PR) / merge request (MR) in plain terms?</summary>

A request on a hosting platform (GitHub, GitLab) to merge one branch into another, with review, comments, and CI checks before the merge happens.
</details>

<details>
<summary><b>12.</b> How do you see what's about to be committed before you commit?</summary>

`git diff --staged` (or `--cached`) shows the staged changes. `git diff` alone shows unstaged changes — useful but not what will be committed.
</details>

<details>
<summary><b>13.</b> What's the purpose of <code>git stash</code>?</summary>

Temporarily shelves uncommitted changes so you can switch branches or pull cleanly. Restore later with `git stash pop` (removes) or `git stash apply` (keeps).
</details>

<details>
<summary><b>14.</b> You accidentally committed a secret. What are the immediate steps? (Conceptual.)</summary>

**Rotate the secret first** — assume it's compromised. Then rewrite history (`git filter-repo` or BFG) and force-push. Finally, add the file to `.gitignore` and consider it a lesson.
</details>

<details>
<summary><b>15.</b> What does <code>origin</code> typically refer to?</summary>

The default name for the remote you cloned from. It's just a label — you can rename it or have several remotes (`upstream`, `fork`, etc.).
</details>

<br>

---

### 🛠️ Hands-on Task

*Walk the full cycle: init → commit → branch → merge → tag → remote → push.*

```bash
# 1. Fresh repo, first commit
mkdir git-practice && cd git-practice
git init
echo "hello" > file.txt
git add file.txt
git commit -m "Initial commit"

# 2. Branch, second commit, merge back
git checkout -b feature
echo "feature" >> file.txt
git commit -am "Add feature line"
git checkout main
git merge feature

# 3. Tag the merge commit
git tag v1.0

# 4. Add a remote (local bare repo in this example)
git init --bare ../git-practice-remote.git
git remote add origin ../git-practice-remote.git

# 5. Push main and the tag
git push -u origin main
git push origin v1.0

# 6. Inspect
git log --oneline --graph --all
```

---

<div align="center">

*Come back, click a few, see what stuck.*

</div>
