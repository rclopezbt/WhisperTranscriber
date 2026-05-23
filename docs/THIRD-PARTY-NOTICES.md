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

The whisper.cpp runtime and its dependencies should be tracked separately from the closed application code. Release packages should include license notices for any bundled whisper.cpp binaries and GPU/CUDA-related runtime files.

## Models

Whisper model files are not bundled. The app lets users download models or select an existing models folder.
