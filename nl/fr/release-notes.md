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

# Notes sur l'édition
{: #release-notes}

Les versions suivantes de {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} sont disponibles. Les informations incluent les nouvelles fonctionnalités et modifications pour chaque version du produit, ainsi que toutes les limitations connues.
{: shortdesc}

## Limitations connues
{: #limitations}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} n'a pas de limitations connues.

## Version 1.0.0 (juin 2019)
{: #v100}

Edition initiale du service. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} est basé sur le service {{site.data.keyword.speechtotextfull}} sur {{site.data.keyword.cloud_notm}} public. Pour plus d'informations sur le service public, voir [A propos de {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} diffère du service {{site.data.keyword.speechtotextshort}} public de l'une des manières suivantes. Ces informations peuvent vous être utiles si vous connaissez déjà le service {{site.data.keyword.speechtotextshort}} sur le {{site.data.keyword.cloud_notm}} public.

-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} utilise des jetons d'accès pour l'authentification. Pour plus d'informations, voir [Demandes au service](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) et [Référence d'API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   Les noeuds finaux de {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} sont spécifiques à votre cluster {{site.data.keyword.icp4dfull_notm}}. Pour plus d'informations, voir [Demandes au service](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) et [Référence d'API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} n'effectue aucune demande de consignation. Vous n'avez pas besoin d'utiliser l'en-tête de demande `X-Watson-Learning-Opt-Out`.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} ne prend pas en charge les jetons Watson. Vous ne pouvez pas utiliser l'en-tête de demande `X-Watson-Authorization-Token` pour l'authentification auprès du service.
