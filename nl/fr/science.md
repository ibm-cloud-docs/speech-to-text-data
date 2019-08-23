---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

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

# Contexte scientifique du service
{: #science}

Comme décrit dans [Pioneering Speech Recognition](https://www.ibm.com/ibm/history/ibm100/us/en/icons/speechreco/){: external}, {{site.data.keyword.IBM}} est à l'avant-garde de la recherche sur la reconnaissance vocale depuis le début des années 60. Par exemple, [Bahl, Jelinek et Mercer (1983)](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#bahl1983) décrivent l'approche mathématique de base de la reconnaissance vocale employée dans l'ensemble des systèmes de reconnaissance vocale modernes. [Jelinek (1985)](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#jelinek1985) décrit la création du premier système de reconnaissance vocale à vocabulaire étendu en temps réel pour la dictée. Ce document décrit également des problèmes qui restent des sujets de recherche non résolus à ce jour.
{: shortdesc}

{{site.data.keyword.IBM_notm}} poursuit cette riche tradition de recherche et développement avec {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. {{site.data.keyword.IBM_notm}} a démontré la précision de la reconnaissance vocale d'excellence de l’industrie sur les jeux de données de référence publics pour la transcription Conversational Telephone Speech (CTS) ([Saon et al., 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#saon2017)) et Broadcast News (BN) ([Thomas et al., 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#thomas2019)). {{site.data.keyword.IBM_notm}} a tiré parti des réseaux de neurones pour la modélisation linguistique ([Kurata et al., 2017a](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2017a) et [Kurata et al., 2017b](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2017a)), en plus de démontrer l'efficacité de la modélisation acoustique. 

Les annonces suivantes résument les réalisations récentes de {{site.data.keyword.IBM_notm}} en matière de reconnaissance vocale : 

-   [Reaching new records in speech recognition](https://www.ibm.com/blogs/watson/2017/03/reaching-new-records-in-speech-recognition/){: external}
-   [{{site.data.keyword.IBM_notm}} Breaks Industry Record for Conversational Speech Recognition by Extending Deep Learning Technologies](https://www-03.ibm.com/press/us/en/pressrelease/51790.wss){: external}
-   [{{site.data.keyword.IBM_notm}} Sets New Transcription Performance Milestone on Automatic Broadcast News Captioning](https://www.ibm.com/blogs/research/2019/05/automatic-broadcast-news-captioning/){: external}

Ces réalisations contribuent à faire progresser les services vocaux de {{site.data.keyword.IBM_notm}}. Parmi les idées récentes qui conviennent le mieux au service {{site.data.keyword.speechtotextshort}} basé sur le cloud, notons : 

-   *Pour la modélisation du langage, * {{site.data.keyword.IBM_notm}} utilise un modèle de langage basé sur un réseau neuronal pour générer un texte d'entraînement ([Suzuki et al., 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#suzuki2019)).
-   *Pour la modélisation acoustique,* {{site.data.keyword.IBM_notm}} utilise un modèle assez compact pour tenir compte des limites de ressources du cloud. Pour former ce modèle compact, {{site.data.keyword.IBM_notm}} utilise la "formation étudiant-élève / la distillation des connaissances". Les réseaux neuronaux volumineux et puissants tels que la mémoire à court terme (LSTM), VGG et le réseau résiduel (ResNet) sont d'abord formés. La sortie de ces réseaux est ensuite utilisée comme signal d'enseignement pour former un modèle compact en vue d’un déploiement réel ([Fukuda et al., 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#fukuda2017)).

Pour aller encore plus loin, {{site.data.keyword.IBM_notm}} se concentre également sur la modélisation de bout en bout. Par exemple, il a mis en place un solide pipeline de modèles pour les modèles directs acoustique-mot ([Audhkhasi et al., 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#audhkhasi2017) et [Audhkhasi et al., 2018](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#audhkhasi2018)) qu’il continue à améliorer ([Saon et al., 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#saon2019)). Il s'efforce également de créer des modèles compacts de bout en bout pour un déploiement futur dans le cloud ([Kurata and Audhkhasi, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2019)).

Pour plus d'informations sur la recherche scientifique à l'origine de ce service, voir les documents répertoriés dans [Références de recherche](/docs/services/speech-to-text-data?topic=speech-to-text-data-references).
