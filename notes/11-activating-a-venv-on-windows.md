# Activating a Python virtual environment on Windows

A venv ships one activation script per shell, and using the wrong one does nothing
useful:

| Shell | Command |
|---|---|
| cmd.exe | `.venv\Scripts\activate.bat` |
| PowerShell | `.venv\Scripts\Activate.ps1` |
| Git Bash | `source .venv/Scripts/activate` |

If PowerShell refuses to run the script, allow it for the current window only:

```powershell
Set-ExecutionPolicy -Scope Process Bypass
```

## Check it worked

```bat
where python
python --version
python -c "import sys; print(sys.prefix)"
```

`where python` should list `.venv\Scripts\python.exe` first, and `sys.prefix`
should point at the `.venv` folder.

## In scripts, skip activation

Activation only changes the current shell. In scripts and CI it is simpler to call
`.venv\Scripts\python.exe -m pytest ...` directly, which always uses the right
interpreter.
