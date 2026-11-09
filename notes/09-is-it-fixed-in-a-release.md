# Is a bug already fixed in a given release?

Reporters often run an older version. To check whether a fix or feature is in a tag:

```bash
# find the commit that introduced the change
git log main -S "SOME_CONSTANT" --format="%h %ad %s" --date=short -- path/to/file

# does the release tag contain it at all?
gh api "repos/OWNER/REPO/contents/path/to/file?ref=v1.2.3" --jq .content \
  | base64 -d | grep SOME_CONSTANT
```

`gh api repos/OWNER/REPO/compare/<tag>...<sha>` is less useful when releases are cut
from separate branches, because the status comes back as `diverged`. Reading the
file at the tag gives a direct yes or no.
