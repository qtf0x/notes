---
tags:
  - git
  - version-control
---
A git feature that caches manual hunk conflict resolutions so that identical conflicts may be resolved automatically in the future. This is most useful for **rebasing a long-running branch or multiple branches** that might contain some of the same changes.

Turn the feature on with:

```bash
git config set rerere.enabled true
```

Changes are stored in plaintext in `.git/rr-cache/`, so you may delete this directory in order to clear the resolution cache.