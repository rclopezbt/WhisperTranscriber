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

## 4. Instalar yt-dlp para URLs publicas

Para transcrever videos da web, o app usa `yt-dlp` para baixar o melhor audio disponivel de URLs publicas.

Baixe em:

https://github.com/yt-dlp/yt-dlp/releases

No Windows, procure o asset:

```text
yt-dlp.exe
```

Teste no `cmd`:

```bat
yt-dlp.exe --version
where yt-dlp.exe
```

Se nao estiver no PATH, use **Runtime > Escolher** e selecione a pasta que contem `yt-dlp.exe`.

Observacoes:

- O suporte depende do yt-dlp e pode variar por site.
- URLs com login obrigatorio, cookies, OAuth, tokens, DRM ou restricoes de acesso nao sao suportadas nesta fase.
- Lives/streams ao vivo ainda nao sao suportados; use videos ja publicados/VOD.

## 5. Instalar Deno para melhorar YouTube

O YouTube pode exigir que o yt-dlp resolva desafios JavaScript. Para isso, instale o Deno:

https://github.com/denoland/deno/releases

No Windows, procure o asset:

```text
deno-x86_64-pc-windows-msvc.zip
```

Extraia o ZIP e teste:

```bat
deno.exe --version
```

Se nao estiver no PATH, use **Runtime > Escolher** e selecione a pasta que contem `deno.exe`.

Mesmo com Deno, alguns videos podem falhar se o YouTube exigir login/cookies, aplicar bloqueio anti-bot ou restringir o video.

## 6. Usar sessao do navegador

Alguns sites, especialmente YouTube, podem pedir login/cookies ou bloquear downloads anonimos. Nesses casos, o app pode pedir autorizacao para o yt-dlp ler a sessao do navegador selecionado apenas durante aquela execucao.

O WhisperTranscriber nao salva cookies, tokens ou senhas. Use essa opcao apenas com conteudo que voce tem permissao para acessar e respeitando os termos da plataforma.

Navegadores inicialmente previstos:

```text
chrome
edge
firefox
```

No Windows, Firefox costuma ser mais confiavel para essa integracao. Chrome e Edge podem falhar com DPAPI mesmo fechados, dependendo da versao/configuracao do navegador.

Se aparecer:

```text
Could not copy Chrome cookie database
```

feche completamente o Chrome/Edge antes de tentar novamente. No Windows, navegadores Chromium podem bloquear o banco de cookies enquanto estao abertos, impedindo o yt-dlp de copiar a sessao.

Se aparecer:

```text
Failed to decrypt with DPAPI
```

tente uma destas alternativas:

- usar Firefox e selecionar `firefox` no app;
- exportar cookies para um arquivo Netscape `cookies.txt` usando uma ferramenta/extensao de sua confianca e selecionar `cookies.txt` no app;
- usar outro perfil/navegador onde voce esteja logado.

## 7. Erro VCRUNTIME140.dll ou MSVCP140.dll

Se o Windows disser que `VCRUNTIME140.dll` ou `MSVCP140.dll` nao foi encontrado, instale o Microsoft Visual C++ Redistributable x64:

https://aka.ms/vs/17/release/vc_redist.x64.exe

Depois feche e reabra o terminal.

## 8. Erro -1073741795 / 0xc000001d

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

## 9. Teste manual completo

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

## 10. Teste manual de URL publica

Baixe somente o melhor audio de uma URL publica:

```bat
yt-dlp.exe --no-playlist -f "bestaudio/best" -o "%TEMP%\web_audio.%%(ext)s" "https://URL_PUBLICA"
```

Depois use o arquivo baixado no teste manual completo acima.

Para testar com Deno e sessao do navegador:

```bat
yt-dlp.exe --no-playlist --js-runtimes "deno:C:\CAMINHO\deno.exe" --cookies-from-browser chrome -f "bestaudio/best" -o "%TEMP%\web_audio.%%(ext)s" "https://URL_PUBLICA"
```

## 11. Logs do WhisperTranscriber

O app grava logs em:

```text
%LOCALAPPDATA%\WhisperTranscriber\logs\WhisperTranscriber.log
```
