# Merge driver for clang format.

A very simple merge driver that allows you to automatically rebase and merge
commits using clang-format.

## Git Wrapper

`git-wrapper` contains a wrapper script which will install this merge driver,
and then uninstall it immediately after the command has completed. This
wrapper can be used for running rebases.

```shell
$ /path/to/git-wrapper rebase central/branches/default/tip
```

Do note that if a merge conflict occurs, `git-wrapper rebase --continue`
should be used rather than using `git` directly.

## Manual Setup

In `.git/config`:

```
[merge "clang-format"]
  name = clang-format merge driver
  driver = /path/to/clang-format-merge %O %A %B %P
  recursive = binary
```

In `.git/info/attributes`:

```
*.cpp merge=clang-format
*.h   merge=clang-format
*.mm  merge=clang-format
```

And you should be ready, happy gitting.
