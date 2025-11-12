---
tags:
  - git
  - version-control
---
Really, they're not so bad. If a merge conflict occurs, Git will helpfully inject the contents of both "our" changes (those from `HEAD`) and "their" changes (those from the branch being merged) into the same file in the working tree.

```bash
git merge main

# <<<<<<< HEAD
#         count = 1
#         count += 1
# =======
#         count = 2
#         count++
# >>>>>>> main
```

We may then manually modify the file(s), `add` them back to the index, and finish the merge with `git merge --continue`.

## Use `checkout` to avoid manual merging

During a merge conflict, we often just want to keep changes from one branch and discard those from the other (more common with code than with content). Git makes this easy with the [`checkout`](https://git-scm.com/docs/git-checkout) command.

```bash
# Keep only changes from HEAD
git checkout --ours <pathspec>

# Keep only changes from branch being merged
git checkout --theirs <pathspec>
```