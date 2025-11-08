---
tags:
  - linux
  - scripting
---
```bash
# Redirect stdout with > and stderr with 2>
echo "Hello, world!" > hello.txt
cd /dev/null 2> error.log

# Append instead of overwrite with >>
echo "Goodbye, world..." >> hello.txt

# Make one stream a copy of another with &
ls > dirlist 2>&1
# (this will send the same output to stdout and stderr)
ls &> dirlist
# (equivalent)
```

If you want to redirect output to a file **and** to, e.g., `stdout` (also a file but, hey, who's counting), `tee` is probably the best option:
```bash
echo ":3" | tee -a fiuwu
```

## References
https://www.gnu.org/software/bash/manual/html_node/Redirections.html
https://askubuntu.com/a/1416100