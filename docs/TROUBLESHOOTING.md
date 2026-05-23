# Troubleshooting

Este guia ajuda a instalar e testar as dependencias do WhisperTranscriber no Windows.

## 1. Instalar FFmpeg

Baixe o FFmpeg em:

https://ffmpeg.org/download.html

Depois de instalar, abra um novo `cmd` e teste:

```bat
ffmpeg -version
where ffmpeg
```

Se `ffmpeg -version` funcionar, o WhisperTranscriber deve conseguir usar o FFmpeg globalmente.

## 2. Instalar whisper.cpp / whisper-cli

Baixe os binarios do `whisper.cpp` em:

https://github.com/ggml-org/whisper.cpp/releases

No Windows, procure um asset de binario, extraia o ZIP e encontre a pasta que contem diretamente:

```text
whisper-cli.exe
```

Teste no `cmd` usando caminho completo:

```bat
"C:\CAMINHO\PARA\WhisperCPP\whisper-cli.exe" --help
```

Se isso funcionar, voce pode usar o botao **Runtime > Escolher** no WhisperTranscriber e selecionar essa pasta.

## 3. Colocar whisper-cli no PATH

Opcionalmente, adicione ao PATH a pasta que contem diretamente `whisper-cli.exe`.

Exemplo:

```text
C:\Users\SeuUsuario\Documents\WhisperCPP
```

Depois feche e reabra o terminal e teste:

```bat
where whisper-cli.exe
whisper-cli.exe --help
```

Se `where whisper-cli.exe` nao encontrar nada, a pasta ainda nao esta no PATH do terminal atual.

## 4. Erro VCRUNTIME140.dll ou MSVCP140.dll

Se o Windows disser que `VCRUNTIME140.dll` ou `MSVCP140.dll` nao foi encontrado, instale o Microsoft Visual C++ Redistributable x64:

https://aka.ms/vs/17/release/vc_redist.x64.exe

Depois feche e reabra o terminal.

## 5. Erro -1073741795 / 0xc000001d

Se o `whisper-cli.exe` termina com:

```text
-1073741795
0xc000001d
```

isso significa `Illegal Instruction`: o build baixado do `whisper-cli` nao e compativel com a CPU ou com a VM atual.

Isso pode acontecer em VMs, especialmente quando o VirtualBox/VMware/Hyper-V nao expoe AVX/AVX2 para o Windows convidado.

Solucoes possiveis:

- testar em maquina fisica;
- usar outro build do `whisper.cpp` mais generico;
- habilitar recursos de CPU/virtualizacao no hypervisor;
- compilar `whisper.cpp` para a CPU/VM alvo.

## 6. Teste manual completo

Converta um video/audio para WAV temporario:

```bat
ffmpeg -y -i "C:\CAMINHO\video.mp4" -ar 16000 -ac 1 -c:a pcm_s16le "%TEMP%\whisper_test.wav"
```

Rode o whisper:

```bat
whisper-cli.exe -m "C:\CAMINHO\MODELOS\ggml-small.bin" -f "%TEMP%\whisper_test.wav" -otxt -osrt -l en -of "%TEMP%\whisper_test_output"
echo %ERRORLEVEL%
dir "%TEMP%\whisper_test_output*"
```

Se gerar `.txt` ou `.srt`, o runtime esta funcionando.

## 7. Logs do WhisperTranscriber

O app grava logs em:

```text
%LOCALAPPDATA%\WhisperTranscriber\logs\WhisperTranscriber.log
```
