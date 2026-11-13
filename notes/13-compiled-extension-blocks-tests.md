# When a compiled extension blocks local tests

A Python project I contribute to started importing a Rust extension module at the
top of the package. From that commit on, a plain source checkout failed straight
away:

```
ImportError: cannot import name '_native' from 'package.rust_bridge'
```

No test could run, not even ones unrelated to the Rust code.

## What it means for a contributor

- the package now has to be built, here with `maturin`, before tests can import it
- on Windows that needs a Rust toolchain plus a C linker (MSVC Build Tools or MinGW)
- an older checkout from before the change still imports, which is easy to mistake
  for "my code is fine"

## Practical options

- build the extension once and keep it in a separate worktree
- for changes that do not touch Python (UI, docs, Terraform), test those parts on
  their own
- be honest in the PR when something could only be checked by CI
