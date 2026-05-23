# Distribution Strategy

## Public repo role

This repository is the public distribution channel. It should contain documentation, manifests and release metadata, not the private source code and not local runtime folders.

End users should download one file from GitHub Releases. The repository tree itself is not the product install folder.

## Recommended release asset

Near term:

- Publish a single ZIP: `WhisperTranscriber-x.y.z-win-x64.zip`.
- The ZIP may include the app executable and any runtime files that are legally and operationally safe to redistribute.

Target state:

- Publish a single setup/bootstrapper executable: `WhisperTranscriber-Setup-x.y.z.exe`.
- The bootstrapper creates the install structure, checks dependencies, asks consent before downloading optional third-party runtime, then launches the app.

## Suggested installed layout

```text
%LOCALAPPDATA%\WhisperTranscriber\
  app\
    WhisperTranscriber.exe
    icon.ico
    logo.png
  runtime\
    whisper-cli.exe
    ffmpeg.exe
    *.dll
  models\
  logs\
```

User settings should live in:

```text
%APPDATA%\WhisperTranscriber\config.json
```

Downloads and caches can live in:

```text
%LOCALAPPDATA%\WhisperTranscriber\downloads\
```

## Version and update flow

1. The app has a compiled version, for example `0.1.0`.
2. On startup, the app checks the stable manifest.
3. If `manifest.version` is newer, it shows release notes and offers update.
4. The updater downloads the release asset, verifies SHA-256, then runs installer or replaces the portable app after closing.
5. The app logs update attempts and results.

## Logging

Suggested log file:

```text
%LOCALAPPDATA%\WhisperTranscriber\logs\WhisperTranscriber.log
```

Log useful lifecycle events only: startup, selected models folder, dependency checks, downloads, transcriptions, update checks and errors.
