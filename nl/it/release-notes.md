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

# Note sulla release
{: #release-notes}

Sono disponibili le seguenti versioni di {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. Le informazioni includono le nuove funzioni e le modifiche per ciascuna versione del prodotto e tutte le limitazioni note.
{: shortdesc}

## Limitazioni note
{: #limitations}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} non ha limitazioni note. 

## Versione 1.0.0 (giugno 2019)
{: #v100}

La release iniziale del servizio. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} è basato sul servizio {{site.data.keyword.speechtotextfull}} sul {{site.data.keyword.cloud_notm}} pubblico. Per ulteriori informazioni sul servizio pubblico, vedi [About {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}. 

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} è diverso dal servizio {{site.data.keyword.speechtotextshort}} pubblico nei seguenti modi. Potresti trovare utili queste informazioni se hai già familiarità con il servizio {{site.data.keyword.speechtotextshort}} su {{site.data.keyword.cloud_notm}} pubblico.

-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} utilizza i token di accesso per l'autenticazione. Per ulteriori informazioni, vedi [Effettuazione delle richieste al servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) e la [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   Gli endpoint per {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} sono specifici per il tuo cluster {{site.data.keyword.icp4dfull_notm}}. Per ulteriori informazioni, vedi [Effettuazione delle richieste al servizio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) e la [Guida di riferimento API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} non esegue alcuna registrazione della richiesta. Non hai bisogno di utilizzare l'intestazione della richiesta `X-Watson-Learning-Opt-Out`.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} non supporta i token Watson. Non puoi utilizzare l'intestazione della richiesta `X-Watson-Authorization-Token` per l'autenticazione con il servizio.
