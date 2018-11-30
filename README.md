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

In `.git/info/attributes`:

```
*.cpp merge=clang-format
*.h   merge=clang-format
*.mm  merge=clang-format
```

And you should be ready, happy gitting.

## Disclaimer

This is tested, but needs the patch in
https://bugzilla.mozilla.org/show_bug.cgi?id=1511258 to work in Gecko.

Tested with:

```shell
$ clang-format -i -style=WebKit layout/base/RestyleManager.cpp
$ git commit -am "Reformat RestyleManager.cpp to WebKit style"
$ git revert HEAD # Undo that, just want the patch to cherry-pick
$ ./mach clang-format -i layout/base/RestyleManager.cpp
$ git commit -am "The big reformat"
$ # This is the hard thing where the driver comes at play.
$ git cherry-pick HEAD~~~ # cherry-pick the WebKit reformat commit.
$ Merging layout/base/RestyleManager.cpp in repo /home/emilio/src/moz/gecko-2
Formatting .merge_file_lwMX2O as layout/base/RestyleManager.cpp
Formatting .merge_file_zuW2Wv as layout/base/RestyleManager.cpp
Formatting .merge_file_sV0dRc as layout/base/RestyleManager.cpp
[detached HEAD bec1475bb141] Reformat RestyleManager.cpp to WebKit style.
$ git show HEAD # Success!
```

