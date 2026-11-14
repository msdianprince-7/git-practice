# Keep the PR description in sync with the code

A PR description goes stale quickly. After a review I added a second rule to a fix,
and three parts of the description were suddenly wrong:

- the summary still described the old behaviour
- the "how it solves it" list missed the new rule
- the proof of fix named a commit that was no longer the tip

## What I do after every behaviour-changing commit

1. Re-run the proof of fix at the new tip and replace the old output
2. Update the commit hash it names
3. Update the summary and any caveats the change affects
4. Reply to the reviewer in one or two lines, naming the commit that addressed it

```bash
gh pr edit 1234 --body-file pr_body.md
gh pr comment 1234 --body "Added in abc1234, the model setting wins, then the provider"
```

A reviewer should never have to read the diff to find out the description is out
of date.
