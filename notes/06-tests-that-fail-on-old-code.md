# Check that a regression test actually catches the bug

A test that passes on both the old and the new code proves nothing. Before pushing a
fix I now run the new test against the old source file:

```bash
cp src/module.py /tmp/fixed.py
git show main:src/module.py > src/module.py
pytest tests/test_module.py -k NewTest     # expect failures here
cp /tmp/fixed.py src/module.py
pytest tests/test_module.py -k NewTest     # expect all green
```

## What to look for

- the case for the reported bug fails on the old code
- control cases (behaviour that should not change) pass on both
- after a follow-up commit, the new case fails on the previous commit too

## Watch out for mocks

Two older tests mocked the function my fix stopped calling. They kept passing no
matter what the code did. Replace that kind of mock with real input data.
