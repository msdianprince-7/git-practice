# Freeing disk space on Windows without breaking things

Measure first. On my machine the usual caches (pip, npm, browser) were small, and
most of C: was Windows itself, installed programs and the page file.

## Safe to delete

- editor extension versions the editor itself marked obsolete
- cached extension installers the editor re-downloads when needed
- browser cache, cleared from the browser's own settings

## Leave alone

- the shared temp folder while apps are running, other programs may hold files there
- Python installs that virtual environments point to
- anything under Desktop or Downloads without checking it first

## Bigger wins that need admin

- move the page file to another drive (needs a restart)
- Settings > Storage > Temporary files > Windows Update Cleanup
