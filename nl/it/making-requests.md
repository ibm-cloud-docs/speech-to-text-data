---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

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

# Effettuazione delle richieste al servizio
{: #making-requests}

Per effettuare richieste autenticate a {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}, esegui il provisioning di un'istanza del servizio e ottieni le credenziali. Utilizza un URL diverso per le interfacce HTTP e WebSocket del servizio. Se utilizzi un certificato autofirmato, devi disabilitare la verifica SSL per le richieste al servizio.
{: shortdesc}

## Provisioning di un'istanza e ottenimento delle credenziali
{: #making-requests-provisioning}

Prima di utilizzare il servizio {{site.data.keyword.speechtotextshort}}, devi eseguire il provisioning di un'istanza del servizio e ottenere le tue credenziali. Per ulteriori informazioni, vedi [Prima di cominciare](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#before-you-begin). Nell'ultimo passo di tale procedura, copia `{token}` e `{URL}` per la tua istanza del servizio:

-   `{token}` fornisce il tuo token di accesso per l'autenticazione al servizio. Puoi utilizzare il token di accesso visualizzato nel client web {{site.data.keyword.icp4dfull_notm}}. Tuttavia, in un ambiente di produzione, utilizza un token che hai generato in modo programmatico per la tua istanza del servizio. Per ulteriori informazioni ed esempi, vedi la sezione *Autenticazione* nella [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data#authentication){: external}.

    Esegui l'autenticazione al servizio {{site.data.keyword.speechtotextshort}} passando il tuo token di accesso con ogni richiesta. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} è una soluzione cloud a più tenant. Le tue credenziali forniscono l'accesso solo ai tuoi dati e i tuoi dati sono isolati dagli altri utenti.
-   `{URL}` fornisce l'endpoint di base che utilizzi per chiamare i metodi del servizio.

L'URL contiene i seguenti componenti: 

```
https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api
```
{: codeblock}

I valori di variabile tra `{}` (parentesi graffe) forniscono le seguenti informazioni:

-   `{icp4d_cluster_host}` è il nome o l'indirizzo IP dell'host su cui viene distribuito il tuo cluster {{site.data.keyword.icp4dfull_notm}}.
-   `{:port}` è il numero di porta su cui il servizio ascolta le richieste sull'host specificato. Devi far precedere il numero di porta da un simbolo `:` (due punti).
-   `{release}` è il nome della release specificato quando è stato installato il grafico Helm.
-   `{instance_id}` è l'identificativo della tua istanza del servizio. 

Le parentesi graffe indicano le stringhe di variabili che devi sostituire con i valori letterali. Non includere le parentesi graffe nelle chiamate effettive al servizio.
{: note}

## Effettuazione di una richiesta HTTP autenticata
{: #httpRequest}

Il servizio {{site.data.keyword.speechtotextshort}} offre due interfacce HTTP:

-   L'[interfaccia HTTP sincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fornisce l'accesso a tutte le funzionalità del servizio, incluse le interfacce di personalizzazione. 
-   L'[interfaccia HTTP asincrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fornisce i metodi solo per il riconoscimento vocale.

Entrambe le interfacce HTTP accettano le richieste sul protocollo HTTP Secure che a sua volta si basa sul protocollo SSL (Secure Sockets Layer) (o TLS (Transport Layer Security)). Tutti gli URL per le richieste a un'interfaccia HTTP iniziano con la specifica del protocollo `https`.

Gli esempi presenti in questa documentazione utilizzano il comando `curl` per chiamare le interfacce HTTP del servizio. Per ulteriori informazioni, vedi [Utilizzo degli esempi curl](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#getting-started-curl). Il formato di base di una richiesta HTTP con `curl` include i seguenti componenti:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

I valori di variabile tra parentesi graffe forniscono le seguenti informazioni: 

-   `{http_method}` specifica il metodo di richiesta HTTP per l'esempio: `POST`, `PUT`, `GET` o `DELETE`. Il metodo di richiesta è necessario con `curl` per qualsiasi elemento diverso da `GET`.
-   `{token}` fornisce il token di accesso per la tua istanza del servizio. Devi utilizzare il token di accesso per effettuare una richiesta sicura al servizio. 
-   `{method}` è il metodo del servizio che stai chiamando. Ad esempio, utilizza il metodo `recognize` per effettuare una richiesta HTTP sincrona al servizio. 

I valori di variabile rimanenti forniscono le informazioni descritte in precedenza. Molti metodi hanno nomi più lunghi e includono parametri di percorso che devi specificare come parte della richiesta. La maggior parte degli esempi include anche intestazioni della richiesta, parametri di query e altri valori. 

Gli esempi mostrano l'URL per le chiamate alle interfacce HTTP come `{url}/v1/{method}`. Sostituisci `{url}` con i valori appena descritti.
{: note}

## Effettuazione di una richiesta WebSocket autenticata
{: #websocketRequest}

Il servizio {{site.data.keyword.speechtotextshort}} offre un'[interfaccia WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) che fornisce solo il riconoscimento vocale. Il servizio accetta le richieste sul protocollo WebSocket Secure che di nuovo si basa sul protocollo SSL (Secure Sockets Layer) (o TLS (Transport Layer Security)). Tutti gli URL per le richieste all'interfaccia WebSocket iniziano con la specifica del protocollo `wss`. 

Puoi chiamare l'interfaccia WebSocket solo dal codice dell'applicazione. Non puoi chiamare l'interfaccia WebSocket dalla riga di comando. Stabilisci una connessione WebSocket al servizio nel seguente endpoint.

```
wss://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/recognize
```
{: codeblock}

I valori di variabile forniscono le informazioni descritte in precedenza. Passa il tuo token di accesso tramite il parametro di query `access_token` del metodo.

Gli esempi mostrano l'URL per le chiamate all'interfaccia WebSocket come `{ws_url}/v1/recognize`. Sostituisci `{ws_url}` con i valori appena descritti.
{: note}

## Disabilitazione della verifica SSL
{: #SSLverification}

Tutti i servizi Watson utilizzano SSL (o TLS) per le connessioni sicure e le comunicazioni tra il client e il server. La connessione viene verificata rispetto all'archivio certificati locale per garantire l'autenticazione, l'integrità e la riservatezza.

{{site.data.keyword.icp4dfull_notm}} installa un certificato autofirmato. Questo certificato non può essere verificato correttamente per impostazione predefinita. Puoi eseguire una delle seguenti operazioni per connetterti correttamente a un'istanza del servizio: 

-   Aggiungi il certificato autofirmato al truststore per il tuo agent utente.

    Ad esempio, per effettuare richieste sicure con `curl`, aggiungi il certificato al truststore per `curl`. Per effettuare richieste sicure dal tuo browser, aggiungi il certificato al truststore per il browser.
-   Disabilita la verifica SSL. 

    La disabilitazione della verifica SSL compromette la sicurezza della connessione e dei dati. Ti sconsigliamo vivamente di effettuare tale operazione. Disabilita SSL solo se è assolutamente necessario ed esegui i passi per abilitarlo il prima possibile.
    {: important}

    -   Per disabilitare la verifica SSL per una richiesta `curl`, utilizza l'opzione `--insecure` (`-k`) con la richiesta. Questa opzione indica al comando di ignorare la verifica dei certificati SSL dello strumento. 
    -   Per disabilitare la verifica SSL per una richiesta WebSocket, utilizza l'approccio appropriato per la tua libreria client oppure utilizza uno degli SDK {{site.data.keyword.ibmwatson}} {{site.data.keyword.speechtotextshort}}.

Per ulteriori informazioni sulla disabilitazione della verifica SSL per le chiamate al servizio, vedi *Disabilitazione della verifica SSL* nella [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data#disabling-ssl){: external}. Le informazioni includono esempi per `curl` e per tutti gli SDK.
