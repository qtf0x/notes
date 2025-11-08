---
tags:
  - git
  - version-control
---
Everything tracked in a Git repository (essentially, the contents of `.git/objects/`) is a binary file. Each file is some type of [**object**](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects), for example:
- Tree (collection/directory of other objects)
- Blob (regular file)
- Commit (snapshot of repo after some changes)

If we look at the structure of a `.git/objects/` directory, we can see that each object is identified by its hash digest. As of Git 2.x, this uses SHA-1, which is good enough that we can almost always just use the **first seven bytes** of the digest to uniquely identify an object.
```
.git/objects/
├── 0c
│   └── 527a5bdcbd78d410cf9170901e7ddee0155c53
├── 14
│   └── bf50928ccbb6d75039d2a24d8ce85a49eb4cc1
├── 15
│   └── e7127acb8e1268f3b3de775ef056e657575352
├── 18
│   └── d53b21a68cf7f8d8b4fb2c293ed409fb967cd3
├── 1e
│   └── 5372bb7147aab453239bc790aacd9fd1b9f785
├── 37
│   └── 712fab0aa902b37e2197ebb71e4e1ba4f45f3d
├── 49
│   └── 49bfbfb95de385eb4cefece7717bf58022b193
├── 5b
│   └── 21d4f16a4b07a6cde5a3242187f6a5a68b060f
├── 66
│   └── 693b8d72daef9170108c6ab4b3abd7f3950dd2
├── 75
│   └── d403873e8ca4516678b18fe90434cbe644b1b9
├── 95
│   └── 6b9b03cd99bddef5bdd3cd92693aa761e001bb
├── e3
│   └── a37010eda5aeb5f8dd068a982f3948e8c06b4c
├── ef
│   └── 7e93fc61a91deecaa551c4707e4c3049af42c9
├── f7
│   └── f75a4a6c871d79fdde2a8b38de7dc9e8eccd52
├── info
└── pack
```

## What's in an object

The object files here are binary, but we can read them using the Git plumbing command [`cat-file`](https://git-scm.com/docs/git-cat-file):
```bash
#             v 'pretty print'
git cat-file -p 0c527a5

# tree 37712fab0aa902b37e2197ebb71e4e1ba4f45f3d
# parent 956b9b03cd99bddef5bdd3cd92693aa761e001bb
# author qtf0x <qtf0x@pm.me> 1762535241 -0700
# committer qtf0x <qtf0x@pm.me> 1762535241 -0700
# gpgsig -----BEGIN PGP SIGNATURE-----
#
# iHUEABYKAB0WIQSr+4Rpgq+NJCBqYT/PzCv8g8HYawUCaQ4nSQAKCRDPzCv8g8HY
# azX4AQCL+mr2Y0pa1cxqBRkmcJ0hTpUwYBg78onPAojXIwVo5AD/WIbYFUoUZmWR
# x1oCc//1By1GO3L4mcypnRGJ0dYBKAY=
# =H2BI
# -----END PGP SIGNATURE-----

# B: add titles
```

Clearly, this is a commit object. See that `tree` digest there? That's the collection of objects contained in this commit:
```bash
git cat-file -p 37712fa

# 100644 blob ef7e93fc61a91deecaa551c4707e4c3049af42c9	contents.md
# 100644 blob 66693b8d72daef9170108c6ab4b3abd7f3950dd2	titles.md
```

And each of those `blob` digests refers to a full snapshot of the corresponding file at the time of this commit:
```bash
git cat-file -p ef7e93f

# # contents
```

## Wait, we're not just storing diffs?

Nope! Commits refer to full snapshots of all files. Of course, we say "refer to" because each commit doesn't exactly "contain" a full snapshot of every file. Instead, blobs and trees are compressed, [packed](https://git-scm.com/book/en/v2/Git-Internals-Packfiles) and deduplicated such that **if a file doesn't change between commits, it will only be stored once**.

## References
https://git-scm.com/book/en/v2/Git-Internals-Git-Objects
https://git-scm.com/docs/git-cat-file
https://git-scm.com/book/en/v2/Git-Internals-Packfiles