# Finding an issue nobody is already fixing

In a busy open source repo most new bugs get a PR within a day. Checks I run before
picking one:

1. **Linked PRs**: the issue timeline's cross-reference events, fetched for many
   issues at once with one GraphQL query
2. **Claim comments**: phrases like "I'd like to take this", "working on a fix" or
   "I have a branch", in the body and in the comments
3. **Unlinked PRs**: `gh pr list --search "<key words>"`, because many PRs never
   mention the issue number
4. **Still broken on main**: read the current code, reporters often run an old
   release where the bug is already fixed

## Lesson

A detailed, confident issue body is not evidence that the bug still exists. One
report I checked described a feature that had simply not shipped in the reporter's
version yet.
