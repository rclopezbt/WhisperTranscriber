# Changelog

Todas as mudancas relevantes deste projeto serao documentadas aqui.

## 0.1.5 - 2026-05-30

- Adiciona planejamento implementado para transcricao por URL publica com yt-dlp.
- Adiciona instalacao guiada de yt-dlp e whisper-cli na tela Runtime.
- Adiciona instalacao guiada de Deno para melhorar compatibilidade do yt-dlp com YouTube.
- Adiciona opcao explicita para usar sessao do navegador em sites que exigem login/cookies.
- Adiciona suporte a arquivo cookies.txt para contornar falhas DPAPI do Chrome/Edge no Windows.
- Mantem FFmpeg como instalacao manual/assistida, sem embutir binario por padrao.
- Melhoria na exibição da transcrição durante processamento
- Precisão ampliada no cálculo de tempo restante
- Interface visual melhorada, para melhor legibilidade
- Autoinstalador de dependências/runtime
- Adiciona seleção de formatos de exportação
- Adiciona suporte ao format .VTT

\* A disponibilidade dos vídeos no modo de transcrição web varia com base nas políticas e features do site correspondente e da extensão _yt-dlp,_ não estando sob responsabilidade do WhisperTranscriber.

\** A lista completa de sites suportados pode ser encontrada na [documentação oficial do runtime](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md).

## 0.1.4 - 2026-05-26

- Adiciona janela de progresso durante transcricao.
- Mostra etapa atual, percentual quando disponivel, tempo decorrido, ETA e botao para cancelar.
- Usa progresso real do FFmpeg durante a conversao e progresso do whisper-cli quando o build informa percentual.

## 0.1.3 - 2026-05-26

- Corrige falha ao selecionar arquivos, pastas ou modelos com colchetes `[]` no caminho.

## 0.1.0 - Em preparo

- Estrutura inicial de distribuicao publica.
- Manifesto de atualizacao do canal estavel.
- Politica inicial para modelos, runtime e configuracoes de usuario.
