---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

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

# Effettuazione di una richiesta di riconoscimento
{: #basic-request}

Per richiedere il riconoscimento vocale con {{site.data.keyword.speechtotextdatafull}} per {{site.data.keyword.icp4dfull}}, devi fornire solo l'audio che deve essere trascritto. Il servizio offre le stesse funzionalità di trascrizione di base con ciascuna delle sue interfacce.
{: shortdesc}

Le seguenti sezioni mostrano le richieste di trascrizione di base per ognuna delle interfacce del servizio: 

-   Gli esempi inoltrano un breve file FLAC chiamato <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>.
-   Gli esempi utilizzano il modello di lingua predefinito, `en-US_BroadbandModel`.

[Descrizione dei risultati del riconoscimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-response) descrive la risposta del servizio per questi esempi.

Se utilizzi un certificato autofirmato, devi disabilitare la verifica SSL per consentire una richiesta al servizio. Per ulteriori informazioni, vedi [Disabilitazione della verifica SSL](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests#SSLverification).
{: important}

## Invio di audio con una richiesta
{: #basic-request-audio}

L'audio che passi al servizio deve essere in uno dei formati supportati dal servizio. Per la maggior parte dei tipi di audio, il servizio può rilevare automaticamente il formato. Per alcuni tipi di audio, devi specificare il formato con `Content-Type` o un parametro equivalente. Per ulteriori informazioni, vedi [Formati audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats). (Per maggiore chiarezza, i seguenti esempi specificano il formato audio con tutte le richieste.)

Le interfacce del servizio accettano quantità massime di audio diverse. Devi inviare almeno 100 byte di audio con qualsiasi richiesta.

-   Con le interfacce WebSocket e HTTP sincrona, puoi passare un massimo di 100 MB di dati audio con una singola richiesta.
-   Con l'interfaccia HTTP asincrona, puoi passare un massimo di 1 GB di dati audio con una richiesta.

Se riconosci grandi quantità di audio, puoi dividere manualmente l'audio in porzioni più piccole. Ma di solito è più efficiente e conveniente convertire l'audio in un formato compresso e con perdita. La compressione può massimizzare la quantità di dati che puoi inviare con una singola richiesta. Soprattutto se l'audio è in formato WAV o FLAC, convertirlo in un formato con perdita può fare una differenza considerevole.

-   Per ulteriori informazioni sui formati audio che utilizzano la compressione, vedi [Formati audio supportati](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#formats).
-   Per ulteriori informazioni sugli effetti della compressione e sulla conversione dell'audio in un formato che la utilizza, vedi [Limiti e compressione dei dati](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#limits) e [Conversione audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#conversion).

## Utilizzo dell'interfaccia WebSocket
{: #basic-request-websocket}

[L'interfaccia WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) fornisce un'implementazione efficiente che offre bassa latenza e velocità effettiva elevata su una connessione full duplex. Tutte le richieste e le risposte vengono inviate tramite la stessa connessione WebSocket. Grazie ai loro vantaggi, i WebSocket sono il meccanismo preferito per il riconoscimento vocale. Per ulteriori informazioni, vedi [Vantaggi dell'interfaccia WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview#advantages).

Per utilizzare l'interfaccia WebSocket, devi prima utilizzare il metodo `/v1/recognize` per stabilire una connessione con il servizio. Specifica i parametri come il modello di lingua e qualsiasi modello personalizzato da utilizzare per le richieste inviate tramite la connessione. Quindi, registra i listener di eventi per gestire le risposte fornite dal servizio. Per effettuare una richiesta, invia un messaggio di testo JSON che include il formato audio e qualsiasi parametro aggiuntivo. Passa l'audio come messaggio binario (blob), quindi invia un messaggio di testo per segnalare la fine dell'audio.

Il seguente esempio fornisce il codice JavaScript che stabilisce una connessione e invia i messaggi di testo e binari per una richiesta di riconoscimento. L'esempio non include il codice per installare i gestori eventi.

```javascript
var my_access_token = '{token}';
var wsURI = '{ws_url}/v1/recognize'
  + '?access_token=' + my_access_token;
var websocket = new WebSocket(wsURI);

websocket.send(JSON.stringify({
  action: 'start',
  content-type: 'audio/flac'
}));
websocket.send(blob);
websocket.send(JSON.stringify({'action': 'stop'}));
```
{: codeblock}

## Utilizzo dell'interfaccia HTTP sincrona
{: #basic-request-http}

[L'interfaccia HTTP sincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fornisce il modo più semplice per effettuare una richiesta di riconoscimento. Utilizza il metodo `POST /v1/recognize` per effettuare una richiesta al servizio. Passa l'audio e tutti i parametri con la singola richiesta.

Il seguente esempio `curl` mostra una richiesta di riconoscimento HTTP di base:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @audio-file.flac
"{url}/v1/recognize"
```
{: pre}

## Utilizzo dell'interfaccia HTTP asincrona
{: #basic-request-async}

[L'interfaccia HTTP asincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fornisce un'interfaccia non bloccante per la trascrizione dell'audio. Puoi utilizzare l'interfaccia con o senza la previa registrazione di un URL di callback con il servizio. Con un URL di callback, il servizio invia notifiche di callback con lo stato del lavoro e i risultati del riconoscimento.

L'interfaccia utilizza le firme HMAC-SHA1 basate su un segreto specificato dall'utente per fornire l'autenticazione e l'integrità dei dati per le sue notifiche. Senza un URL di callback, devi eseguire il polling del servizio per ottenere lo stato del lavoro e i risultati. Con entrambi gli approcci, utilizzi il metodo `POST /v1/recognitions` per effettuare una richiesta di riconoscimento.

Il seguente esempio `curl` mostra una semplice richiesta di riconoscimento HTTP asincrona. La richiesta non include un URL di callback, quindi devi eseguire il polling del servizio per ottenere lo stato del lavoro e la trascrizione risultante.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @audio-file.flac
"{url}/v1/recognitions"
```
{: pre}
