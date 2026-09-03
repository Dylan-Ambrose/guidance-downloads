# Guidance, Downloads

This repo hosts downloadable builds of Guidance, the launcher hub that ties
together the other desktop apps.

**No source code lives here**, this repo exists solely to distribute
release binaries. Guidance's source is developed privately.

## Get Guidance

See the [Releases](../../releases) page for the latest `Guidance-Setup.exe`.
It installs per-user, no admin rights needed, no UAC prompt.

## How the app catalogue works

Guidance no longer reads a hand-maintained list. On startup it lists every
public repo under this account and checks each one whose name ends in
`-downloads` (skipping this repo itself) for a `manifest.json` at its root.
Publishing that file is the only step needed for an app to show up in
Guidance with a Download card, nothing here or in Guidance itself needs to
change.

```json
{
  "id": "example",
  "name": "Example",
  "version": "1.0.0",
  "tag": "Utility",
  "description": "One-line description shown on the download card.",
  "download_url": "https://github.com/<owner>/<repo>/releases/download/<tag>/<Installer>.exe",
  "install_check_path": "%LOCALAPPDATA%\\Programs\\<AppName>\\<AppName>.exe",
  "icon_url": "https://raw.githubusercontent.com/<owner>/<repo>/main/icon.png",
  "previous_names": []
}
```

`install_check_path` should match wherever that app's own Inno Setup
installer actually installs it, Guidance checks it directly rather than
querying the Windows registry. A manifest with no `download_url` is read
but never offered as a Download card (this is how Blindspot's retired
web-only listing stays out of the catalogue without deleting its repo).
