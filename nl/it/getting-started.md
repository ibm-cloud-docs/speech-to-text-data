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

# Esercitazione introduttiva
{: #gettingStarted}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} trascrive l'audio in testo per abilitare le funzionalità di trascrizione vocale per le applicazioni. Questa esercitazione basata su curl può aiutarti a iniziare a utilizzare subito il servizio. Gli esempi ti mostrano come chiamare il metodo `POST /v1/recognize` per richiedere una trascrizione.
{: shortdesc}

## Prima di cominciare
{: #before-you-begin}

Per utilizzare {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, devi completare innanzitutto la seguente procedura:

1.  Esegui il provisioning di un'istanza di {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}. Per ulteriori informazioni sul provisioning, vedi [Installazione del servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).
1.  Dal menu del client web {{site.data.keyword.icp4dfull_notm}}, scegli **My Instances**.
1.  Fai clic sull'istanza {{site.data.keyword.speechtotextshort}} per aprire la pagina della panoramica. Copia i valori credenziale `{token}` e `{URL}`. 

### Utilizzo degli esempi curl
{: #getting-started-curl}

Questa esercitazione utilizza il comando `curl` per chiamare tutti i metodi dell'interfaccia HTTP del servizio. Assicurati di avere il comando `curl` installato sul tuo sistema. 

1.  Per verificare se `curl` è installato, esegui il seguente comando sulla riga di comando. Se l'output elenca la versione `curl` che supporta SSL (Secure Sockets Layer), sei pronto per l'esercitazione. 

    ```bash
    curl -V
    ```
    {: pre}

1.  Se necessario, installa la versione di `curl` con SSL abilitato per il tuo sistema operativo da [curl.haxx.se](https://curl.haxx.se/){: external}.

Ometti le parentesi graffe dagli esempi. Indicano i valori delle variabili.
{: tip}

## Passo 1: trascrivi l'audio senza opzioni
{: #transcribe}

Chiama il metodo `POST /v1/recognize` per richiedere una trascrizione di base di un file audio FLAC senza parametri di richiesta aggiuntivi.

1.  Scarica il file audio di esempio <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>.
1.  Immetti il seguente comando per chiamare il metodo `/v1/recognize` del servizio per la trascrizione di base senza parametri. L'esempio utilizza l'intestazione `Content-Type` per indicare il tipo di audio, `audio/flac`. Per la trascrizione, l'esempio utilizza il modello di lingua predefinito `en-US_BroadbandModel`.
    -   Sostituisci `{token}` con il token di accesso per la tua istanza del servizio. 
    -   Sostituisci `{url}` con l'URL per la tua istanza del servizio. 
    -   Modifica `{path_to_file}` per specificare l'ubicazione del file `audio-file.flac`.

    *Utenti Windows,* sostituisci la barra retroversa (``\`) alla fine di ciascuna riga con un accento circonflesso (``^`). Assicurati che non ci siano spazi finali.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize"
    ```
    {: pre}

    Il servizio restituisce i seguenti risultati di trascrizione:

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

## Passo 2: trascrivi l'audio con opzioni
{: #transcribeOptions}

Chiama il metodo `POST /v1/recognize` per trascrivere lo stesso file audio FLAC, ma specificando due parametri di trascrizione.

1.  Se necessario, scarica il file audio di esempio <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Icona link esterno" title="Icona link esterno"></a>.
1.  Immetti il seguente comando per chiamare il metodo `/v1/recognize` del servizio con due parametri supplementari. Imposta il parametro `timestamps` su `true` per indicare l'inizio e la fine di ogni parola nel flusso audio. Imposta il parametro `max_alternatives` su `3` per ricevere le tre alternative più probabili per la trascrizione. L'esempio utilizza l'intestazione `Content-Type` per indicare il tipo di audio, `audio/flac` e la richiesta utilizza il modello predefinito, `en-US_BroadbandModel`.
    -   Sostituisci `{token}` con il token di accesso per la tua istanza del servizio. 
    -   Sostituisci `{url}` con l'URL per la tua istanza del servizio. 
    -   Modifica `{path_to_file}` per specificare l'ubicazione del file `audio-file.flac`.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize?timestamps=true&max_alternatives=3"
    ```
    {: pre}

    Il servizio restituisce i seguenti risultati, che includono le date/ore e tre trascrizioni alternative:

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
              "transcript": "several tornadoes touch down as a line
of severe thunderstorms swept through Colorado on Sunday "
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

## Passi successivi

-   Ottieni ulteriori informazioni sulle interfacce e sugli SDK disponibili per effettuare richieste di riconoscimento vocale nella [Panoramica per gli sviluppatori](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).
-   Ottieni informazioni su come effettuare le richieste al servizio in [Effettuazione delle richieste al servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Vedi le richieste di riconoscimento vocale di base per ciascuna delle interfacce del servizio in [Effettuazione di una richiesta di riconoscimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Trova informazioni dettagliate su tutti i metodi delle interfacce del servizio nella [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
