# Line-ending noise that blocks a rebase

On Windows, a few files in one repo always showed as modified even though
`git diff` showed no real change. Git then refused to rebase or merge because the
working tree was "dirty".

The cause was line endings. Git warns about it like this:

```
warning: in the working copy of 'path/to/file', LF will be replaced by CRLF
```

## Fix for the moment

If the diff is empty apart from line endings, throw the noise away:

```bash
git diff --stat              # confirm there is no real change
git checkout -- path/to/file
```

## Fix for good

Add a `.gitattributes` rule, or set `core.autocrlf` to match the project's
convention, so the same file is not rewritten on every checkout.
