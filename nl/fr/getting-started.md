---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-25"

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
{:download: .download}

# Tutoriel d'initiation
{: #gettingStarted}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} transcrit les données audio sous forme de texte pour activer les fonctions de transcription vocale pour les applications. Ce tutoriel qui fait appel à la commande curl peut vous aider à expérimenter rapidement le service. Les exemples vous montrent comment appeler la méthode `POST /v1/recognize` du service pour demander une retranscription.
{: shortdesc}

## Avant de commencer
{: #before-you-begin}

Pour utiliser {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, vous devez d'abord effectuer les étapes suivantes :

1.  Mettez à disposition une instance de {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}. Pour plus d'informations sur la mise à disposition, voir [Installation du service](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).
1.  Dans le menu du client Web {{site.data.keyword.icp4dfull_notm}}, sélectionnez **Mes instances**.
1.  Cliquez sur l'instance {{site.data.keyword.speechtotextshort}} pour ouvrir la page de présentation. Copiez les valeurs de données d'identification `{token}` et `{URL}`. 

### Utilisation des exemples curl
{: #getting-started-curl}

Ce tutoriel utilise la commande `curl` pour appeler les méthodes de l'interface HTTP du service. Vérifiez que la commande `curl` est installée sur votre système.

1.  Pour vérifier si `curl` est installé, exécutez la commande suivante sur la ligne de commande. Si la sortie répertorie la version `curl` qui prend en charge SSL (Secure Sockets Layer), le tutoriel est défini. 

    ```bash
    curl -V
    ```
    {: pre}

1.  Si nécessaire, installez la version de `curl` avec SSL activé pour votre système d'exploitation à partir de [curl.haxx.se](https://curl.haxx.se/){: external}.

Omettez les accolades des exemples. Elles indiquent des valeurs de variable.
{: tip}

## Etape 1 : Transcription audio sans options
{: #transcribe}

Appelez la méthode `POST /v1/recognize` pour demander une retranscription de base d'un fichier audio FLAC sans aucun paramètre de demande supplémentaire.

1.  Téléchargez l'exemple de fichier audio <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>.
1.  Exécutez la commande suivante pour appeler la méthode `/v1/recognize` du service pour effectuer une transcription de base sans paramètre. L'exemple utilise l'en-tête `Content-Type` pour indiquer le type d'audio, `audio/flac`. L'exemple utilise le modèle de langue par défaut, `en-US_BroadbandModel`, pour la transcription.
    -   Remplacez `{token}` par le jeton d'accès de votre instance de service.
    -   Remplacez `{url}` par l'URL de votre instance de service.
    -   Remplacez `{path_to_file}` en indiquant l'emplacement du fichier `audio-file.flac`.

    Les *utilisateurs Windows* remplacent la barre oblique inversée (``\`) à la fin de chaque ligne par un caret (``^`). Vérifiez qu'il n'y a aucun espace de fin.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize"
    ```
    {: pre}

    Le service renvoie les résultats de transcription suivants :

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "confidence": 0.96,
              "transcript": "several tornadoes touch down as a line of
severe thunderstorms swept through Colorado on Sunday "
            }
          ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Etape 2 : Transcription audio avec options
{: #transcribeOptions}

Appelez la méthode `POST /v1/recognize` pour transcrire le même fichier audio FLAC, mais cette fois en spécifiant deux paramètres de transcription.

1.  Si nécessaire, téléchargez l'exemple de fichier audio <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe" title="Icône de lien externe"></a>.
1.  Exécutez la commande suivante pour appeler la méthode `/v1/recognize` du service avec deux paramètres supplémentaires. Définissez le paramètre `timestamps` avec la valeur `true` pour indiquer le début et la fin de chaque mot dans le flux audio. Définissez le paramètre `max_alternatives` avec la valeur `3` pour recevoir les trois alternatives les plus plausibles pour la transcription. L'exemple utilise l'en-tête `Content-Type` pour indiquer le type d'audio, `audio/flac` et la demande utilise le modèle de langue par défaut, `en-US_BroadbandModel`.
    -   Remplacez `{token}` par le jeton d'accès de votre instance de service.
    -   Remplacez `{url}` par l'URL de votre instance de service.
    -   Remplacez `{path_to_file}` en indiquant l'emplacement du fichier `audio-file.flac`.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize?timestamps=true&max_alternatives=3"
    ```
    {: pre}

    Le service renvoie les résultats suivants, qui comprennent des horodatages (timestamps) et trois transcriptions alternatives :

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "timestamps": [
                ["several":, 1.0, 1.51],
                ["tornadoes":, 1.51, 2.15],
                ["touch":, 2.15, 2.5],
                . . .
              ]
            },
            {
              "confidence": 0.96,
              "transcript": "several tornadoes touch down as a line
of severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touched down as a line of
severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touch down as a line
of severe thunderstorms swept through Colorado and Sunday "
            }
          ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Etapes suivantes

-   Pour en savoir plus sur les interfaces et les logiciels SDK disponibles pour effectuer des demandes de reconnaissance vocale, consultez la rubrique [Présentation destinée aux développeurs](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).
-   Découvrez comment faire des demandes au service dans la rubrique [Demandes au service](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Consultez les demandes de reconnaissance vocale de base pour chacune des interfaces du service dans la rubrique [Effectuer une demande de reconnaissance](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Vous trouverez des informations détaillées sur toutes les méthodes des interfaces du service dans la [référence d'API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
