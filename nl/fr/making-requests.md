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

# Demandes au service
{: #making-requests}

Pour faire des demandes authentifiées à {{site.data.keyword.speechtotextdatafull}} pour {{site.data.keyword.icp4dfull}}, vous devez mettre à disposition une instance du service et obtenir des données d'identification. Vous utilisez une URL différente pour les interfaces HTTP et WebSocket du service. Si vous utilisez un certificat autosigné, vous devez désactiver la vérification SSL pour les demandes au service.
{: shortdesc}

## Mise à disposition d'une instance et obtention des données d'identification
{: #making-requests-provisioning}

Avant d'utiliser le service {{site.data.keyword.speechtotextshort}}, vous devez mettre à disposition une instance du service et obtenir vos données d'identification. Pour plus d'informations, reportez-vous à la rubrique [Avant de commencer](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#before-you-begin).
Lors de la dernière étape de cette procédure, vous copiez les éléments `{token}` et `{URL}` correspondant à votre instance de service :

-   `{token}` fournit votre jeton d'accès pour l'authentification au service. Vous pouvez utiliser le jeton d'accès affiché dans le client Web {{site.data.keyword.icp4dfull_notm}}. Toutefois, dans un environnement de production, utilisez un jeton que vous générez à l'aide d'un programme pour votre instance de service. Pour plus d'informations et pour des exemples, voir *Authentification* dans la [référence d'API](https://{DomainName}/apidocs/speech-to-text-data#authentication){: external}.

    Vous vous authentifiez auprès du service {{site.data.keyword.speechtotextshort}} en transmettant votre jeton d'accès à chaque demande. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} est une solution cloud à service partagé. Vos données d'identification permettent d'accéder uniquement à vos données et vos données sont isolées des autres utilisateurs.
-   `{URL}` fournit le noeud final de base que vous utilisez pour appeler des méthodes du service.

L'URL contient les composants suivants : 

```
https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api
```
{: codeblock}

Les valeurs de variable dans `{}` (accolades) fournissent les informations suivantes :

-   `{icp4d_cluster_host}` est le nom ou l'adresse IP de l'hôte sur lequel est déployé votre cluster {{site.data.keyword.icp4dfull_notm}}.
-   `{:port}` est le numéro de port sur lequel le service écoute les demandes sur l'hôte spécifié. Vous devez faire précéder le numéro de port par un signe deux-points (`:`).
-   `{release}` est le nom de l'édition qui a été spécifié lors de l'installation de la Charte Helm.
-   `{instance_id}` est l'identificateur de votre instance de service.

Les accolades indiquent les chaînes de variables que vous devez remplacer par des valeurs littérales. N'incluez pas les accolades dans les appels réels au service.
{: note}

## Création d'une demande HTTP authentifiée
{: #httpRequest}

Le service {{site.data.keyword.speechtotextshort}} offre deux interfaces HTTP :

-   L'[interface HTTP synchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) permet d'accéder à toutes les fonctionnalités du service, y compris les interfaces de personnalisation.
-   L'[interface HTTP asynchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fournit des méthodes uniquement pour la reconnaissance vocale.

Les deux interfaces HTTP acceptent les requêtes sur le protocole HTTP Secure qui, à son tour, repose sur le protocole SSL (Secure Sockets Layer) ou TLS (Transport Layer Security). Toutes les URL des demandes adressées à une interface HTTP commencent par la spécification de protocole `https`.

Les exemples de cette documentation utilisent la commande `curl` pour appeler les interfaces HTTP du service. Pour plus d'informations, voir [Utilisation des exemples curl](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#getting-started-curl). Le format de base d'une demande HTTP avec `curl` inclut les composants suivants :

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Les valeurs des variables dans les accolades fournissent les informations suivantes :

-   `{http_method}` spécifie la méthode de demande HTTP pour l'exemple : `POST`, `PUT`, `GET` ou `DELETE`. La méthode de demande est requise avec `curl` pour tout autre élément que `GET`.
-   `{token}` fournit le jeton d'accès de votre instance de service. Vous devez utiliser le jeton d'accès pour faire une demande sécurisée au service.
-   `{method}` est la méthode du service que vous appelez. Par exemple, vous utilisez la méthode `recognize` pour effectuer une demande HTTP synchrone vers le service.

Les valeurs de variable restantes fournissent les informations décrites précédemment. De nombreuses méthodes ont des noms plus longs et incluent des paramètres de chemin que vous devez spécifier dans la demande. La plupart des exemples incluent également des en-têtes de demande, des paramètres de requête et d'autres valeurs.

Les exemples illustrent l'URL des appels vers les interfaces HTTP en tant que `{url}/v1/{method}`. Remplacez `{url}` par les valeurs que vous venez de décrire.
{: note}

## Création d'une demande WebSocket authentifiée
{: #websocketRequest}

Le service {{site.data.keyword.speechtotextshort}} offre une [interface WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) qui fournit uniquement la reconnaissance vocale. Le service accepte les demandes via le protocole WebSocket Secure, qui repose à nouveau sur le protocole SSL (Secure Sockets Layer) ou TLS (Transport Layer Security). Toutes les adresses URL des demandes adressées à l'interface WebSocket commencent par la spécification de protocole `wss`.

Vous pouvez appeler l'interface WebSocket uniquement à partir du code d'application. Vous ne pouvez pas appeler l'interface WebSocket à partir de la ligne de commande. Vous établissez une connexion WebSocket au service sur le noeud final suivant. 

```
wss://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/recognize
```
{: codeblock}

Les valeurs des variables fournissent les informations décrites précédemment. Vous transmettez votre jeton d'accès via le paramètre de requête `access_token` de la méthode.

Les exemples illustrent l'URL des appels vers l'interface WebSocket en tant que `{ws_url}/v1/recognize`. Remplacez `{ws_url}` par les valeurs que vous venez de décrire.
{: note}

## Désactivation de la vérification SSL
{: #SSLverification}

Tous les services Watson utilisent SSL (ou TLS) pour les connexions sécurisées et les communications entre le client et le serveur. La connexion est vérifiée par rapport au magasin de certificats local pour garantir l'authentification, l'intégrité et la confidentialité.

{{site.data.keyword.icp4dfull_notm}} installe un certificat autosigné. Ce certificat ne peut pas être vérifié par défaut. Pour vous connecter à une instance de service, vous pouvez effectuer l'une des actions suivantes :

-   Ajoutez le certificat autosigné au fichier de clés certifiées pour votre agent utilisateur.

    Par exemple, pour effectuer des requêtes sécurisées avec `curl`, ajoutez le certificat au fichier de clés certifiées pour `curl`. Pour effectuer des demandes sécurisées à partir de votre navigateur, ajoutez le certificat au fichier de clés certifiées du navigateur.
-   Désactivez la vérification SSL.

    La désactivation de la vérification SSL compromet la sécurité de la connexion et des données. Elle est fortement déconseillée. Désactivez SSL uniquement si cela est absolument nécessaire, et prenez les mesures nécessaires pour activer SSL dès que possible.
    {: important}

    -   Pour désactiver la vérification SSL pour une demande `curl`, utilisez l'option `--insecure` (`-k`) avec la demande. Cette option demande à la commande de contourner la vérification des certificats SSL par l'outil. 
    -   Pour désactiver la vérification SSL pour une demande WebSocket, utilisez l'approche appropriée pour votre bibliothèque client ou utilisez l'un des SDK {{site.data.keyword.ibmwatson}}{{site.data.keyword.speechtotextshort}}.

Pour plus d'informations sur la désactivation de la vérification SSL pour les appels au service, voir *Désactivation de la vérification SSL* dans la [référence d'API](https://{DomainName}/apidocs/speech-to-text-data#disabling-ssl){: external}. Les informations incluent des exemples pour `curl` et pour tous les SDK.
