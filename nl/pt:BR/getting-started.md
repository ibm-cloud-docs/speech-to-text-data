---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-25"

subcollection: speech-to-text-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Tutorial de introdução
{: #gettingStarted}

O {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} transcreve áudio para texto para ativar os recursos de transcrição de fala para aplicativos. Esse tutorial baseado em curl pode ajudá-lo a começar rapidamente com o serviço. Os exemplos mostram como chamar o método `POST /v1/recognize` do serviço para solicitar uma transcrição.
{: shortdesc}

## Antes de iniciar
{: #before-you-begin}

Para usar o {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, deve-se primeiro concluir as etapas a seguir:

1.  Provisione uma instância do {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}. Para obter mais informações sobre o provisionamento, consulte [Instalando o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).
1.  No menu do Web client do {{site.data.keyword.icp4dfull_notm}}, escolha **Minhas instâncias**.
1.  Clique na instância do {{site.data.keyword.speechtotextshort}} para abrir a página de visão geral. Copie os valores de credencial de `{token}` e de `{URL}`.

### Usando os exemplos de curl
{: #getting-started-curl}

Esse tutorial usa o comando `curl` para chamar métodos da interface HTTP do serviço. Certifique-se de ter o comando `curl` instalado em seu sistema.

1.  Para testar se o `curl` está instalado, execute o comando a seguir na linha de comandos. Se a saída listar a versão do `curl` que suporta Secure Sockets Layer (SSL), tudo estará configurado para o tutorial.

    ```bash
    curl -V
    ```
    {: pre}

1.  Se necessário, instale a versão do `curl` com SSL ativado para seu sistema operacional em
[curl.haxx.se](https://curl.haxx.se/){: external}.

Omita as chaves nos exemplos. Eles indicam valores de variáveis.
{: tip}

## Etapa 1: Transcrições de áudio sem opções
{: #transcribe}

Chame o método `POST /v1/recognize` para solicitar uma transcrição básica de um arquivo de áudio FLAC sem nenhum parâmetro de solicitação adicional.

1.  Faça download do arquivo de áudio de amostra <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>.
1.  Emita o comando a seguir para chamar o método `/v1/recognize` do serviço para a transcrição básica sem parâmetros. O exemplo usa o cabeçalho `Content-Type` para indicar o tipo de áudio, `audio/flac`. O exemplo usa o modelo de idioma padrão, `en-US_BroadbandModel` para transcrição.
    -   Substitua `{token}` pelo token de acesso para a sua instância de serviço.
    -   Substitua `{url}` pela URL para sua instância de serviço.
    -   Modifique `{path_to_file}` para especificar a localização do arquivo `audio-file.flac`.

    *Usuários do Windows,* substituam a barra invertida (``\`) no final de cada linha por um acento circunflexo (``^`). Certifiquem-se de que não haja espaços à direita.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize"
    ```
    {: pre}

    O serviço retorna os resultados da transcrição a seguir:

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "confidence": 0.96,
          "transcript": "several tornadoes touch down as a line of
severe thunderstorms swept through Colorado on Sunday "
        }
          ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Etapa 2: Transcrever áudio com opções
{: #transcribeOptions}

Chame o método `POST /v1/recognize` para transcrever o mesmo arquivo de áudio FLAC, mas especifique dois parâmetros de transcrição.

1.  Se necessário, faça download do arquivo de áudio de amostra <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>.
1.  Emita o comando a seguir para chamar o método `/v1/recognize` do serviço com dois parâmetros extras. Configure o parâmetro `timestamps` como `true` para indicar o início e o fim de cada palavra no fluxo de áudio. Configure o parâmetro `max_alternatives` como `3` para receber as três alternativas mais prováveis para a transcrição. O exemplo usa o cabeçalho `Content-Type` para indicar o tipo de áudio, `audio/flac` e a solicitação usa o modelo padrão, `en-US_BroadbandModel`.
    -   Substitua `{token}` pelo token de acesso para a sua instância de serviço.
    -   Substitua `{url}` pela URL para sua instância de serviço.
    -   Modifique `{path_to_file}` para especificar a localização do arquivo `audio-file.flac`.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize?timestamps=true&max_alternatives=3"
    ```
    {: pre}

    O serviço retorna os resultados a seguir, que incluem os registros de data e hora e três transcrições alternativas:

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "timestamps": [
                ["several":, 1.0, 1.51],
                ["tornadoes":, 1.51, 2.15],
                ["touch":, 2.15, 2.5],
                . . .
              ]
            },
            {
              "confidence": 0.96,
          "transcript": "several tornadoes touch down as a line of
severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touched down as a line of
severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touch down as a line
of severe thunderstorms swept through Colorado and Sunday "
            }
          ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Próximas Etapas

-   Saiba mais sobre as interfaces e os SDKs que estão disponíveis para fazer solicitações de reconhecimento de voz na [Visão geral para desenvolvedores](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).
-   Saiba como fazer solicitações para o serviço em [Fazendo solicitações para o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Consulte as solicitações básicas de reconhecimento de voz para cada uma das interfaces do serviço em [Fazendo uma solicitação de reconhecimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Localize informações detalhadas sobre todos os métodos das interfaces do serviço na [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
