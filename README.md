# retarget-symlink

A perl script for bulk retargeting symlinks, similar to classic `rename` script.

## usage

```
retarget-symlink [-v] [-n] perlexpr [FILES...]

-v, --verbose   print name of each file about to be rewritten
-n, --dry-run   don't actually execute
```

`perlexpr` is a arbitrary Perl expression that takes original link target path in `$_`, and returns new link tatget path in `$_`.

if `FILES` are not given, file names are read from stdin.

Each file is rewritten only when:
1. it is actually a symlink.
2. evaluating `perlexpr` on the original link target path yields a different path name from the original.

## example

Suppose you have the following symlinks and you want to retarget them to `/opt/python3.12/*` :

```
/usr/local/bin/python3 -> /opt/python3.11/bin/python3
/usr/local/bin/pip3 -> /opt/python3.11/bin/pip3
/usr/local/bin/pydoc3 -> /opt/python3.11/bin/pydoc3
```

You can do it like this:
```
$ sudo retarget-symlink 's/python3.11/python3.12/' /usr/local/bin/*
```

When in doubt, always use --dry-run first.
