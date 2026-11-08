# Fork PR checks that never ran

After pushing a merge commit to a PR from my fork, the PR showed "2 checks passed"
where it used to show more than 80.

The missing runs were not failing. They had the status `action_required`, which
means GitHub was waiting for a maintainer to approve workflow runs from a fork.

```bash
gh api "repos/OWNER/REPO/actions/runs?head_sha=$SHA" \
  --jq '.workflow_runs[] | "\(.name) \(.status) \(.conclusion)"'
```

## Takeaways

- a small number of green checks is not the same as green CI
- pushing again does not start the runs, only a maintainer approval does
- until then the code is untested, so say that instead of calling it passing
