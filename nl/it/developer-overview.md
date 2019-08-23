---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-26"

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

# Panoramica per gli sviluppatori
{: #developerOverview}

Puoi accedere alle funzionalità di {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} utilizzando un'interfaccia WebSocket e usando le interfacce REST (Representational State Transfer) HTTP sincrone o asincrone. Puoi anche personalizzare i modelli di lingua del servizio per adattarli al tuo dominio e al tuo ambiente. Sono disponibili degli SDK per semplificare lo sviluppo delle applicazioni in molti linguaggi di programmazione.
{: shortdesc}

Esegui l'autenticazione al servizio {{site.data.keyword.speechtotextshort}} passando un token di accesso con ogni richiesta. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} è una soluzione cloud a più tenant. Le tue credenziali forniscono l'accesso solo ai tuoi dati e i tuoi dati sono isolati dagli altri utenti. 

## Programmazione con il servizio
{: #programming}

[Effettuazione di una richiesta di riconoscimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request) ti mostra come richiedere la trascrizione di base con ciascuna delle interfacce di programmazione del servizio:

-   [L'interfaccia WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) offre un'efficiente implementazione a bassa latenza e velocità effettiva elevata su una connessione full duplex.
-   [L'interfaccia HTTP sincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fornisce un'interfaccia di base per trascrivere l'audio con richieste bloccanti.
-   [L'interfaccia HTTP asincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fornisce un'interfaccia non bloccante che ti consente di registrare un URL di callback per ricevere le notifiche o eseguire il polling del servizio per ottenere lo stato del lavoro e i risultati.

Le interfacce forniscono funzionalità di riconoscimento vocale simili, ma potresti specificare lo stesso parametro come intestazione di richiesta, parametro di query o parametro di un oggetto JSON in base all'interfaccia che utilizzi. 

Le interfacce WebSocket e HTTP sincrona accettano un massimo di 100 MB di dati audio con una singola richiesta. L'interfaccia HTTP asincrona accetta un massimo di 1 GB di dati audio con una richiesta. 

-   Per informazioni su come effettuare le richieste con ciascuna delle interfacce {{site.data.keyword.speechtotextshort}}, vedi [Effettuazione delle richieste al servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Per degli esempi di richieste di riconoscimento vocale di base con ciascuna delle interfacce del servizio, vedi [Effettuazione di una richiesta di riconoscimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Per le descrizioni di tutti i parametri di riconoscimento vocale disponibili, vedi il [Riepilogo dei parametri](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   Per le descrizioni di tutti i metodi e dei relativi parametri, insieme ad esempi, vedi la [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Vantaggi dell'interfaccia WebSocket
{: #advantages}

L'interfaccia WebSocket presenta numerosi vantaggi rispetto all'interfaccia HTTP:

-   L'interfaccia WebSocket fornisce un canale di comunicazione full duplex a singolo socket. L'interfaccia consente al client di inviare richieste e audio al servizio e di ricevere i risultati su una singola connessione in modo asincrono.
-   Fornisce un'esperienza di programmazione molto più semplice e più potente. Il servizio invia risposte basate su eventi ai messaggi del client, eliminando la necessità per il client di eseguire il polling del server.
-   Ti consente di stabilire e utilizzare una singola connessione autenticata per un tempo illimitato. Le interfacce HTTP richiedono di autenticare ogni chiamata al servizio.
-   Riduce la latenza. I risultati del riconoscimento arrivano più velocemente perché il servizio li invia direttamente al client. L'interfaccia HTTP richiede quattro richieste e connessioni distinte per ottenere gli stessi risultati.
-   Riduce l'utilizzo della rete. Il protocollo WebSocket è leggero. Richiede solo una singola connessione per eseguire il riconoscimento vocale dinamico.
-   Consente di inviare in streaming l'audio direttamente dai browser (client WebSocket HTML5) al servizio.

## Personalizzazione del servizio
{: #customizing}

[L'interfaccia di personalizzazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) ti permette di creare modelli personalizzati per migliorare le funzionalità di riconoscimento vocale del servizio:

-   I [modelli di lingua personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate) ti consentono di definire parole specifiche per il dominio per un modello di base. I modelli di lingua personalizzati espandono il vocabolario di base del servizio con una terminologia specifica per domini come medicina e legge.
-   I [modelli acustici personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic) ti consentono di adattare un modello di base per le caratteristiche acustiche del tuo ambiente e dei tuoi parlanti. I modelli acustici personalizzati migliorano la capacità del servizio di riconoscere il discorso per specifiche caratteristiche acustiche.
-   Le [grammatiche](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) ti consentono di limitare le frasi che il servizio può riconoscere a quelle definite nelle regole della grammatica. Limitando lo spazio di ricerca per le stringhe valide, il servizio può fornire i risultati in modo più veloce e più accurato. Le grammatiche sono supportate con i modelli di lingua personalizzati.

Puoi utilizzare un modello di lingua personalizzato, un modello acustico personalizzato o entrambi per il riconoscimento vocale con qualsiasi interfaccia del servizio.

## Come ottenere le metriche
{: #overview-metrics}

Il servizio offre due tipi di metriche facoltative per le richieste di riconoscimento vocale:

-   Le [metriche di elaborazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) forniscono le informazioni di temporizzazione dettagliate relative all'analisi dell'audio di input del servizio. Il servizio restituisce le metriche agli intervalli specificati e con gli eventi di trascrizioni, ad esempio i risultati provvisori e finali. Puoi utilizzare le metriche per misurare l'avanzamento del servizio nella trascrizione dell'audio. 
-   Le [metriche audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) forniscono le informazioni dettagliate sulle caratteristiche di segnale dell'audio di input. I risultati forniscono le metriche aggregate per l'intero audio di input alla conclusione dell'elaborazione del discorso. Puoi utilizzare le metriche per determinare le caratteristiche e la qualità dell'audio.

Puoi richiedere le metriche di elaborazione con le interfacce WebSocket e HTTP asincrona. Puoi richiedere le metriche audio con una qualsiasi delle interfacce del servizio. Per impostazione predefinita, il servizio non restituisce metriche. 

## Supporto CORS
{: #cors}

Il servizio supporta CORS (Cross-Origin Resource Sharing). Utilizzando CORS, le pagine web possono richiedere le risorse direttamente da un dominio esterno. CORS aggira la politica di sicurezza della stessa origine, che altrimenti impedisce tali richieste. Poiché il servizio supporta CORS, una pagina web può comunicare direttamente con il servizio senza passare la richiesta attraverso il server web che ospita la pagina.

Ad esempio, una pagina web caricata da un server in {{site.data.keyword.cloud}} può chiamare direttamente l'API di personalizzazione, ignorando il server {{site.data.keyword.cloud_notm}}. Per ulteriori informazioni, vedi [enable-cors.org](https://enable-cors.org/){: external}.

## Utilizzo di SDK (Software Development Kit)
{: #sdks}

Gli SDK sono disponibili per il servizio {{site.data.keyword.speechtotextshort}} per semplificare lo sviluppo di applicazioni di riconoscimento vocale. Gli SDK {{site.data.keyword.ibmwatson}} sono disponibili per molti linguaggi di programmazione e piattaforme comuni.

-   Per un elenco completo di SDK e link agli SDK su GitHub, vedi [Utilizzo di SDK](/docs/services/watson?topic=watson-using-sdks).
-   Per informazioni dettagliate su tutti i metodi degli SDK Node, Java&trade;, Python, Ruby e Go per il servizio {{site.data.keyword.speechtotextshort}}, vedi la [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
