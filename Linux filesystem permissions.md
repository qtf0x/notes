---
tags:
  - linux
  - filesystems
---
```
   |--------- owner
   |   |----- group
   |   |   |- others
d rwx rwx rwx
^
directory or file?
```

Obviously this is represented as a **bit field**, not actual characters. We use **octal** for this, as each part of the field is three bits, all of whose possible values may be represented by a single octit (0-7).

## Modify permissions

The [chmod](https://man7.org/linux/man-pages/man1/chmod.1.html) command modifies file permissions (or "file mode bits"). Using it is pretty simple:
```bash
chmod -R u=rwx,g+r,o-u DIR
#      ^ recursive for all files in DIR

chmod 0700 FILE
```

You can probably guess what the options do (`=` overwrites, `+` ORs on new bits, `-` masks off unwanted bits). The first of the four octits controls some additional things you can read about in the man page.

Leaving off the specific `ugoa` settings and just writing something like
```bash
cmod +x FILE
```
will be equivalent to using `a`; that is, permissions are changed for *all* users.

---

The [chown](https://man7.org/linux/man-pages/man1/chown.1.html) command changes the user (owner) or group of a file. For example:
```bash
sudo chown -R root DIR
# ^ almost certainly must be run as root!
```

### What does "executing" a directory mean, anyway?

We can't execute a directory, so instead the execute bit indicates whether we can **access** or **search** the directory. Even if we have permissions for the files inside the directory, we can't access them without execute permissions on the directory.

The most important effect this has is that we can't `cd` into a directory to make it our current working directory without execute perms.