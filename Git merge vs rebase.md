---
tags:
  - git
  - version-control
---
## Merge

A **merge** will create a new commit on the current branch which has *two parents*: one from the current branch and one from the branch being merged.

In order to detect conflicts, Git must walk the commit tree, starting from the **merge base/best common ancestor** of the two branches. This will be a commit with *two children*, likely the location where one branch splits off from the other, or at the most recent merge. From here, Git walks the commits from the two branches, looking for conflicts.

If a conflict can be resolved automatically, it will be. Otherwise, the user will be presented with a text editor to manually resolve conflicts.

Finally, a **merge commit** is created on the current branch, whose parents are the tip of the branch being merged and the last commit to the current branch.

In this example, commit `F` is a merge commit with parents `C` and `E`:

```bash
# A - B - C    main
#   \
#    D - E     feature_branch

git switch main
git merge feature_branch

# A - B - C - F    main
#   \       /
#    D  -  E       feature_branch
```

### Fast-forward merge

When a merge commit is created, as above, this is called a **true merge**. However, if the current branch doesn't have any changes which the branch being merged doesn't have, a simpler **fast-forward merge** will be performed.

This will simply move the current branch to the tip of the branch being merged:

```bash
#       C     other_branch
#      /
# A - B       main

git switch main
git merge other_branch

#             other_branch
# A - B - C   main
```

## Rebase

Say we're on a feature branch, and want to integrate changes from the main branch. We could merge main into our branch. Or, if we didn't want to create a merge commit, we could use **rebase** to move the base of our feature branch (where it diverges from main) to the tip of main.

```bash
# A - B - C    main
#   \
#     D - E    feature_branch

git switch feature_branch
git rebase main

# A - B - C         main
#          \
#           D - E   feature_branch
```

This will attempt to apply each of the commits from `feature_branch` on top of commit `C`, checking for conflicts. It will not affect `main` in any way whatsoever.

Now, we could integrate the changes from `feature_branch` into `main` using a fast-forward merge, without creating any merge commits. Our commit history will be totally *linear*!

**Warning**: Never rebase a public branch (one checked out/used by others)! It will change the branch's history, causing lots of issues for everyone.

## Pros and cons

Using true merges preserves the true history of changes in the repository, at the cost of creating extra commits.

Using rebase creates a linear commit history, which might be easier to read.