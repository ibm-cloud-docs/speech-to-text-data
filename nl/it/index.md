---

Copyright:
  years: 2018, 2019
lastupdated: "2019-07-24"

subcollection: speech-to-text-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Informazioni
{: #about}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} fornisce funzionalità di riconoscimento vocale per le tue applicazioni. Il servizio sfrutta il machine learning per combinare la conoscenza della grammatica, la struttura della lingua e la composizione dei segnali audio e vocali per trascrivere accuratamente la voce umana. Aggiorna e perfeziona continuamente la sua trascrizione man mano che riceve più discorsi.
{: shortdesc}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} fornisce varie interfacce che lo rendono adatto a qualsiasi applicazione in cui il discorso è l'input e una trascrizione testuale è l'output. Le applicazioni di esempio includono

-   Controllo vocale di applicazioni, dispositivi integrati e accessori per veicoli
-   Trascrizione di riunioni e conference call
-   Dettatura di messaggi e-mail e note

Il servizio è ideale per i clienti che devono estrarre trascrizioni vocali ad alta qualità dall'audio di un call center. I clienti in settori come i servizi finanziari, l'assistenza sanitaria, le assicurazioni e le telecomunicazioni possono sviluppare applicazioni native cloud per il servizio clienti, la voce del cliente, l'assistenza agent e altre soluzioni. 

Per informazioni sull'installazione e la configurazione di {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, vedi [Installazione del servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} è basato sul servizio {{site.data.keyword.speechtotextfull}} sul {{site.data.keyword.cloud_notm}} pubblico. Per ulteriori informazioni sul servizio pubblico, vedi [About {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.
{: note}

## Interfacce supportate
{: #interfaces}

Il servizio {{site.data.keyword.speechtotextshort}} offre più interfacce per il riconoscimento vocale: 

-   Un'[interfaccia WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) per stabilire connessioni persistenti, full duplex e a bassa latenza con il servizio. Puoi passare un massimo di 100 MB di dati audio al servizio con una singola richiesta.
-   Un'[interfaccia HTTP sincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) per le chiamate HTTP di base al servizio. Puoi passare un massimo di 100 MB di dati audio con una richiesta.
-   Un'[interfaccia HTTP asincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) per chiamate non bloccanti al servizio. Puoi passare fino a 1 GB di dati audio con una richiesta.

Il servizio fornisce anche un'[interfaccia di personalizzazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) che puoi utilizzare per ottimizzare il riconoscimento vocale per i tuoi requisiti di lingua e acustici. Puoi espandere il vocabolario di un modello con la terminologia specifica per il dominio o adattare un modello per le caratteristiche acustiche del tuo audio. Puoi anche aggiungere delle [grammatiche](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) per limitare le frasi che il servizio può riconoscere.

-   Per informazioni su come effettuare le richieste con ciascuna delle interfacce {{site.data.keyword.speechtotextshort}}, vedi [Effettuazione delle richieste al servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Per degli esempi di richieste di riconoscimento vocale di base con ciascuna delle interfacce del servizio, vedi [Effettuazione di una richiesta di riconoscimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Per una descrizione di alto livello dello sviluppo di applicazioni con il servizio, vedi [Panoramica per gli sviluppatori](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).

Sono disponibili degli SDK in molti linguaggi di programmazione per semplificare l'utilizzo del servizio. Per ulteriori informazioni, vedi la [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Funzioni di input
{: #inputFeatures}

Le interfacce del servizio condividono molte funzioni di input comuni per la trascrizione da voce a testo: 

-   [Formati audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats) - Puoi trascrivere l'audio Ogg o Web Media (WebM) con il codec Opus o Vorbis, MP3 (o MPEG), WAV (Waveform Audio File Format), FLAC (Free Lossless Audio Codec), PCM (Pulse-Code Modulation) lineare a 16 bit, G.729, A-law, mu-law (o u-law) e audio di base. Utilizzando un formato che supporta la compressione, puoi massimizzare la quantità di dati audio che puoi inviare con una richiesta.
-   [Lingue e modelli](/docs/services/speech-to-text-data?topic=speech-to-text-data-models) - Puoi trascrivere l'audio utilizzando modelli a banda larga o a banda stretta. Utilizza la banda larga per l'audio campionato a una frequenza minima di 16 kHz. Utilizza la banda stretta per l'audio campionato a una frequenza minima di 8 kHz.
-   [Trasmissione audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission) - Puoi passare l'audio come flusso continuo di porzioni di dati o come fornitura unica che passa tutti i dati in una volta. Con l'invio in streaming, il servizio applica dei [timeout](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts) di inattività e di sessione.

## Funzioni di output
{: #outputFeatures}

La maggior parte delle interfacce supporta anche le seguenti funzioni di output comuni:

-   Le [etichette del parlante](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels) riconoscono parlanti diversi dall'audio in inglese americano, giapponese o spagnolo. La trascrizione etichetta i contributi di ciascun parlante a una conversazione tra più partecipanti. (Funzionalità beta.)
-   L'[individuazione di parole chiave](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting) identifica le frasi pronunciate che corrispondono alle stringhe di parole chiave specificate con un livello di attendibilità definito dall'utente. L'individuazione di parole chiave è particolarmente utile quando le singole frasi dall'audio sono più importanti della trascrizione completa. Ad esempio, un sistema di supporto clienti potrebbe identificare le parole chiave per determinare come instradare le richieste degli utenti.
-   I [risultati provvisori](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim) restituiscono ipotesi continuamente perfezionate durante lo svolgimento della trascrizione. Il servizio restituisce i risultati finali al termine della trascrizione. I risultati provvisori sono disponibili solo con l'interfaccia WebSocket.
-   Il [numero massimo di alternative](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives) fornisce possibili trascrizioni alternative. Il servizio indica i risultati finali in cui ha la massima attendibilità.
-   Le [alternative alle parole](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives) richiedono parole alternative che siano acusticamente simili alle parole di una trascrizione.
-   L'[attendibilità delle parole](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence) restituisce i livelli di attendibilità per ogni parola di una trascrizione.
-   Le [date/ore delle parole](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps) restituiscono le date e ore per l'inizio e la fine di ogni parola di una trascrizione.
-   La [formattazione intelligente](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting) converte date, ore, numeri, valori di valuta, numeri di telefono e indirizzi Internet in formati convenzionali più leggibili nelle trascrizioni finali. Per l'inglese americano, puoi anche fornire frasi di parole chiave per includere determinati simboli di punteggiatura nelle trascrizioni finali. La formattazione intelligente è supportata per l'audio in inglese americano, giapponese e spagnolo. (Funzionalità beta.)
-   L'[oscuramento numerico](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction) oscura, o maschera, i dati numerici da una trascrizione finale. L'oscuramento ha lo scopo di rimuovere le informazioni personali sensibili, come i numeri delle carte di credito, dalle trascrizioni. La funzione è supportata per l'audio in inglese americano, giapponese e coreano. (Funzionalità beta.)
-   Il [filtro di contenuto volgare](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter) censura il contenuto volgare nelle trascrizioni in inglese americano.
-   Le [metriche di elaborazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) forniscono le informazioni di temporizzazione dettagliate relative all'analisi dell'audio di input del servizio. 
-   Le [metriche audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) forniscono le informazioni dettagliate sulle caratteristiche di segnale dell'audio di input. 

## Supporto delle lingue
{: #languages}

Il servizio offre modelli per le seguenti lingue: portoghese brasiliano, francese, tedesco, giapponese, coreano, cinese mandarino, arabo standard moderno, spagnolo, inglese britannico e inglese americano. Il servizio non supporta tutte le funzioni per tutte le lingue. Inoltre, supporta alcune funzioni come generalmente disponibili (GA) per l'uso in produzione e altre come offerte beta per diverse lingue.

-   Le interfacce WebSocket e HTTP sincrone e asincrone sono generalmente disponibili per tutte le lingue. 
-   Il servizio offre sia i modelli a banda larga che a banda stretta per tutte le lingue. Per ulteriori informazioni, vedi [Lingue e modelli](/docs/services/speech-to-text-data?topic=speech-to-text-data-models).
-   Alcune funzioni di riconoscimento vocale sono disponibili solo per determinate lingue e solo con alcune interfacce. Per ulteriori informazioni, vedi il [Riepilogo dei parametri](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   L'interfaccia di personalizzazione del modello di lingua è generalmente disponibile per tutte le lingue. L'interfaccia di personalizzazione del modello acustico è disponibile come funzionalità beta per tutte le lingue. Per ulteriori informazioni, vedi [Supporto delle lingue per la personalizzazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).

## Prova il servizio
{: #tryOut}

Per esempi del servizio {{site.data.keyword.speechtotextshort}} in azione, vedi

-   Una [demo rapida](https://speech-to-text-demo.ng.bluemix.net/){: external} che trascrive il testo dall'immissione audio in streaming o da un file che carichi. 
-   Applicazioni nei {{site.data.keyword.ibmwatson}} [Kit starter](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} che mostrano il servizio. 
-   Il post del blog {{site.data.keyword.watson}} [Getting robots to listen: Using {{site.data.keyword.watson}}'s {{site.data.keyword.speechtotextshort}} service](https://www.ibm.com/blogs/watson/2016/07/getting-robots-listen-using-watsons-speech-text-service/){: external} che mostra come utilizzare l'interfaccia WebSocket del servizio con Python per estrarre il discorso dall'audio. Il post fornisce un'esercitazione approfondita che descrive il codice e i passi coinvolti.
