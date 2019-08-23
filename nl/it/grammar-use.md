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

# Utilizzo di una grammatica per il riconoscimento vocale
{: #grammarUse}

Una volta creato e addestrato il tuo modello di lingua personalizzato con la tua grammatica, puoi utilizzare la grammatica nelle richieste di riconoscimento vocale con le interfacce WebSocket e HTTP sincrone e asincrone del servizio.
{: shortdesc}

-   Utilizza il parametro `language_customization_id` per specificare l'ID (GUID) di personalizzazione del modello di lingua personalizzato per il quale è definita la grammatica. Devi immettere la richiesta con le credenziali per l'istanza del servizio proprietaria del modello.

-   Utilizza il parametro `grammar_name` per specificare il nome della grammatica. Puoi specificare solo una singola grammatica con una richiesta.

Quando utilizzi una grammatica, il servizio riconosce solo le parole dalla grammatica specificata. Il servizio non utilizza le parole personalizzate che sono state aggiunte dai corpora, che sono state aggiunte o modificate singolarmente o che sono riconosciute da altre grammatiche.

-   Per l'[interfaccia WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets), devi prima specificare l'ID di personalizzazione con il parametro `language_customization_id` del metodo `/v1/recognize`. Questo metodo ti consente di stabilire una connessione WebSocket con il servizio.

    ```javascript
    var my_access_token = '{token}';
    var wsURI = '{ws_url}/v1/recognize'
      + '?access_token=' + my_access_token
      + '&language_customization_id={customization_id}';
    var websocket = new WebSocket(wsURI);
    ```
    {: codeblock}

    Quindi, specifica il nome della grammatica con il parametro `grammar_name` nel messaggio `start` JSON per la connessione attiva. Il passaggio di questo valore con il messaggio `start` ti consente di modificare la grammatica in modo dinamico per ogni richiesta che invii tramite la connessione.

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
-   Per l'[interfaccia HTTP sincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http), passa entrambi i parametri con il metodo `POST /v1/recognize`.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognize?language_customization_id={customization_id}&grammar_name={grammar_name}"
    ```
    {: pre}
-   Per l'[interfaccia HTTP asincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async), passa entrambi i parametri con il metodo `POST /v1/recognitions`.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognitions?language_customization_id={customization_id}&grammar_name={grammar_name}"
    ```
    {: pre}
