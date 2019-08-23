---

Copyright:
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

# A propos de
{: #about}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} fournit des fonctions de reconnaissance vocale pour vos applications. Le service tire parti de l'apprentissage automatique pour combiner les connaissances grammaticales et morphologiques du langage et la composition des signaux audio et vocaux afin d'obtenir une transcription précise de la voix humaine. Il met à jour et affine sa transcription en mode continu à mesure qu'il reçoit les paroles.
{: shortdesc}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} fournit différentes interfaces qui lui permettent de s'adapter à toute application avec des paroles en entrée et une retranscription textuelle en sortie. Exemples d'applications :

-   Contrôle vocal des applications, des appareils embarqués et des accessoires automobiles
-   Transcription des réunions et des conférences téléphoniques
-   Dictée de courriers électroniques et de notes

Le service est idéal pour les clients qui doivent extraire des transcriptions vocales de haute qualité de l'audio du centre d'appels. Les clients des secteurs tels que les services financiers, les soins de santé, les assurances et les télécommunications peuvent développer des applications dans le cloud pour le service client, la voix client, l'assistance d'agent et d'autres solutions. 

Pour plus d'informations sur l'installation et la configuration de {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, voir [Installation du service](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} est basé sur le service {{site.data.keyword.speechtotextfull}} sur {{site.data.keyword.cloud_notm}} public. Pour plus d'informations sur le service public, voir [A propos de {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.
{: note}

## Interfaces prises en charge
{: #interfaces}

Le service {{site.data.keyword.speechtotextshort}} offre plusieurs interfaces pour la reconnaissance vocale :

-   Une [interface WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) pour établir des connexions permanentes, en duplex intégral et à faible temps d'attente avec le service. Vous pouvez transmettre une quantité maximale de 100 Mo de données audio au service avec une seule demande.
-   Une [interface HTTP synchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) pour les appels HTTP de base au service. Vous pouvez transmettre une quantité maximale de 100 Mo de données audio avec une demande.
-   Une [interface HTTP asynchrone](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) pour les appels non bloquants au service. Vous pouvez transmettre jusqu'à 1 Go de données audio avec une demande.

Le service propose également une [interface de personnalisation](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) que vous pouvez utiliser pour optimiser la reconnaissance vocale en fonction de votre langue et en tenant compte de vos exigences acoustiques. Vous pouvez enrichir le vocabulaire d'un modèle avec une terminologie spécifique à un domaine ou adapter un modèle aux caractéristiques acoustiques de vos données audio. Vous pouvez également ajouter des [grammaires](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) pour limiter les expressions reconnaissables par le service.

-   Pour plus d'informations sur la création de demandes avec chacune des interfaces {{site.data.keyword.speechtotextshort}}, voir [Demandes au service](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Pour obtenir des exemples de demandes de reconnaissance vocale de base pour chacune des interfaces du service, voir [Effectuer une demande de reconnaissance](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Pour obtenir une description détaillée du développement d'application avec le service, voir [Présentation destinée aux développeurs](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).

Des logiciels SDK sont disponibles dans de nombreux langages de programmation pour vous faciliter la tâche lorsque vous utilisez le service. Pour plus d'informations, reportez-vous à la rubrique [Référence d'API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Fonctions d'entrée
{: #inputFeatures}

Les interfaces du service partagent de nombreuses fonctions d'entrée communes pour la transcription parole-texte :

-   [Formats audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats) - Vous pouvez transcrire des données audio au format Ogg ou WebM (Web Media) avec le codec Opus ou Vorbis, MP3 (ou MPEG), Waveform Audio File Format (WAV), Free Lossless Audio Codec (FLAC), PCM (Pulse-Code Modulation) linéaire 16 bits, G.729, A-law, mu-law (ou u-law) et basic audio. En utilisant un format prenant en charge la compression, vous pouvez maximiser la quantité de données audio que vous pouvez envoyer avec une demande.
-   [Langues et modèles](/docs/services/speech-to-text-data?topic=speech-to-text-data-models) - Vous pouvez transcrire des données audio en utilisant des modèles à large bande ou à bande étroite. Les modèles à large bande conviennent aux données audio échantillonnées à une fréquence minimale de 16 kHz. Utilisez des modèles à bande étroite pour les données audio échantillonnées à une fréquence minimale de 8 kHz.
-   [Transmission audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission) - Vous pouvez effectuer une transmission audio en diffusion continue de blocs de données ou en diffusion ponctuelle transmettant la totalité des données en une seule fois. Avec la diffusion en continu, le service impose des [délais d'attente](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts) d'inactivité et de session.

## Fonctions de sortie
{: #outputFeatures}

La plupart des interfaces prennent également en charge les fonctions de sortie communes suivantes :

-   Les [étiquettes de locuteur (speaker labels)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels) reconnaissent différents locuteurs audio de l'anglais américain, du japonais ou de l'espagnol. La transcription identifie les contributions de chaque locuteur d'une conversation à plusieurs intervenants. (Fonctionnalité bêta.)
-   La [détection de mots clés (keyword spotting)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting) identifie des expressions parlées correspondant à des chaînes de mots clés spécifiées selon un niveau de confiance défini par l'utilisateur. La détection de mots clés est particulièrement utile lorsque des expressions individuelles dans les données audio sont plus importantes que la transcription globale. Par exemple, un système de support clientèle peut identifier les mots clés permettant de déterminer comment acheminer les demandes des utilisateurs.
-   Les [résultats intermédiaires (interim results)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim) renvoient des hypothèses continuellement affinées au fur et à mesure des progrès de la transcription. Le service renvoie les résultats finaux lorsque la transcription est terminée. Les résultats intermédiaires sont disponibles uniquement avec l'interface WebSocket.
-   Le [nombre maximal d'alternatives (max alternatives)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives) fournit d'autres retranscriptions possibles. Le service indique les résultats finaux auxquels il accorde le plus haut niveau de confiance.
-   Les [autres propositions de mots (word alternatives)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives) demandent d'autres propositions de mots avec des caractéristiques acoustiques similaires aux mots d'une retranscription.
-   Le [confiance des mots (word confidence)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence) renvoie des niveaux de confiance pour chaque mot d'une retranscription.
-   Les [horodatages de mots (word timestamps)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps) renvoient des horodatages pour le début et la fin de chaque mot d'une retranscription.
-   Le [formatage intelligent (smart formatting)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting) convertit des dates, des heures, des nombres, des valeurs de devise, des numéros de téléphone et des adresses Internet sous forme plus lisible et plus conventionnelle dans les retranscriptions finales. Pour l'anglais américain, vous pouvez également fournir des groupes de mots clés pour inclure certains signes de ponctuation dans les retranscriptions finales. Le formatage intelligent est pris en charge pour les données audio en anglais américain, en japonais et en espagnol. (Fonctionnalité bêta.)
-   L'[occultation numérique (numeric redaction)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction) occulte, ou masque, les données numériques dans une retranscription finale. L'occultation est conçue pour supprimer des informations personnelles sensibles, comme les numéros de carte de crédit, dans les retranscriptions. Cette fonction est prise en charge pour les données audio en anglais américain, en japonais et en coréen. (Fonctionnalité bêta.)
-   Le [filtrage des grossièretés (profanity filtering)](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter) censure les grossièretés des retranscriptions en anglais américain.
-   Les [métriques de traitement](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) (Processing metrics) fournissent des informations de synchronisation détaillées sur l'analyse de l'audio d'entrée par le service. 
-   Les [métriques audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) (Audio metrics) fournissent des informations détaillées sur les caractéristiques de signal de l'entrée audio. 

## Support de langue
{: #languages}

Le service offre des modèles pour les langues suivantes : allemand, anglais britannique, anglais américain, arabe standard moderne, chinois mandarin, coréen, espagnol, français, japonais et portugais brésilien. Le service ne prend pas en charge toutes les fonctions pour toutes les langues. Cependant, il prend en charge certaines fonctions en version GA pour une utilisation en production et d'autres en tant qu'offres en version bêta pour les différentes langues.

-   Les interfaces WebSocket et HTTP synchrones et asynchrones sont disponibles en version GA pour toutes les langues.
-   Le service offre à la fois des modèles à large bande et des modèles à bande étroite pour toutes les langues. Pour plus d'informations, voir [Langues et modèles](/docs/services/speech-to-text-data?topic=speech-to-text-data-models).
-   Certaines fonctions de reconnaissance vocale sont disponibles uniquement pour certaines langues et uniquement avec certaines interfaces. Pour plus d'informations, voir [Récapitulatif des paramètres](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   L'interface de personnalisation du modèle de langue est disponible en version GA pour toutes les langues. L'interface de personnalisation de modèle acoustique est disponible en fonctionnalité bêta pour toutes les langues. Pour plus d'informations, voir [Support de langue pour la personnalisation](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).

## Expérimentation du service
{: #tryOut}

Pour obtenir des exemples de fonctionnement du service {{site.data.keyword.speechtotextshort}}, voir

-   Une [démonstration rapide](https://speech-to-text-demo.ng.bluemix.net/){: external} qui transcrit le texte à partir d'une entrée audio en continu ou d'un fichier que vous téléchargez.
-   Les applications dans les [Kits de démarrage](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} d'{{site.data.keyword.ibmwatson}} qui proposent une démonstration du service.
-   L'article de blogue {{site.data.keyword.watson}} [Getting robots to listen: Using {{site.data.keyword.watson}}'s {{site.data.keyword.speechtotextshort}} service](https://www.ibm.com/blogs/watson/2016/07/getting-robots-listen-using-watsons-speech-text-service/){: external} qui montre comment utiliser l'interface WebSocket du service avec Python pour extraire des paroles d'une séquence audio. Cet article fournit un tutoriel complet qui présente le code et la procédure à suivre.
