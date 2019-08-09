---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-26"

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

# Übersicht für Entwickler
{: #developerOverview}

Auf die Funktionalität von {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} können Sie mithilfe einer WebSocket-Schnittstelle oder unter Verwendung von synchronen bzw. asynchronen HTTP-Schnittstellen für Representational State Transfer (REST) zugreifen. Außerdem können Sie die Sprachmodelle des Service an Ihr Fachgebiet und Ihre Umgebung anpassen. Zur Vereinfachung der Anwendungsentwicklung in vielen Programmiersprachen sind SKDs verfügbar.
{: shortdesc}

Für die Authentifizierung beim {{site.data.keyword.speechtotextshort}}-Service übergeben Sie mit jeder Anforderung ein Zugriffstoken. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} ist eine Multi-Tenant-Cloudlösung. Mit Ihren Berechtigungsnachweisen ist nur Zugriff auf Ihre Daten möglich, und Ihre Daten werden von anderen Benutzern isoliert.


## Programmierung beim Service
{: #programming}

Im Abschnitt [Erkennungsanforderung ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request) erfahren Sie, wie Sie mit jeder Programmierschnittstelle des Service eine Basistranskription anfordern:

-   Die [WebSocket-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) bietet eine effiziente Implementierung über eine Vollduplexverbindung mit niedriger Latenzzeit und hohem Durchsatz.
-   Die [synchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) bietet eine Basisschnittstelle für die Transkription von Audiodaten mit blockierenden Anforderungen.
-   Die [asynchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) bietet eine nicht blockierende Schnittstelle, mit der Sie eine Callback-URL für den Empfang von Benachrichtigungen registrieren oder den Service nach Jobstatus und Ergebnissen abfragen können.

Die Schnittstellen stellen zwar vergleichbare Spracherkennungsfunktionen zur Verfügung, aber je nach der verwendeten Schnittstelle müssen Sie denselben Parameter möglicherweise als Anforderungsheader, als Abfrageparameter oder als Parameter eines JSON-Objekts angeben. 

Die WebSocket-Schnittstelle und die synchrone HTTP-Schnittstelle akzeptieren bei einer einzelnen Anforderung Audiodaten mit einer Größe von maximal 100 MB. Die asynchrone HTTP-Schnittstelle akzeptiert Audiodaten mit einer maximalen Größe von 1 GB bei einer Anforderung. 

-   Informationen zur Ausführung von Anforderungen mit diesen {{site.data.keyword.speechtotextshort}}-Schnittstellen finden Sie in [Anforderungen an den Service ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests). 
-   Beispiele für Basisanforderungen zur Spracherkennung mit jeder Schnittstelle des Service enthält der Abschnitt [Erkennungsanforderung ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Eine Beschreibung aller verfügbaren Parameter für die Spracherkennung finden Sie in der [Parameterübersicht](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   Beschreibungen aller Methoden und ihrer Parameter sind zusammen mit Beispielen in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external} zu finden. 

## Vorteile der WebSocket-Schnittstelle
{: #advantages}

Die WebSocket-Schnittstelle bietet gegenüber den HTTP-Schnittstellen eine Reihe von Vorteilen:

-   Die WebSocket-Schnittstelle stellt einen Kanal für die Vollduplexübertragung mit einem einzigen Socket zur Verfügung. Mithilfe der Schnittstelle kann der Client über eine einzige Verbindung asynchron Anforderungen und  Audiodaten an den Service senden und Ergebnisse empfangen.
-   Sie bietet eine viel einfachere und leistungsfähigere Programmiererfahrung. Der Service sendet ereignisgesteuerte Antworten auf die Nachrichten des Clients, was eine Abfrage des Servers durch den Client überflüssig macht.
-   Sie ermöglicht Ihnen die Einrichtung und unbegrenzte Verwendung einer einzigen authentifizierten Verbindung. Bei den HTTP-Schnittstellen müssen Sie sich für jeden Aufruf des Service authentifizieren.
-   Sie verringert die Latenzzeit. Erkennungsergebnisse treffen schneller ein, weil der Service sie direkt an den Client sendet. Bei den HTTP-Schnittstellen benötigen Sie vier verschiedene Anforderungen und Verbindungen, um dieselben Ergebnisse zu erzielen.
-   Sie reduziert die Netzauslastung. Das WebSocket-Protokoll ist ein einfaches Protokoll. Bei diesem Protokoll ist für eine Spracherkennung im Live-Modus nur eine einzige Verbindung erforderlich.
-   Sie ermöglicht das direkte Streaming von Audiodaten aus Browsern (HTML5-WebSocket-Clients) an den Service.

## Anpassung des Service
{: #customizing}

Mithilfe der [Anpassungsschnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) können Sie angepasste Modelle erstellen, um die Spracherkennungsfunktionen des Service zu verbessern:

-   In [angepassten  Sprachmodellen](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate) können Sie fachspezifische Wörter für ein Basismodell definieren. Angepasste Sprachmodelle erweitern das Grundvokabular des Service durch spezifische Terminologie für Fachgebiete wie Medizin und Jura.
-   In [angepassten Akustikmodellen](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic) können Sie ein Basismodell an die akustischen Besonderheiten Ihrer Umgebung und Sprecher anpassen. Angepasste Akustikmodelle verbessern die Fähigkeit des Service, Sprache bei bestimmten akustischen Besonderheiten zu erkennen.
-   In [Grammatiken](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) können Sie die vom Service erkennbaren Ausdrücke auf die in den Regeln der Grammatik definierten Ausdrücke beschränken. Durch die Einschränkung des Suchbereichs auf gültige Zeichenfolgen kann der Service Ergebnisse schneller und präziser liefern. Grammatiken werden bei angepassten Sprachmodellen unterstützt.

Die Verwendung eines angepassten Sprachmodells und/oder angepassten Akustikmodells ist bei jeder Schnittstelle des Service möglich.

## Metriken abrufen
{: #overview-metrics}

Der Service bietet zwei Typen optionaler Metriken für Spracherkennungsanforderungen: 

-   [Verarbeitungsmetriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) stellen detaillierte Zeitinformationen über die Analyse der Audioeingabedaten durch den Service bereit. Der Service gibt die Metriken in festgelegten Intervallen und mit Transkriptionsereignissen zurück, z. B. als Zwischen- und Endergebnisse. Mithilfe der Metriken können Sie den Fortschritt des Service bei der Transkription der Audiodaten messen. 
-   [Audiometriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) stellen detaillierte Informationen über die Signalmerkmale der Audioeingabedaten bereit. In den Ergebnissen sind Metriken für die gesamten Audioeingabedaten zum Abschluss der Sprachverarbeitung zusammengefasst. Mithilfe der Metriken können Sie die Merkmale und die Qualität der Audiodaten feststellen. 

Sie können Verarbeitungsmetriken mit der WebSocket-Schnittstelle und mit der asynchronen HTTP-Schnittstelle anfordern. Audiometriken können Sie mit jeder Schnittstelle des Service anfordern. In der Standardeinstellung gibt der Service keine Metriken zurück. 

## CORS-Unterstützung
{: #cors}

Der Service unterstützt Cross-Origin Resource Sharing (CORS). Mithilfe von CORS können Webseiten Ressourcen direkt aus einer fremden Domäne anfordern. CORS umgeht die Sicherheitsrichtlinie für einen identischen Ursprung, die solche Anforderungen andernfalls verhindert. Da der Service CORS unterstützt, kann eine Webseite direkt mit dem Service kommunizieren, ohne die Anforderung über den Webserver zu übergeben, der die Seite hostet.

Beispielsweise kann eine Webseite, die aus einem Server in {{site.data.keyword.cloud}} geladen wird, die Anpassungs-API unter Umgehung des {{site.data.keyword.cloud_notm}}-Servers direkt aufrufen. Weitere Informationen finden Sie unter [enable-cors.org](https://enable-cors.org/){: external}. 

## Software-Development-Kits verwenden
{: #sdks}

Für den {{site.data.keyword.speechtotextshort}}-Service sind SDKs verfügbar, die die Entwicklung von Sprachanwendungen vereinfachen. {{site.data.keyword.ibmwatson}} SDKs stehen für viele gängige Programmiersprachen und Plattformen zur Verfügung.

-   Eine vollständige Liste der SDKs und Links zu den SDKs bei GitHub finden Sie im Abschnitt [SDKs verwenden](/docs/services/watson?topic=watson-using-sdks).
-   Ausführliche Informationen zu allen Methoden der Node-, Java&trade;-, Python-, Ruby- und Go-SDKs für den {{site.data.keyword.speechtotextshort}}-Service finden Sie in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external}. 
