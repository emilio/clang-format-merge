# Merge driver for clang format.

A very simple merge driver that allows you to automatically rebase and merge
commits using clang-format.

## Setup

In `.git/config`:

```
[merge "clang-format"]
  name = clang-format merge driver
  driver = /path/to/clang-format-merge %O %A %B %P
	recursive = binary
```

In `.gitattributes`:

```
*.cpp merge=clang-format
*.h   merge=clang-format
*.mm  merge=clang-format
```

And you should be ready, happy gitting.
