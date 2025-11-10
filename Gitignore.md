---
tags:
  - git
  - version-control
---
Just like you might expect, `.gitignore` files **may be nested**, with more specific scopes overriding more general ones.

The most important syntax is as follows:
```gitignore
# This is a comment

# Matches any path containing a section (directory or file name) named ignore_me at or below this .gitignore file
ignore_me

# Wildcard matches any characters except a directory separator /
*ignore_me

# Starting with a / anchors the pattern to the directory containing the .gitignore file
/ignore_me

# Unignore a file
!dont_ignore_me
```