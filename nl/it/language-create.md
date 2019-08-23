---

copyright:
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

# Creazione di un modello di lingua personalizzato
{: #languageCreate}

Attieniti alla seguente procedura per creare un modello di lingua personalizzato per {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}:
{: shortdesc}

1.  [Crea un modello di lingua personalizzato](#createModel-language). Puoi creare più modelli personalizzati per lo stesso dominio o per domini differenti. Il processo è lo stesso per qualsiasi modello che crei. Puoi tuttavia specificare solo un singolo modello personalizzato per volta con una richiesta di riconoscimento.
1.  [Aggiungi un corpus al modello di lingua personalizzato](#addCorpus). Un corpus è un documento di testo semplice che utilizza la terminologia dal dominio in contesto. Il servizio crea un vocabolario per un modello personalizzato estraendo i termini dai corpora che non esistono nel suo vocabolario di base. Puoi aggiungere più corpora a un modello personalizzato.
1.  [Aggiungi parole a un modello di lingua personalizzato](#addWords). Puoi anche aggiungere parole personalizzate a un modello singolarmente. Puoi inoltre utilizzare gli stessi metodi per modificare le parole personalizzate estratte dai corpora. I metodi ti consentono di specificare la pronuncia delle parole e il modo in cui le parole vengono visualizzate in una trascrizione vocale.
1.  [Addestra il modello di lingua personalizzato](#trainModel-language). Una volta che hai aggiunto le parole al modello personalizzato, devi addestrare il modello sulle parole. L'addestramento prepara il modello personalizzato per l'utilizzo nel riconoscimento vocale. Il modello non utilizza parole nuove o modificate fino a che non lo addestri.
1.  Dopo aver addestrato il tuo modello personalizzato, puoi utilizzarlo con le richieste di riconoscimento. Se l'audio passato per le trascrizioni contiene delle parole specifiche per il dominio che sono definite nel modello personalizzato, i risultati della richiesta riflettono il vocabolario migliorato del modello. Per ulteriori informazioni, vedi [Utilizzo di un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse).

La procedura per creare un modello di lingua personalizzato è iterativa. Puoi aggiungere corpora e parole e addestrare o riaddestrare un modello tutte le volte che lo ritieni necessario.

Puoi anche aggiungere grammatiche a un modello di lingua personalizzato. Le grammatiche limitano la risposta del servizio alle sole parole da esse riconosciute. Per ulteriori informazioni, vedi [Utilizzo di grammatiche con i modelli di lingua personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars).

La personalizzazione del modello di lingua è disponibile per la maggior parte delle lingue. Per ulteriori informazioni, vedi [Supporto delle lingue per la personalizzazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
{: note}

## Crea un modello di lingua personalizzato
{: #createModel-language}

Utilizzi il metodo `POST /v1/customizations` per creare un nuovo modello di lingua personalizzato. Puoi creare qualsiasi numero di modelli di lingua personalizzati ma puoi utilizzare solo un singolo modello per volta con una richiesta di riconoscimento vocale. Il metodo accetta un oggetto JSON che definisce gli attributi del nuovo modello personalizzato come corpo della richiesta.

<table>
  <caption>Tabella 1. Attributi di un nuovo modello di lingua personalizzato</caption>
  <tr>
    <th style="width:20%; text-align:left">Parametro</th>
    <th style="width:12%; text-align:center">Tipo di dati</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>      Obbligatorio
    </em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Un nome definito dall'utente per il nuovo modello personalizzato. Utilizza un nome che
      descrive il dominio del modello personalizzato, come ad esempio <code>Medical
        custom model</code> o <code>Legal custom model</code>. Utilizza un
      nome che sia univoco tra tutti i modelli di lingua personalizzati di tua proprietà.
      Utilizza un nome localizzato che corrisponda alla lingua del modello personalizzato.
    </td>
  </tr>
  <tr>
    <td><code>base_model_name</code><br/><em>      Obbligatorio
    </em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Il nome del modello di lingua che deve essere personalizzato dal
      nuovo modello personalizzato. Specifica uno dei modelli di lingua supportati
      di cui esegue la restituzione il metodo <code>GET /v1/models</code>. Il nuovo
      modello può essere utilizzato solo con il modello di base che personalizza.
    </td>
  </tr>
  <tr>
    <td><code>dialect</code><br/><em>      Facoltativo
    </em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Il dialetto della lingua specificata che deve essere utilizzato con il
      modello personalizzato. Per impostazione predefinita, il dialetto corrisponde alla lingua del
      modello di base; ad esempio, il dialetto è <code>en-US</code>
      per entrambi i modelli di lingua inglese (Stati Uniti),
      <code>en-US_BroadbandModel</code> o
      <code>en-US_NarrowbandModel</code>.<br/></br>
      Il parametro è significativo solo per i modelli in spagnolo, per cui
      il servizio crea un modello personalizzato adatto per un discorso nel
      dialetto indicato:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-ES</code> per lo spagnolo castigliano (il valore predefinito)
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-LA</code> per lo spagnolo dell'America Latina
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-US</code> per lo spagnolo del Nord America (messicano)
        </li>
      </ul>
      Se specifichi un dialetto, deve essere valido per il modello di base.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>      Facoltativo
    </em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Una descrizione del nuovo modello. Utilizza una descrizione localizzata che
      corrisponda alla lingua del modello personalizzato.
    </td>
  </tr>
</table>

Il seguente esempio crea un nuovo modello di lingua personalizzato denominato `Example model`. Il modello viene creato per il modello di base `en-US-BroadbandModel` e ha la descrizione `Example custom language model`. L'intestazione `Content-Type` specifica che al metodo si stanno passando dei dati JSON.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/json"
--data "{\"name\": \"Example model\",
  \"base_model_name\": \"en-US_BroadbandModel\",
  \"description\": \"Example custom language model\"}"
"{url}/v1/customizations"
```
{: pre}

L'esempio restituisce l'ID di personalizzazione del nuovo modello. Ogni modello personalizzato è identificato da un ID di personalizzazione univoco, che è un GUID (Globally Unique Identifier). Specifichi il GUID di un modello personalizzato con il parametro `customization_id` delle chiamate associate al modello.

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96"
}
```
{: codeblock}

Il nuovo modello personalizzato è di proprietà dell'istanza del servizio di cui vengono utilizzate le credenziali per crearlo. Per ulteriori informazioni, vedi [Proprietà di modelli personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#customOwner).

## Aggiungi un corpus al modello di lingua personalizzato
{: #addCorpus}

Dopo che hai creato il tuo modello di lingua personalizzato, il passo successivo consiste nell'aggiungere dati (parole specifiche per il dominio) al modello. Il metodo consigliato per popolare un modello personalizzato con nuove parole consiste nell'aggiungere uno o più corpora.

Un corpus è un file di testo semplice che idealmente contiene frasi di esempio dal tuo dominio. Il servizio analizza il contenuto di un file di corpus ed estrae le parole che non sono presenti nel suo vocabolario di base. Tali parole sono indicate come parole OOV (out-of-vocabulary).

-   Per ulteriori informazioni sull'utilizzo dei corpora, vedi [Utilizzo dei corpora](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingCorpora).
-   Per ulteriori informazioni su come il servizio aggiunge i corpora a un modello, vedi [Cosa succede quando aggiungo un file di corpus?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseCorpus)

Fornendo frasi che includono nuove parole, i corpora consentono al servizio di imparare le parole in contesto. Puoi quindi aumentare o modificare le parole del modello singolarmente. Addestrare un modello solo su singole parole invece che sulle parole aggiunte dai corpora è più dispendioso in termini di tempo e può produrre risultati meno efficaci.
{: tip}

Utilizzi il metodo `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` per aggiungere un corpus a un modello personalizzato:

-   Specifica l'ID di personalizzazione del modello personalizzato con il parametro di percorso `customization_id`.
-   Specifica un nome per il corpus con il parametro di percorso `corpus_name`. Utilizza un nome localizzato che corrisponda alla lingua del modello personalizzato e riflette il contenuto del corpus.
    -   Includi un massimo di 128 caratteri nel nome.
    -   Non utilizzare i caratteri che devono essere codificati in URL. Ad esempio, non utilizzare spazi, barre, barre rovesciate, due punti, e commerciale, virgolette, segni più, segni uguale, punti interrogativi e così via nel nome. (Il servizio non impedisce l'utilizzo di questi caratteri. Ma poiché devono essere codificati in URL ovunque vengano utilizzati, ti sconsigliamo vivamente di utilizzarli). 
    -   Non utilizzare il nome di un corpus o di una grammatica che è già stato aggiunto al modello personalizzato. 
    -   Non utilizzare il nome `user`, che è riservato dal servizio per denotare le parole personalizzate aggiunte o modificate dall'utente.
    -   Non utilizzare il nome `base_lm` o `default_lm`. Entrambi i nomi sono riservati per essere utilizzati in futuro dal servizio. 
-   Passa il file di testo di corpus come corpo della richiesta.

Puoi aggiungere un massimo di 90.000 parole OOV e 10 milioni di parole in totale da tutte le origini combinate. Questo include le parole da corpora e grammatiche e le parole che aggiungi direttamente. Per ulteriori informazioni, vedi [Di quanti dati ho bisogno?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#wordsResourceAmount)
{: note}

Il seguente esempio aggiunge il file di testo di corpus `healthcare.txt` al modello personalizzato con l'ID specificato. L'esempio denomina il corpus `healthcare`.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--data-binary @healthcare.txt
"{url}/v1/customizations/{customization_id}/corpora/healthcare"
```
{: pre}

Il metodo accetta anche un parametro di query `allow_overwrite` facoltativo che sovrascrive un corpus esistente per un modello personalizzato. Utilizza il parametro se devi aggiornare un file di corpus dopo averlo aggiunto a un modello.

Il metodo è asincrono. Il suo completamento può richiedere uno o due minuti. La durata dell'operazione dipende dal numero totale di parole nel corpus, dal numero di nuove parole che il servizio trova nel corpus e dal carico corrente sul servizio. Per ulteriori informazioni sul controllo dello stato di un corpus, vedi [Monitoraggio della richiesta di aggiunta del corpus](#monitorCorpus).

Puoi aggiungere qualsiasi numero di corpora a un modello personalizzato richiamando il metodo una volta per ciascun file di testo di corpus. L'aggiunta di un corpus deve essere del tutto completa prima di poterne aggiungere un altro. Dopo che hai aggiunto un corpus a un modello personalizzato, esamina le nuove parole personalizzate per controllare l'eventuale presenza di errori di battitura e di altro tipo. Per ulteriori informazioni, vedi [Convalida di una risorsa di parole](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).

### Monitoraggio della richiesta di aggiunta del corpus
{: #monitorCorpus}

Il servizio restituisce un codice di risposta 201 se il corpus è valido. Elabora quindi in modo asincrono il contenuto del corpus ed estrae automaticamente le nuove parole. Non puoi inoltrare le richieste di aggiunta di dati al modello personalizzato o di addestramento del modello fino al completamento dell'analisi del corpus da parte del servizio per la richiesta corrente.

Per determinare lo stato dell'analisi, utilizza il metodo `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` per eseguire il polling dello stato del corpus. Il metodo accetta l'ID del modello e il nome del corpus, come mostrato nel seguente esempio:

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/corpora/corpus1"
```
{: pre}

La risposta include lo stato del corpus:

```javascript
{
  "name": "corpus1",
  "total_words": 5037,
  "out_of_vocabulary_words": 401,
  "status": "analyzed"
}
```
{: codeblock}

Il campo `status` ha uno dei seguenti valori:

-   `analyzed` indica che il servizio ha eseguito correttamente l'analisi del corpus.
-   `being_processed` indica che il servizio sta ancora analizzando il corpus.
-   `undetermined` indica che il servizio ha riscontrato un errore durante l'elaborazione del corpus.

Utilizza un loop per controllare lo stato del corpus ogni 10 secondi fino a quando non diventa `analyzed`. Per ulteriori informazioni sul controllo dello stato dei corpora di un modello, vedi [Elenco dei corpora per un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).

## Aggiungi parole al modello di lingua personalizzato
{: #addWords}

Anche se l'aggiunta di corpora è il metodo consigliato per aggiungere parole a un modello di lingua personalizzato, puoi anche aggiungere delle singole parole personalizzate al modello direttamente. Il servizio aggiunge le parole personalizzate al modello personalizzato proprio come fa con le parole OOV che rileva dai corpora.

Se hai solo una o poche parole da aggiungere a un modello, utilizzare i corpora per aggiungere le parole potrebbe non essere pratico o neanche fattibile. L'approccio più semplice consiste nell'aggiungere una parola con solo la sua ortografia. Puoi però anche fornire più pronunce per la parola e indicare come deve essere visualizzata la parola.

-   Per ulteriori informazioni sull'aggiunta di parole direttamente, vedi [Utilizzo delle parole personalizzate](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingWords).
-   Per ulteriori informazioni su come il servizio aggiunge parole personalizzate a un modello, vedi [Cosa succede quando aggiungo o modifico una parola personalizzata?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseWord)

Puoi utilizzare i seguenti metodi per aggiungere parole a un modello personalizzato:

-   Il metodo `POST /v1/customizations/{customization_id}/words` aggiunge più parole per volta. Passi un oggetto JSON che fornisce informazioni su ciascuna parola tramite il corpo della richiesta. Il seguente esempio aggiunge due parole personalizzate, `HHonors` e `IEEE`, al modello personalizzato con l'ID specificato. L'intestazione `Content-Type` specifica che al metodo si stanno passando dei dati JSON.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data "{\"words\": [
      {\"word\": \"HHonors\", \"sounds_like\": [\"hilton honors\", \"H. honors\"], \"display_as\": \"HHonors\"},
      {\"word\": \"IEEE\", \"sounds_like\": [\"I. triple E.\"]}]}"
    "{url}/v1/customizations/{customization_id}/words"
    ```
    {: pre}

    Puoi anche aggiungere le parole da un file. Ad esempio, il file `words.json` definisce le stesse due parole personalizzate.

    ```
    {"words":
      [
        {"word": "HHonors", "sounds_like": ["hilton honors", "H. honors"], "display_as": "HHonors"},
        {"word": "IEEE", "sounds_like": ["I. triple E."]}
      ]
    }
    ```
    {: codeblock}

    Il seguente comando aggiunge le parole dal file:

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data-binary @words.json
    "{url}/v1/customizations/{customization_id}/words"
    ```
    {: pre}

    Questo metodo è asincrono. Il tempo che ci vuole per completare l'operazione dipende dal numero di parole che aggiungi e dal carico corrente sul servizio. Per ulteriori informazioni sul controllo dello stato dell'operazione, vedi [Monitoraggio della richiesta di aggiunta di parole](#monitorWords).
-   Il metodo `PUT /v1/customizations/{customization_id}/words/{word_name}` aggiunge singole parole. Passi un oggetto JSON che fornisce le informazioni sulla parola. Il seguente esempio aggiunge la parola `NCAA` al modello con l'ID specificato. Ancora, l'intestazione `Content-Type` indica che si stanno passando dei dati JSON al metodo.

    ```bash
    curl -X PUT
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data "{\"sounds_like\": [\"N. C. A. A.\", \"N. C. double A.\"]}"
    "{url}/v1/customizations/{customization_id}/words/NCAA"
    ```
    {: pre}

    Questo metodo è sincrono. Il servizio restituisce un codice di risposta che notifica l'esito positivo o negativo della richiesta immediatamente.

Come con l'aggiunta di corpora, esamina le nuove parole personalizzate per controllare l'eventuale presenza di errori di battitura e di altro tipo. Questo controllo è particolarmente importante quando aggiungi più parole contemporaneamente. Per ulteriori informazioni, vedi [Convalida di una risorsa di parole](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).

### Monitoraggio della richiesta di aggiunta di parole
{: #monitorWords}

Quando utilizzi il metodo `POST /v1/customizations/{customization_id}/words`, il servizio restituisce un codice di risposta 201 se i dati di input non sono validi. Elabora quindi in modo asincrono le parole per aggiungerle al modello. L'operazione è generalmente più veloce dell'aggiunta di un corpus o dell'addestramento di un modello ma la sua durata dipende dal numero di nuove parole aggiunte e dal carico corrente sul servizio. Non puoi inoltrare richieste di aggiunta di dati al modello personalizzato o di addestramento del modello fino a quando il servizio non completa la richiesta di aggiunta di nuove parole.

Per determinare lo stato della richiesta, utilizza il metodo `GET /v1/customizations/{customization_id}` per eseguire il polling dello stato del modello. Il metodo accetta l'ID di personalizzazione del modello e restituisce le informazioni che includono lo stato del modello, come nel seguente esempio:

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
  "created": "2016-06-01T18:42:25.324Z",
  "updated": "2016-06-01T18:45:11.737Z",
  "language": "en-US",
  "dialect": "en-US",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model",
  "description": "Example custom language model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "pending",
  "progress": 0
}
```
{: codeblock}

Il campo `status` notifica lo stato corrente del modello. Mentre il servizio sta elaborando le nuove parole, lo stato rimane `pending`. Utilizza un loop per controllare lo stato ogni 10 secondi finché non diventa `ready` per indicare che l'operazione è stata completata. Per ulteriori informazioni sui possibili valori di `status`, vedi [Monitoraggio della richiesta di addestramento del modello](#monitorTraining-language).

### Modifica di parole in un modello personalizzato
{: #modifyWord}

Puoi anche utilizzare i metodi `POST /v1/customizations/{customization_id}/words` e `PUT /v1/customizations/{customization_id}/words/{word_name}` per modificare o aumentare una parola in un modello personalizzato. Potresti dover utilizzare i metodi per correggere un errore di battitura oppure un altro errore che era stato fatto quando una parola è stata aggiunta al modello. Potresti anche dover aggiungere delle definizioni di suono simile (sounds-like) per una parola esistente.

Utilizzi i metodi per modificare la definizione di una parola esistente esattamente come fai per aggiungere una parola. I nuovi dati che fornisci per la parola sovrascrivono la definizione esistente della parola.

## Addestra il modello di lingua personalizzato
{: #trainModel-language}

Dopo che hai popolato un modello di lingua personalizzato con nuove parole (aggiungendo corpora e grammatiche oppure direttamente le parole), devi addestrare il modello sui nuovi dati. L'addestramento prepara il modello personalizzato a utilizzare i dati nel riconoscimento vocale. Il modello non utilizza le parole che aggiungi servendoti di un qualsiasi metodo finché non ne esegui l'addestramento sui dati.

Utilizzi il metodo `POST /v1/customizations/{customization_id}/train` per addestrare un modello personalizzato. Passi al metodo l'ID di personalizzazione del modello che vuoi addestrare, come nel seguente esempio:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/train"
```
{: pre}

Il metodo è asincrono. Il completamento dell'addestramento può richiedere qualche minuto, a seconda del numero di nuove parole su cui si sta eseguendo l'addestramento del modello e del carico corrente sul servizio. Per ulteriori informazioni sul controllo dello stato di un'operazione di addestramento, vedi [Monitoraggio della richiesta di addestramento del modello](#monitorTraining-language).

Il metodo include i seguenti parametri di query facoltativi:

-   Il parametro `word_type_to_add` specifica le parole su cui deve essere addestrato il modello personalizzato: 
    -   Specifica `all` oppure ometti il parametro per addestrare il modello su tutte le sue parole, indipendentemente dalla loro origine.
    -   Specifica `user` per addestrare il modello solo sulle parole che erano state aggiunte o modificate dall'utente, ignorando quelle estratte solo da corpora o grammatiche.

    Questa opzione è utile se aggiungi dei corpora con dati che contengono informazioni extra senza senso, come ad esempio delle parole che contengono errori di battitura. Prima di addestrare il modello su tali dati, puoi utilizzare il parametro di query `word_type` del metodo `GET /v1/customizations/{customization_id}/words` per esaminare le parole estratte da corpora e grammatiche. Per ulteriori informazioni, vedi [Elenco delle parole da un modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).
-   Il parametro `customization_weight` specifica il peso relativo che viene dato alle parole dal modello personalizzato invece che alle parole dal vocabolario di base quando il modello personalizzato viene utilizzato per il riconoscimento vocale. Puoi anche specificare un peso di personalizzazione con qualsiasi richiesta di riconoscimento che utilizza il modello personalizzato. Per ulteriori informazioni, vedi [Utilizzo del peso di personalizzazione](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse#weight).
-   Il parametro `strict` indica se l'addestramento deve proseguire se il modello personalizzato contiene una combinazione di risorse valide e non valide (corpora, grammatiche e parole). Per impostazione predefinita, l'addestramento ha esito negativo se il modello contiene una o più risorse non valide. Imposta il parametro su `false` per consentire il proseguimento dell'addestramento fino a quando il modello contiene almeno una risorsa valida. Il servizio esclude le risorse non valide dall'addestramento. Per ulteriori informazioni, vedi [Errori di addestramento](#failedTraining-language).

### Monitoraggio della richiesta di addestramento del modello
{: #monitorTraining-language}

Il servizio restituisce un codice di risposta 200 se inizia il processo di addestramento con esito positivo. Il servizio non può accettare richieste di addestramento successive, o richieste di aggiunta di nuovi corpora, grammatiche o parole, fino a quando la richiesta esistente non viene completata.

Per determinare lo stato di una richiesta di addestramento, utilizza il metodo `GET /v1/customizations/{customization_id}` per eseguire il polling dello stato del modello. Il metodo accetta l'ID di personalizzazione del modello e restituisce le informazioni relative al modello.

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
  "created": "2016-06-01T18:42:25.324Z",
  "updated": "2016-06-01T18:45:11.737Z",
  "language": "en-US",
  "dialect": "en-US",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model",
  "description": "Example custom language model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "training",
  "progress": 0
}
```
{: codeblock}

La risposta include i campi `status` e `progress` che notificano lo stato del modello personalizzato. Il significato del campo `progress` dipende dallo stato del modello. Il campo `status` può avere uno dei seguenti valori:

-   `pending` indica che il modello è stato creato ma che sta attendendo che vengano aggiunti i dati di addestramento validi o che il servizio termini l'analisi dei dati che erano stati aggiunti. Il campo `progress` è `0`.
-   `ready` indica che il modello contiene dati validi ed è pronto per essere addestrato. Il campo `progress` è `0`.

    Se il modello contiene una combinazione di risorse valide e non valide (ad esempio, sia parole personalizzate valide che non valide), l'addestramento del modello avrà esito negativo a meno che non imposti il parametro di query `strict` su `false`. Per ulteriori informazioni, vedi [Errori di addestramento](#failedTraining-language).
-   `training` indica che il modello è in fase di addestramento. Il campo `progress` cambia da `0` a `100` al termine dell'addestramento. <!-- The `progress` field indicates the progress of the training as a percentage complete. -->
-   `available` indica che il modello è addestrato e pronto per l'uso. Il campo `progress` è `100`.
-   `upgrading` indica che il modello è in fase di upgrade. Il campo `progress` è `0`.
-   `failed` indica che l'addestramento del modello non è riuscito. Il campo `progress` è `0`. Per ulteriori informazioni, vedi [Errori di addestramento](#failedTraining-language).

Utilizza un loop per controllare lo stato ogni 10 secondi fino a quando non diventa `available`. Per ulteriori informazioni sul controllo dello stato di un modello personalizzato, vedi [Elenco dei modelli di lingua personalizzati](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).

### Errori di addestramento
{: #failedTraining-language}

L'addestramento non viene avviato se il servizio sta gestendo un'altra richiesta per il modello di lingua personalizzato. Ad esempio, l'avvio di una richiesta di addestramento non riesce con un codice di stato 409 se il servizio sta 

-   Elaborando un corpus o una grammatica per generare un elenco di parole OOV
-   Elaborando parole personalizzate per convalidare o generare automaticamente pronunce dal suono simile (sounds-like)
-   Gestendo un'altra richiesta di addestramento

Inoltre, l'avvio dell'addestramento non riesce con un codice di stato 400 se il modello personalizzato

-   Non contiene nuovi dati di addestramento validi (corpora, grammatiche o parole) da quando è stato creato o da quando ne è stato eseguito l'addestramento l'ultima volta 
-   Contiene uno o più corpora, grammatiche o parole non validi (ad esempio, una parola personalizzata ha una pronuncia dal suono simile non valida)

Se la richiesta di addestramento non riesce con un codice di stato 400, il servizio imposta lo stato del modello personalizzato su `failed`. Esegui una delle seguenti operazioni: 

-   Utilizza i metodi dell'interfaccia personalizzata per esaminare le risorse del modello e correggere eventuali errori che rilevi: 
    -   Per un corpus non valido, puoi correggere il file di testo del corpus e utilizzare il parametro `allow_overwrite` del metodo `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` per aggiungere il file corretto al modello. Per ulteriori informazioni, vedi [Aggiungi un corpus al modello di lingua personalizzato](#addCorpus).
    -   Per una grammatica non valida, puoi correggere il file di grammatica e utilizzare il parametro `allow_overwrite` del metodo `POST /v1/customizations/{customization_id}/grammars/{grammar_name}` per aggiungere il file corretto al modello. Per ulteriori informazioni, vedi [Aggiungi una grammatica al modello di lingua personalizzato](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
    -   Per una parola personalizzata non valida, puoi utilizzare i metodi `POST /v1/customizations/{customization_id}/words` o `PUT /v1/customizations/{customization_id}/words/{word_name}` per modificare la parola direttamente nella risorsa di parole del modello. Per ulteriori informazioni, vedi [Modifica di parole in un modello personalizzato](#modifyWord).

    Per ulteriori informazioni sulla convalida delle parole in un modello di lingua personalizzato, vedi [Convalida di una risorsa di parole](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).
-   Imposta il parametro `strict` del metodo `POST /v1/customizations/{customization_id}/train` su `false` per escludere le risorse non valide dall'addestramento. Il modello deve contenere almeno una risorsa valida (corpus, grammatica o parola) per consentire l'addestramento. Il parametro `strict` è utile per l'addestramento di un modello personalizzato che contiene una combinazione di risorse valide e non valide. 
