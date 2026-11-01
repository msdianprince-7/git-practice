# Git running out of memory on Windows

On a large repo, `git worktree add` and `git merge` sometimes die with
`Out of memory, malloc failed` while reading pack files.

The dangerous part is that the checkout can be left half written. In my case one
large data file was silently skipped, so it showed up as an unstaged deletion, and
the next commit would have deleted it from the branch.

## Fix

Lower the memory git uses for pack access:

```bash
git -c core.packedGitLimit=256m \
    -c core.packedGitWindowSize=32m \
    -c core.deltaBaseCacheLimit=64m \
    -c pack.windowMemory=64m \
    merge upstream/main
```

## Check before committing

```bash
git ls-files -d   # tracked files missing on disk, should print nothing
```

If anything shows up, restore it with `git checkout -- <path>` before committing.
