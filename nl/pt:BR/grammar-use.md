---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# Usando uma gramática para reconhecimento de voz
{: #grammarUse}

Depois de criar e treinar seu modelo de idioma customizado com sua gramática, é possível usar a gramática em solicitações de reconhecimento de voz com as interfaces do WebSocket e de HTTP síncrona e assíncrona do serviço.
{: shortdesc}

-   Use o parâmetro `language_customization_id` para especificar o ID de customização (GUID) do modelo de idioma customizado para o qual a gramática está definida. Deve-se emitir a solicitação com credenciais para a instância do serviço que possui o modelo.
-   Use o parâmetro `grammar_name` para especificar o nome da gramática. É possível especificar somente uma única gramática com uma solicitação.

Quando você usa uma gramática, o serviço reconhece apenas palavras da gramática especificada. O serviço não usa palavras customizadas que foram incluídas dos corpora, que foram incluídas ou modificadas individualmente ou que são reconhecidas por outras gramáticas.

-   Para a [interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets), você primeiro especifica o ID de customização com o parâmetro `language_customization_id` do método `/v1/recognize`. Você usa esse método para estabelecer uma conexão do WebSocket com o serviço.

    ```javascript
    var my_access_token = '{token}';
    var wsURI = '{ws_url}/v1/recognize'
      + '?access_token=' + my_access_token
      + '&language_customization_id={customization_id}';
    var websocket = new WebSocket(wsURI);
    ```
    {: codeblock}

    Em seguida, especifique o nome da gramática com o parâmetro `grammar_name` na mensagem JSON `start` para a conexão ativa. Transmitir esse valor com a mensagem `start` permite mudar a gramática dinamicamente para cada solicitação que você envia por meio da conexão.

    ```javascript
    function onOpen(evt) {
      var message = {
        action: 'start',
        content-type: 'audio/l16;rate=22050',
        grammar_name: '{grammar_name}'
      };
      websocket.send(JSON.stringify(message));
      websocket.send(blob);
    }
    ```
    {: codeblock}
-   Para a [interface HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http), passe os dois parâmetros com o método `POST /v1/recognize`.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognize?language_customization_id={customization_id}&grammar_name={grammar_name}"
    ```
    {: pre}
-   Para a [interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async), passe os dois parâmetros com o método `POST /v1/recognitions`.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognitions?language_customization_id={customization_id}&grammar_name={grammar_name}"
    ```
    {: pre}
