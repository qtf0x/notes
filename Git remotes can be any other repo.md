---
tags:
  - git
  - version-control
---
A Git **remote** is literally just *any other repository* to which we can provide some URI. This doesn't have to be an HTTPS or SSH URL, like we might use to point at, e.g., a GitHub repo. It could also be a path to some other directory on the same machine!

Once a remote is added, we can treat it like the entirely separate repo that it is (with a separate commit graph), though usually its commits will match some or all of ours. That means we can **merge** between our branches and remote branches, or even **log** the commit history from a remote branch!

Use the [fetch](https://git-scm.com/docs/git-fetch) command to download all of the refs and objects from a remote. This does nothing to your working tree or index.

The [pull](https://git-scm.com/docs/git-pull) command will perform a fetch followed by a merge. A fast-forward merge will happen automatically, while the command will refuse to reconcile divergent branches unless the user explicitly specifies whether to use rebase or merge (either with the `--[no]-rebase` flag or the `pull.rebase` config option).

The [push](https://git-scm.com/docs/git-push) command is similar to pull, except that it expects to be able to upload objects from the current branch to the remote and do a fast-forward, only bringing the remote refs up to match the local ones.
- By default, refuses to overwrite a remote ref which isn't an ancestor of the local ref (without something like the `--force` flag).
- Without more options, will push to the remote branch matching the local one, but we can specify a more explicit push:

```bash
git push origin <localbranch>:<remotebranch>

# A trick: the following will DELETE A REMOTE BRANCH
git push origin :<remotebranch>
```