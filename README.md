# Guidance — Downloads

This repo hosts downloadable builds of Guidance, the launcher hub that ties
Listic and future apps together, plus `catalog.json` — the list of apps
Guidance itself knows how to offer a download for.

**No source code lives here** — this repo exists solely to distribute
release binaries and the catalog. Both Guidance's and Listic's source are
developed privately.

## Get Guidance

See the [Releases](../../releases) page for the latest `Guidance-Setup.exe`.
It installs per-user — no admin rights needed, no UAC prompt.

## catalog.json

Guidance fetches this file at startup to show apps you haven't installed
yet, each with a Download button. Adding an app here is all it takes for
it to show up in Guidance — no update to Guidance itself required.

```json
{
  "apps": [
    {
      "id": "listic",
      "name": "Listic",
      "description": "One-line description shown on the download card.",
      "download_url": "https://github.com/<owner>/<repo>/releases/download/<tag>/<Installer>.exe",
      "install_check_path": "%LOCALAPPDATA%\\Programs\\<AppName>\\<AppName>.exe"
    }
  ]
}
```

`install_check_path` should match wherever that app's own Inno Setup
installer actually installs it — Guidance checks it directly rather than
querying the Windows registry.
