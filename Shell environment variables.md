---
tags:
  - linux
  - scripting
  - bash
---
```bash
# Local variables
FOO='Hello'

# Environment (global) variables
export BAR='world'

# Expand variables inline
echo "$FOO, ${BAR}!"

# Set variables only during single command execution
FOOBAR='uwu' BAZ=':3' ./scwipt.sh

# Delete variables by using unset or setting to empty string
unset FOO
BAR=''
```

Note: Even environment variables only exist for the **current session**.