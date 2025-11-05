---
tags:
  - linux
  - scripting
---
Using the default clipboard (will not be accessible elsewhere using `<C-v>`):
```bash
command | xclip
xclip -o | command
```

If we want `<C-v>`, etc., use:
```bash
command | xclip -sel clip
```