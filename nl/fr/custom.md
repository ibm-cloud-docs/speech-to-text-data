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

# L'interface de personnalisation
{: #customization}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} offre une interface de personnalisation que vous pouvez utiliser pour étendre ses fonctions de reconnaissance vocale. Vous pouvez utiliser la personnalisation pour améliorer la précision des demandes de reconnaissance vocale en personnalisant un modèle de base pour votre domaine et vos données audio. La personnalisation du modèle de langue est généralement disponible pour toutes les langues ; la personnalisation du modèle acoustique est une fonctionnalité bêta pour toutes les langues. Pour plus d'informations, voir [Support de langue pour la personnalisation](#languageSupport).
{: shortdesc}

L'interface de personnalisation prend en charge les modèles de langue personnalisés et les modèles acoustiques personnalisés. Les interfaces correspondant à ces deux types de modèle sont semblables et simples à utiliser. L'utilisation des deux types de modèle personnalisé avec une demande de reconnaissance est également simple : il vous suffit d'indiquer l'ID de personnalisation du modèle avec la demande.

La reconnaissance vocale fonctionne de la même manière avec ou sans modèle personnalisé. Lorsque vous utilisez un modèle personnalisé pour la reconnaissance vocale, vous pouvez inclure tous les paramètres d'entrée et de sortie qui sont en principe disponibles avec une demande de reconnaissance. Pour plus d'informations sur tous les paramètres disponibles, voir [Récapitulatif des paramètres](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).

## Personnalisation de modèle de langue
{: #customLanguage-intro}

Le service a été développé à l'intention du grand public. Le vocabulaire de base du service contient de nombreux mots utilisés dans la conversation de tous les jours. Ses modèles offrent une reconnaissance suffisamment précise pour convenir à de nombreuses applications. Mais il leur manque parfois la connaissance de termes spécifiques associés à des domaines particuliers.

L'interface de *personnalisation de modèle de langue* peut améliorer la précision de la reconnaissance vocale dans des domaines tels que la médecine, le droit, les technologies de l'information, etc. En utilisant la personnalisation de modèle de langue, vous pouvez étendre et personnaliser le vocabulaire d'un modèle de base pour inclure une terminologie spécifique à un domaine.

Vous créez un modèle de langue personnalisé et ajoutez des corpus et des mots spécifiques à votre domaine. Lorsque vous avez entraîné le modèle de langue personnalisé avec votre vocabulaire enrichi, vous pouvez l'utiliser dans le cadre d'une reconnaissance vocale personnalisée. Le service peut en principe entraîner un modèle personnalisé en l'espace de quelques minutes. Le niveau d'effort nécessaire pour créer un modèle dépend des données dont vous disposez pour le modèle.

Pour plus d'informations, voir

-   [Création d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate)
-   [Utilisation d'un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse)

## Personnalisation de modèle acoustique
{: #customAcoustic-intro}

De même, le service a été développé avec des modèles acoustiques de base qui fonctionnent bien pour différentes caractéristiques audio. Mais dans certains cas, l'adaptation d'un modèle de base à vos données audio peut améliorer la reconnaissance vocale :

-   Votre environnement de canal acoustique est unique. Par exemple, l'environnement peut être bruyant, la qualité du micro ou son réglage peuvent laisser à désirer ou la qualité audio peut souffrir d'effets indirects.
-   Le langage parlé de vos locuteurs est atypique. Par exemple, un locuteur parle beaucoup trop vite ou la source audio comprend des conversations informelles.
-   Les accents de vos locuteurs sont marqués. Par exemple, votre source audio comprend des locuteurs qui ne parlent pas dans leur langue maternelle ou s'expriment dans une autre langue.

L'interface de *personnalisation de modèle acoustique* peut adapter un modèle de base à votre environnement et à vos locuteurs. Vous créez un modèle acoustique personnalisé et ajoutez des données audio (ressources audio) qui correspondent le plus à la signature acoustique des données audio que vous souhaitez transcrire. Lorsque vous avez entraîné le modèle acoustique personnalisé avec vos ressources audio, vous pouvez l'utiliser dans le cadre d'une reconnaissance vocale personnalisée.

La durée d'entraînement du modèle personnalisé par le service dépend de la quantité de données que contient le modèle. En général, l'entraînement dure deux fois plus longtemps que les données audio cumulées. Le niveau d'effort nécessaire pour créer un modèle dépend des données audio dont vous disposez pour le modèle. Il varie aussi selon que vous utilisiez ou non des transcriptions audio.

Pour plus d'informations, voir

-   [Création d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic)
-   [Utilisation d'un modèle acoustique personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-acousticUse)

## Grammaires
{: #grammars-intro}

Les modèles de langue personnalisés vous permettent d'enrichir le vocabulaire de base du service. Les *grammaires* vous permettent de limiter les mots que le service peut reconnaître à partir de ce vocabulaire. Lorsque vous utilisez une grammaire avec un modèle de langue personnalisé pour la reconnaissance vocale, le service ne reconnaît que les mots, les expressions et les chaînes reconnus par la grammaire. Comme la grammaire définit un espace de recherche limité pour les correspondances valides, le service peut délivrer des résultats plus rapides et plus précis.

Vous ajoutez une grammaire à un modèle de langue personnalisé et entraînez le modèle de la même manière que pour un corpus. Contrairement à un corpus, vous devez spécifier explicitement qu'une grammaire doit être utilisée avec un modèle personnalisé lors de la reconnaissance vocale.

Pour plus d'informations, voir

-   [Utilisation de grammaires avec des modèles de langue personnalisés](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars)
-   [Ajout d'une grammaire à un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd)
-   [Utilisation d'une grammaire pour la reconnaissance vocale](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarUse)

## Utilisation conjointe de la personnalisation acoustique et linguistique
{: #combined}

L'utilisation d'un modèle acoustique personnalisé uniquement peut améliorer les fonctions de la reconnaissance du service. Mais si des transcriptions ou des corpus associés sont disponibles pour vos échantillons de données audio, vous pouvez utiliser ces données pour obtenir une meilleure qualité de reconnaissance vocale en fonction du modèle acoustique personnalisé.

En créant un modèle de langue personnalisé qui vient compléter votre modèle acoustique personnalisé, vous pouvez améliorer la reconnaissance vocale en utilisant les deux modèles à la fois. Lorsque vous entraînez un modèle acoustique personnalisé, vous pouvez spécifier un modèle de langue personnalisé qui comprend les transcriptions des ressources audio ou un vocabulaire de mots spécifiques à un domaine à partir de ces ressources. De même, lorsque vous transcrivez des données audio, le service accepte un modèle de langue personnalisé, un modèle acoustique personnalisé ou ces deux types de modèle. Et si votre modèle de langue personnalisé comprend une grammaire, vous pouvez utiliser ce modèle et cette grammaire avec un modèle acoustique personnalisé pour la reconnaissance vocale.

Pour plus d'informations, voir [Utilisation d'un modèle acoustique personnalisé avec un modèle de langue personnalisé](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth).

## Support de langue pour la personnalisation
{: #languageSupport}

La personnalisation des modèles de langue et des modèles acoustiques est disponible pour quelques langues seulement. Le tableau suivant documente le niveau de compatibilité du service avec la personnalisation pour chaque langue.

-   *GA* indique que l'interface est disponible en version GA pour être utilisée en production.
-   *Bêta* indique que l'interface est disponible en tant qu'offre en version bêta.
-   *Non prise en charge* indique que l'interface n'est pas disponible pour cette langue.

Vous pouvez utiliser des modèles à large bande et à bande étroite disponibles avec les langues prises en charge. Si une langue prend en charge la personnalisation de modèle de langue, elle prend également en charge les grammaires. Pour obtenir la liste de tous les modèles disponibles, voir [Modèles de langue pris en charge](/docs/services/speech-to-text-data?topic=speech-to-text-data-models#modelsList).

<table>
  <caption>Tableau 1. Support de langue pour la personnalisation</caption>
  <tr>
    <th style="text-align:left; vertical-align:bottom; width 24%">
      Langue
    </th>
    <th style="text-align:center; vertical-align:bottom; width 37%">
      Support de personnalisation de modèle de langue
    </th>
    <th style="text-align:center; vertical-align:bottom; width 37%">
      Support de personnalisation de modèle acoustique
    </th>
  </tr>
  <tr>
    <td>Portugais brésilien</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Français</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Allemand</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Japonais</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Coréen</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Chinois mandarin</td>
    <td style="text-align:center">Non prise en charge</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Arabe standard moderne</td>
    <td style="text-align:center">Non prise en charge</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Espagnol</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Anglais britannique</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
  <tr>
    <td>Anglais américain</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">Bêta</td>
  </tr>
</table>

Vous pouvez utiliser les méthodes `GET /v1/models` et `GET /v1/models/{model_id}` pour vérifier si un modèle de langue prend en charge la personnalisation de modèle de langue. Dans l'affirmative, la zone `supported_features` de la sortie de la méthode correspondant au modèle définit la zone `custom_language_model` avec la valeur `true`.

## Utilisation de remarques pour la personnalisation
{: #customUsage}

Les remarques d'utilisation suivantes s'appliquent à la fois à la personnalisation de modèle de langue et à la personnalisation de modèle acoustique.

### Propriété des modèles personnalisés
{: #customOwner}

Un modèle personnalisé appartient à l'instance du service {{site.data.keyword.speechtotextshort}} dont les données d'identification sont utilisées pour le créer. Pour utiliser le modèle personnalisé de quelque manière que ce soit, vous devez utiliser les données d'identification de cette instance du service avec les méthodes de l'interface de personnalisation. Les données d'identification créées pour d'autres instances du service ne peuvent pas afficher ou accéder au modèle personnalisé.

Toutes les données d'identification obtenues pour la même instance du service {{site.data.keyword.speechtotextshort}} partagent l'accès à tous les modèles personnalisés créés pour cette instance de service. Pour limiter l'accès à un modèle personnalisé, créez une instance de service distincte et utilisez uniquement les données d'identification de cette instance de service pour créer et utiliser le modèle. Les données d'identification des autres instances de service ne peuvent pas affecter le modèle personnalisé.

L'un des avantages de partager la propriété avec les données d'identification d'une instance de service réside dans le fait que vous pouvez annuler un ensemble de données d'identification, par exemple, si elles venaient à être compromises. Vous pouvez ensuite créer d'autres données d'identification pour la même instance de service et conserver la propriété et l'accès aux modèles personnalisés créés avec les données d'identification initiales.

### Sécurité des informations
{: #customSecurity}

Vous pouvez associer un ID client aux données ajoutées ou mises à jour pour les modèles de langue personnalisés et les modèles acoustiques personnalisés. Vous associez un ID client aux corpus, aux mots personnalisés, aux grammaires et aux ressources audio en transmettant l'en-tête `X-Watson-Metadata` avec les méthodes suivantes :

-   `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word_name}`
-   `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`
-   `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`

Si nécessaire, vous pouvez ensuite supprimer les données en utilisant la méthode `DELETE /v1/user_data`. Pour plus d'informations, voir [Sécurité des informations](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security).
