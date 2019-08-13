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

# Usando um modelo acústico customizado
{: #acousticUse}

Depois de criar e treinar seu modelo acústico customizado, é possível utilizá-lo em solicitações de reconhecimento de voz. Use o parâmetro de consulta `acoustic_customization_id` para especificar o modelo acústico customizado para uma solicitação, conforme mostrado nos exemplos a seguir. Deve-se emitir a solicitação com credenciais para a instância do serviço que possui o modelo.
{: shortdesc}

Também é possível especificar um modelo de idioma customizado a ser usado com a solicitação, que pode aumentar a precisão da transcrição. Para obter mais informações, consulte [Usando modelos acústico e de idioma customizados durante o reconhecimento de voz](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth#useBothRecognize).

É possível criar múltiplos modelos acústicos customizados para os mesmos domínios ou ambientes ou para domínios ou ambientes diferentes. No entanto, é possível especificar apenas um modelo acústico customizado por vez com o parâmetro `acoustic_customization_id`.

-   Para a [interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets), use o método `/v1/recognize`. O modelo customizado especificado é usado para todas as solicitações que são enviadas por meio da conexão.

    ```javascript
    var my_access_token = '{token}';
    var wsURI = '{ws_url}/v1/recognize'
      + '?access_token=' + my_access_token
      + '&model=en-US_NarrowbandModel'
      + '&acoustic_customization_id={customization_id}';
    var websocket = new WebSocket(wsURI);
    ```
    {: codeblock}

-   Para a [interface de HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http), use o método `POST /v1/recognize`. O modelo customizado especificado é usado para essa solicitação.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file1.flac
    "{url}/v1/recognize?acoustic_customization_id={customization_id}"
    ```
    {: pre}

-   Para a [interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async), use o método `POST /v1/recognitions`. O modelo customizado especificado é usado para essa solicitação.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognitions?acoustic_customization_id={customization_id}"
    ```
    {: pre}

Será possível omitir o modelo de idioma por meio da solicitação se o modelo customizado for baseado no modelo padrão, `en-US_BroadbandModel`. Caso contrário, deve-se usar o parâmetro `model` para especificar o modelo base, conforme mostrado para o exemplo do WebSocket. Um modelo customizado pode ser usado somente com o modelo base para o qual ele é criado.
