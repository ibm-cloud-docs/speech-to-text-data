---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

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

# Erkennungsanforderung ausgeben
{: #basic-request}

Zum Anfordern der Spracherkennung mit {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} müssen Sie lediglich die Audiodaten bereitstellen, die transkribiert werden sollen. Der Service bietet bei jeder seiner Schnittstellen dieselben Basistranskriptionsfunktionen.
{: shortdesc}

In den folgenden Abschnitten sind Basistranskriptionsanforderungen für jede Schnittstelle des Service dargestellt: 

-   In den Beispielen wird eine kurze FLAC-Datei namens <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a> übergeben.
-   Die Beispiele verwenden das Standardsprachmodell `en-US_BroadbandModel`.

Die Antwort des Service auf diese Beispiele ist im Abschnitt [Wissenswertes über Erkennungsergebnisse](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-response) beschrieben.

Wenn Sie ein selbst signiertes Zertifikat verwenden, müssen Sie die SSL-Verifizierung inaktivieren, damit eine Anforderung an den Service erfolgreich ausgeführt werden kann. Weitere Informationen finden Sie in [SSL-Verifizierung inaktivieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests#SSLverification).
{: important}

## Audiodaten mit einer Anforderung senden
{: #basic-request-audio}

Die Audiodaten, die Sie an den Service übergeben, müssen in einem der vom Service unterstützten Formate vorliegen. Für die meisten Audiodaten kann der Service das Format automatisch erkennen. Bei einigen Audioformaten müssen Sie das Format mit dem Parameter `Content-Type` oder einem äquivalenten Parameter angeben. Weitere Informationen finden Sie unter [Audioformate](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats). (Zur Verdeutlichung ist in den folgenden Beispielen das Audioformat bei allen Anforderungen angegeben.)

Das von den Schnittstellen des Service akzeptierte maximale Volumen der Audiodaten ist unterschiedlich. Mit jeder Anforderung müssen Audiodaten mit einer Mindestgröße von 100 Byte gesendet werden.

-   Mit der WebSocket-Schnittstelle und der synchronen HTTP-Schnittstelle können Sie in einer einzelnen Anforderung Audiodaten mit einer Größe von maximal 100 MB übergeben.
-   Mit der asynchronen HTTP-Schnittstelle können Sie Audiodaten mit einer maximalen Größe von 1 GB in einer Anforderung übergeben. 

Falls die Erkennung für große Mengen von Audiodaten erfolgen soll, können Sie die Audiodaten manuell in kleinere Blöcke unterteilen. In der Regel ist es jedoch effizienter und komfortabler, die Audiodaten in ein komprimiertes und verlustbehaftetes Format zu konvertieren. Die Komprimierung kann das mit einer einzigen Anforderung gesendete Datenvolumen maximieren. Insbesondere bei Audiodaten im WAF- oder FLAC-Format kann die Konvertierung in ein verlustbehaftetes Format einen deutlichen Unterschied machen.

-   Weitere Informationen zu Audioformaten, die eine Komprimierung verwenden, finden Sie im Abschnitt [Unterstützte Audioformate](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#formats).
-   Zusätzliche Angaben über die Auswirkungen der Komprimierung und über die Konvertierung Ihrer Audiodaten in ein Format, das die Komprimierung verwendet, enthalten die Abschnitte [Datengrenzwerte und Komprimierung](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#limits) und  [Konvertierung von Audiodaten](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#conversion).

## WebSocket-Schnittstelle verwenden
{: #basic-request-websocket}

Die [WebSocket-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) bietet eine effiziente Implementierung über eine Vollduplexverbindung mit niedriger Latenzzeit und hohem Durchsatz. Alle Anforderungen und Antworten werden über dieselbe WebSocket-Verbindung gesendet. Aufgrund ihrer Vorteile ist die WebSocket-Schnittstelle das bevorzugte Verfahren für die Spracherkennung. Weitere Informationen finden Sie im Abschnitt [Vorteile der WebSocket-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview#advantages).

Zur Verwendung der WebSocket-Schnittstelle müssen Sie zunächst mit der Methode `/v1/recognize` eine Verbindung zum Service herstellen. Hierbei geben Sie Parameter wie das Sprachmodell und alle angepassten Modelle an, die für die über die Verbindung gesendeten Anforderungen verwendet werden sollen. Anschließend registrieren Sie die Ereignislistener, um Antworten vom Service zu verarbeiten. Zum Ausgeben einer Anforderung senden Sie eine JSON-Textnachricht, die das Audioformat und alle weiteren Parameter enthält. Die Audiodaten übergeben Sie als binäre Nachricht (BLOB); anschließend senden Sie eine Textnachricht, um das Ende der Audiodaten zu signalisieren.

Das folgende Beispiel zeigt JavaScript-Code, der eine Verbindung aufbaut und die Textnachrichten sowie binären Nachrichten für eine Erkennungsanforderung sendet. Das Beispiel enthält nicht den Code für die Installation der Ereignishandler.

```javascript
var my_access_token = '{token}';
var wsURI = '{ws_url}/v1/recognize'
  + '?access_token=' + my_access_token;
var websocket = new WebSocket(wsURI);

websocket.send(JSON.stringify({
  action: 'start',
  content-type: 'audio/flac'
}));
websocket.send(blob);
websocket.send(JSON.stringify({'action': 'stop'}));
```
{: codeblock}

## Synchrone HTTP-Schnittstelle verwenden
{: #basic-request-http}

Die [synchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) bietet das einfachste Verfahren für eine Erkennungsanforderung. Sie verwenden die Methode `POST /v1/recognize`, um eine Anforderung an den Service auszugeben. Zusammen mit dieser einzelnen Anforderung übergeben Sie die Audiodaten und alle Parameter.

Das folgende `curl`-Beispiel zeigt eine einfache HTTP-Erkennungsanforderung:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @audio-file.flac
"{url}/v1/recognize"
```
{: pre}

## Asynchrone HTTP-Schnittstelle verwenden
{: #basic-request-async}

Die [asynchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) stellt eine nicht blockierende Schnittstelle für die Transkription von Audiodaten bereit. Sie können die Schnittstelle mit oder ohne vorherige Registrierung einer Callback-URL beim Service verwenden. Bei Registrierung einer Callback-URL sendet der Service Callback-Benachrichtigungen mit dem Jobstatus und den Erkennungsergebnissen.

Die Schnittstelle verwendet auf einem vom Benutzer angegebenen geheimen Schlüssel basierende HMAC-SHA1-Signaturen, um Authentifizierung und Datenintegrität für seine Benachrichtigungen zu gewährleisten. Ohne eine Callback-URL müssen Sie den Jobstatus und die Ergebnisse beim Service abfragen. Bei beiden Ansätzen verwenden Sie die Methode `POST /v1/recognitions`, um eine Erkennungsanforderung auszugeben.

Das folgende `curl`-Beispiel zeigt eine einfache asynchrone HTTP-Erkennungsanforderung. Die Anforderung enthält keine Callback-URL; Sie müssen daher den Service abfragen, um den Jobstatus und die resultierende Transkription zu erhalten.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @audio-file.flac
"{url}/v1/recognitions"
```
{: pre}
