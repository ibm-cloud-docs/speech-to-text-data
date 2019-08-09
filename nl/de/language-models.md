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

# Angepasste Sprachmodelle verwalten
{: #manageLanguageModels}

Die Anpassungsschnittstelle enthält die Methode `POST /v1/customizations` zum Erstellen eines angepassten Sprachmodells. Außerdem enthält die Schnittstelle die Methode `POST /v1/customizations/train` zum Trainieren eines angepassten Modells mit den aktuellen Daten der zugehörigen Wörterressource. Weitere Informationen finden Sie in den folgenden Abschnitten:
{: shortdesc}

-   [Angepasstes Sprachmodell erstellen](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language)
-   [Angepasstes Sprachmodell trainieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language)

Darüber hinaus enthält die Schnittstelle Methoden zum Auflisten von Informationen zu angepassten Sprachmodellen, zum Zurücksetzen eines angepassten Modells in den Anfangsstatus sowie zum Aktualisieren und zum Löschen eines angepassten Modells. Das Trainieren, Zurücksetzen, Aktualisieren oder Löschen eines angepassten Modells ist nicht möglich, während der Service eine andere Operation für das Modell ausführt. Dazu gehört auch das Hinzufügen von Ressourcen zum Modell. 

## Angepasste Sprachmodelle auflisten
{: #listModels-language}

Die Anpassungsschnittstelle bietet zwei Methoden zum Auflisten von Informationen zu den angepassten Sprachmodellen, deren Eigner die angegebenen Berechtigungsnachweise sind: 

-   Die Methode `GET /v1/customizations` listet Informationen zu allen angepassten Sprachmodellen oder zu allen angepassten Sprachmodellen für eine angegebene Sprache auf.
-   Die Methode `GET /v1/customizations/{customization_id}` listet Informationen zu einem angegebenen angepassten Sprachmodell auf. Verwenden Sie diese Methode, um im Service den Status einer Trainingsanforderung oder einer Anforderung zum Hinzufügen neuer Wörter abzufragen.

Beide Methoden geben die folgenden Informationen zu einem angepassten Modell zurück:

-   `customization_id` gibt die GUID (Globally Unique Identifier) des angepassten Modells zurück. Die GUID dient zum Identifizieren des Modells in den Methoden der Schnittstelle.
-   `created` gibt das Datum und die Uhrzeit für die Erstellung des angepassten Modells in koordinierter Weltzeit (UTC) an.
-   `updated` gibt das Datum und die Uhrzeit für die letzte Änderung des angepassten Modells in koordinierter Weltzeit (UTC) an. 
-   `language` ist die Sprache des angepassten Modells.
-   `dialect` ist der Dialekt der Sprache für das angepasste Sprachmodell.
-   `owner` gibt die Berechtigungsnachweise der Serviceinstanz an, die Eigner des angepassten Modells ist.
-   `name` ist der Name des angepassten Modells.
-   `description` ist eine Beschreibung des angepassten Modells, sofern beim Erstellen des Modells eine Beschreibung angegeben wurde.
-   `base_model` gibt den Namen des Sprachmodells an, für das das angepasste Modell erstellt wurde.
-   `versions` stellt eine Liste der verfügbaren Versionen des angepassten Modells zur Verfügung. Jedes Element in dem Array gibt eine Version des Basismodells an, mit der das angepasste Modell verwendet werden kann. Mehrere Versionen sind nur vorhanden, wenn das angepasste Modell aktualisiert wird. Andernfalls wird nur eine einzige Version angezeigt. Weitere Informationen finden Sie im Abschnitt [Versionsinformationen für ein angepasstes Modell auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-customUpgrade#upgradeList).

Die Methode gibt außerdem ein Feld `status` zurück, das den Status des angepassten Modells angibt.

-   `pending` gibt an, dass das Modell erstellt wurde. Es befindet sich im Wartestatus, da entweder noch keine gültigen Trainingsdaten (Korpora, Grammatiken oder Wörter) hinzugefügt wurden oder die Analyse der hinzugefügten Daten noch nicht abgeschlossen ist. 
-   `ready` gibt an, dass das Modell gültige Daten enthält und jetzt für das Training bereit ist. Wenn das Modell eine Mischung aus gültigen und ungültigen Ressourcen enthält, schlägt das Training des Modells fehl, falls Sie den Abfrageparameter `strict` nicht auf `false` gesetzt haben. Weitere Informationen finden Sie in [Fehler beim Training](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#failedTraining-language).

-   `training` gibt an, dass das Modell momentan mit Daten trainiert wird.
-   `available` gibt an, dass das Modell trainiert wurde und nun in einer Erkennungsanforderung verwendet werden kann.
-   `upgrading` gibt an, dass das Modell momentan aktualisiert wird.
-   `failed` gibt an, dass das Trainieren des Modells fehlgeschlagen ist. Prüfen Sie die Wörter in der Wörterressource des Modells auf Fehler, die das Trainieren des Modells verhindern.

Darüber hinaus enthält die Ausgabe ein Feld `progress`, in dem der aktuelle Fortschritt beim Trainieren des angepassten Modells angegeben wird. Wenn Sie das Training für das Modell mithilfe der Methode `POST /v1/customizations/{customization_id}/train` gestartet haben, wird in diesem Feld der aktuelle Fortschritt der zugehörigen Anforderung als Prozentwert angegeben. Bei Fertigstellung des Trainings wird im Feld der Wert `100` angegebenen, sofern der Status `available` lautet; andernfalls wird der Wert `0` angegeben.

### Beispiele für Anforderungen und Antworten
{: #listExample-language}

Das folgende Beispiel enthält den Abfrageparameter `language`, um alle angepassten Sprachmodelle für amerikanisches Englisch aufzulisten, deren Eigner die angegebenen Berechtigungsnachweise sind:


```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations?language=en-US"
```
{: pre}

Die Berechtigungsnachweise sind Eigner von zwei solchen Modellen. Das erste Modell ist für Daten empfangsbereit oder wird vom Service verarbeitet. Das zweite Modell ist vollständig trainiert und betriebsbereit.

```javascript
{
  "customizations": [
    {
      "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
      "created": "2016-06-01T18:42:25.324Z",
      "updated": "2016-06-01T18:42:25.324Z",
      "language": "en-US",
      "dialect": "en-US",
      "versions": [
        "en-US_BroadbandModel.v07-06082016.06202016",
        "en-US_BroadbandModel.v2017-11-15"
      ],
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "name": "Example model",
      "description": "Example custom language model",
      "base_model_name": "en-US_BroadbandModel",
      "status": "pending",
      "progress": 0
    },
    {
      "customization_id": "8391f918-3b76-e109-763c-b7732fae4829",
      "created": "2016-06-01T18:51:37.291Z",
      "updated": "2016-06-01T20:02:10.624Z",
      "language": "en-US",
      "dialect": "en-US",
      "versions": [
        "en-US_BroadbandModel.v2017-11-15"
      ],
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "name": "Example model two",
      "description": "Example custom language model two",
      "base_model_name": "en-US_BroadbandModel",
      "status": "available",
      "progress": 100
    }
  ]
}
```
{: codeblock}

Das folgende Beispiel gibt Informationen zu dem angepassten Modell zurück, das die angegebene Anpassungs-ID aufweist:

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
      "updated": "2016-06-01T18:42:25.324Z",
      "language": "en-US",
      "dialect": "en-US",
      "versions": [
        "en-US_BroadbandModel.v07-06082016.06202016",
    "en-US_BroadbandModel.v2017-11-15"
  ],
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model",
  "description": "Example custom language model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "pending",
  "progress": 0
}
```
{: codeblock}

## Angepasstes Sprachmodell zurücksetzen
{: #resetModel-language}

Mit der Methode `POST /v1/customizations/{customization_id}/reset` können Sie ein angepasstes Modell zurücksetzen. Beim Zurücksetzen eines Modells werden alle Korpora und Wörter aus dem Modell entfernt, d. h. das Modell wird auf den ursprünglichen Erstellungsstatus zurückgesetzt. Die Methode löscht weder das Modell noch die zugehörigen Metadaten wie Name und Sprache. Nach dem Zurücksetzen des Modells ist die zugehörige Wörterressource leer und muss erneut erstellt werden (durch Hinzufügen von Korpora und Wörtern).

### Beispielanforderung
{: #resetExample-language}

Im folgenden Beispiel wird das angepasste Modell mit der angegebenen Anpassungs-ID zurückgesetzt:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/reset"
```
{: pre}

## Angepasstes Sprachmodell löschen
{: #deleteModel-language}

Mit der Methode `DELETE /v1/customizations/{customization_id}` können Sie ein angepasstes Sprachmodell löschen, das nicht mehr benötigt wird. Diese Methode löscht alle Korpora und Wörter, die dem angepassten Modell zugeordnet sind, sowie das Modell selbst. Verwenden Sie diese Methode mit Vorsicht: Nach dem Löschen können Sie das angepasste Modell und die zugehörigen Daten nicht wiederherstellen.

### Beispielanforderung
{: #deleteExample-language}

Im folgenden Beispiel wird das angepasste Modell mit der angegebenen Anpassungs-ID gelöscht:

```bash
curl -X DELETE
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}
