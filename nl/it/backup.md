---

copyright:
  years: 2019
lastupdated: "2019-06-22"

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

# Backup e ripristino
{: #backup}

Per eseguire il ripristino da potenziali perdite di dati, devi eseguire il backup ed essere preparato a ripristinare {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. Sei responsabile della comprensione della configurazione, della personalizzazione e dell'utilizzo del servizio. Sei anche responsabile di essere pronto a ricreare un'istanza del servizio e ripristinare i tuoi dati.
{: shortdesc}

Il ripristino di emergenza può diventare un problema se nella tua soluzione cloud si verifica un guasto significativo che include la potenziale perdita di dati. Nel caso di perdita di dati, devi ripristinare i tuoi dati per riportare l'istanza del servizio al suo stato più recente. 

Per il servizio {{site.data.keyword.speechtotextshort}}, i dati per i modelli di lingua personalizzati, i modelli acustici personalizzati e le richieste di riconoscimento vocale asincrone vengono archiviati nel cloud. Il tuo piano di ripristino di emergenza include la conoscenza, la conservazione e la preparazione per il ripristino di questi dati.

La ricreazione dei modelli personalizzati, in particolare dei modelli acustici personalizzati, dai dati salvati può richiedere molto tempo. Mantenere le configurazioni dei servizi parallele può eliminare il tempo di risposta associato al ripristino di emergenza.
{: note}

### Ripristino di emergenza per i modelli di lingua personalizzati
{: #disaster-recovery-language}

Per i modelli di lingua personalizzati, devi conservare ed essere pronto a ricreare e ripristinare i tuoi modelli e i relativi corpora, grammatiche e parole personalizzate. Devi anche essere pronto a riaddestrare i tuoi modelli di lingua personalizzati sulle loro risorse di dati e parole.

#### Backup dei modelli di lingua personalizzati
{: #disaster-recovery-language-backup}

Conserva le seguenti informazioni sui tuoi modelli di lingua personalizzati:

-   Un elenco di tutti i tuoi modelli di lingua personalizzati e le relative definizioni. Per elencare le informazioni sui tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/customizations` per elencare le informazioni su tutti i modelli personalizzati.
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}` per elencare le informazioni su un modello personalizzato specificato.

    Per ulteriori informazioni, vedi [Elenco dei modelli di lingua personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).
-   Copie di tutti i file di testo di corpus che aggiungi ai tuoi modelli di lingua personalizzati. Per elencare le informazioni sui corpora per i tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/corpora` per elencare tutti i corpora per un modello personalizzato.
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` per elencare le informazioni su un corpus specificato per un modello personalizzato.

    Per ulteriori informazioni, vedi [Elenco dei corpora per un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).
-   Copie di tutti i file grammatica che aggiungi ai tuoi modelli di lingua personalizzati. Per elencare le informazioni sulle grammatiche per i tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/grammars` per elencare le informazioni su tutte le grammatiche per un modello personalizzato.
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/grammars/{grammar_name}` per elencare le informazioni su una grammatica specificata per un modello personalizzato.

    Per ulteriori informazioni, vedi [Elenco delle grammatiche per un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageGrammars#listGrammars).
-   Informazioni su tutte le parole personalizzate, incluse le loro definizioni di suono simile (sounds-like) e di modalità di visualizzazione (display-as), che aggiungi direttamente ai tuoi modelli di lingua personalizzati. Per elencare le informazioni sulle parole OOV (out-of-vocabulary) per i tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/words` per elencare le informazioni sulle parole da un modello personalizzato. Puoi utilizzare il parametro `word_type` per elencare tutte (`all`) le parole da un modello, le parole aggiunte direttamente dall'utente (`user`), le parole estratte dai `corpora` o le parole riconosciute dalle grammatiche (`grammars`).
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/words/{word_name}` per elencare le informazioni su una parola specificata da un modello personalizzato.

    Per ulteriori informazioni, vedi [Elenco delle parole da un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).

È consigliabile conservare queste informazioni in un formato che puoi utilizzare per ricreare i tuoi modelli di lingua personalizzati in caso di guasto. Conservare in modo attivo le informazioni sui tuoi modelli personalizzati e i loro dati e preparare in anticipo le chiamate elencate nella seguente sezione, può permetterti di eseguire un ripristino il più rapidamente possibile.

#### Ripristino dei modelli di lingua personalizzati
{: #disaster-recovery-language-restore}

Se hai bisogno di eseguire un ripristino di emergenza, puoi utilizzare le informazioni di backup per ricreare i tuoi modelli di lingua personalizzati e i relativi dati:

1.  Per ricreare i tuoi modelli di lingua personalizzati, utilizza il metodo `POST /v1/customizations`. Per ulteriori informazioni, vedi [Crea un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language).
1.  Per aggiungere i file di testo di corpus ai tuoi modelli personalizzati, utilizza il metodo `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`. Per ulteriori informazioni, vedi [Aggiungi un corpus al modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addCorpus).
1.  Per aggiungere i file di grammatica ai tuoi modelli personalizzati, utilizza il metodo `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`. Per ulteriori informazioni, vedi [Aggiungi una grammatica al modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
1.  Per aggiungere più parole ai tuoi modelli personalizzati, utilizza il metodo `POST /v1/customizations/{customization_id}/words`. Per aggiungere singole parole ai tuoi modelli personalizzati, utilizza il metodo `PUT /v1/customizations/{customization_id}/words/{word_name}`. Per ulteriori informazioni, vedi [Aggiungi parole al modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addWords).
1.  Per addestrare i tuoi modelli personalizzati una volta ripristinati i corpora, le grammatiche e le parole personalizzate, utilizza il metodo `POST /v1/customizations/{customization_id}/train`. Per ulteriori informazioni, vedi [Addestra il modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language).

I metodi che utilizzi per aggiungere corpora, grammatiche e parole personalizzate e per addestrare un modello di lingua personalizzato sono asincroni. Devi monitorare le richieste fino al loro completamento.

Puoi aggiungere i dati e addestrare i tuoi modelli di lingua personalizzati in modo incrementale anziché aggiungere tutti i dati prima di addestrare i modelli. Ad esempio, puoi aggiungere i tuoi corpora e quindi addestrare i modelli prima di aggiungere le grammatiche e le singole parole. Puoi anche aggiungere e addestrare in modo incrementale i tuoi modelli su singoli file di testo di corpus, file di grammatica e gruppi di parole personalizzate.

### Ripristino di emergenza per i modelli acustici personalizzati
{: #disaster-recovery-acoustic}

Per i modelli acustici personalizzati, devi conservare ed essere pronto a ricreare e ripristinare i tuoi modelli acustici personalizzati e le relative risorse audio. Devi anche essere pronto a riaddestrare i tuoi modelli acustici personalizzati sulle loro risorse audio.

#### Backup dei modelli acustici personalizzati
{: #disaster-recovery-acoustic-backup}

Conserva le seguenti informazioni sui tuoi modelli acustici personalizzati:

-   Un elenco di tutti i tuoi modelli acustici personalizzati e le relative definizioni. Per elencare le informazioni sui tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/acoustic_customizations` per elencare le informazioni su tutti i modelli personalizzati.
    -   Utilizza il metodo `GET /v1/acoustic_customizations/{customization_id}` per elencare le informazioni su un modello personalizzato specificato.

    Per ulteriori informazioni, vedi [Elenco dei modelli acustici personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic).
-   Copie di tutte le risorse audio, sia i singoli file audio che i file di archivio, che aggiungi ai tuoi modelli acustici personalizzati. Per elencare le informazioni sulle risorse audio per i tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/acoustic_customizations/{customization_id}/audio` per elencare le informazioni su tutte le risorse audio per un modello personalizzato.
    -   Utilizza il metodo `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` per elencare le informazioni su una risorsa audio specificata per un modello personalizzato.

    Per ulteriori informazioni, vedi [Elenco delle risorse audio per un modello acustico personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

È consigliabile conservare queste informazioni in un formato che puoi utilizzare per ricreare i tuoi modelli acustici personalizzati in caso di guasto. Conservare in modo attivo le informazioni sui tuoi modelli personalizzati e le loro risorse audio e preparare in anticipo le chiamate elencate nella seguente sezione, può permetterti di eseguire un ripristino il più rapidamente possibile.

#### Ripristino dei modelli acustici personalizzati
{: #disaster-recovery-acoustic-restore}

Se hai bisogno di eseguire un ripristino di emergenza, puoi utilizzare le informazioni di backup per ricreare i tuoi modelli acustici personalizzati e i relativi dati:

1.  Per ricreare i tuoi modelli acustici personalizzati, utilizza il metodo `POST /v1/acoustic_customizations`. Per ulteriori informazioni, vedi [Crea un modello acustico personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic).
1.  Per aggiungere le risorse audio ai tuoi modelli personalizzati, utilizza il metodo `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`. Per ulteriori informazioni, vedi [Aggiungi l'audio al modello acustico personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio).
1.  Per addestrare i tuoi modelli personalizzati una volta ripristinate le tue risorse audio, utilizza il metodo `POST /v1/acoustic_customizations/{customization_id}/train`. Per ulteriori informazioni, vedi [Addestra il modello acustico personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic).

I metodi che utilizzi per aggiungere le risorse audio e per addestrare un modello acustico personalizzato sono asincroni. Devi monitorare le richieste fino al loro completamento.

Puoi aggiungere le risorse audio e addestrare i tuoi modelli acustici personalizzati in modo incrementale anziché aggiungere tutti i dati prima di addestrare i modelli. Ad esempio, puoi aggiungere le risorse audio una alla volta o in gruppi, addestrando i tuoi modelli sui sottoinsiemi delle risorse audio anziché su tutto l'audio contemporaneamente.

### Ripristino di emergenza per i lavori di riconoscimento vocale asincroni
{: #disaster-recovery-async}

Per il riconoscimento vocale con l'interfaccia HTTP asincrona, devi conservare le seguenti informazioni:

-   Tutti gli URL di callback che inserisci in whitelist per l'utilizzo con l'interfaccia asincrona. Se si verifica un guasto, potresti dover utilizzare il metodo `POST /v1/register_callback` per registrare nuovamente gli URL. Il metodo restituisce una risposta appropriata se un URL è già inserito in whitelist.
-   Copie dei file audio che inoltri all'interfaccia asincrona per il riconoscimento vocale. Se si verifica un guasto prima di ricevere o richiamare i risultati di un lavoro asincrono completato, devi utilizzare il metodo `POST /v1/recognitions` per inoltrare nuovamente i file audio quando il servizio viene ripristinato. Una volta ottenuti i risultati di un lavoro asincrono completato, non hai più bisogno di conservare i file audio.

Per ulteriori informazioni, vedi [L'interfaccia HTTP asincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async). Come con i dati di backup per i modelli personalizzati, puoi conservare attivamente queste informazioni ed essere pronto a riemettere in anticipo le richieste necessarie.
