---
tags:
  - git
  - version-control
---
**Ref**: A named pointer to a specific commit (stored as plaintext representation of the commit's digest).
**Branch**: A ref pointing to the "tip" of a specific path in commit graph.

It really is that simple; by naming a specific commit (saving a ref to it), we can then start adding commits to that new branch in the commit graph.
```
.git/refs/
├── heads
│   ├── add_classics
│   └── main
└── tags
```

```bash
file .git/refs/heads/main
# .git/refs/heads/main: ASCII text

cat .git/refs/heads/main
# e3a37010eda5aeb5f8dd068a982f3948e8c06b4c
```

When we have a specific branch checked out, making a commit pushes that branch up to the new commit. This latest commit on the branch is called the **tip** or **head** of the that branch.

## Branching commands

List, create, or delete a branch using [`branch`](https://git-scm.com/docs/git-braanch):
```bash
git branch                              # list
git branch <branch-name>                # create
git branch -d <branch-name>             # delete
git branch -m <old-branch> <new-branch> # rename
```

Switch to a branch using [`switch`](https://git-scm.com/docs/git-switch) or [`checkout`](https://git-scm.com/docs/git-checkout):
```bash
git switch -c <branch-name>
# or the older
git checkout -b <branch-name>

# The -c and -b flags both mean "create the branch if it doesn't exist."
```