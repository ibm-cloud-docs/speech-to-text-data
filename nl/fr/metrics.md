---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-16"

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

# Fonctions de métrique
{: #metrics}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} peut renvoyer deux types de métriques facultatifs pour une demande de reconnaissance vocale :

-   Les [métriques de traitement](#processing_metrics) fournissent des informations périodiques sur le traitement de l'entrée audio par le service. Utilisez les métriques pour évaluer la progression du service dans la transcription de l'audio. Les métriques de traitement sont disponibles avec les interfaces WebSocket et les interfaces HTTP asynchrones.
-   Les [métriques audio](#audio_metrics) fournissent des informations sur les caractéristiques de signal de l'entrée audio. Utilisez les métriques pour déterminer les caractéristiques et la qualité de l'audio. Les métriques audio sont disponibles avec toutes les interfaces de reconnaissance vocale.

Par défaut, le service ne renvoie aucune métrique pour une demande.

## Métriques de traitement 
{: #processing_metrics}

Les métriques de traitement fournissent des informations de synchronisation détaillées sur l'analyse de l'audio d'entrée par le service. Le service renvoie les métriques à des intervalles spécifiés et avec des événements de transcription, tels que des résultats intermédiaires et finaux. 

Les métriques incluent des statistiques sur la quantité d'audio reçue par le service, la quantité d'audio transférée par le service au moteur de reconnaissance vocale et la durée depuis laquelle le service traite l'audio. Si vous demandez des étiquettes de locuteur, les informations indiquent également la quantité de données audio traitées par le service pour déterminer les étiquettes de locuteur. 

Les métriques de traitement peut vous aider à évaluer l’avancement d’une demande de reconnaissance. Elles peuvent également vous aider à distinguer l'absence de résultats pour les raisons suivantes 

-   Absence de son.
-   Absence de parole dans l'audio soumis. 
-   Le moteur se bloque sur le serveur et le réseau se bloque entre le client et le serveur. Pour permettre de différencier les blocages moteur et les blocages réseau, les résultats sont périodiques et non événementiels. 

Les métriques peuvent également vous aider à estimer l'instabilité des réponses en examinant les heures d'arrivée périodiques. Les métriques sont générées à un intervalle constant, ainsi toute différence dans les heures d'arrivée est provoquée par la gigue. 

### Demande de métriques de traitement
{: #processing_metrics_request}

Pour demander des métriques de traitement, utilisez les paramètres facultatifs suivants :

-   `processing_metrics` est une valeur booléenne qui indique si le service doit renvoyer des métriques de traitement. Indiquez `true` pour demander les métriques. Par défaut, le service ne renvoie aucune métrique.
-   `processing_metrics_interval` est un nombre flottant qui spécifie l'intervalle en secondes d'une période d'horloge réelle au cours de laquelle le service doit renvoyer des métriques. Par défaut, le service renvoie des métriques une fois par seconde. Le service ignore ce paramètre excepté si le paramètre `processing_metrics` est défini sur `true`.

    Le paramètre accepte une valeur minimale de 0,1 seconde. Le niveau de précision n'est pas limité, vous pouvez donc spécifier des valeurs telles que 0,25 et 0,125. Le service n'impose pas de valeur maximale.

La manière dont vous fournissez les paramètres et la façon dont le service renvoie les métriques de traitement diffèrent selon l'interface :

-   Avec l'interface WebSocket, vous spécifiez les paramètres avec le message JSON `start` pour une demande de reconnaissance vocale. Le service calcule et renvoie des métriques en temps réel à l'intervalle demandé.
-   Avec l'interface HTTP asynchrone, vous spécifiez des paramètres de requête avec une demande de reconnaissance vocale. Le service calcule les métriques à l'intervalle demandé, mais il renvoie toutes les métriques pour l'audio avec les résultats de la transcription finale.

Le service renvoie également des métriques de traitement des événements de transcription. Si vous demandez des résultats intermédiaires avec l'interface WebSocket, vous pouvez recevoir des métriques plus fréquentes que l'intervalle demandé.

Pour recevoir des métriques de traitement uniquement pour les événements de transcription au lieu d'intervalles périodiques, définissez l'intervalle de traitement sur un nombre important. Si l'intervalle est supérieur à la durée de l'audio, le service renvoie les métriques de traitement uniquement pour les événements de transcription.

### Compréhension des métriques de traitement
{: #processing_metrics_understand}

Le service renvoie des mesures de traitement dans la zone `processing_metrics` de l'objet `SpeechRecognitionResults`. Pour les métriques générées à des intervalles périodiques, l'objet ne contient que la zone `processing_metrics`, comme illustré dans l'exemple suivant.

```javascript
{
  "processing_metrics": {
    "processed_audio": {
      "received": float,
      "seen_by_engine": float,
      "transcription": float,
      "speaker_labels": float
    },
    "wall_clock_since_first_byte_received": float,
    "periodic": boolean
  }
}
```
{: codeblock}

La zone `processing_metrics` inclut un objet `ProcessingMetrics` qui comporte les zones suivantes :

-   `wall_clock_since_first_byte_receivedwall_clock_since_first_byte_received` correspond à la quantité de temps réel en secondes qui s'est écoulée depuis que le service a reçu le premier octet de l'entrée audio. Les valeurs de cette zone sont généralement des multiples de l'intervalle de métriques spécifié, avec deux différences :
    -   Les valeurs peuvent ne pas refléter des intervalles exacts tels que 0,25, 0,5, etc. Les valeurs réelles peuvent, par exemple, être 0,27, 0,52, etc., en fonction du moment où le service reçoit et traite les données audio.
    -   Les valeurs des événements de transcription ne sont pas liées à l'intervalle de traitement. Le service renvoie les résultats axés sur les événements au fur et à mesure qu'ils se produisent.
-   `periodic` indique si les mesures s'appliquent à un intervalle périodique ou à un événement de transcription :
    -   `true` signifie que la réponse a été déclenchée par un intervalle de traitement. Les informations ne contiennent que des métriques de traitement.
    -   `false` signifie que la réponse a été déclenchée par un événement de transcription. Ces informations contiennent des métriques de traitement et des résultats de transcription.

    Utilisez cette zone pour identifier la raison pour laquelle le service a généré la réponse et pour filtrer des résultats différents si nécessaire.
-   `processed_audio` inclut un objet `ProcessedAudio` qui fournit des informations de synchronisation détaillées sur le traitement de l'entrée audio par le service.

L'objet `ProcessedAudio` inclut les zones suivantes. Toutes les zones font référence à des secondes d'audio à la suite de cette réponse. Seule la zone `wall_clock_since_first_byte_received` fait référence au temps écoulé.

-   `received` est le nombre de secondes audio reçues par le service.
-   `seen_by_engine` est le nombre de secondes audio que le service a transmis à son moteur de traitement de la parole. 
-   `transcription` est le nombre de secondes audio que le service a traité pour la reconnaissance vocale.
-   `speaker_labels` est le nombre de secondes audio traitées par le service pour les étiquettes de locuteur. La réponse inclut cette zone uniquement si vous demandez des étiquettes de locuteur.

Le moteur de traitement de la parole analyse l'entrée audio plusieurs fois. L'objet `processed_audio` affiche des valeurs audio que le moteur a traitées et ne lira plus. Les données audio traitées n'ont aucun effet sur les futures hypothèses de reconnaissance.

Les métriques indiquent la progression et la complexité du traitement du moteur :

-   `seen_by_engine` est l'audio que le service a lu et transmis au moteur au moins une fois.
-   `received` - `seen_by_engine` est l'audio qui a été mis en mémoire tampon au niveau du service mais n'a pas encore été vu ou traité par le moteur.
-   La relation entre les temps est `received` >= `seen_by_engine` >= `transcription` >= `speaker_labels`.

Les relations suivantes peuvent également vous aider à comprendre les résultats :

-   Les valeurs des zones `received` et `seen_by_engine` sont supérieures aux valeurs des zones `transcription` et `speaker_labels` lors du traitement de la reconnaissance vocale. Le service doit recevoir l'audio pour commencer à traiter les résultats. 
-   Les valeurs des zones `received` et `seen_by_engine` sont identiques lorsque le service a terminé le traitement de l'audio. Les valeurs finales des zones peuvent être supérieures aux valeurs des zones `transcription` et `speaker_labels` par un nombre de secondes fractionnel.
-   La valeur de la zone `speaker_labels` est généralement la valeur de la zone `transcription` lors du traitement de la reconnaissance vocale. Les valeurs des zones `transcription` et `speaker_labels` sont identiques lorsque le service a terminé le traitement de l'audio. 

### Exemple de métriques de traitement : interface WebSocket
{: #processing_metrics_example_websocket}

L'exemple suivant illustre le message `start` transmis pour une demande à l'interface WebSocket. La demande active le traitement des métriques et définit l'intervalle des métriques de traitement à 0,25 secondes. Elle définit également les paramètres `interim_results` et `speaker_labels` sur `true`. L'audio contient le message simple "hello world long pause stop." 

```javascript
function onOpen(evt) {
  var message = {
    action: 'start',
    content-type: 'audio/flac',
    processing_metrics: true,
    processing_metrics_interval: 0.25,
    interim_results: true,
    speaker_labels: true
  };
  websocket.send(JSON.stringify(message));
  websocket.send(blob);
}
```
{: codeblock}

L'exemple de sortie suivant montre les premiers résultats de métriques de traitement que le service renvoie pour la demande.

```javascript
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 1.59,
      "transcription": 0.49,
      "speaker_labels": 0.0
    },
    "wall_clock_since_first_byte_received": 0.32,
    "periodic": true
  }
}
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 1.59,
      "transcription": 0.49,
      "speaker_labels": 0.0
    },
    "wall_clock_since_first_byte_received": 0.51,
    "periodic": false
  },
  "results": [
    {
      "alternatives": [
        {
          "timestamps": [
            [
              "hello",
              0.43,
              0.76
            ],
            [
              "world",
              0.76,
              1.22
            ]
          ],
          "transcript": "hello world "
        }
      ],
      "final": false
    }
  ],
  "result_index": 0
}
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 2.59,
      "transcription": 1.25,
      "speaker_labels": 0.0
    },
    "wall_clock_since_first_byte_received": 0.57,
    "periodic": true
  }
}
. . .
```
{: codeblock}

### Exemple de métriques de traitement : interface HTTP asynchrone
{: #processing_metrics_example_http}

L'exemple suivant illustre une demande de reconnaissance vocale pour la méthode `/v1/recognitions` de l'interface HTTP asynchrone. La demande active le traitement des métriques et spécifie un intervalle de 0,25 secondes. Le fichier audio inclut à nouveau le message "hello world long pause stop".

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognitions?processing_metrics=true&processing_metrics_interval=0.25"
```
{: pre}

L'exemple de sortie suivant montre les deux premiers résultats de métriques de traitement que le service renvoie pour la demande.

```javascript
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 1.59,
      "transcription": 0.49
    },
    "wall_clock_since_first_byte_received": 0.32,
    "periodic": true
  }
}
{
  "processing_metrics": {
    "processed_audio": {
      "received": 7.04,
      "seen_by_engine": 2.59,
      "transcription": 1.25
    },
    "wall_clock_since_first_byte_received": 0.57,
    "periodic": true
  }
}
. . .
```
{: codeblock}

## Métriques audio
{: #audio_metrics}

Les métriques audio fournissent des informations détaillées sur les caractéristiques de signal de l'entrée audio. Les résultats fournissent des métriques agrégées pour l'ensemble des données audio en entrée à la fin du traitement de la parole. Pour un utilisateur techniquement sophistiqué, les métriques peuvent fournir un éclairage significatif sur les caractéristiques détaillées de l'audio.

Vous pouvez utiliser des métriques audio pour fournir une indication en temps réel d'un problème avec l'entrée audio et peut-être même une solution potentielle. Par exemple, vous pouvez indiquer un message tel que "Il y a trop de bruit de fond" ou "Veuillez vous rapprocher du micro". Vous pouvez également utiliser un outil d'analyse hors ligne pour examiner les caractéristiques du signal et suggérer des données qui conviennent aux futures mises à jour de modèle.

### Demande de métriques audio
{: #audio_metrics_request}

Pour demander des métriques audio, définissez le paramètre booléen `audio_metrics` sur `true`. Par défaut, le service ne renvoie aucune métrique.

-   Avec l'interface WebSocket, vous spécifiez le paramètre avec le message JSON `start` pour une demande de reconnaissance vocale. 
-   Avec les interfaces HTTP, vous spécifiez un paramètre de requête avec une demande de reconnaissance vocale. 

Le service renvoie des métriques audio avec les résultats de transcription finaux. Il renvoie les métriques une seule fois pour l'intégralité du flux audio. Même si le service renvoie plusieurs résultats de transcription (pour différents blocs audio), il ne renvoie qu'une seule instance des métriques à la fin des résultats.

L'interface WebSocket accepte plusieurs flux audio (ou fichiers) avec une seule connexion. Vous délimitez différents flux en envoyant des messages `stop` ou des objets blob binaires vides au service. Dans ce cas, le service renvoie des métriques distinctes pour chaque flux audio délimité.

### Compréhension des métriques audio
{: #audio_metrics_understand}

Le service renvoie les métriques dans la zone `audio_metrics` de l'objet `SpeechRecognitionResults`.

```javascript
{
  "results": [
    . . .
  ],
  "result_index": integer,
  "audio_metrics": {
    "sampling_interval": float,
    "accumulated": {
      "final": boolean,
      "end_time": float,
      "signal_to_noise_ratio": float,
      "speech_ratio": float,
      "high_frequency_loss": float,
      "direct_current_offset": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ],
      "clipping_rate": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ],
      "speech_level": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ],
      "non_speech_level": [
        {"begin": float, "end": float, "count": integer},
        . . .
      ]
    }
  }
}
```
{: codeblock}

La zone `audio_metrics` inclut un objet `AudioMetrics` qui comporte deux zones :

-   `sampling_interval` indique l'intervalle en secondes (généralement 0,1 seconde) au cours duquel le service a calculé les métriques audio.
-   `accumulated` inclut un objet `AudioMetricsDetails` qui fournit des informations détaillées sur les caractéristiques de signal de l'entrée audio.

Les zones suivantes de l'objet `AudioMetricsDetails` fournissent des valeurs unaires :

-   `final` indique si les métriques concernent la fin du flux audio, ce qui signifie que la transcription est terminée. Actuellement, la zone est toujours `true`. Le service renvoie des métriques une seule fois par flux audio. Les résultats fournissent des métriques agrégées pour le flux complet.
-   `end_time` indique l'heure de fin en secondes de l'audio auquel les mesures s'appliquent. Etant donné que les métriques s'appliquent à l'ensemble du flux audio, l'heure de fin est toujours la longueur de l'audio.
-   `signal_to_noise_ratio` fournit le rapport signal / bruit (SNR) pour le signal audio. La valeur indique le rapport parole / bruit dans l'audio. Une valeur valide est comprise entre 0 et 100 décibels (dB). Le service omet la zone s'il ne peut pas calculer le SNR pour l'audio.
-   `speech_ratio` est le rapport entre les segments de parole et de non parole dans le signal audio. La valeur est comprise entre 0 et 1.
-   `high_frequency_loss` indique la probabilité pour le signal audio d'une perte de la moitié supérieure de son contenu de fréquence.
    -   Une valeur proche de 1 indique généralement des données audio échantillonnées artificiellement, ce qui a une incidence négative sur l'exactitude des résultats de la transcription.
    -   Une valeur égale ou proche de 0 indique que le signal audio est bon et présente un spectre complet. 
    -   Une valeur proche de 0,5 signifie que la détection du contenu de fréquence est peu fiable ou indisponible. 

Les zones suivantes de l'objet `AudioMetricsDetails` fournissent des histogrammes pour les caractéristiques de signal. Chaque zone fournit un tableau d'objets `AudioMetricsHistogrambin`. Une unité unique de chaque histogramme est calculée en fonction d'une longueur d'audio `sampling_interval`.

-   `direct_current_offset` définit un histogramme du composant courant continu (CC) du signal audio.
-   `clipping_rate` définit un histogramme du taux de coupure pour les segments audio. Le taux de coupure est défini comme la fraction d'échantillons du segment qui atteint la valeur maximale ou minimale offerte par la plage de quantification audio. 

Le service détecte automatiquement une plage audio (-32768 à +32767) à modulation de code d'impulsion (PCM) 16 bits ou une plage d'unités (-1 à +1). Le taux de coupure est compris entre 0 et 1. Des valeurs plus élevées indiquent une dégradation possible de la reconnaissance vocale.
-   `speech_level` définit un histogramme du niveau de signal dans les segments de l'audio qui contiennent la parole. Le niveau du signal est calculé en tant que valeur racine (RMS) sur une échelle en décibels (dB) normalisée dans la plage allant de 0 (niveau minimal) à 1 (niveau maximal). 
-   `non_speech_level` définit un histogramme du niveau de signal dans les segments audio qui ne contiennent pas de parole. Le niveau de signal est calculé en tant que valeur RMS dans une échelle de décibels normalisée pour la plage 0 (niveau minimal) à 1 (niveau maximal).

Chaque objet `AudioMetricsHistogrambin` décrit un casier avec les limites `begin` et `end` définies. Chaque casier indique `count` ou le nombre de valeurs dans la plage des caractéristiques de signal pour ce casier. Les premier et les dernier casiers d'un histogramme sont les casiers de limites. Ils couvrent les intervalles entre l'infini négatif et la première limite, et entre la dernière limite et l'infini positif, respectivement.

### Exemple de métriques audio
{: #audio_metrics_example}

L'exemple suivant illustre une demande de reconnaissance vocale avec l'interface HTTP synchrone qui renvoie des métriques audio. Le fichier audio inclut le message simple "hello world long pause stop".

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognitize?audio_metrics=true"
```
{: pre}

La réponse inclut les métriques audio pour l'entrée audio complète, dont la durée est de 7 secondes. L’audio en entrée contient légèrement plus de segments de parole que de non parole : 37 à 33 segments, pour un rapport `speech_ratio` de 0,529. Le taux de coupure est très faible, ce qui indique une entrée audio de haute qualité.

La zone `high_frequency_loss` a une valeur 0,5, ce qui signifie que la détection du contenu de la fréquence par le service n'est pas fiable ou n'est pas disponible. Les résultats omettent la zone `signal_to_noise_ratio` car le service n'a pas pu calculer le SNR pour l'audio.

```javascript
{
  "results": [
    {
      "alternatives": [
        {
          "confidence": 0.96,
          "transcript": "hello world "
        }
      ],
         "final": true
      },
      {
      "alternatives": [
        {
          "confidence": 0.79,
          "transcript": "long pause "
        }
      ],
         "final": true
      },
      {
      "alternatives": [
        {
          "confidence": 0.97,
          "transcript": "stop "
        }
      ],
      "final": true
    }
  ],
  "result_index": 0,
  "audio_metrics": {
    "sampling_interval": 0.1,
    "accumulated": {
      "final": true,
      "end_time": 7.0,
      "speech_ratio": 0.529,
      "high_frequency_loss": 0.5,
      "direct_current_offset": [
        {"begin": -1.0, "end": -0.9, "count": 0},
        {"begin": -0.9, "end": -0.7, "count": 0},
        {"begin": -0.7, "end": -0.5, "count": 0},
        {"begin": -0.5, "end": -0.3, "count": 0},
        {"begin": -0.3, "end": -0.1, "count": 0},
        {"begin": -0.1, "end": 0.1, "count": 70},
        {"begin": 0.1, "end": 0.3, "count": 0},
        {"begin": 0.3, "end": 0.5, "count": 0},
        {"begin": 0.5, "end": 0.7, "count": 0},
        {"begin": 0.7, "end": 0.9, "count": 0},
        {"begin": 0.9, "end": 1.0, "count": 0}
      ],
      "clipping_rate": [
        {"begin": 0.0, "end": 1e-05, "count": 70},
        {"begin": 1e-05, "end": 0.0001, "count": 0},
        {"begin": 0.0001, "end": 0.001, "count": 0},
        {"begin": 0.001, "end": 0.01, "count": 0},
        {"begin": 0.01, "end": 0.1, "count": 0},
        {"begin": 0.1, "end": 1.0, "count": 0}
      ],
      "speech_level": [
        {"begin": 0.0, "end": 0.1, "count": 37},
        {"begin": 0.1, "end": 0.2, "count": 0},
        {"begin": 0.2, "end": 0.3, "count": 0},
        {"begin": 0.3, "end": 0.4, "count": 0},
        {"begin": 0.4, "end": 0.5, "count": 0},
        {"begin": 0.5, "end": 0.6, "count": 0},
        {"begin": 0.6, "end": 0.7, "count": 0},
        {"begin": 0.7, "end": 0.8, "count": 0},
        {"begin": 0.8, "end": 0.9, "count": 0},
        {"begin": 0.9, "end": 1.0, "count": 0}
      ],
      "non_speech_level": [
        {"begin": 0.0, "end": 0.1, "count": 33},
        {"begin": 0.1, "end": 0.2, "count": 0},
        {"begin": 0.2, "end": 0.3, "count": 0},
        {"begin": 0.3, "end": 0.4, "count": 0},
        {"begin": 0.4, "end": 0.5, "count": 0},
        {"begin": 0.5, "end": 0.6, "count": 0},
        {"begin": 0.6, "end": 0.7, "count": 0},
        {"begin": 0.7, "end": 0.8, "count": 0},
        {"begin": 0.8, "end": 0.9, "count": 0},
        {"begin": 0.9, "end": 1.0, "count": 0}
      ]
    }
  }
}
```
{: codeblock}
