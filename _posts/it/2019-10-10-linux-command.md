---
title: Linux Command
categories: [it]
tags: [Linux, Search]
---

## Find
`find start-point expression`

`expression` default is `-print`.

- Find files `*.jpg` or `*.JPG` in the directory `dir`:
```bash
find dir/ -type f -iname '*.jpg'
```

### Tests

- `-iname pattern` for case-insensitive, `-name pattern` for case-sensitive.
- `-inum n` for inode number **n**.
- `-empty` for empty files or directories.
- `-type c` for file type.
- `-mtime/-ctime/-atime [+/-]n` for time about the file.
- `-size n[cwbkMG]` for the size of files.


### Actions
Actions have side effects (such as printing something on standard output) and
return either true of flase. After finding files you wanted, **Actions** tell us how to deal with the result. (such as `-print`)

### Global options
Global options affect the operation of tests and actions specified on any part
of the command line. Global options always return true.

- `-maxdepth levels` descend at most levels of directories below the starting-
points.
