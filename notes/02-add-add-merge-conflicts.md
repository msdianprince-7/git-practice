# Add/add merge conflicts

Most conflicts I hit when updating a long-lived PR branch were not real
disagreements. Both sides had added something new at the same spot:

- my branch added a test class at the end of a file, main added a different one
- both sides added a name to the same `from x import (...)` block

## How to resolve

Keep both sides. Never drop one just to make the markers go away.

Then check the details a linter will catch:

- two blank lines between top-level classes and functions
- imports inside one block stay sorted, otherwise ruff `I001` fails
- if main deleted a line next to your change, check whether anything still uses it
  before keeping it

## Quick check that nothing is left

```bash
grep -n '^<<<<<<<\|^=======$\|^>>>>>>>' path/to/file
git diff --name-only --diff-filter=U
```
