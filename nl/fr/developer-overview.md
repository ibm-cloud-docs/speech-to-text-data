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

# Présentation destinée aux développeurs
{: #developerOverview}

Vous pouvez accéder aux fonctionnalités de {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} à l'aide d'une interface WebSocket et en utilisant des interfaces REST (Representational State Transfer) HTTP synchrones ou asynchrones. Vous pouvez également personnaliser les modèles de langue du service pour les adapter à votre domaine et à votre environnement. Des logiciels SDK sont disponibles pour simplifier le développement d'application dans de nombreux langages de programmation.
{: shortdesc}

Vous vous authentifiez auprès du service {{site.data.keyword.speechtotextshort}} en transmettant un jeton d'accès à chaque demande. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} est une solution cloud à service partagé. Vos données d'identification permettent d'accéder uniquement à vos données et vos données sont isolées des autres utilisateurs.

## Programmation avec le service
{: #programming}

La rubrique [Effectuer une demande de reconnaissance](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request) vous montre comment solliciter une transcription de base avec les différentes interfaces de programmation du service :

-   [L'interface WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) offre une implémentation efficace, à faible temps d'attente et à haut débit via une connexion en duplex intégral.
-   [L'interface HTTP synchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fournit une interface de base pour la transcription audio avec des demandes bloquantes.
-   [L'interface HTTP asynchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fournit une interface non bloquante qui vous laisse enregistrer une URL de rappel permettant de recevoir des notifications ou d'interroger le service pour obtenir le statut et les résultats d'un travail.

Ces interfaces offrent des fonctions similaires de reconnaissance vocale, mais vous pouvez spécifier le même paramètre en tant qu'en-tête de demande, paramètre de requête ou paramètre d'un objet JSON en fonction de l'interface que vous utilisez. 

Les interfaces WebSocket et HTTP synchrone acceptent un maximum de 100 Mo de données audio avec une seule demande. L'interface HTTP asynchrone accepte jusqu'à 1 Go de données audio maximum avec une demande.

-   Pour plus d'informations sur la création de demandes avec chacune des interfaces {{site.data.keyword.speechtotextshort}}, voir [Demandes au service](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Pour obtenir des exemples de demandes de reconnaissance vocale de base pour chacune des interfaces du service, voir [Effectuer une demande de reconnaissance](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Pour obtenir la description de tous les paramètres de reconnaissance vocale disponibles, voir [Récapitulatif des paramètres](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   Pour une description de toutes les méthodes et de leurs paramètres, ainsi que des exemples, voir la [référence d'API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Avantages de l'interface WebSocket
{: #advantages}

L'interface WebSocket comporte un certain nombre d'avantages par rapport à l'interface HTTP :

-   L'interface WebSocket fournit un canal de communication en duplex intégral sur un seul socket. L'interface laisse le client envoyer des demandes et des données audio au service et recevoir les résultats via une connexion unique de manière asynchrone.
-   Elle offre une expérience de programmation beaucoup plus simple et encore plus efficace. Le service envoie des réponses basées sur des événements dans les messages du client, évitant ainsi au client d'avoir à interroger le serveur.
-   Elle vous permet d'établir et d'utiliser une connexion unique authentifiée indéfiniment. Les interfaces HTTP nécessitent que vous authentifiez chaque appel au service.
-   Elle réduit les temps d'attente. Les résultats de la reconnaissance arrivent plus rapidement car le service les envoie directement au client. L'interface HTTP nécessite quatre demandes et connexions distinctes pour parvenir au même résultat.
-   Elle réduit l'utilisation du réseau. WebSocket est un protocole léger. Il lui suffit d'une seule connexion pour effectuer une reconnaissance vocale en direct.
-   Elle permet la diffusion en continu des données audio au service directement à partir des navigateurs (clients WebSocket HTML5).

## Personnalisation du service
{: #customizing}

[L'interface de personnalisation](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) vous permet de créer des modèles personnalisés pour améliorer les fonctions de reconnaissance vocale du service :

-   [Les modèles de langue personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate) vous permettent de définir les mots spécifiques à un domaine pour un modèle de base. Les modèles de langue personnalisés enrichissent le vocabulaire de base du service avec la terminologie spécifique à des domaines, tels que la médecine ou le droit.
-   [Les modèles acoustiques personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic) vous permettent d'adapter un modèle de base aux caractéristiques acoustiques de votre environnement et de vos locuteurs. Les modèles acoustiques personnalisés améliorent la capacité du service à reconnaître la parole en tenant compte de caractéristiques acoustiques spécifiques.
-   [Les grammaires](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) vous permettent de restreindre les expressions que le service peut reconnaître à celles définies dans les règles de grammaire. En limitant l'espace de recherche aux chaînes valides, le service peut délivrer des résultats plus rapides et plus précis. Les grammaires sont prises en charge avec les modèles de langue personnalisés.

Vous pouvez utiliser un modèle de langue personnalisé, un modèle acoustique personnalisé ou ces deux types de modèle pour la reconnaissance vocale avec n'importe quelle interface du service.

## Obtention de métriques
{: #overview-metrics}

Le service offre deux types de métriques facultatives pour les demandes de reconnaissance vocale : 

-   Les [métriques de traitement](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) fournissent des informations de synchronisation détaillées sur l'analyse de l'audio d'entrée par le service. Le service renvoie les métriques à des intervalles spécifiés et avec des événements de transcription, tels que des résultats intermédiaires et finaux. Vous pouvez utiliser les métriques pour évaluer la progression du service dans la transcription de l'audio. 
-   Les [métriques audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) fournissent des informations détaillées sur les caractéristiques de signal de l'entrée audio. Les résultats fournissent des métriques agrégées pour l'ensemble des données audio en entrée à la fin du traitement de la parole. Vous pouvez utiliser les métriques pour déterminer les caractéristiques et la qualité de l'audio. 

Vous pouvez demander des métriques de traitement avec les interfaces WebSocket et les interfaces HTTP asynchrones. Vous pouvez demander des métriques audio avec n'importe laquelle des interfaces du service. Par défaut, le service ne renvoie aucune métrique.

## Prise en charge de CORS
{: #cors}

Le service prend en charge le partage de ressources d'origine croisée (CORS). Avec CORS, les pages Web peuvent directement demander des ressources en provenance d'un domaine externe. CORS permet de contourner les règles de sécurité d'origine identique, qui empêcheraient les demandes de ce type. Comme le service prend en charge CORS, une page Web peut communiquer directement avec le service sans avoir à passer par le serveur Web qui héberge la page pour transmettre la demande.

Par exemple, une page Web chargée depuis un serveur dans {{site.data.keyword.cloud}} peut appeler directement l'API de personnalisation, en ignorant le serveur {{site.data.keyword.cloud_notm}}. Pour plus d'informations, voir [enable-cors.org](https://enable-cors.org/){: external}.

## Utilisation de logiciels SDK
{: #sdks}

Des logiciels SDK sont disponibles pour le service {{site.data.keyword.speechtotextshort}} afin de simplifier le développement des applications vocales. Les logiciels {{site.data.keyword.ibmwatson}} SDK sont disponibles pour de nombreux langages de programmation et plateformes populaires.

-   Pour obtenir une liste complète de logiciels SDK et de liens vers les logiciels SDK sur GitHub, voir [Utilisation des logiciels SDK](/docs/services/watson?topic=watson-using-sdks).
-   Pour des informations détaillées sur toutes les méthodes des SDK Node, Java&trade;, Python, Ruby et Go pour le service {{site.data.keyword.speechtotextshort}}, voir [Référence d'API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
