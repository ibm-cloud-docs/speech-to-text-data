---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-25"

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
{:download: .download}

# Lernprogramm 'Einführung'
{: #gettingStarted}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} transkribiert Audiodaten in Text und aktiviert auf diese Weise Sprachtranskriptionsfunktionalität für Anwendungen. Dieses curl-basierte Lernprogramm unterstützt Sie beim schnellen Einstieg in die Verwendung des Service. In den Beispielen wird veranschaulicht, wie Sie die Methode `POST /v1/recognize` des Service aufrufen, um eine Transkription anzufordern.
{: shortdesc}

## Vorbereitende Schritte
{: #before-you-begin}

Damit Sie {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} verwenden können, müssen Sie zunächst die folgenden Schritte ausführen: 

1.  Stellen Sie eine Instanz von {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} bereit. Weitere Informationen zur Bereitstellung finden Sie in [Service installieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-install). 
1.  Wählen Sie im Menü des {{site.data.keyword.icp4dfull_notm}}-Web-Clients **Eigene Instanzen** aus. 
1.  Klicken Sie auf die {{site.data.keyword.speechtotextshort}}-Instanz, um die Übersichtsseite zu öffnen. Kopieren Sie die Berechtigungsnachweiswerte für `{token}` und `{URL}`. 

### curl-Beispiele verwenden
{: #getting-started-curl}

In diesem Lernprogramm wird der Befehl `curl` verwendet, um Methoden der HTTP-Schnittstelle des Service aufzurufen. Stellen Sie sicher, dass der Befehl `curl` in Ihrem System installiert ist. 

1.  Führen Sie den folgenden Befehl in der Befehlszeile aus, um zu testen, ob `curl` installiert ist. Wenn in der Ausgabe die `curl`-Version aufgelistet wird, die Secure Sockets Layer (SSL) unterstützt, sind Sie für das Lernprogramm bereit. 

    ```bash
    curl -V
    ```
    {: pre}

1.  Falls erforderlich, installieren Sie die Version von `curl` (SSL-fähig) für Ihr Betriebssystem (siehe [curl.haxx.se](https://curl.haxx.se/){: external}). 

Lassen Sie die geschweiften Klammern in den Beispielen weg. Sie geben Variablenwerte an.
{: tip}

## Schritt 1: Audiodaten ohne Optionen transkribieren
{: #transcribe}

Rufen Sie die Methode `POST /v1/recognize` auf, um eine Basistranskription einer FLAC-Audiodatei ohne zusätzliche Parameter anzufordern.

1.  Laden Sie die Audiobeispieldatei <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a> herunter.
1.  Geben Sie den folgenden Befehl aus, um die Methode `/v1/recognize` des Service für eine Basistranskription ohne Parameter aufzurufen. Beim Beispiel wird der Typ der Audiodaten (`audio/flac`) mit dem Header `Content-Type` angegeben. Das Beispiel verwendet für die Transkription das Standardsprachmodell `en-US_BroadbandModel`.
    -   Ersetzen Sie `{token}` durch das Zugriffstoken für Ihre Serviceinstanz. 
    -   Ersetzen Sie `{url}` durch die URL für Ihre Serviceinstanz. 
    -   Ändern Sie den Wert für `{path_to_file}`, um die Position der Datei `audio-file.flac` anzugeben.

    *Windows-Benutzer* müssen den umgekehrten Schrägstrich (``\`) am Ende jeder Zeile durch ein Winkelzeichen (``^`) ersetzen. Stellen Sie sicher, dass keine nachgestellten Leerzeichen vorhanden sind.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize"
    ```
    {: pre}

    Der Service gibt die folgenden Transkriptionsergebnisse zurück:

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "confidence": 0.96,
          "transcript": "several tornadoes touch down as a line of
severe thunderstorms swept through Colorado on Sunday "
        }
      ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Schritt 2: Audiodaten mit Optionen transkribieren
{: #transcribeOptions}

Rufen Sie die Methode `POST /v1/recognize` auf, um dieselbe FLAC-Audiodatei zu transkribieren. Geben Sie nun jedoch zwei Transkriptionsparameter an.

1.  Laden Sie bei Bedarf die Audiobeispieldatei <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link" title="Symbol für externen Link"></a> herunter.
1.  Geben Sie den folgenden Befehl aus, um die Methode `/v1/recognize` des Service mit zwei zusätzlichen Parametern aufzurufen. Legen Sie für den Parameter `timestamps` die Einstellung `true` fest, damit der Anfang und das Ende jedes Wortes im Audiodatenstrom angegeben werden. Geben Sie für den Parameter `max_alternatives` den Wert `3` an, um die drei wahrscheinlichsten Alternativen für die Transkription zu erhalten. Beim Beispiel wird der Header `Content-Type` verwendet, um den Typ der Audiodaten anzugeben (`audio/flac`); die Anforderung verwendet das Standardmodell `en-US_BroadbandModel`.
    -   Ersetzen Sie `{token}` durch das Zugriffstoken für Ihre Serviceinstanz. 
    -   Ersetzen Sie `{url}` durch die URL für Ihre Serviceinstanz. 
    -   Ändern Sie den Wert für `{path_to_file}`, um die Position der Datei `audio-file.flac` anzugeben.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize?timestamps=true&max_alternatives=3"
    ```
    {: pre}

    Der Service gibt die folgenden Ergebnisse zurück, die Zeitmarken und drei alternative Transkriptionen enthalten:

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "timestamps": [
                ["several":, 1.0, 1.51],
                ["tornadoes":, 1.51, 2.15],
                ["touch":, 2.15, 2.5],
                . . .
              ]
            },
            {
              "confidence": 0.96,
          "transcript": "several tornadoes touch down as a line of
severe thunderstorms swept through Colorado on Sunday "
        },
            {
              "transcript": "several tornadoes touched down as a line of
severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touch down as a line of
severe thunderstorms swept through Colorado and Sunday "
        }
      ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Nächste Schritte

-   Informieren Sie sich im Abschnitt [Übersicht für Entwickler](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview) über die Schnittstellen und SDKs, die zur Ausgabe von Spracherkennungsanforderungen verfügbar sind.
-   Informationen zur Ausführung von Anforderungen im Service finden Sie in [Anforderungen an den Service ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests). 
-   Beschäftigen Sie sich mit den Basisanforderungen für die Spracherkennung, die für jede Schnittstelle des Service unter [Erkennungsanforderung ausgeben](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request) beschrieben sind.
-   Ausführliche Informationen zu allen Methoden der Serviceschnittstellen sind in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data){: external} zu finden. 
