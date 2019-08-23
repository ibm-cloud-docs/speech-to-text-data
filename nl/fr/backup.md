---

copyright:
  years: 2019
lastupdated: "2019-06-22"

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

# Sauvegarde et restauration
{: #backup}

Pour récupérer des sinistres potentiels, vous devez sauvegarder et être prêt à restaurer {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. Il vous appartient de bien connaître la configuration, la personnalisation et l'utilisation du service. Il vous incombe également d'être prêt à créer à nouveau une instance du service et de restaurer vos données.
{: shortdesc}

La reprise après incident peut devenir problématique si votre solution de cloud connaît une défaillance importante, notamment la perte potentielle des données. En cas de perte de données, vous devez restaurer vos données pour rétablir votre instance de service à son état le plus récent. 

Pour le service {{site.data.keyword.speechtotextshort}}, les données des modèles de langue personnalisés, des modèles acoustiques personnalisés et des demandes de reconnaissance vocale asynchrones sont stockées dans le cloud. Votre plan de reprise après incident comprend la connaissance, la conservation et la préparation à la restauration de ces données. 

Recréer des modèles personnalisés, notamment des modèles acoustiques personnalisés, à partir de données sauvegardées peut prendre beaucoup de temps. Assurer des configurations de services parallèles à plusieurs emplacements peut éliminer le délai de réponse associé à une reprise après incident.
{: note}

### Reprise après incident pour les modèles de langues personnalisés
{: #disaster-recovery-language}

Pour les modèles de langue personnalisés, vous devez conserver vos modèles de langue personnalisés et être disposé à les recréer et à les restaurer avec leurs corpus, leurs grammaires et leurs mots personnalisés. Vous devez également être prêt à entraîner à nouveau vos modèles de langue personnalisés sur leurs données et leurs ressources de mots.

#### Sauvegarde des modèles de langue personnalisés
{: #disaster-recovery-language-backup}

Conservez les informations suivantes sur vos modèles de langue personnalisés :

-   Une liste de tous vos modèles de langue personnalisées et leurs définitions. Pour répertorier les informations sur vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/customizations` pour répertorier les informations sur tous les modèles personnalisés.
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}` pour répertorier les informations concernant un modèle personnalisé spécifié.

Pour plus d'informations, voir [Affichage de la liste des modèles de langue personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).
-   Des copies de tous les fichiers texte de corpus que vous ajoutez à vos modèles de langue personnalisés. Pour répertorier les informations sur les corpus de vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/corpora` pour répertorier tous les corpus d'un modèle personnalisé.
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` pour répertorier les informations sur un corpus spécifié pour un modèle personnalisé.

    Pour plus d'informations, voir [Affichage de la liste des corpus d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).
-   Des copies de tous les fichiers de grammaire que vous ajoutez à vos modèles de langue personnalisés. Pour répertorier les informations sur les grammaires de vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/grammars` pour répertorier les informations sur toutes les grammaires d'un modèle personnalisé.
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/grammars/{grammar_name}` pour répertorier les informations sur une grammaire spécifiée pour un modèle personnalisé.

    Pour plus d'informations, voir [Affichage de la liste des grammaires d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageGrammars#listGrammars).
-   Des informations sur tous les mots personnalisés, notamment leurs définitions sounds-like et display-as, que vous ajoutez directement dans vos modèles de langue personnalisés. Pour répertorier les informations sur les mots OOV (Out-Of-Vocabulary) de vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/words` pour répertorier les informations sur les mots d'un modèle personnalisé. Vous pouvez utiliser le paramètre `word_type` pour afficher la liste de tous (`all`) les mots d'un modèle, des mots ajoutés directement par l'utilisateur (`user`), des mots extraits des corpus (`corpora`) ou des mots reconnus par des grammaires (`grammars`).
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/words/{word_name}` pour répertorier les informations sur un mot spécifié dans un modèle personnalisé.

    Pour plus d'informations, voir [Affichage de la liste des mots d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).

Il est recommandé de conserver ces informations dans un format que vous pouvez utiliser pour recréer vos modèles de langue personnalisés en cas d'incident. Conserver de manière active les informations relatives à vos modèles personnalisés et leurs données, et préparer à l'avance les appels indiqués dans la section suivante, sont des opérations qui vous permettent d'assurer une restauration dans les plus brefs délais.

#### Restauration des modèles de langue personnalisés
{: #disaster-recovery-language-restore}

Pour assurer la reprise après un incident, vous pouvez utiliser des informations de sauvegarde pour recréer vos modèles de langue personnalisés et leurs données :

1.  Pour recréer vos modèles de langue personnalisés, utilisez la méthode `POST /v1/customizations`. Pour plus d'informations, voir [Création d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language).
1.  Pour ajouter les fichiers texte de corpus à vos modèles personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`. Pour plus d'informations, voir [Ajout d'un corpus au modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addCorpus).
1.  Pour ajouter des fichiers de grammaire à vos modèles personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`. Pour plus d'informations, voir [Ajout d'une grammaire au modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
1.  Pour ajouter plusieurs mots à vos modèles personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/words`. Pour ajouter des mots uniques à vos modèles personnalisés, utilisez la méthode `PUT /v1/customizations/{customization_id}/words/{word_name}`. Pour plus d'informations, voir [Ajout de mots au modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addWords).
1.  Pour entraîner vos modèles personnalisés dès que vous restaurez vos corpus, grammaires et mots personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/train`. Pour plus d'informations, voir [Entraînement du modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language).

Les méthodes que vous utilisez pour ajouter des corpus, des grammaires et des mots, ainsi que pour entraîner un modèle de langue personnalisé sont asynchrones. Vous devez surveiller les demandes jusqu'à ce qu'elles soient terminées.

Vous pouvez ajouter des données de manière incrémentielle et entraîner vos modèles de langue personnalisés au lieu d'ajouter toutes les données avant d'entraîner les modèles. Vous pouvez, par exemple, ajouter vos corpus, puis entraîner vos modèles avant d'ajouter des grammaires et des mots individuels. Vous pouvez également ajouter et entraîner vos modèles sur des fichiers texte de corpus, des fichiers de grammaire et des groupes de mots personnalisés de manière incrémentielle.

### Reprise après incident des modèles acoustiques personnalisés
{: #disaster-recovery-acoustic}

Pour les modèles acoustiques personnalisés, vous devez conserver vos modèles acoustiques personnalisés et être disposé à les recréer et à les restaurer avec leurs corpus et leurs ressources audio. Vous devez également être prêt à entraîner à nouveau vos modèles acoustiques personnalisés sur leurs ressources audio.

#### Sauvegarde de vos modèles acoustiques personnalisés
{: #disaster-recovery-acoustic-backup}

Conservez les informations suivantes sur vos modèles acoustiques personnalisés :

-   Une liste de tous vos modèles acoustiques personnalisées et leurs définitions. Pour répertorier les informations sur vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/acoustic_customizations` pour répertorier les informations sur tous les modèles personnalisés.
    -   Utilisez la méthode `GET /v1/acoustic_customizations/{customization_id}` pour répertorier les informations concernant un modèle personnalisé spécifié.

Pour plus d'informations, voir [Affichage de la liste des modèles acoustiques personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic).
-   Des copies de toutes les ressources audio, qu'il s'agisse des fichiers audio individuels ou des fichiers archive, que vous ajoutez à vos modèles acoustiques personnalisés. Pour répertorier les informations sur les ressources audio de vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/acoustic_customizations/{customization_id}/audio` pour répertorier les informations sur toutes les ressources audio d'un modèle personnalisé.
    -   Utilisez la méthode `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` pour répertorier les informations sur une ressource audio spécifiée pour un modèle personnalisé.

    Pour plus d'informations, voir [Affichage de la liste des ressources audio d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

Il est recommandé de conserver ces informations dans un format que vous pouvez utiliser pour recréer vos modèles acoustiques personnalisés en cas d'incident. Conserver de manière active les informations relatives à vos modèles personnalisés et leurs ressources audio, et préparer à l'avance les appels indiqués dans la section suivante, sont des opérations qui vous permettent d'assurer une restauration dans les plus brefs délais.

#### Restauration de vos modèles acoustiques personnalisés
{: #disaster-recovery-acoustic-restore}

Pour assurer la reprise après un incident, vous pouvez utiliser des informations de sauvegarde pour recréer vos modèles acoustiques personnalisés et leurs données :

1.  Pour recréer vos modèles acoustiques personnalisés, utilisez la méthode `POST /v1/acoustic_customizations`. Pour plus d'informations, voir [Création d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic).
1.  Pour ajouter les ressources audio à vos modèles personnalisés, utilisez la méthode `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`. Pour plus d'informations, voir [Ajout de données audio au modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio).
1.  Pour entraîner vos modèles personnalisés dès que vous restaurez vos ressources audio, utilisez la méthode `POST /v1/acoustic_customizations/{customization_id}/train`. Pour plus d'informations, voir [Entraînement du modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic).

Les méthodes que vous utilisez pour ajouter des ressources audio et entraîner un modèle acoustique personnalisé sont asynchrones. Vous devez surveiller les demandes jusqu'à ce qu'elles soient terminées.

Vous pouvez ajouter des ressources audio de manière incrémentielle et entraîner vos modèles acoustiques personnalisés au lieu d'ajouter toutes les données avant d'entraîner les modèles. Vous pouvez, par exemple, ajouter vos ressources audio une par une ou les regrouper, en entraînant vos modèles sur des sous-ensembles de ressources audio au lieu de les entraîner sur toutes les données audio en une seule fois.

### Reprise après incident pour des travaux de reconnaissance vocale asynchrones
{: #disaster-recovery-async}

Dans le cadre d'une reconnaissance vocale avec l'interface HTTP asynchrone, vous devez conserver les informations suivantes :

-   Toutes les URL de rappel sur liste blanche à utiliser avec l'interface asynchrone. En cas d'incident, il vous faudra peut-être utiliser la méthode `POST /v1/register_callback` pour enregistrer à nouveau les URL. Cette méthode renvoie une réponse appropriée si l'URL figure déjà sur la liste blanche.
-   Des copies des fichiers audio que vous soumettez à l'interface asynchrone pour la reconnaissance vocale. En cas d'incident avant de recevoir ou de récupérer les résultats d'un travail asynchrone terminé, vous devez utiliser la méthode `POST /v1/recognitions` pour soumettre à nouveau les fichiers audio lorsque le service est restauré. Après avoir récupéré les résultats d'un travail asynchrone terminé, vous n'avez plus besoin de conserver les fichiers audio.

Pour plus d'informations, voir [L'interface HTTP asynchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-async). A l'instar des données de sauvegarde des modèles personnalisés, vous pouvez conserver ces informations de manière active et vous préparer à l'avance à relancer les demandes nécessaires.
