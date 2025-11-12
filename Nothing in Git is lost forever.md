---
tags:
  - git
  - version-control
---
Even `git reset --hard` has its limits. We can use the [`reflog`](https://git-scm.com/docs/git-reflog) command to see a complete history of every time the tip of a reference is moved. Thus, even if a branch is deleted or a hard reset performed, we could recover any lost file, **as long as it was committed at some point**. A hard reset, for example, will clobber uncommitted files if they conflict with its operation.

## Reference syntax

There's some special syntax for referring to refs that is super unintuitive. Consider `HEAD`, the reference to the current branch tip (it's a double pointer!). We may navigate to other commits like so:

```bash
# The nth ancestor commit of HEAD, always choosing the first parent at merges
HEAD~n

# If n is omitted, we can also just chain tildes
HEAD~  === HEAD~1
HEAD~~ === HEAD~1~1 === HEAD~2

# ------------------------------------------------------------------------------

# Selects the nth parent commit of HEAD
HEAD^n

# Chaining carets doesn't replace using n, it selects parents while walking
HEAD^  === HEAD~
HEAD^^ === HEAD~2

# ------------------------------------------------------------------------------

# Selects the nth entry IN THE REFLOG
HEAD@{n}
```

## Merging with commitishs

Just as the `merge` command may be supplied a branch (a reference to a commit), it may be supplied other refs as well. For example, we can undo a hard reset without digging around in the reflog like so:

```bash
git reset --hard HEAD~1 # undo the last commit
git merge HEAD@{1}      # (fast-forward) merge back in the commit the HEAD was just at
```

If it can be eventually dereferenced to a commit (it's a "commitish"), we can merge with it!