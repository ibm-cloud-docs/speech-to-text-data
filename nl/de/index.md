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

# Produktinformation
{: #about}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} stellt Spracherkennungsfunktionen für Ihre Anwendungen bereit. Er nutzt maschinelles Lernen, um menschliche Stimme mithilfe von Kenntnissen über Grammatik, Sprachstruktur sowie die Bildung von Audio- und Sprachsignalen präzise zu transkribieren. Der Service aktualisiert und optimiert die Transkription kontinuierlich, sobald er weitere Spracheingabe empfängt.
{: shortdesc}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} bietet verschiedene Schnittstellen, die es für jede Anwendung geeignet machen, bei der die Eingabe aus Sprache und die Ausgabe aus einer Transkription in Text besteht. Beispiele für solche Anwendungen:

-   Sprachsteuerung von Anwendungen, integrierten Einheiten und Fahrzeugzubehör
-   Transkriptionen von Besprechungen und Telefonkonferenzen
-   Diktate von E-Mail-Nachrichten und Memos

Der Service ist eine ideale Lösung für die Extraktion hochwertiger Sprachtranskripte aus den Audiodaten eines Call-Centers. Im Bereich der Finanzdienstleistungen, des Gesundheits- und Versicherungswesens sowie der Telekommunikation können für die Cloud native Anwendungen zum Zweck der Kundenbetreuung, der Berücksichtigung von Kundenforderungen, der Unterstützung durch Mitarbeiter und für andere Lösungen entwickelt werden. 

Informationen zur Installation und Konfiguration von {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} finden Sie in [Service installieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-install). 

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} basiert auf dem {{site.data.keyword.speechtotextfull}}-Service in der öffentlichen {{site.data.keyword.cloud_notm}}. Weitere Informationen zum öffentlichen Service finden Sie in [Produktinformation {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.
{: note}

## Unterstützte Schnittstellen
{: #interfaces}

Für die Spracherkennung bietet der {{site.data.keyword.speechtotextshort}}-Service mehrere Schnittstellen: 

-   [WebSocket-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) zum Aufbau von permanenten Vollduplexverbindungen zum Service mit niedriger Latenzzeit. Mit einer einzigen Anforderung können Sie maximal 100 MB Audiodaten an den Service übergeben.
-   [Synchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) für HTTP-Basisaufrufe des Service. Mit einer Anforderung können Sie maximal 100 MB Audiodaten übergeben.
-   [Asynchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) für nicht blockierende Aufrufe des Service. Mit einer Anforderung können Sie bis zu 1 GB Audiodaten übergeben.

Der Service bietet darüber hinaus eine [Anpassungsschnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization), mit der Sie die Spracherkennung für Ihre Sprache und Ihre akustischen Anforderungen optimieren können. Hierbei können Sie das Vokabular eines Modells durch fachspezifische Terminologie erweitern oder ein Modell für die akustischen Merkmale Ihrer Audiodaten anpassen. Außerdem können Sie [Grammatiken](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) hinzufügen, um die durch den Service erkennbaren Ausdrücke einzuschränken.

-   Informationen zur Ausführung von Anforderungen mit diesen {{site.data.keyword.speechtotextshort}}-Schnittstellen finden Sie in [Anforderungen an den Service ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests). 
-   Beispiele für Basisanforderungen zur Spracherkennung mit jeder Schnittstelle des Service enthält der Abschnitt [Erkennungsanforderung ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Eine allgemeine Beschreibung der Anwendungsentwicklung mit dem Service finden Sie unter [Übersicht für Entwickler](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).

SDKs sind in vielen Programmiersprachen verfügbar, um die Verwendung des Service zu vereinfachen. Weitere Informationen finden Sie in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external}. 

## Eingabefunktionen
{: #inputFeatures}

Die Schnittstellen des Service nutzen gemeinsam zahlreiche gängige Eingabefunktionen, um Sprache in Text zu transkribieren:

-   [Audioformate](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats) - Sie können Audiodaten in den Formaten 'Ogg' oder 'Web Media' (WebM) mit Opus- oder Vorbis-Codec, MP3 (oder MPEG), WAV (Waveform Audio File Format), FLAC (Free Lossless Audio Codec), linearer 16-Bit-Pulscodemodulation (PCM), G.729 sowie A-Law-, Mu-Law- (bzw. U-Law) und Basisaudiodaten transkribieren. Wenn Sie ein Format verwenden, das Komprimierung unterstützt, können Sie die Menge der Audiodaten maximieren, die Sie mit einer Anforderung senden können.
-   [Sprachen und Modelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-models) - Sie können Audiodaten mithilfe von Breitband- oder Schmalbandmodellen transkribieren. Verwenden Sie Breitbandmodelle für Audiodaten, die mit einer Frequenz von mindestens 16 kHz abgetastet werden. Verwenden Sie Schmalbandmodelle für Audiodaten, die mit einer Frequenz von mindestens 8 kHz abgetastet werden.
-   [Übertragung von Audiodaten](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission) - Sie können Audiodaten als zusammenhängenden Strom von Datenblöcken oder in Form einer Einmallieferung übergeben, bei der alle Daten gleichzeitig übertragen werden. Beim Streaming setzt der Service [Zeitlimits](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts) für Inaktivität und Sitzungen durch.

## Ausgabefunktionen
{: #outputFeatures}

Die Mehrzahl der Schnittstellen unterstützt außerdem die folgenden gängigen Ausgabefunktionen:

-   Die Funktion [Sprecherbezeichnungen](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels) erkennt unterschiedliche Sprecher aus Audiodaten in amerikanischem Englisch, Japanisch oder Spanisch. In der Transkription sind die Beiträge jedes einzelnen Sprechers zu einem Gespräch mit mehreren Teilnehmern gekennzeichnet. (Hierbei handelt es sich um Beta-Funktionalität.)
-   Die Funktion [Schlüsselworterkennung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting) ermittelt gesprochene Wortfolgen, die mit angegebenen Schlüsselwortzeichenfolgen übereinstimmen, auf einem benutzerdefinierten Konfidenzniveau. Die auch als 'Keyword Spotting' bezeichnete Schlüsselworterkennung ist besonders von Nutzen, wenn einzelne Wortfolgen in den Audiodaten wichtiger als die vollständige Transkription sind. Beispielsweise könnte ein Kundendienstsystem durch die Erkennung von Schlüsselwörtern bestimmen, wie Benutzeranfragen weitergeleitet werden müssen.
-   Die Funktion [Zwischenergebnisse](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim) gibt während der laufenden Verarbeitung der Transkription kontinuierlich präzisierte Hypothesen zurück. Nach Abschluss der Transkription gibt der Service die Endergebnisse zurück. Zwischenergebnisse sind nur bei Verwendung der WebSocket-Schnittstelle verfügbar.
-   Die Funktion [Maximale Anzahl Alternativen](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives) stellt mögliche alternative Transkriptionen bereit. Der Service gibt die Endergebnisse mit der größen Übereinstimmungswahrscheinlichkeit an.
-   Die Funktion [Wortalternativen](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives) fordert alternative Wörter an, die den Wörtern einer Transkription akustisch ähneln.
-   Die Funktion [Wortkonfidenz](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence) gibt für jedes Wort einer Transkription das Konfidenzniveau zurück.
-   Die Funktion [Wortzeitmarken](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps) gibt Zeitmarken für den Anfang und das Ende jedes Wortes in einer Transkription zurück.
-   Die Funktion [Intelligente Formatierung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting) konvertiert Datumsangaben, Uhrzeiten, Zahlen, Währungswerte, Telefonnummern und Internetadressen in der Endfassung der Transkriptionen in besser lesbare und herkömmliche Formate. Für amerikanisches Englisch können Sie außerdem Schlüsselwortphrasen angeben, damit die Endfassung von Transkriptionen bestimmte Interpunktionssymbole enthalten. Die intelligente Formatierung wird für Audiodaten in amerikanischem Englisch, Japanisch und Spanisch unterstützt. (Hierbei handelt es sich um Beta-Funktionalität.)
-   Die Funktion [Zahlenschwärzung](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction) macht numerische Daten in der Endfassung einer Transkription unkenntlich. Zweck der Schwärzung ist es, sensible personenbezogene Daten wie beispielsweise Kreditkartennummern aus Transkriptionen zu entfernen. Die Funktion wird für Audiodaten in amerikanischem Englisch, Japanisch und Koreanisch unterstützt. (Hierbei handelt es sich um Beta-Funktionalität.)
-   Die Funktion [Vulgäre Ausdrücke filtern](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter) zensiert Vulgärsprache in Transkriptionen für amerikanisches Englisch.
-   [Verarbeitungsmetriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) stellen detaillierte Zeitinformationen über die Analyse der Audioeingabedaten durch den Service bereit. 
-   [Audiometriken](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) stellen detaillierte Informationen über die Signalmerkmale der Audioeingabedaten bereit. 

## Sprachunterstützung
{: #languages}

Der Service bietet Modelle für die folgenden Sprachen: brasilianisches Portugiesisch, Französisch, Deutsch, Japanisch, Koreanisch, Mandarin, modernes Hocharabisch, Spanisch, britisches Englisch und amerikanisches Englisch. Es werden durch den Service nicht alle Funktionen für alle Sprachen unterstützt. Zudem werden für unterschiedliche Sprachen einige Funktionen als allgemein verfügbare Funktionen für den Produktionseinsatz unterstützt, während andere Funktionen als Betaversion angeboten werden.

-   Die WebSocket-Schnittstelle und die synchronen und asynchronen HTTP-Schnittstellen sind für alle Sprachen allgemein verfügbar. 
-   Der Service bietet sowohl Breitband- als auch Schmalbandmodelle für alle Sprachen. Weitere Informationen finden Sie unter [Sprachen und Modelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-models). 
-   Einige Spracherkennungsfunktionen sind nur für bestimmte Sprachen und bei bestimmten Schnittstellen verfügbar. Weitere Informationen enthält der Abschnitt [Parameterübersicht](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   Die Anpassungsschnittstelle für Sprachmodelle ist für alle Sprachen allgemein verfügbar. Die Anpassungsschnittstelle für Akustikmodelle ist für alle Sprachen als Beta-Funktionalität verfügbar. Weitere Informationen finden Sie unter [Sprachunterstützung bei der Anpassung](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).

## Service ausprobieren
{: #tryOut}

Beispiele für die Ausführung des {{site.data.keyword.speechtotextshort}}-Service bieten die folgenden Quellen:

-   Eine [Kurzdemo](https://speech-to-text-demo.ng.bluemix.net/){: external} zeigt die Transkription von Text aus einer Streaming-Audio-Eingabe oder einer hochgeladenen Datei. 
-   Anwendungen in den {{site.data.keyword.ibmwatson}} [Starter-Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} veranschaulichen den Service. 
-   Im {{site.data.keyword.watson}}-Blogbeitrag [Getting robots to listen: Using {{site.data.keyword.watson}}'s {{site.data.keyword.speechtotextshort}} service](https://www.ibm.com/blogs/watson/2016/07/getting-robots-listen-using-watsons-speech-text-service/){: external} erfahren Sie, wie die WebSocket-Schnittstelle mit Python eingesetzt wird, um Sprache aus Audiodaten zu extrahieren. Der Beitrag bietet ein umfassendes Lernprogramm, das den verwendeten Code und die betreffenden Schritte veranschaulicht.
