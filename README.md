# WhisperTranscriber

WhisperTranscriber transcreve audios e videos localmente usando Whisper. Ele pode gerar `.txt` e `.srt`, baixar modelos pelo proprio aplicativo, usar uma pasta externa de modelos ja existentes e transcrever URLs publicas compativeis com yt-dlp.

## Download

Baixe sempre a versao mais recente em:

https://github.com/rclopezbt/WhisperTranscriber/releases/latest

A distribuicao publica deve ser feita por um unico arquivo anexado ao GitHub Releases, por exemplo:

- `WhisperTranscriber-Setup-x.y.z.exe`, quando houver instalador/bootstrapper.
- `WhisperTranscriber-x.y.z-win-x64.zip`, enquanto a distribuicao for portavel.

O codigo fonte nao e publicado neste repositorio.

## Modelos

Modelos Whisper nao sao incluidos no repositorio nem no instalador. Eles sao grandes e podem ser baixados pelo gerenciador de modelos do aplicativo, ou voce pode apontar o app para uma pasta onde ja existam modelos compativeis.

A preferencia da pasta de modelos fica salva em `%APPDATA%\WhisperTranscriber\config.json`.

## Dependencias

Dependencias de runtime, como `ffmpeg`, `yt-dlp`, `deno` e binarios do `whisper.cpp`, podem ser instaladas manualmente, detectadas no PATH ou configuradas pela tela Runtime. O app pode oferecer download guiado para algumas dependencias, sempre com aviso de origem/licenca antes do download. Consulte as notas da release para saber o que esta incluido em cada versao.

Guia de instalacao e erros comuns:

[docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)

## Atualizacoes

O arquivo `manifests/stable.json` e o manifesto publicado em Releases ficam reservados para o autoupdater. A aplicacao deve comparar a versao instalada com o manifesto do canal estavel e oferecer a atualizacao quando existir uma versao nova.

## Licenca

Uso gratuito. Codigo fonte fechado.
