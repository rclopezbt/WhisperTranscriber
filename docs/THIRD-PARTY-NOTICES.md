# Third-party Runtime Notes

WhisperTranscriber depends on external runtime components for some workflows.

## ffmpeg

Do not assume every ffmpeg binary can be redistributed under the same terms. FFmpeg itself is generally available under LGPL or GPL depending on how it is configured and which external libraries are enabled. Some prebuilt binaries may include GPL components or other libraries with additional terms.

Recommended approach for the first public distribution:

- Do not commit ffmpeg binaries to this repository.
- Prefer asking the user before downloading ffmpeg runtime.
- Show source, license notice and destination before download.
- Keep third-party notices with each release package.

## whisper.cpp

Project: https://github.com/ggml-org/whisper.cpp

License: MIT License

The whisper.cpp runtime and its dependencies should be tracked separately from the closed application code. The app may offer guided download of official whisper.cpp release binaries, such as the Windows x64 package containing `whisper-cli.exe`. Release packages should include license notices for any bundled or downloaded whisper.cpp binaries and GPU/CUDA-related runtime files.

## yt-dlp

Project: https://github.com/yt-dlp/yt-dlp

License: Unlicense for the core project, with some bundled/auxiliary components under their own permissive licenses depending on the official package.

The app may offer guided download of official `yt-dlp.exe` releases for public URL transcription. Site compatibility depends on yt-dlp and can change when platforms change their websites, APIs, authentication, or access policies.

## Deno

Project: https://github.com/denoland/deno

License: MIT License

The app may offer guided download of official Deno Windows x64 releases. Deno is used as an optional JavaScript runtime for yt-dlp, especially for YouTube compatibility. It does not grant access to private content and does not bypass login, cookies, OAuth, tokens, DRM, or platform restrictions.

## Models

Whisper model files are not bundled. The app lets users download models or select an existing models folder.

## Web URLs

WhisperTranscriber does not attempt to bypass DRM, OAuth, tokens, or access restrictions. URL transcription is intended for public videos/audio or direct media links that the user is allowed to access. When the user explicitly enables browser session usage, yt-dlp may read cookies from the selected browser or a user-selected `cookies.txt` file for that run; WhisperTranscriber does not store those cookies.
