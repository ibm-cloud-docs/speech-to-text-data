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

# Parameterübersicht
{: #summary}

Die folgende Übersicht enthält alle für die Spracherkennung verfügbaren Parameter. Weitere Informationen zu allen Methoden des {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}-Service finden Sie in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external}.
{: shortdesc}

Beachten Sie beim Erstellen einer Spracherkennungsanforderung die folgenden Grundvoraussetzungen:

-   Bei Methodennamen muss die Groß-/Kleinschreibung beachtet werden.
-   HTTP-Anforderungsheader sind von Groß-/Kleinschreibung unabhängig.
-   Bei HTTP- und WebSocket-Abfrageparametern muss die Groß-/Kleinschreibung beachtet werden.
-   Bei JSON-Feldnamen muss die Groß-/Kleinschreibung beachtet werden.
-   Für alle Inhalte von JSON-Antworten wird der UTF-8-Zeichensatz verwendet.

Beachten Sie außerdem die folgenden servicespezifischen Anforderungen:

-   Sie müssen nur die Audioeingabedaten angeben. Alle anderen Parameter sind optional.
-   Wenn Sie einen ungültigen Abfrageparameter oder ein ungültiges JSON-Feld in der Eingabe angeben, enthält die Antwort ein Feld `warnings`, in dem das ungültige Argument beschrieben wird. Die Anforderung wird trotz der angegebenen Warnungen erfolgreich ausgeführt.

## access_token
{: #summary-access-token}

Ein Zugriffstoken zum Herstellen einer authentifizierten Verbindung zur WebSocket-Schnittstelle. Weitere Informationen finden Sie im Abschnitt [Verbindung öffnen](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets#WSopen).

<table>
  <caption>Tabelle 1. Parameter 'access_token'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:30%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Abfrageparameter für Verbindungsanforderung mit der Methode <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Nicht unterstützt
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Nicht unterstützt
    </td>
  </tr>
</table>

## acoustic_customization_id
{: #summary-acoustic-customization-id}

Eine optionale Anpassungs-ID für ein angepasstes Akustikmodell, das auf die Akustikmerkmale Ihrer Umgebung und der zugehörigen Sprecher abgestimmt ist. Standardmäßig wird kein angepasstes Modell verwendet. Weitere Informationen finden Sie im Abschnitt [Angepasste Modelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabelle 2. Parameter 'acoustic_customization_id'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Betaversion für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Abfrageparameter für Verbindungsanforderung mit der Methode <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## audio_metrics
{: #summary-audio-metrics}

Ein optionaler boolescher Wert, der angibt, ob der Service Metriken zu den Signalmerkmalen der Audioeingabedaten zurückgibt. Die Standardeinstellung `false` gibt an, dass der Service keine Audiometriken zurückgibt. Weitere Informationen finden Sie unter [Audiometriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics). 

<table style="width:90%">
  <caption>Tabelle 3. Parameter 'audio_metrics'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## base_model_version
{: #summary-base-model-version}

(Optional) Eine Version eines Basismodells. Der Parameter ist in erster Linie für die Verwendung mit angepassten Modellen bestimmt, die für ein neues Basismodell aktualisiert werden, kann aber auch ohne ein angepasstes Modell verwendet werden. Der Standardwert ist davon abhängig, ob der Parameter mit oder ohne ein angepasstes Modell verwendet wird. Weitere Informationen finden Sie im Abschnitt [Version des Basismodells](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#version).

<table style="width:90%">
  <caption>Tabelle 4. Parameter 'base_model_version'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Abfrageparameter für Verbindungsanforderung mit der Methode <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## Content-Type
{: #summary-content-type}

(Optional) Ein Audioformat (MIME-Typ) zum Angeben des Formats der Audiodaten, die Sie an den Service übergeben. Der Service kann das Format der meisten Audiodaten automatisch erkennen; d. h. der Parameter ist für die meisten Formate optional. Er ist jedoch erforderlich für die Formate `audio/alaw`, `audio/basic`, `audio/l16` und `audio/mulaw`. Weitere Informationen finden Sie im Abschnitt [Audioformate](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).

<table style="width:90%">
  <caption>Tabelle 5. Parameter 'Content-Type'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter <code>content-type</code> der JSON-Nachricht
      <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Anforderungsheader der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Anforderungsheader der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## customization_weight
{: #summary-customization-weight}

Ein optionales Doppelzeichen zwischen 0,0 und 1,0, das die relative Gewichtung angibt, die der Service den Wörtern aus einem angepassten Sprachmodell im Verhältnis zu Wörtern aus dem Basisvokabular zuordnet. Der Standardwert ist 0,3, sofern beim Trainieren des angepassten Sprachmodells keine andere Gewichtung angegeben wurde. Weitere Informationen finden Sie im Abschnitt [Angepasste Modelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabelle 6. Parameter 'customization_weight'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für amerikanisches Englisch, britisches Englisch, brasilianisches Portugiesisch, Französisch, Deutsch, Japanisch, Koreanisch und Spanisch
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## grammar_name
{: #summary-grammar-name}

Eine optionale Zeichenfolge, die eine Grammatik angibt, die für die Spracherkennung verwendet werden soll. Der Service erkennt nur Zeichenfolgen, die von der Grammatik definiert sind. Sie müssen sowohl den Namen der Grammatik angeben als auch die Anpassungs-ID des angepassten Sprachmodells, für das die Grammatik definiert ist. Weitere Informationen finden Sie im Abschnitt [Grammatiken](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#grammars-input).

<table style="width:90%">
  <caption>Tabelle 7. Parameter 'grammar_name'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Betaversion für amerikanisches Englisch, britisches Englisch, brasilianisches Portugiesisch, Französisch, Deutsch, Japanisch, Koreanisch und Spanisch
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## inactivity_timeout
{: #summary-inactivity-timeout}

Ein optionaler ganzzahliger Wert, der die Anzahl der Sekunden für das Inaktivitätszeitlimit des Service angibt. Inaktivität bedeutet, dass der Service keine Spracherkennung für die Streaming-Audiodaten durchführt. Der Standardwert ist 30 Sekunden. Der Wert `-1` bedeutet 'Unendlich'. Weitere Informationen finden Sie im Abschnitt [Inaktivitätszeitlimit](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts-inactivity).

<table style="width:90%">
  <caption>Tabelle 8. Parameter 'inactivity_timeout'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## interim_results
{: #summary-interim-results}

Ein optionaler boolescher Wert, der den Service anweist, temporäre Hypothesen zurückzugeben, die bis zum endgültigen Transkript noch geändert werden können. Die Standardeinstellung `false` gibt an, dass keine Zwischenergebnisse zurückgegeben werden. Weitere Informationen finden Sie unter [Zwischenergebnisse](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim).

<table style="width:90%">
  <caption>Tabelle 9. Parameter 'interim_results'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Nicht unterstützt
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Nicht unterstützt
    </td>
  </tr>
</table>

## keywords
{: #summary-keywords}

Ein optionales Array mit Schlüsselwortzeichenfolgen, die der Service in den Audioeingabedaten erkennt. Die Funktion für Schlüsselworterkennung ist standardmäßig inaktiviert. Weitere Informationen finden Sie im Abschnitt [Schlüsselworterkennung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting).

<table style="width:90%">
  <caption>Tabelle 10. Parameter 'keywords'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## keywords_threshold
{: #summary-keywords-threshold}

Ein optionales Doppelzeichen zwischen 0,0 und 1,0, das den Mindestschwellenwert für eine positive Schlüsselwortübereinstimmung angibt. Die Funktion für Schlüsselworterkennung ist standardmäßig inaktiviert. Weitere Informationen finden Sie im Abschnitt [Schlüsselworterkennung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting).

<table style="width:90%">
  <caption>Tabelle 11. Parameter 'keywords_threshold'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## language_customization_id
{: #summary-language-customization-id}

Eine optionale Anpassungs-ID für ein angepasstes Sprachenmodell, das Terminologie aus Ihrem Fachgebiet enthält. Standardmäßig wird kein angepasstes Modell verwendet. Weitere Informationen finden Sie im Abschnitt [Angepasste Modelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabelle 12. Parameter 'language_customization_id'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für amerikanisches Englisch, britisches Englisch, brasilianisches Portugiesisch, Französisch, Deutsch, Japanisch, Koreanisch und Spanisch
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Abfrageparameter für Verbindungsanforderung mit der Methode <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## max_alternatives
{: #summary-max-alternatives}

Ein optionaler ganzzahliger Wert, der die maximale Anzahl alternativer Hypothesen angibt, die vom Service zurückgegeben werden. Standardmäßig gibt der Service eine einzige endgültige Hypothese zurück. Weitere Informationen finden Sie im Abschnitt [Maximale Anzahl Alternativen](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives).

<table style="width:90%">
  <caption>Tabelle 13. Parameter 'max_alternatives'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## model
{: #summary-model}

Ein optionales Modell, das die Sprache angibt, in der die Audiodaten gesprochen werden, und die Abtastfrequenz, mit der sie erfasst wurden (Breitband oder Schmalband). Standardmäßig wird `en-US_BroadbandModel` verwendet. Weitere Informationen finden Sie unter [Sprachen und Modelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-models). 

<table style="width:90%">
  <caption>Tabelle 14. Parameter 'model'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Abfrageparameter für Verbindungsanforderung mit der Methode <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## processing_metrics
{: #summary-processing-metrics}

Ein optionaler boolescher Wert, der angibt, ob der Service Metriken zur Verarbeitung der Audioeingabedaten zurückgibt. Die Standardeinstellung `false` gibt an, dass der Service keine Verarbeitungsmetriken zurückgibt. Weitere Informationen finden Sie unter [Verarbeitungsmetriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics). 

<table style="width:90%">
  <caption>Tabelle 15. Parameter 'processing_metrics'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Nicht unterstützt
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## processing_metrics_interval
{: #summary-processing-metrics-interval}

Ein optionaler Gleitkommawert von mindestens 0,1, der das Intervall angibt, in dem der Service Verarbeitungsmetriken zurückgeben soll. Lautet der Wert des Parameters `processing_metrics` `true`, gibt der Service Verarbeitungsmetriken standardmäßig alle 1,0 Sekunden zurück. Weitere Informationen finden Sie unter [Verarbeitungsmetriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics). 

<table style="width:90%">
  <caption>Tabelle 16. Parameter 'processing_metrics_interval'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Nicht unterstützt
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## profanity_filter
{: #summary-profanity-filter}

Ein optionaler boolescher Wert, der angibt, ob der Service vulgäre Ausdrücke aus einem Transkript filtert (zensiert). Der Standardwert `true` bedeutet, dass vulgäre Ausdrücke aus dem Transkript gefiltert werden. Weitere Informationen finden Sie im Abschnitt [Vulgäre Ausdrücke filtern](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter).

<table style="width:90%">
  <caption>Tabelle 17. Parameter 'profanity_filter'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für amerikanisches Englisch
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## redaction
{: #summary-redaction}

Ein optionaler boolescher Wert, der angibt, ob der Service numerische Daten mit mindestens drei aufeinanderfolgenden Ziffern aus einem Transkript schwärzt (maskiert). Wenn Sie den Parameter `redaction` auf `true` setzen, erzwingt der Service automatisch, dass der Parameter `smart_formatting` auf `true` gesetzt wird. Die Standardeinstellung `false` gibt an, dass numerische Daten nicht geschwärzt werden. Weitere Informationen finden Sie im Abschnitt [Zahlenschwärzung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction).

<table style="width:90%">
  <caption>Tabelle 18. Parameter 'redaction'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Betaversion für amerikanisches Englisch, Japanisch und Koreanisch
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## smart_formatting
{: #summary-smart-formatting}

Ein optionaler boolescher Wert, der angibt, ob der Service Datums- und Zeitangaben, Zahlen sowie Währungswerte und ähnliche Werte im endgültigen Transkript in eine konventionelle Darstellung umwandelt. Für amerikanisches Englisch wandelt die Funktion außerdem bestimmte Schlüsselwortausdrücke in Interpunktionszeichen um. Die Standardeinstellung `false` gibt an, dass keine intelligente Formatierung vorgenommen wird. Weitere Informationen finden Sie im Abschnitt [Intelligente Formatierung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting).

<table style="width:90%">
  <caption>Tabelle 19. Parameter 'smart_formatting'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Betaversion für amerikanisches Englisch, Japanisch und Spanisch
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## speaker_labels
{: #summary-speaker-labels}

Ein optionaler boolescher Wert, der angibt, ob der Service markiert, welche Personen in einer Konversation mit mehreren Beteiligten welche Worte gesprochen haben. Wenn Sie den Parameter `speaker_labels` auf `true` setzen, erzwingt der Service automatisch, dass der Parameter `timestamps` auf `true` gesetzt wird. Die Standardeinstellung `false` gibt an, dass keine Sprecherbezeichnungen zurückgegeben werden. Weitere Informationen finden Sie im Abschnitt [Sprecherbezeichnungen](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels).

<table style="width:90%">
  <caption>Tabelle 20. Parameter 'speaker_labels'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Betaversion für amerikanisches Englisch, Japanisch und Spanisch (Breitband- und Schmalbandmodelle) und britisches Englisch (nur Schmalbandmodell)
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## timestamps
{: #summary-timestamps}

Ein optionaler boolescher Wert, der angibt, ob der Service Zeitmarken für die Wörter des Transkripts erstellt. Die Standardeinstellung `false` gibt an, dass keine Zeitmarken zurückgegeben werden. Weitere Informationen finden Sie im Abschnitt [Wortzeitmarken](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps).

<table style="width:90%">
  <caption>Tabelle 21. Parameter 'timestamps'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## Transfer-Encoding
{: #summary-transfer-encoding}

Ein optionaler Wert für `chunked`, der bewirkt, dass die Audiodaten per Streaming zum Service übertragen werden. Standardmäßig werden die Audiodaten alle auf einmal als Einzelübertragung gesendet. Weitere Informationen finden Sie im Abschnitt [Übertragung von Audiodaten](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission).

<table style="width:90%">
  <caption>Tabelle 22. Parameter 'Transfer-Encoding'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Nicht zutreffend; immer per Streaming
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Anforderungsheader der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Anforderungsheader der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## word_alternatives_threshold
{: #summary-word-alternatives-threshold}

Ein optionales Doppelzeichen zwischen 0,0 und 1,0, das den Schwellenwert angibt, ab dem der Service automatisch ähnliche Alternativen für Wörter aus den Audioeingabedaten liefert. Standardmäßig werden keine Wortalternativen zurückgegeben. Weitere Informationen finden Sie im Abschnitt [Wortalternativen](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives).

<table style="width:90%">
  <caption>Tabelle 23. Parameter 'word_alternatives_threshold'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## word_confidence
{: #summary-word-confidence}

Ein optionaler boolescher Wert, der angibt, ob der Service Konfidenzwerte für die Wörter des Transkripts bereitstellt. Die Standardeinstellung `false` gibt an, dass keine Konfidenzwerte für Wörter zurückgegeben werden. Weitere Informationen finden Sie im Abschnitt [Wortkonfidenz](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence).

<table style="width:90%">
  <caption>Tabelle 24. Parameter 'word_confidence'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parameter der JSON-Nachricht <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Abfrageparameter der Methode <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## X-Watson-Metadata
{: #summary-x-watson-metadata}

Eine optionale Zeichenfolge, die eine Kunden-ID den Daten zuordnet, die für Erkennungsanforderungen übergeben werden. Der Parameter akzeptiert das Argument `customer_id={id}`. Standardmäßig wird den Daten keine Kunden-ID zugeordnet. Weitere Informationen finden Sie im Abschnitt [Informationssicherheit](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security).

<table style="width:90%">
  <caption>Tabelle 25. Parameter 'X-Watson-Metadata'</caption>
  <tr>
    <th>Verfügbarkeit und Verwendung</th>
    <th style="vertical-align:bottom">Beschreibung</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Verfügbarkeit**
    </td>
    <td style="text-align:left">
      Allgemein verfügbar für alle Sprachen
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Abfrageparameter <code>x-watson-metadata</code> der Verbindungsanforderung
      <code>/v1/recognize</code> (das Argument muss URL-codiert sein,
      zum Beispiel `customer_id%3dmy_customer_ID`).
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Synchrones HTTP**
    </td>
    <td style="text-align:left">
      Anforderungsheader der Methode <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **Asynchrones HTTP**
    </td>
    <td style="text-align:left">
      Anforderungsheader der Methode <code>POST /v1/register_callback</code> und
      <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>
