# WhisperTranscriber

WhisperTranscriber transcreve audios e videos localmente usando Whisper. Ele pode gerar `.txt` e `.srt`, baixar modelos pelo proprio aplicativo e usar uma pasta externa de modelos ja existentes.

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

Dependencias de runtime, como `ffmpeg` e binarios do `whisper.cpp`, podem ser instaladas pelo pacote, pelo instalador, ou baixadas sob confirmacao do usuario quando necessario. Consulte as notas da release para saber o que esta incluido em cada versao.

## Atualizacoes

O arquivo `manifests/stable.json` e o manifesto publicado em Releases ficam reservados para o autoupdater. A aplicacao deve comparar a versao instalada com o manifesto do canal estavel e oferecer a atualizacao quando existir uma versao nova.

## Licenca

Uso gratuito. Codigo fonte fechado.
