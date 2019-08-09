---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# Angepasste Akustikmodelle verwalten
{: #manageAcousticModels}

Die Anpassungsschnittstelle enthält die Methode `POST /v1/acoustic_customizations` für das Erstellen eines angepassten Akustikmodells. Sie bietet außerdem die Methode `POST /v1/acoustic_customizations/train`, um ein angepasstes Modell mit den neuesten Audioressourcen zu trainieren. Weitere Informationen finden Sie in den folgenden Abschnitten:
{: shortdesc}

-   [Angepasstes Akustikmodell erstellen](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic)
-   [Angepasstes Akustikmodell trainieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic)

Darüber hinaus enthält die Schnittstelle Methoden zum Auflisten von Informationen zu angepassten Akustikmodellen, zum Zurücksetzen eines angepassten Modells in den Anfangsstatus sowie zum Aktualisieren und zum Löschen eines angepassten Modells. Das Trainieren, Zurücksetzen, Aktualisieren oder Löschen eines angepassten Modells ist nicht möglich, während der Service eine andere Operation für das Modell ausführt. Dazu gehört auch das Hinzufügen von Audioressourcen zum Modell. 

## Angepasste Akustikmodelle auflisten
{: #listModels-acoustic}

Die Anpassungsschnittstelle bietet zwei Methoden für das Auflisten von Informationen zu den angepassten Akustikmodellen, deren Eigner die angegebenen Berechtigungsnachweise sind: 

-   Die Methode `GET /v1/acoustic_customizations` listet Informationen zu allen angepassten Akustikmodellen oder zu allen angepassten Akustikmodellen für eine bestimmte Sprache auf.
-   Die Methode `GET /v1/acoustic_customizations/{customization_id}` listet Informationen zu einem angegebenen angepassten Akustikmodell auf. Mit dieser Methode können Sie den Status einer Trainingsanforderung vom Service abfragen.

Beide Methoden geben die folgenden Informationen zu einem angepassten Akustikmodell zurück:

-   `customization_id` gibt die GUID (Globally Unique Identifier) des angepassten Modells zurück. Mit der GUID wird das Modell in den Methoden der Schnittstelle angegeben.
-   `created` gibt das Datum und die Uhrzeit für die Erstellung des angepassten Modells in koordinierter Weltzeit (UTC) an.
-   `updated` gibt das Datum und die Uhrzeit für die letzte Änderung des angepassten Modells in koordinierter Weltzeit (UTC) an. 
-   `language` ist die Sprache des angepassten Modells.
-   `owner` gibt die Berechtigungsnachweise der Serviceinstanz an, die Eigner des angepassten Modells ist.
-   `name` ist der Name des angepassten Modells.
-   `description` ist eine Beschreibung des angepassten Modells, sofern beim Erstellen des Modells eine Beschreibung angegeben wurde.
-   `base_model_name` gibt den Namen des Sprachmodells an, für das das angepasste Modell erstellt wurde.
-   `versions` stellt eine Liste der verfügbaren Versionen des angepassten Modells zur Verfügung. Jedes Element des Arrays gibt eine Version des Basismodells an, mit der das angepasste Modell verwendet werden kann. Mehrere Versionen sind nur dann vorhanden, wenn für das angepasste Modell ein Upgrade durchgeführt wurde. Andernfalls wird nur eine einzige Version angezeigt. Weitere Informationen finden Sie im Abschnitt [Versionsinformationen für ein angepasstes Modell auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-customUpgrade#upgradeList).

Die Methode gibt außerdem ein Feld `status` zurück, in dem der Status des angepassten Modells angegeben ist:

-   `pending`: Das Modell wurde erstellt. Es befindet sich im Wartestatus, da entweder noch keine gültigen Trainingsdaten (Audioressourcen) hinzugefügt wurden oder die Analyse der hinzugefügten Daten noch nicht abgeschlossen ist. 
-   `ready` gibt an, dass das Modell gültige Audiodaten enthält und jetzt für das Training bereit ist. Wenn das Modell eine Mischung aus gültigen und ungültigen Audioressourcen enthält, schlägt das Training des Modells fehl, falls Sie den Abfrageparameter `strict` nicht auf `false` gesetzt haben. Weitere Informationen finden Sie in [Fehler beim Training](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#failedTraining-acoustic).

-   `training` gibt an, dass das Modell momentan mit Audiodaten trainiert wird.
-   `available` gibt an, dass das Modell trainiert wurde und nun für Erkennungsanforderungen verwendet werden kann. 
-   `upgrading` gibt an, dass das Modell momentan aktualisiert wird.
-   `failed` gibt an, dass das Trainieren des Modells fehlgeschlagen ist. Stellen Sie durch eine Untersuchung der Audioressourcen im Modell fest, wodurch das Training des Modells verhindert wurde. Mögliche Fehler sind nicht ausreichende Audiodaten, zu viele Audiodaten oder eine ungültige Audioressource.

Die Ausgabe enthält außerdem ein Feld `progress`, in dem der aktuelle Verarbeitungsfortschritt beim Training des angepassten Modells angegeben ist. Falls Sie das Training des Modells mit der Methode `POST /v1/acoustic_customizations/{customization_id}/train` gestartet haben, ist der aktuelle Verarbeitungsfortschritt dieser Anforderung in diesem Feld als Prozentsatz der Fertigstellung angegeben. Der Wert des Feldes ist `100`, falls der Status `available` (= verfügbar) lautet, andernfalls ist er `0`.

### Beispielanforderungen und -antworten
{: #listExample-acoustic}

Das folgende Beispiel enthält den Abfrageparameter `language`, um alle angepassten Akustikmodelle für amerikanisches Englisch aufzulisten, deren Eigner die angegebenen Berechtigungsnachweise sind:


```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/acoustic_customizations?language=en-US"
```
{: pre}

Die Berechtigungsnachweise sind Eigner von zwei solchen Modellen. Das erste Modell wartet auf Daten oder wird vom Service verarbeitet. Das zweite Modell ist vollständig trainiert und bereit für die Verwendung.

```javascript
{
  "customizations": [
    {
      "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
      "created": "2016-06-01T18:42:25.324Z",
      "updated": "2016-06-01T18:42:25.324Z",
      "language": "en-US",
      "versions": [
        "en-US_BroadbandModel.v07-06082016.06202016",
        "en-US_BroadbandModel.v2017-11-15"
      ],
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "name": "Example model one",
      "description": "Example custom acoustic model",
      "base_model_name": "en-US_BroadbandModel",
      "status": "pending",
      "progress": 0
    },
    {
      "customization_id": "8391f918-3b76-e109-763c-b7732fae4829",
      "created": "2016-06-01T18:51:37.291Z",
      "updated": "2016-06-01T19:21:06.825Z",
      "language": "en-US",
      "versions": [
        "en-US_BroadbandModel.v2017-11-15"
      ],
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "name": "Example model two",
      "description": "Example custom acoustic model two",
      "base_model_name": "en-US_BroadbandModel",
      "status": "available",
      "progress": 100
    }
  ]
}
```
{: codeblock}

Das folgende Beispiel gibt Informationen zu dem angepassten Modell mit der angegebenen Anpassungs-ID zurück:

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
      "updated": "2016-06-01T18:42:25.324Z",
      "language": "en-US",
      "versions": [
        "en-US_BroadbandModel.v07-06082016.06202016",
    "en-US_BroadbandModel.v2017-11-15"
  ],
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model one",
  "description": "Example custom acoustic model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "pending",
  "progress": 0
}
```
{: codeblock}

## Angepasstes Akustikmodell zurücksetzen
{: #resetModel-acoustic}

Zum Zurücksetzen eines angepassten Akustikmodells verwenden Sie die Methode `POST /v1/acoustic_customizations/{customization_id}/reset`. Beim Zurücksetzen eines angepassten Modells werden alle Audioressourcen aus dem Modell entfernt und das Modell hierdurch mit dem Zustand bei seiner Erstellung initialisiert. Das Modell selbst oder Metadaten wie Name und Sprache werden von der Methode nicht gelöscht. Wenn Sie ein Modell zurücksetzen, werden allerdings seine Audioressourcen entfernt und müssen erneut erstellt werden.

### Beispielanforderung
{: #resetExample-acoustic}

Im folgenden Beispiel wird das angepasste Akustikmodell mit der angegebenen Anpassungs-ID zurückgesetzt:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/acoustic_customizations/{customization_id}/reset"
```
{: pre}

## Angepasstes Akustikmodell löschen
{: #deleteModel-acoustic}

Mit der Methode `DELETE /v1/acoustic_customizations/{customization_id}` können Sie ein angepasstes Akustikmodell löschen, das Sie nicht mehr benötigen. Die Methode löscht alle zum angepassten Modell gehörenden Audiodaten und das Modell selbst. Verwenden Sie diese Methode mit Vorsicht: Ein angepasstes Modell und die zugehörigen Daten können nicht wiederhergestellt werden, nachdem Sie das Modell gelöscht haben.

### Beispielanforderung
{: #deleteExample-acoustic}

Im folgenden Beispiel wird das angepasste Akustikmodell mit der angegebenen Anpassungs-ID gelöscht:

```bash
curl -X DELETE
--header "Authorization: Bearer {token}"
"{url}/v1/acoustic_customizations/{customization_id}"
```
{: pre}
