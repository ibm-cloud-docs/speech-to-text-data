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

# Création d'un modèle de langue personnalisé
{: #languageCreate}

Procédez comme suit pour créer un modèle de langue personnalisé pour {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} :
{: shortdesc}

1.  [Créez un modèle de langue personnalisé](#createModel-language). Vous pouvez créer plusieurs modèles personnalisés pour un même domaine ou pour des domaines différents. Le processus est le même quel que soit le modèle que vous créez. Cependant, vous ne pouvez spécifier qu'un seul modèle personnalisé à la fois avec une demande de reconnaissance.
1.  [Ajoutez un corpus au modèle de langue personnalisé](#addCorpus). Un corpus est un document en texte brut qui utilise la terminologie d'un domaine en contexte. Le service élabore un vocabulaire pour un modèle personnalisé en extrayant des termes de différents corpus qui n'existent pas à l'origine dans son vocabulaire de base. Vous pouvez ajouter plusieurs corpus à un modèle personnalisé.
1.  [Ajoutez des mots au modèle de langue personnalisé](#addWords). Vous pouvez également ajouter des mots personnalisés à un modèle individuellement. Par ailleurs, vous pouvez utiliser les mêmes méthodes pour modifier des mots personnalisés extraits des corpus. Les méthodes vous permettent de spécifier la prononciation des mots et leur mode d'affichage dans la retranscription de la parole.
1.  [Entraînez le modèle de langue personnalisé](#trainModel-language). Lorsque vous ajoutez des mots au modèle personnalisé, vous devez entraîner le modèle avec ces mots. Cet entraînement prépare le modèle personnalisé pour qu'il soit utilisé dans la reconnaissance vocale. Le modèle n'utilise pas de mots nouveaux ou modifiés tant que vous ne l'avez pas entraîné.
1.  Après avoir entraîné votre modèle personnalisé, vous pouvez l'utiliser avec des demandes de reconnaissance. Si les données audio transmises pour la transcription contiennent des mots spécifiques à un domaine définis dans le modèle personnalisé, les résultats de la demande reflètent le vocabulaire amélioré du modèle. Pour plus d'informations, voir [Utilisation d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse).

Les étapes de création d'un modèle de langue personnalisé sont itératives. Vous pouvez ajouter des corpus, ajouter des mots, et entraîner ou ré-entraîner un modèle aussi souvent que nécessaire.

Vous pouvez également ajouter des grammaires à un modèle de langue personnalisé. Les grammaires limitent la réponse du service uniquement aux mots qu'elles reconnaissent. Pour plus d'informations, voir [Utilisation de grammaires avec des modèles de langue personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars).

La personnalisation de modèle de langue est disponible pour la plupart des langues. Pour plus d'informations, voir [Support de langue pour la personnalisation](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
{: note}

## Création d'un modèle de langue personnalisé
{: #createModel-language}

Vous utilisez la méthode `POST /v1/customizations` pour créer un modèle de langue personnalisé. Vous pouvez créer autant de modèles personnalisés que vous voulez, mais vous ne pouvez utiliser qu'un seul modèle à la fois avec une demande de reconnaissance vocale. Cette méthode accepte un objet JSON qui définit les attributs du nouveau modèle personnalisé en tant que corps de la demande.

<table>
  <caption>Tableau 1. Attributs d'un nouveau modèle de langue personnalisé</caption>
  <tr>
    <th style="width:20%; text-align:left">Paramètre</th>
    <th style="width:12%; text-align:center">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Nom défini par l'utilisateur pour désigner le nouveau modèle personnalisé. Utilisez un nom
      caractéristique du domaine du modèle personnalisé, par exemple <code>Medical
        custom model</code> ou <code>Legal custom model</code>. Utilisez un
      nom unique par rapport à tous les modèles de langue personnalisés que vous possédez.
      Utilisez un nom localisé qui correspond à la langue du modèle personnalisé.
    </td>
  </tr>
  <tr>
    <td><code>base_model_name</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Nom du modèle de langue qui doit être personnalisé par le nouveau
      modèle personnalisé. Spécifiez l'un des modèles de langue pris en charge
      renvoyé par la méthode <code>GET /v1/models</code>. Le nouveau
      modèle ne peut être utilisé qu'avec le modèle de base qu'il personnalise.
    </td>
  </tr>
  <tr>
    <td><code>dialect</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Dialecte de la langue spécifiée qui doit être utilisé avec le
      modèle personnalisé. Par défaut, le dialecte correspond à la langue
      du modèle de base ; par exemple, le dialecte est <code>en-US</code>
      pour les modèles <code>en-US_BroadbandModel</code> ou
      <code>en-US_NarrowbandModel</code> correspondant à
      l'anglais américain.<br/></br>
      Ce paramètre n'est pertinent que pour les modèles espagnols,
      pour lesquels le service crée un modèle personnalisé qui convient
      aux discours dans le dialecte indiqué :
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-ES</code> pour l'espagnol castillan (valeur par défaut)
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-LA</code> pour l'espagnol latino-américain
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-US</code> pour l'espagnol d'Amérique du Nord (mexicain)
        </li>
      </ul>
      Si vous spécifiez un dialecte, il doit être valide pour le modèle de base.
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

L'exemple suivant crée un modèle de langue personnalisé nommé `Example model`. Ce modèle est créé pour le modèle de base `en-US-BroadbandModel` avec la description `Example custom language model`. L'en-tête `Content-Type` indique que les données JSON sont transmises à la méthode.

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

L'exemple renvoie l'ID de personnalisation (customization_id) du nouveau modèle. Chaque modèle personnalisé est identifié par un ID de personnalisation unique, correspondant à un identificateur global unique (GUID). Vous spécifiez le GUID d'un modèle personnalisé dans le paramètre `customization_id` des appels qui sont associés au modèle.

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96"
}
```
{: codeblock}

Le nouveau modèle personnalisé appartient à l'instance du service dont les données d'identification sont utilisées pour la créer. Pour plus d'informations, voir [Propriété des modèles personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#customOwner).

## Ajout d'un corpus au modèle de langue personnalisé
{: #addCorpus}

Lorsque vous avez créé votre modèle de langue personnalisé, la prochaine étape consiste à lui ajouter des données (mots spécifiques à un domaine). La méthode recommandée pour alimenter un modèle personnalisé avec des mots nouveaux est d'ajouter un ou plusieurs corpus.

Un corpus est un fichier en texte brut qui contient idéalement des exemples de phrases tirées de votre domaine. Le service analyse le contenu d'un fichier de corpus et en extrait les mots qui ne figurent pas dans son vocabulaire de base. Ces mots sont désignés par OOV (Out-Of-Vocabulary).

-   Pour plus d'informations sur l'utilisation des corpus, voir [Utilisation des corpus](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingCorpora).
-   Pour en savoir plus sur comment le service ajoute des corpus à un modèle, voir [Que se passe-t-il lorsque j'ajoute un fichier de corpus ?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseCorpus)

En fournissant des phrases avec des mots nouveaux, les corpus permettent au service d'apprendre ces mots dans leur contexte. Vous pouvez enrichir ou modifier les mots du modèle individuellement. L'entraînement d'un modèle uniquement sur des mots individuels par opposition à des corpus prend plus de temps et peut produire des résultats moins probants.
{: tip}

Vous utilisez la méthode `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` pour ajouter un corpus à un modèle personnalisé :

-   Spécifiez l'ID de personnalisation du modèle personnalisé avec le paramètre de chemin `customization_id`.
-   Indiquez un nom pour le corpus avec le paramètre de chemin `corpus_name`. Utilisez un nom localisé qui correspond à la langue du modèle personnalisé et qui reflète le contenu du corpus.
    -   Indiquez un nom ne dépassant pas 128 caractères.
    -   N'utilisez pas de caractères qui doivent être codés au format URL. Par exemple, n'utilisez pas d'espaces, de barres obliques, de barres obliques inversées, de signes deux-points, de perluètes, de guillemets, de signes plus, de signes égal, de points d'interrogation, etc. dans le nom. (Le service n'empêche pas l'utilisation de ces caractères. Mais, dans la mesure où ils doivent être codés en URL partout où ils sont utilisés, leur utilisation est fortement déconseillé.)
    -   N'utilisez pas le nom d'un corpus ou d'une grammaire qui a déjà été ajouté au modèle personnalisé.
    -   N'utilisez pas le nom `user`, qui est réservé par le service pour désigner des mots personnalisés ajoutés ou modifiés par l'utilisateur.
    -   N'utilisez pas le nom `base_lm` ou `default_lm`. Les deux noms sont réservés pour une utilisation future par le service.
-   Transmettez le fichier texte du corpus en tant que corps de la demande.

Vous pouvez ajouter jusqu'à 90 mille mots OOV maximum et 10 millions de mots au total provenant de toutes sources confondues. Ces valeurs comprennent les mots issus de corpus et de grammaires, ainsi que les mots que vous ajoutez directement. Pour plus d'informations, voir [De quelle quantité de données ai-je besoin ?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#wordsResourceAmount)
{: note}

L'exemple suivant ajoute le fichier texte de corpus `healthcare.txt` au modèle personnalisé avec l'ID spécifié. Dans cet exemple, le corpus est nommé `healthcare`.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--data-binary @healthcare.txt
"{url}/v1/customizations/{customization_id}/corpora/healthcare"
```
{: pre}

La méthode accepte également le paramètre de requête facultatif `allow_overwrite` qui remplace un corpus existant pour un modèle personnalisé. Utilisez ce paramètre si vous devez mettre à jour un fichier de corpus après l'avoir ajouté à un modèle.

Cette méthode est asynchrone. Son exécution nécessite environ une minute ou deux. La durée de l'opération dépend du nombre total de mots dans le corpus, du nombre de mots nouveaux que le service détecte dans le corpus et de la charge en cours sur le service. Pour plus d'informations sur la vérification du statut d'un corpus, voir [Surveillance de la demande d'ajout d'un corpus](#monitorCorpus).

Vous pouvez ajouter n'importe quel nombre de corpus à un modèle personnalisé en appelant la méthode une fois pour chaque fichier texte de corpus. L'ajout d'un corpus doit être entièrement terminé avant d'en ajouter un autre. Après avoir ajouté un corpus à un modèle personnalisé, examinez les nouveaux mots personnalisés pour rechercher d'éventuelles erreurs de typographie ou d'autres erreurs. Pour plus d'informations, voir [Validation d'une ressource de mots](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).

### Surveillance de la demande d'ajout d'un corpus
{: #monitorCorpus}

Le service renvoie le code de réponse 201 si le corpus est valide. Il traite ensuite le contenu du corpus de manière asynchrone et extrait automatiquement les mots nouveaux. Vous ne pouvez pas soumettre de demande d'ajout de données à un modèle personnalisé ou entraîner le modèle tant que le service n'a pas terminé l'analyse du corpus pour la demande en cours.

Pour déterminer le statut de l'analyse, utilisez la méthode `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` permettant d'interroger le statut du corpus. Cette méthode accepte l'ID du modèle et le nom du corpus, comme illustré dans l'exemple suivant :

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/corpora/corpus1"
```
{: pre}

La réponse comprend le statut du corpus :

```javascript
{
  "name": "corpus1",
  "total_words": 5037,
  "out_of_vocabulary_words": 401,
  "status": "analyzed"
}
```
{: codeblock}

La zone `status` a l'une des valeurs suivantes :

-   `analyzed` indique que l'analyse du corpus par le service a abouti.
-   `being_processed` indique que le service est encore en train d'analyser le corpus.
-   `undetermined` indique que le service a rencontré une erreur lors du traitement du corpus.

Utilisez une boucle pour vérifier le statut du corpus toutes les 10 secondes jusqu'à ce qu'il passe à `analyzed`. Pour plus d'informations sur la vérification de statut des corpus d'un modèle, voir [Affichage de la liste des corpus d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).

## Ajout de mots au modèle de langue personnalisé
{: #addWords}

Bien que l'ajout de corpus soit la méthode recommandée pour ajouter des mots à un modèle de langue personnalisé, vous pouvez également ajouter directement des mots personnalisés individuels au modèle. Le service ajoute ces mots au modèle personnalisé de la même manière que les mots OOV qu'il a reconnus dans les corpus.

Si vous n'avez qu'un seul mot ou quelques mots à ajouter au modèle, l'utilisation de corpus pour ajouter les mots n'apparaît pas comme une solution pratique ou viable. L'approche la plus simple est d'ajouter un mot avec son orthographe. Mais vous pouvez également fournir plusieurs prononciations du mot et indiquer comment il doit être affiché.

-   Pour plus d'informations sur l'ajout direct de mots, voir [Utilisation des mots personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingWords).
-   Pour en savoir plus sur comment le service ajoute des mots personnalisés à un modèle, voir [Que se passe-t-il lorsque j'ajoute ou modifie un mot personnalisé ?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseWord)

Vous pouvez utiliser les méthodes suivantes pour ajouter des mots à un modèle personnalisé :

-   La méthode `POST /v1/customizations/{customization_id}/words` ajoute plusieurs mots à la fois. Vous transmettez un objet JSON qui fournit des informations sur chaque mot via le corps de la demande. L'exemple suivant ajoute deux mots personnalisés, `HHonors` et `IEEE`, au modèle personnalisé avec l'ID spécifié. L'en-tête `Content-Type` indique que les données JSON sont transmises à la méthode.

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

    Vous pouvez également ajouter ces mots à partir d'un fichier. Par exemple, le fichier `words.json` définit ces deux mots personnalisés.

    ```
    {"words":
      [
        {"word": "HHonors", "sounds_like": ["hilton honors", "H. honors"], "display_as": "HHonors"},
        {"word": "IEEE", "sounds_like": ["I. triple E."]}
      ]
    }
    ```
    {: codeblock}

    La commande suivante ajoute les mots à partir du fichier :

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data-binary @words.json
    "{url}/v1/customizations/{customization_id}/words"
    ```
    {: pre}

    Cette méthode est asynchrone. Sa durée d'exécution dépend du nombre de mots que vous ajoutez et de la charge en cours sur le service. Pour plus d'informations sur la vérification du statut de l'opération, voir [Surveillance de la demande d'ajout de mots](#monitorWords).
-   La méthode `PUT /v1/customizations/{customization_id}/words/{word_name}` ajoute des mots individuels. Vous transmettez un objet JSON qui fournit des informations sur le mot. L'exemple suivant ajoute le mot `NCAA` au modèle avec l'ID spécifié. L'en-tête `Content-Type` indique à nouveau que les données JSON sont transmises à la méthode.

    ```bash
    curl -X PUT
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data "{\"sounds_like\": [\"N. C. A. A.\", \"N. C. double A.\"]}"
    "{url}/v1/customizations/{customization_id}/words/NCAA"
    ```
    {: pre}

    Cette méthode est synchrone. Le service renvoie un code de réponse qui indique le succès ou la réussite d'une demande immédiatement.

Comme pour l'ajout de corpus, examinez les nouveaux mots personnalisés pour rechercher d'éventuelles erreurs typographiques ou d'autres erreurs. Cette vérification est importante lorsque vous ajoutez plusieurs mots en même temps. Pour plus d'informations, voir [Validation d'une ressource de mots](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).

### Surveillance de la demande d'ajout de mots
{: #monitorWords}

Lorsque vous utilisez la méthode `POST /v1/customizations/{customization_id}/words`, le service renvoie le code de réponse 201 si les données d'entrée sont valides. Il traite ensuite les mots de manière asynchrones pour les ajouter au modèle. L'opération est en général plus rapide que l'ajout d'un corpus ou l'entraînement d'un modèle, mais sa durée dépend du nombre de mots nouveaux que vous ajoutez et de la charge en cours sur le service. Vous ne pouvez pas soumettre des demandes d'ajout de données au modèle personnalisé, ni entraîner le modèle tant que le service n'a pas terminé la demande d'ajout des mots nouveaux.

Pour déterminer le statut de la demande, utilisez la méthode `GET /v1/customizations/{customization_id}` pour interroger le statut du modèle. La méthode accepte l'ID de personnalisation du modèle et renvoie les informations avec le statut du modèle, comme illustré dans l'exemple suivant :

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

La zone `status` indique l'état en cours du modèle. Tant que le service traite les mots nouveaux, le statut reste `pending`. Utilisez une boucle pour vérifier le statut toutes les 10 secondes jusqu'à ce qu'il passe à `ready` pour indiquer que l'opération est terminée. Pour plus d'informations sur les valeurs possibles pour `status`, voir [Surveillance de la demande d'entraînement du modèle](#monitorTraining-language).

### Modification des mots dans un modèle personnalisé
{: #modifyWord}

Vous pouvez également utiliser les méthodes `POST /v1/customizations/{customization_id}/words` et `PUT /v1/customizations/{customization_id}/words/{word_name}` pour modifier ou compléter un mot dans un modèle personnalisé. Vous serez peut-être amené à utiliser ces méthodes pour corriger une erreur typographique ou une autre faute qui s'est glissée lorsque le mot a été ajouté au modèle. Il vous faudra peut-être également ajouter des définitions de prononciations possibles pour un mot existant.

Vous utilisez ces méthodes pour modifier la définition d'un mot existant exactement de la même manière que vous procédez pour ajouter un mot. Les nouvelles données que vous fournissez au mot remplacent la définition existante du mot.

## Entraînement du modèle de langue personnalisé
{: #trainModel-language}

Lorsque vous avez alimenté un modèle de langue personnalisé avec des mots nouveaux (en ajoutant des corpus, des grammaires ou par ajout direct de mots), vous devez entraîner le modèle sur les nouvelles données. Cet entraînement prépare le modèle personnalisé à utiliser ces données dans la reconnaissance vocale. Le modèle n'utilise pas les mots que vous ajoutez avec la méthode de votre choix, tant que vous ne l'entraînez pas sur les données.

Pour entraîner un modèle personnalisé, vous utilisez la méthode `POST /v1/customizations/{customization_id}/train`. Vous transmettez à la méthode, l'ID de personnalisation (customization_id) du modèle que vous souhaitez entraîner, comme illustré dans l'exemple suivant :

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/train"
```
{: pre}

Cette méthode est asynchrone. L'entraînement peut prendre quelques minutes en fonction du nombre de mots nouveaux sur lesquels est entraîné le modèle et de la charge en cours sur le service. Pour plus d'informations sur la vérification du statut d'une opération d'entraînement, voir [Surveillance de la demande d'entraînement du modèle](#monitorTraining-language).

La méthode inclut les paramètres de requête facultatifs suivants :

-   Le paramètre `word_type_to_add` spécifie les mots sur lesquels le modèle personnalisé doit être formé :
    -   Spécifiez `all` ou omettez ce paramètre pour entraîner le modèle sur tous les mots qu'il comporte, quelle que soit leur origine.
    -   Spécifiez `user` pour entraîner le modèle uniquement sur les mots qui ont été ajoutés ou modifiés par l'utilisateur, en ignorant les mots qui ont été extraits uniquement à partir des corpus ou des grammaires.

    Cette option s'avère utile si vous ajoutez des corpus avec des données bruitées, par exemple des mots contenant des erreurs typographiques. Avant d'entraîner le modèle sur des données de ce type, utilisez le paramètre de requête `word_type` de la méthode `GET /v1/customizations/{customization_id}/words` pour réviser les mots extraits de corpus ou de grammaires. Pour plus d'informations, voir [Affichage de la liste des mots d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).
-   Le paramètre `customization_weight` indique le poids relatif attribué aux mots du modèle personnalisé par opposition aux mots du vocabulaire de base lorsque le modèle personnalisé est utilisé pour la reconnaissance vocale. Vous pouvez également indiquer un poids de personnalisation avec toutes les demandes de reconnaissance utilisant le modèle personnalisé. Pour plus d'informations, voir [Utilisation d'un poids de personnalisation](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse#weight).
-   Le paramètre `strict` indique si l'entraînement doit se poursuivre si le modèle personnalisé contient un mélange de ressources valides et non valides (corpus, grammaires et mots). Par défaut, la formation échoue si le modèle contient une ou plusieurs ressources non valides. Définissez le paramètre sur `false` pour permettre à l'entraînement de se poursuivre tant que le modèle contient au moins une ressource valide. Le service exclut les ressources non valides de l'entraînement. Pour plus d'informations, voir [Echecs d'entraînement](#failedTraining-language).

### Surveillance de la demande d'entraînement du modèle
{: #monitorTraining-language}

Le service renvoie le code de réponse 200 s'il a initié avec succès le processus d'entraînement. Il n'accepte pas d'autres demandes d'entraînement ou des demandes d'ajout de nouveaux corpus, de nouvelles grammaires ou de mots nouveaux, tant que la demande existante n'est pas terminée.

Pour déterminer le statut d'une demande d'entraînement, utilisez la méthode `GET /v1/customizations/{customization_id}` pour interroger le statut du modèle. La méthode accepte l'ID de personnalisation du modèle et renvoie des informations concernant le modèle.

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

La réponse comprend les zones `status` et `progress` qui indiquent l'état du modèle personnalisé. La signification de la zone `progress` dépend du statut du modèle. La zone `status` peut avoir l'une des valeurs suivantes :

-   `pending` indique que le modèle a été créé mais attend que des données d'entraînement valides soient ajoutées ou que le service termine l'analyse des données qui ont été ajoutées. La zone `progress` a la valeur `0`.
-   `ready` indique que le modèle contient des données valides et qu'il est prêt à être entraîné. La zone `progress` a la valeur `0`.

Si le modèle contient un mélange de ressources valides et non valides (par exemple, des mots personnalisés valides et non valides), l'entraînement du modèle échoue sauf si vous définissez le paramètre de requête `strict` sur `false`. Pour plus d'informations, voir [Echecs d'entraînement](#failedTraining-language).
-   `training` indique que le modèle est en cours d'entraînement. La zone `progress` passe de `0` à `100` lorsque l'entraînement est terminé. <!-- The `progress` field indicates the progress of the training as a percentage complete. -->
-   `available` indique que l'entraînement du modèle est terminé et que le modèle est prêt à l'emploi. La zone `progress` a la valeur `100`.
-   `upgrading` indique que le modèle est en cours de mise à niveau. La zone `progress` a la valeur `0`.
-   `failed` indique que l'entraînement du modèle a échoué. La zone `progress` a la valeur `0`. Pour plus d'informations, voir [Echecs d'entraînement](#failedTraining-language).

Utilisez une boucle pour vérifier le statut toutes les 10 secondes jusqu'à ce qu'il passe à `available`. Pour plus d'informations sur la vérification du statut d'un modèle personnalisé, voir [Affichage de la liste des modèles de langue personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).

### Echecs d'entraînement
{: #failedTraining-language}

L'entraînement ne parvient pas à démarrer si le service traite une autre demande pour le modèle de langue personnalisé. Par exemple, une demande d'entraînement échoue avec un code de statut 409 si le service est en train d'effectuer les opérations suivantes :

-   Traitement d'un corpus ou d'une grammaire pour générer une liste de mots OOV (Out Of Vocabulary)
-   Traitement de mots personnalisés pour valider ou générer automatiquement des prononciations possibles
-   Traitement d'une autre demande d'entraînement

L'entraînement échoue également avec un code de statut 400 si le modèle personnalisé : 

-   Ne contient aucune nouvelle donnée d'entraînement valide (corpus, grammaires ou mots) depuis sa création ou son dernier entraînement 
-   Contient un ou plusieurs corpus, grammaires ou mots non valides (par exemple, un mot personnalisé a une prononciation non valide semblable à un son) 

Si la demande d'entraînement échoue avec un code de statut 400, le service définit le statut du modèle personnalisé sur `failed`. Effectuez
l'une des actions ci-dessous :

-   Utilisez des méthodes de l'interface de personnalisation pour examiner les ressources du modèle et corriger les erreurs que vous trouvez : 
    -   Pour un corpus non valide, vous pouvez corriger le fichier texte du corpus et utiliser le paramètre `allow_overwrite` de la méthode `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` pour ajouter le fichier corrigé au modèle. Pour plus d'informations, voir [Ajout d'un corpus au modèle de langue personnalisé](#addCorpus).
    -   Pour une grammaire non valide, vous pouvez corriger le fichier texte de la grammaire et utiliser le paramètre `allow_overwrite` de la méthode `POST /v1/customizations/{customization_id}/grammars/{grammar_name}` pour ajouter le fichier corrigé au modèle. Pour plus d'informations, voir [Ajout d'une grammaire au modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
    -   Pour un mot personnalisé non valide, vous pouvez utiliser la méthode `POST /v1/customizations/{customization_id}/words` ou `PUT /v1/customizations/{customization_id}/words/{word_name}` pour modifier le mot directement dans la ressource de mots du modèle. Pour plus d'informations, voir [Modification des mots dans un modèle personnalisé](#modifyWord).

Pour plus d'informations sur la validation des mots dans un modèle de langue personnalisé, voir [Validation d'une ressource de mots](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).
-   Définissez le paramètre `strict` de la méthode `POST /v1/customizations/{customization_id}/train` sur `false` pour exclure les ressources non valides de l'entraînement. Le modèle doit contenir au moins une ressource valide (corpus, grammaire ou mot) pour que l'entraînement aboutisse. Le paramètre `strict` permet d'entraîner un modèle personnalisé contenant un mélange de ressources valides et non valides.
