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

# Releaseinformationen
{: #release-notes}

Die folgenden Versionen von {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} stehen zur Verfügung. Die Informationen enthalten neue Funktionen und Änderungen für jede Version des Produkts sowie alle bekannten Einschränkungen.
{: shortdesc}

## Bekannte Einschränkungen
{: #limitations}

Für {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} gibt es keine bekannten Einschränkungen. 

## Version 1.0.0 (Juni 2019)
{: #v100}

Das erste Release des Service. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} basiert auf dem {{site.data.keyword.speechtotextfull}}-Service in der öffentlichen {{site.data.keyword.cloud_notm}}. Weitere Informationen zum öffentlichen Service finden Sie in [Produktinformation {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.


Zwischen {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} und dem öffentlichen {{site.data.keyword.speechtotextshort}}-Service gibt es die folgenden Unterschiede. Diese Informationen könnten hilfreich für Sie sein, falls Sie bereits mit dem {{site.data.keyword.speechtotextshort}}-Service in der öffentlichen {{site.data.keyword.cloud_notm}} vertraut sind. 

-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} verwendet Zugriffstoken für die Authentifizierung. Weitere Informationen finden Sie unter [Anforderungen an den Service ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) und in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external}. 
-   Die Endpunkte für {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} gelten speziell für Ihren {{site.data.keyword.icp4dfull_notm}}-Cluster. Weitere Informationen finden Sie unter [Anforderungen an den Service ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) und in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external}. 
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} führt keine Protokollierung von Anforderungen durch. Sie müssen nicht den Anforderungsheader `X-Watson-Learning-Opt-Out` verwenden. 
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} unterstützt keine Watson-Tokens. Sie können nicht den Anforderungsheader `X-Watson-Authorization-Token` für die Authentifizierung beim Service verwenden. 
