---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-24"

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

# Création d'un modèle acoustique personnalisé
{: #acoustic}

Procédez comme suit pour créer un modèle acoustique personnalisé pour {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} :
{: shortdesc}

1.  [Créez un modèle acoustique personnalisé](#createModel-acoustic). Vous pouvez créer plusieurs modèles personnalisés pour des domaines ou environnements identiques ou différents. Le processus est le même quel que soit le modèle que vous créez. Cependant, vous ne pouvez spécifier qu'un seul modèle acoustique personnalisé à la fois avec une demande de reconnaissance.
1.  [Ajoutez des données audio au modèle acoustique personnalisé](#addAudio). Le service accepte les mêmes formats de fichier audio pour la modélisation acoustique et la reconnaissance vocale. Il accepte également les fichiers archive contenant plusieurs fichiers audio. Les fichiers archive constituent le moyen privilégié pour ajouter des ressources audio. Vous pouvez répéter la procédure pour ajouter d'autres fichiers de type audio ou archive à un modèle personnalisé.
1.  [Entraînez le modèle acoustique personnalisé](#trainModel-acoustic). Après avoir ajouté des ressources audio au modèle personnalisé, vous devez entraîner le modèle. Cet entraînement prépare le modèle acoustique personnalisé pour qu'il soit utilisé dans la reconnaissance vocale. L'entraînement peut prendre un temps relativement long. La durée d'entraînement dépend de la quantité de données audio que contient le modèle.

    Vous pouvez spécifier un modèle de langue personnalisé auxiliaire lors de l'entraînement de votre modèle acoustique personnalisé. Un modèle de langue personnalisé incluant les transcriptions de vos fichiers audio ou de mots OOV (Out Of Vocabulary) issus du domaine de vos fichiers audio peut améliorer la qualité du modèle acoustique personnalisé. Pour plus d'informations, voir [Entraînement d'un modèle acoustique personnalisé avec un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth#useBothTrain).
1.  Après avoir entraîné votre modèle personnalisé, vous pouvez l'utiliser avec des demandes de reconnaissance. Si les qualités acoustiques des données transmises pour la transcription sont semblables à celles des données audio du modèle personnalisé, les résultats témoignent d'une meilleure compréhension du service. Pour plus d'informations, voir [Utilisation d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-acousticUse).

    Vous pouvez transmettre un modèle acoustique personnalisé et un modèle de langue personnalisé dans la même demande de reconnaissance afin d'obtenir une reconnaissance encore plus précise. Pour plus d'informations, voir [Utilisation d'un modèle de langue personnalisé et d'un modèle acoustique personnalisé lors de la reconnaissance vocale](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth#useBothRecognize).

Les étapes de création d'un modèle acoustique personnalisé sont itératives. Vous pouvez ajouter ou supprimer des données audio et entraîner ou ré-entraîner un modèle aussi souvent que nécessaire. Vous devez entraîner à nouveau un modèle pour que les modifications apportées à ses données audio soient appliquées. Lorsque vous entraînez à nouveau un modèle, toutes les données audio sont utilisées dans l'entraînement (et non pas uniquement les nouvelles données). La durée d'entraînement est proportionnelle à la quantité totale de données contenue dans le modèle.

La personnalisation de modèle acoustique est disponible en fonctionnalité bêta pour toutes les langues. Pour plus d'informations, voir [Support de langue pour la personnalisation](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
{: note}

## Création d'un modèle acoustique personnalisé
{: #createModel-acoustic}

Vous utilisez la méthode `POST /v1/acoustic_customizations` pour créer un modèle acoustique personnalisé. Vous pouvez créer autant de modèles acoustiques personnalisés que vous voulez, mais vous ne pouvez utiliser qu'un seul modèle de ce type à la fois avec une demande de reconnaissance vocale. Cette méthode accepte un objet JSON qui définit les attributs du nouveau modèle personnalisé en tant que corps de la demande.

<table>
  <caption>Tableau 1. Attributs d'un nouveau modèle acoustique personnalisé</caption>
  <tr>
    <th style="width:20%; text-align:left">Paramètre</th>
    <th style="width:12%; text-align:center">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Nom défini par l'utilisateur pour désigner le nouveau modèle acoustique personnalisé. Utilisez un nom
      caractéristique de l'environnement acoustique du modèle personnalisé par exemple
      <code>Mobile custom model</code> ou <code>Noisy car custom
      model</code>. Utilisez un nom unique par rapport à tous les modèles acoustiques
      personnalisés que vous possédez. Utilisez un nom localisé qui correspond à
      la langue du modèle personnalisé.
    </td>
  </tr>
  <tr>
    <td><code>base_model_name</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Nom du modèle de base qui doit être personnalisé par le
      nouveau modèle. Vous devez utiliser le nom d'un modèle renvoyé
      par la méthode <code>GET /v1/models</code>. Le nouveau
      modèle personnalisé ne peut être utilisé qu'avec le modèle de base qu'il personnalise.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Description du nouveau modèle. Utilisez une description localisée
      correspondant à la langue du modèle personnalisé.
    </td>
  </tr>
</table>

L'exemple suivant crée un modèle acoustique personnalisé nommé `Example acoustic model`. Le modèle est créé pour le modèle de base `en-US_BroadbandModel` avec la description `Example custom acoustic model`. L'en-tête `Content-Type` indique que les données JSON sont transmises à la méthode.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/json"
--data "{\"name\": \"Example acoustic model\",
  \"base_model_name\": \"en-US_BroadbandModel\",
  \"description\": \"Example custom acoustic model\"}"
"{url}/v1/acoustic_customizations"
```
{: pre}

L'exemple renvoie l'ID de personnalisation (customization_id) du nouveau modèle. Chaque modèle personnalisé est identifié par un ID de personnalisation unique, correspondant à un identificateur global unique (GUID). Vous spécifiez le GUID d'un modèle personnalisé dans le paramètre `customization_id` des appels qui sont associés au modèle.

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96"
}
```
{: codeblock}

Le nouveau modèle personnalisé appartient à l'instance du service dont les données d'identification sont utilisées pour la créer. Pour plus d'informations, voir [Propriété des modèles personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#customOwner).

## Ajout de données audio au modèle acoustique personnalisé
{: #addAudio}

Une fois votre modèle acoustique personnalisé créé, la prochaine étape consiste à lui ajouter des ressources audio. Vous utilisez la méthode `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` pour ajouter une ressource audio à un modèle personnalisé. Vous pouvez ajouter

-   un fichier audio individuel dans un format pris en charge pour la reconnaissance vocale.Pour plus d'informations, voir [Formats audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).
-   un fichier archive (**.zip** ou **.tar.gz**) qui comprend plusieurs fichiers audio. Rassembler plusieurs fichiers audio en un seul fichier archive et charger ce fichier unique est beaucoup plus efficace qu'ajouter des fichiers audio individuellement.

Vous transmettez la ressource audio en tant que corps de la demande et vous lui attribuez un nom `audio_name`. Pour plus d'informations, voir [Utilisation des ressources audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audioResources).

Les exemples suivants illustrent l'ajout de ressources de type audio et de type archive :

-   Cet exemple ajoute une ressource de type audio au modèle acoustique personnalisé avec l'ID de personnalisation (`customization_id`) spécifié. L'en-tête `Content-Type` identifie le type d'audio avec `audio/wav`. Le fichier audio, **audio1.wav**, est transmis en tant que corps de la demande et la ressource est nommée `audio1`.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/wav"
    --data-binary @audio1.wav
    "{url}/v1/acoustic_customizations/{customization_id}/audio/audio1"
    ```
    {: pre}

-   Cet exemple ajoute une ressource de type archive au modèle acoustique personnalisé spécifié. L'en-tête `Content-Type` identifie le type d'archive avec `application/zip`. L'en-tête `Contained-Contented-Type` indique que tous les fichiers contenus dans l'archive sont au format `audio/l16` et échantillonnés à une fréquence de 16 kHz. Le fichier archive, **audio2.zip**, est transmis en tant que corps de la demande et la ressource est nommée `audio2`.

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/zip"
    --header "Contained-Content-Type: audio/l16;rate=16000"
    --data-binary @audio2.zip
    "{url}/v1/acoustic_customizations/{customization_id}/audio/audio2"
    ```
    {: pre}

La méthode accepte également le paramètre de requête facultatif `allow_overwrite` permettant de remplacer une ressource audio existante pour un modèle personnalisé. Utilisez ce paramètre si vous devez mettre à jour une ressource audio après l'avoir ajoutée à un modèle.

Cette méthode est asynchrone. Elle peut prendre plusieurs secondes selon la durée de l'audio. Pour un fichier archive, la durée de l'opération dépend de la durée des fichiers audio. Pour plus d'informations sur la vérification du statut d'une demande d'ajout de ressource audio, voir [Surveillance de la demande d'ajout de données audio](#monitorAudio).

Vous pouvez ajouter n'importe quel nombre de ressources audio à un modèle personnalisé en appelant la méthode une fois pour chaque fichier de type audio ou archive. Vous pouvez effectuer plusieurs demandes pour ajouter différentes ressources audio simultanément.

Vous devez ajouter au minimum 10 minutes et au maximum 200 heures d'audio comprenant uniquement de la parole (pas de silence) à un modèle personnalisé avant de pouvoir l'entraîner. Aucune ressource de type audio ou archive ne peut dépasser 100 Mo. Pour plus d'informations, voir [Instructions pour ajouter des ressources audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audioResources#audioGuidelines).

### Surveillance de la demande d'ajout de données audio
{: #monitorAudio}

Le service renvoie le code de réponse 201 si les données audio sont valides. Il effectue ensuite l'analyse asynchrone du ou des fichiers audio et extrait automatiquement les informations sur les données audio, par exemple la durée, la fréquence d'échantillonnage et le codage. Vous ne pouvez pas entraîner le modèle personnalisé tant que le service n'a pas terminé l'analyse de toutes les ressources audio pour les demandes en cours.

Pour déterminer le statut de la demande, utilisez la méthode `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` permettant d'interroger le statut
des données audio. La méthode accepte l'identificateur global unique (GUID) du modèle personnalisé et le nom de la ressource audio. Sa réponse comprend le statut (`status`) de la ressource, qui peut correspondre à l'une des valeurs suivantes :

-   `ok` indique que les données audio sont acceptables et que l'analyse est terminée.
-   `being_processed` indique que le service est encore en train d'analyser les données audio.
-   `invalid` indique que le fichier audio n'est pas acceptable pour le traitement. Il se peut que son format ou sa fréquence d'échantillonnage soient incorrects ou que ce ne soit pas un fichier audio. Pour un fichier archive, si l'un des fichiers audio qu'il contient est non valide, l'archive dans son intégralité est non valide.

Le contenu de la réponse et l'emplacement de la zone `status` dépendent du type de ressource (audio ou archive).

-   *Pour une ressource de type audio,* la zone `status` se trouve dans l'objet de niveau supérieur (`AudioListing`).

    ```bash
    curl -X GET
    --header "Authorization: Bearer {token}"
    "{url}/v1/acoustic_customizations/{customization_id}/audio/audio1"
    ```
    {: pre}

    ```javascript
    {
      "duration": 131,
      "name": "audio1",
      "details": {
        "codec": "pcm_s16le",
        "type": "audio",
        "frequency": 22050
      }
      "status": "ok"
    }
    ```
    {: codeblock}

-   *Pour une ressource de type archive,* la zone `status` se trouve dans l'objet de deuxième niveau (`AudioResource`) qui est incorporé dans la zone `container`.

    ```bash
    curl -X GET
    --header "Authorization: Bearer {token}"
    "{url}/v1/acoustic_customizations/{customization_id}/audio/audio2"
    ```
    {: pre}

    ```javascript
    {
      "container": {
        "duration": 556,
        "name": "audio2",
        "details": {
          "type": "archive",
          "compression": "zip"
        },
        "status": "ok"
      },
      . . .
    }
    ```
    {: codeblock}

Utilisez une boucle pour vérifier le statut toutes les quelques secondes jusqu'à ce qu'il passe à `ok`. Pour plus d'informations sur les autres zones renvoyées par la méthode, voir [Affichage de la liste des ressources audio pour un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

## Entraînement du modèle acoustique personnalisé
{: #trainModel-acoustic}

Lorsque vous avez alimenté le modèle acoustique personnalisé avec des ressources audio, vous devez l'entraîner sur les nouvelles données. Cet entraînement prépare un modèle personnalisé pour être utilisé dans la reconnaissance vocale. Un modèle ne peut pas être utilisé pour des demandes de reconnaissance tant que vous ne l'avez pas entraîné sur les nouvelles données. De même, les mises à jour d'un modèle personnalisé sous la forme de ressources audio nouvelles ou modifiées ne sont pas répercutées par le modèle, tant que vous ne l'avez pas entraîné avec les modifications effectuées.

Vous utilisez la méthode `POST /v1/acoustic_customizations/{customization_id}/train` pour entraîner un modèle personnalisé. Vous transmettez à la méthode, l'ID de personnalisation (customization_id) du modèle que vous voulez entraîner, comme illustré dans l'exemple suivant.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/acoustic_customizations/{customization_id}/train"
```
{: pre}

Cette méthode est asynchrone. L'entraînement peut prendre de quelques minutes à quelques heures en fonction de la quantité de données audio que contient le modèle acoustique personnalisé et de la charge en cours sur le service. En règle générale, l'entraînement d'un modèle acoustique personnalisé dure approximativement deux à quatre fois plus que la durée de ses données audio. L'échelle de durée dépend du modèle entraîné et de la nature des données audio, selon qu'elles soient nettes ou bruitées. Par exemple, l'entraînement d'un modèle contenant 2 heures d'audio peut prendre 4 à 8 heures. Pour plus d'informations sur la vérification du statut d'une opération d'entraînement, voir [Surveillance de la demande d'entraînement du modèle](#monitorTraining-acoustic).

La méthode inclut les paramètres de requête facultatifs suivants :

-   Le paramètre `custom_language_model_id` spécifie un modèle de langue personnalisé créé séparément qui doit être utilisé lors de l'entraînement. Vous pouvez effectuer l'entraînement avec un modèle de langue personnalisé qui contient les transcriptions de vos fichiers audio ou les corpus ou mots OOV pertinents par rapport au contenu des fichiers audio. Les modèles de langue personnalisés et acoustiques personnalisés doivent être basés sur la même version du même modèle de base pour que l'entraînement réussisse. Pour plus d'informations, voir [Entraînement d'un modèle acoustique personnalisé avec un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth#useBothTrain).
-   Le paramètre `strict` indique si la formation doit se poursuivre si le modèle personnalisé contient un mélange de ressources audio valides et non valides. Par défaut, la formation échoue si le modèle contient une ou plusieurs ressources non valides. Définissez le paramètre sur `false` pour permettre à l'entraînement de se poursuivre tant que le modèle contient au moins une ressource valide. Le service exclut les ressources non valides de l'entraînement. Pour plus d'informations, voir [Echecs d'entraînement](#failedTraining-acoustic).


### Surveillance de la demande d'entraînement du modèle
{: #monitorTraining-acoustic}

Le service renvoie le code de réponse 200 si le processus d'entraînement a été initié avec succès. Il n'accepte pas d'autres demandes d'entraînement ou des demandes d'ajout de ressources audio supplémentaires, tant que la demande existante n'est pas terminée.

Pour déterminer le statut d'une demande d'entraînement, utilisez la méthode `GET /v1/acoustic_customizations/{customization_id}` permettant d'interroger le statut du modèle. La méthode accepte l'ID de personnalisation du modèle acoustique et renvoie son statut, comme illustré dans l'exemple suivant :

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/acoustic_customizations/{customization_id}"
```
{: pre}

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
  "created": "2016-06-01T18:42:25.324Z",
  "updated": "2016-06-01T22:11:13.298Z",
  "language": "en-US",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model",
  "description": "Example custom acoustic model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "training",
  "progress": 0
}
```
{: codeblock}

La réponse comprend les zones `status` et `progress` qui indiquent l'état en cours du modèle. La signification de la zone `progress` dépend du statut du modèle. La zone `status` peut avoir l'une des valeurs suivantes :

-   `pending` indique que le modèle a été créé mais attend que des données d'entraînement valides soient ajoutées ou que le service termine l'analyse des données qui ont été ajoutées. La zone `progress` a la valeur `0`.
-   `ready` indique que le modèle contient des données valides et qu'il est prêt à être entraîné. La zone `progress` a la valeur `0`.

Si le modèle contient un mélange de ressources audio valides et non valides, l'entraînement du modèle échoue sauf si vous définissez le paramètre de requête `strict` sur `false`. Pour plus d'informations, voir [Echecs d'entraînement](#failedTraining-acoustic).
-   `training` indique que le modèle est en cours d'entraînement. La zone `progress` passe de `0` à `100` lorsque l'entraînement est terminé. <!-- The `progress` field indicates the progress of the training as a percentage complete. -->
-   `available` indique que l'entraînement du modèle est terminé et que le modèle est prêt à l'emploi. La zone `progress` a la valeur `100`.
-   `upgrading` indique que le modèle est en cours de mise à niveau. La zone `progress` a la valeur `0`.
-   `failed` indique que l'entraînement du modèle a échoué. La zone `progress` a la valeur `0`. Pour plus d'informations, voir [Echecs d'entraînement](#failedTraining-acoustic).

Utilisez une boucle pour vérifier le statut de l'entraînement toutes les minutes, jusqu'à ce que le modèle passe à l'état `available`. Pour plus d'informations sur les autres zones renvoyées par la méthode, voir [Affichage de la liste des modèles acoustiques personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic).

### Echecs d'entraînement
{: #failedTraining-acoustic}

L'entraînement ne parvient pas à démarrer si le service traite une autre demande pour le modèle acoustique personnalisé. Une demande conflictuelle peut être une autre demande d'entraînement ou une demande d'ajout de ressources audio au modèle. Le service renvoie un code de statut 409.

De même, l'entraînement ne parvient pas à démarrer pour les raisons suivantes :

-   Le modèle personnalisé contient moins de 10 minutes de données audio.
-   Le modèle personnalisé contient plus de 200 heures de données audio.
-   Une ou plusieurs ressources audio du modèle personnalisé ne sont pas valides.
-   Vous avez transmis un modèle de langue personnalisé incompatible avec le paramètre de requête `custom_language_model_id`. Les deux modèles personnalisés doivent être basés sur la même version du même modèle de base.

Le service renvoie un code de statut 400 et définit le statut du modèle personnalisé sur `failed`. Effectuez
l'une des actions ci-dessous :

-   Utilisez les méthodes `GET /v1/acoustic_customizations/{customization_id}/audio` et `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` pour examiner les ressources audio du modèle. Pour plus d'informations, voir [Affichage de la liste des ressources audio d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

    Pour chaque ressource audio non valide, effectuez l'une des actions suivantes :
    -   Corrigez la ressource audio et utilisez le paramètre `allow_overwrite` de la méthode `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` pour ajouter l'audio corrigé au modèle. Pour plus d'informations, voir [Ajout de données audio au modèle acoustique personnalisé](#addAudio).
    -   Utilisez la méthode `DELETE /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` pour supprimer la ressource audio du modèle. Pour plus d'informations, voir [Suppression d'une ressource audio d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#deleteAudio).
-   Définissez le paramètre `strict` de la méthode `POST /v1/acoustic_customizations/{customization_id}/train` sur `false` pour exclure les ressources audio non valides de l'entraînement. Le modèle doit contenir au moins une ressource audio valide pour que l'entraînement aboutisse. Le paramètre `strict` permet d'entraîner un modèle personnalisé contenant un mélange de ressources valides et non valides.
