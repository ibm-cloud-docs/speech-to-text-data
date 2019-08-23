---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-16"

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

# Funzioni delle metriche
{: #metrics}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} può restituire due tipi di metriche facoltative per una richiesta di riconoscimento vocale:

-   Le [metriche di elaborazione](#processing_metrics) forniscono informazioni periodiche sull'elaborazione dell'audio di input del servizio. Utilizza le metriche per misurare l'avanzamento del servizio nella trascrizione dell'audio. Le metriche di elaborazione sono disponibili con le interfacce WebSocket e HTTP asincrona.
-   Le [metriche audio](#audio_metrics) forniscono le informazioni sulle caratteristiche di segnale dell'audio di input. Utilizza le metriche per determinare le caratteristiche e la qualità dell'audio. Le metriche audio sono disponibili con tutte le interfacce di riconoscimento vocale. 

Per impostazione predefinita, il servizio non restituisce metriche per una richiesta. 

## Metriche di elaborazione
{: #processing_metrics}

Le metriche di elaborazione forniscono informazioni di temporizzazione dettagliate relative all'analisi dell'audio di input del servizio. Il servizio restituisce le metriche agli intervalli specificati e con gli eventi di trascrizioni, ad esempio i risultati provvisori e finali. 

Le metriche includono le statistiche sulla quantità di audio ricevuta dal servizio, sulla quantità di audio trasferita dal servizio al motore di riconoscimento vocale e per quanto tempo il servizio ha elaborato l'audio. Se richiedi etichette del parlante, le informazioni mostrano anche la quantità di audio elaborata dal servizio per determinare le etichette del parlante. 

Le metriche di elaborazione possono aiutarti a misurare l'avanzamento di una richiesta di riconoscimento. Possono anche aiutarti a distinguere l'assenza di risultati a causa di 

-   Mancanza di audio.
-   Mancanza di un discorso nell'audio inoltrato. 
-   Rallentamenti del motore nel server e rallentamenti di rete tra il client e il server. Per differenziare tra i rallentamenti del motore e quelli di rete, i risultati sono periodici piuttosto che basati sugli eventi. 

Le metriche possono anche aiutarti a stimare il jitter di risposta esaminando i tempi di arrivo periodici. Le metriche vengono generate a intervalli costanti, quindi qualsiasi differenza nei tempi di arrivo è causata dal jitter.

### Richiesta delle metriche di elaborazione
{: #processing_metrics_request}

Per richiedere le metriche di elaborazione, utilizza i seguenti parametri facoltativi: 

-   `processing_metrics` è un valore booleano che indica se il servizio deve restituire le metriche di elaborazione. Specifica `true` per richiedere le metriche. Per impostazione predefinita, il servizio non restituisce metriche. 
-   `processing_metrics_interval` è un valore mobile che specifica l'intervallo di tempo, in secondi, dell'orologio reale per cui il servizio deve restituire le metriche. Per impostazione predefinita, il servizio restituisce le metriche una volta al secondo. Il servizio ignora questo parametro a meno che il parametro `processing_metrics` non sia impostato su `true`.

    Il parametro accetta un valore minimo di 0,1 secondi. Il livello di precisione non è limitato, quindi puoi specificare valori come 0,25 e 0,125. Il servizio non impone un valore massimo. 

Il modo in cui fornisci i parametri e quello in cui il servizio restituisce le metriche di elaborazione differiscono in base all'interfaccia: 

-   Con l'interfaccia WebSocket, specifica i parametri con il messaggio JSON `start` per una richiesta di riconoscimento vocale. Il servizio calcola e restituisce le metriche in tempo reale all'intervallo richiesto. 
-   Con l'interfaccia HTTP asincrona, specifica i parametri di query con una richiesta di riconoscimento vocale. Il servizio calcola le metriche all'intervallo richiesto, ma restituisce tutte le metriche per l'audio con i risultati finali della trascrizione. 

Il servizio restituisce anche le metriche di elaborazione per gli eventi di trascrizione. Se richiedi dei risultati provvisori con l'interfaccia WebSocket, puoi ricevere le metriche con una frequenza maggiore rispetto all'intervallo richiesto. 

Per ricevere le metriche di elaborazione solo per gli eventi di trascrizione invece che a intervalli periodici, imposta l'intervallo di elaborazione su un numero più grande. Se l'intervallo è maggiore della durata dell'audio, il servizio restituisce le metriche di elaborazione solo per gli eventi di trascrizione. 

### Descrizione delle metriche di elaborazione
{: #processing_metrics_understand}

Il servizio restituisce le metriche di elaborazione nel campo `processing_metrics` dell'oggetto `SpeechRecognitionResults`. Per le metriche generate a intervalli periodici, l'oggetto contiene solo il campo `processing_metrics`, come mostrato nel seguente esempio. 

```javascript
{
  "processing_metrics": {
    "processed_audio": {
      "received": float,
      "seen_by_engine": float,
      "transcription": float,
      "speaker_labels": float
    },
    "wall_clock_since_first_byte_received": float,
    "periodic": boolean
  }
}
```
{: codeblock}

Il campo `processing_metrics` include un oggetto `ProcessingMetrics` che ha i seguenti campi:

-   `wall_clock_since_first_byte_received` è la quantità di tempo reale in secondi trascorso dal momento in cui il servizio ha ricevuto il primo byte dell'audio di input. Generalmente, i valori in questo campo sono multipli dell'intervallo di metriche specificato, con due differenze: 
    -   I valori potrebbero non riflettere gli intervalli esatti come 0,25, 0,5 e così via. I valori effettivi potrebbero, ad esempio, essere 0,27, 0,52 e così via, a seconda di quando il servizio riceve ed elabora l'audio. 
    -   I valori per gli eventi di trascrizione non sono correlati all'intervallo di elaborazione. Il servizio restituisce i risultati basati su eventi man mano che si verificano. 
-   `periodic` indica se le metriche si applicano a un intervallo periodico o a un evento di trascrizione:
    -   `true` indica che la risposta è stata attivata da un intervallo di elaborazione. Le informazioni contengono solo metriche di elaborazione. 
    -   `false` indica che la risposta è stata attivata da un evento di trascrizione. Le informazioni contengono le metriche di elaborazione più i risultati della trascrizione. 

    Utilizza questo campo per identificare il motivo per cui il servizio ha generato la risposta e per filtrare i diversi risultati se necessario.
-   `processed_audio` include un oggetto `ProcessedAudio` che fornisce le informazioni di temporizzazione dettagliate sull'elaborazione dell'audio di input del servizio.

L'oggetto `ProcessedAudio` include i seguenti campi. Tutti i campi fanno riferimento ai secondi dell'audio a partire da questa risposta. Solo il campo `wall_clock_since_first_byte_received` fa riferimento al tempo reale trascorso. 

-   `received` indica i secondi di audio ricevuti dal servizio. 
-   `seen_by_engine` indica i secondi di audio che il servizio ha passato al suo motore di elaborazione del discorso. 
-   `transcription` indica i secondi di audio che il servizio ha elaborato per il riconoscimento vocale. 
-   `speaker_labels` indica il numero di secondi di audio che il servizio ha elaborato per le etichette del parlante. La risposta include questo campo solo se hai richiesto le etichette del parlante. 

Il motore di elaborazione del discorso analizza l'audio di input più volte. L'oggetto `processed_audio` mostra i valori per l'audio che il motore ha elaborato e non li leggerà di nuovo. L'audio elaborato non influisce su ipotesi di riconoscimento future. 

Le metriche indicano l'avanzamento e la complessità dell'elaborazione del motore:

-   `seen_by_engine` indica l'audio che il servizio ha letto e passato al motore almeno una volta. 
-   `received` - `seen_by_engine` indica l'audio che è stato memorizzato nel buffer nel servizio ma che non è stato ancora esaminato o elaborato dal motore.
-   La relazione tra i tempi è `received` >= `seen_by_engine` >= `transcription` >= `speaker_labels`.

Le seguenti relazioni possono essere utili anche nella comprensione dei risultati: 

-   I valori dei campi `received` e `seen_by_engine` sono maggiori dei valori dei campi `transcription` e `speaker_labels` durante l'elaborazione del riconoscimento vocale. Il servizio deve ricevere l'audio prima di poter iniziare a elaborare i risultati. 
-   I valori dei campi `received` e `seen_by_engine` sono identici quando il servizio ha terminato l'elaborazione dell'audio. I valori finali dei campi possono essere maggiori dei valori dei campi `transcription` e `speaker_labels` per un numero frazionario di secondi. 
-   Il valore del campo `speaker_labels` di solito traccia il valore del campo `transcription` durante l'elaborazione del riconoscimento vocale. I valori dei campi `transcription` e `speaker_labels` sono identici quando il servizio ha terminato l'elaborazione dell'audio.

### Esempio di metriche di elaborazione: interfaccia WebSocket
{: #processing_metrics_example_websocket}

Il seguente esempio mostra il messaggio `start` passato per una richiesta all'interfaccia WebSocket. La richiesta abilita le metriche di elaborazione e imposta l'intervallo delle metriche di elaborazione su 0,25 secondi. Imposta anche i parametri `interim_results` e `speaker_labels` su `true`. L'audio contiene il semplice messaggio "hello world long pause stop."

```javascript
function onOpen(evt) {
  var message = {
    action: 'start',
    content-type: 'audio/flac',
    processing_metrics: true,
    processing_metrics_interval: 0.25,
    interim_results: true,
    speaker_labels: true
  };
  websocket.send(JSON.stringify(message));
  websocket.send(blob);
}
```
{: codeblock}

Il seguente output di esempio mostra i primi risultati delle metriche di elaborazione restituite dal servizio per la richiesta. 

```javascript
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 1.59,
      "transcription": 0.49,
      "speaker_labels": 0.0
    },
    "wall_clock_since_first_byte_received": 0.32,
    "periodic": true
  }
}
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 1.59,
      "transcription": 0.49,
      "speaker_labels": 0.0
    },
    "wall_clock_since_first_byte_received": 0.51,
    "periodic": false
  },
  "results": [
    {
      "alternatives": [
        {
          "timestamps": [
            [
              "hello",
              0.43,
              0.76
            ],
            [
              "world",
              0.76,
              1.22
            ]
          ],
          "transcript": "hello world "
        }
      ],
      "final": false
    }
  ],
  "result_index": 0
}
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 2.59,
      "transcription": 1.25,
      "speaker_labels": 0.0
    },
    "wall_clock_since_first_byte_received": 0.57,
    "periodic": true
  }
}
. . .
```
{: codeblock}

### Esempio di metriche di elaborazione: interfaccia HTTP asincrona
{: #processing_metrics_example_http}

Il seguente esempio mostra una richiesta di riconoscimento vocale per il metodo `/v1/recognitions` dell'interfaccia HTTP asincrona. La richiesta abilita le metriche di elaborazione e specifica un intervallo di 0,25 secondi. Di nuovo, il file audio include il messaggio "hello world long pause stop".

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognitions?processing_metrics=true&processing_metrics_interval=0.25"
```
{: pre}

Il seguente output di esempio mostra i primi due risultati delle metriche di elaborazione restituite dal servizio per la richiesta. 

```javascript
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 1.59,
      "transcription": 0.49
    },
    "wall_clock_since_first_byte_received": 0.32,
    "periodic": true
  }
}
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 2.59,
      "transcription": 1.25
    },
    "wall_clock_since_first_byte_received": 0.57,
    "periodic": true
  }
}
. . .
```
{: codeblock}

## Metriche audio
{: #audio_metrics}

Le metriche audio forniscono le informazioni dettagliate sulle caratteristiche di segnale dell'audio di input. I risultati forniscono le metriche aggregate per l'intero audio di input alla conclusione dell'elaborazione del discorso. Per un utente tecnicamente più esperto, le metriche forniscono informazioni approfondite significative sulle caratteristiche dettagliate dell'audio. 

Puoi utilizzare le metriche audio per fornire un'indicazione in tempo reale di un problema con l'audio di input e possibilmente anche una potenziale soluzione. Ad esempio, puoi fornire un messaggio come "There is too much noise in the background" o "Please come closer to the microphone." Puoi anche utilizzare uno strumento analitico offline per esaminare le caratteristiche di segnale e suggerire dati adatti per i futuri aggiornamenti del modello. 

### Richiesta delle metriche audio
{: #audio_metrics_request}

Per richiedere le metriche audio, imposta il parametro booleano `audio_metrics` su `true`. Per impostazione predefinita, il servizio non restituisce metriche. 

-   Con l'interfaccia WebSocket, specifica il parametro con il messaggio JSON `start` per una richiesta di riconoscimento vocale. 
-   Con le interfacce HTTP, specifica un parametro di query con una richiesta di riconoscimento vocale. 

Il servizio restituisce le metriche audio con i risultati finali della trascrizione. Restituisce le metriche solo una volta per l'intero flusso audio. Anche se il servizio restituisce più risultati della trascrizione (per blocchi di audio diversi), restituisce solo una singola istanza delle metriche alla fine dei risultati. 

L'interfaccia WebSocket accetta più flussi (o file) audio con una singola connessione. Delimita i diversi flussi inviando messaggi `stop` o blob binari vuoti al servizio. In questo caso, il servizio restituisce metriche separate per ciascun flusso audio delimitato. 

### Descrizione delle metriche audio
{: #audio_metrics_understand}

Il servizio restituisce le metriche nel campo `audio_metrics` dell'oggetto `SpeechRecognitionResults`. 

```javascript
{
  "results": [
    . . .
  ],
  "result_index": integer,
  "audio_metrics": {
    "sampling_interval": float,
    "accumulated": {
      "final": boolean,
      "end_time": float,
      "signal_to_noise_ratio": float,
      "speech_ratio": float,
      "high_frequency_loss": float,
      "direct_current_offset": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ],
      "clipping_rate": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ],
      "speech_level": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ],
      "non_speech_level": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ]
    }
  }
}
```
{: codeblock}

Il campo `audio_metrics` include un oggetto `AudioMetrics` che ha due campi: 

-   `sampling_interval` indica l'intervallo in secondi (di norma 0,1 secondi) per cui il servizio ha calcolato le metriche audio.
-   `accumulated` include un oggetto `AudioMetricsDetails` che fornisce informazioni dettagliate sulle caratteristiche di segnale dell'audio di input.

I seguenti campi dell'oggetto `AudioMetricsDetails` forniscono valori unari:

-   `final` indica se le metriche si riferiscono alla fine del flusso audio, a indicare che la trascrizione è completa. Attualmente, il campo è sempre `true`. Il servizio restituisce le metriche solo una volta per flusso audio. I risultati forniscono le metriche aggregate per il flusso completo. 
-   `end_time` specifica il tempo di fine, in secondi, dell'audio a cui si applicano le metriche. Poiché le metriche si applicano all'intero flusso audio, il tempo di fine indica sempre la lunghezza dell'audio. 
-   `signal_to_noise_ratio` fornisce l'SNR (signal-to-noise ratio) per il segnale audio. Il valore indica il rapporto discorso/rumore nell'audio. Un valore valido è compreso nell'intervallo da 0 a 100 decibel (dB). Il servizio omette il campo se non può calcolare l'SNR per l'audio.
-   `speech_ratio` è il rapporto dei segmenti vocali e non vocali nel segnale audio. Il valore è compreso nell'intervallo da 0,0 a 1,0.
-   `high_frequency_loss` indica la probabilità che nel segnale audio manchi la metà superiore del suo contenuto di frequenza. 
    -   Un valore vicino a 1,0 di norma indica un audio sovracampionato artificialmente, ciò influisce negativamente sull'accuratezza dei risultati della trascrizione. 
    -   Un valore pari o vicino a 0,0 indica che il segnale audio è buono e ha uno spettro completo.
    -   Un valore intorno a 0,5 indica che il rilevamento del contenuto di frequenza è inaffidabile o non disponibile. 

I seguenti campi dell'oggetto `AudioMetricsDetails` forniscono gli istogrammi per le caratteristiche di segnale. Ogni campo fornisce un array di oggetti `AudioMetricsHistogramBin`. Una singola unità presente in ciascun istogramma viene calcolata in base alla lunghezza di un intervallo di campionamento (`sampling_interval`) dell'audio.

-   `direct_current_offset` definisce un istogramma del componente DC (direct current) cumulativo del segnale audio. 
-   `clipping_rate` definisce un istogramma della frequenza di taglio per i segmenti audio. La frequenza di taglio è definita come la frazione di campioni nel segmento che raggiunge il valore massimo o minimo offerto dall'intervallo di quantizzazione audio. 

    Il servizio rileva automaticamente un intervallo audio PCM (Pulse-Code Modulation) a 16 bit (da -32768 a +32767) o un intervallo di unità (da -1,0 a +1,0). La frequenza di taglio è compresa tra 0,0 e 1,0. Valori più alti indicano la possibile riduzione del riconoscimento vocale.
-   `speech_level` definisce un istogramma del livello di segnale nei segmenti dell'audio che contengono il discorso. Il livello di segnale viene calcolato come il valore RMS (Root-Mean-Square) in una scala di decibel (dB) normalizzata nell'intervallo da 0,0 (livello minimo) a 1,0 (livello massimo).
-   `non_speech_level` definisce un istogramma del livello di segnale nei segmenti dell'audio che non contengono il discorso. Il livello di segnale viene calcolato come il valore RMS in una scala di decibel normalizzata nell'intervallo da 0,0 (livello minimo) a 1,0 (livello massimo). 

Ogni oggetto `AudioMetricsHistogramBin` descrive un contenitore con limiti `begin` e `end` definiti. Ogni contenitore indica il conteggio (`count`) o il numero di valori nell'intervallo delle caratteristiche di segnale di tale contenitore. Il primo e l'ultimo contenitore di un istogramma costituiscono i contenitori limite. Coprono, rispettivamente, gli intervalli compresi tra l'infinito negativo e il primo limite e tra l'ultimo limite e l'infinito positivo. 

### Esempi di metriche audio
{: #audio_metrics_example}

Il seguente esempio mostra una richiesta di riconoscimento vocale con l'interfaccia HTTP sincrona che restituisce le metriche audio. Il file audio include il semplice messaggio "hello world long pause stop".

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognitize?audio_metrics=true"
```
{: pre}

La risposta include le metriche audio per l'audio di input completo che ha una durata di 7,0 secondi. L'audio di input contiene leggermente più segmenti vocali che non vocali: da 37 a 33 segmenti, per un valore di `speech_ratio` pari a 0,529. La frequenza di taglio è bassissima, il che indica un audio di input di alta qualità. 

Il campo `high_frequency_loss` ha un valore pari a 0,5, ciò significa che il rilevamento del contenuto di frequenza del servizio è inaffidabile o non disponibile. I risultati omettono il campo `signal_to_noise_ratio` poiché il servizio non può calcolare l'SNR per l'audio.

```javascript
{
  "results": [
    {
      "alternatives": [
        {
          "confidence": 0.96,
          "transcript": "hello world "
        }
      ],
         "final": true
      },
      {
      "alternatives": [
        {
          "confidence": 0.79,
          "transcript": "long pause "
        }
      ],
         "final": true
      },
      {
      "alternatives": [
        {
          "confidence": 0.97,
          "transcript": "stop "
        }
      ],
      "final": true
    }
  ],
  "result_index": 0,
  "audio_metrics": {
    "sampling_interval": 0.1,
    "accumulated": {
      "final": true,
      "end_time": 7.0,
      "speech_ratio": 0.529,
      "high_frequency_loss": 0.5,
      "direct_current_offset": [
        {"begin": -1.0, "end": -0.9, "count": 0},
        {"begin": -0.9, "end": -0.7, "count": 0},
        {"begin": -0.7, "end": -0.5, "count": 0},
        {"begin": -0.5, "end": -0.3, "count": 0},
        {"begin": -0.3, "end": -0.1, "count": 0},
        {"begin": -0.1, "end": 0.1, "count": 70},
        {"begin": 0.1, "end": 0.3, "count": 0},
        {"begin": 0.3, "end": 0.5, "count": 0},
        {"begin": 0.5, "end": 0.7, "count": 0},
        {"begin": 0.7, "end": 0.9, "count": 0},
        {"begin": 0.9, "end": 1.0, "count": 0}
      ],
      "clipping_rate": [
        {"begin": 0.0, "end": 1e-05, "count": 70},
        {"begin": 1e-05, "end": 0.0001, "count": 0},
        {"begin": 0.0001, "end": 0.001, "count": 0},
        {"begin": 0.001, "end": 0.01, "count": 0},
        {"begin": 0.01, "end": 0.1, "count": 0},
        {"begin": 0.1, "end": 1.0, "count": 0}
      ],
      "speech_level": [
        {"begin": 0.0, "end": 0.1, "count": 37},
        {"begin": 0.1, "end": 0.2, "count": 0},
        {"begin": 0.2, "end": 0.3, "count": 0},
        {"begin": 0.3, "end": 0.4, "count": 0},
        {"begin": 0.4, "end": 0.5, "count": 0},
        {"begin": 0.5, "end": 0.6, "count": 0},
        {"begin": 0.6, "end": 0.7, "count": 0},
        {"begin": 0.7, "end": 0.8, "count": 0},
        {"begin": 0.8, "end": 0.9, "count": 0},
        {"begin": 0.9, "end": 1.0, "count": 0}
      ],
      "non_speech_level": [
        {"begin": 0.0, "end": 0.1, "count": 33},
        {"begin": 0.1, "end": 0.2, "count": 0},
        {"begin": 0.2, "end": 0.3, "count": 0},
        {"begin": 0.3, "end": 0.4, "count": 0},
        {"begin": 0.4, "end": 0.5, "count": 0},
        {"begin": 0.5, "end": 0.6, "count": 0},
        {"begin": 0.6, "end": 0.7, "count": 0},
        {"begin": 0.7, "end": 0.8, "count": 0},
        {"begin": 0.8, "end": 0.9, "count": 0},
        {"begin": 0.9, "end": 1.0, "count": 0}
      ]
    }
  }
}
```
{: codeblock}
