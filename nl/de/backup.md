---

copyright:
  years: 2019
lastupdated: "2019-06-22"

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

# Sicherung und Wiederherstellung
{: #backup}

Damit eine Wiederherstellung nach einem Katastrophenfall möglich ist, müssen Sie eine Sicherungskopie von {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} erstellen und die Wiederherstellung des Service vorbereiten. Sie müssen selbst dafür sorgen, dass Sie Ihre Konfiguration, Ihre Anpassung und Ihre Nutzung des Service kennen. Sie sind ebenfalls dafür verantwortlich, alle Vorbereitungen für die erneute Erstellung einer Instanz des Service und für die Wiederherstellung Ihrer Daten zu treffen.
{: shortdesc}

Die Disaster-Recovery kann problematisch sein, falls in Ihrer Cloudlösung ein erheblicher Fehler auftritt, der auch einen möglichen Datenverlust einschließt. Bei einem Datenverlust müssen Sie Ihre Daten wiederherstellen, um die Serviceinstanz wieder in den aktuellen Zustand zu versetzen. 

Beim {{site.data.keyword.speechtotextshort}}-Service werden Daten für angepasste Sprachmodelle, angepasste Akustikmodelle und asynchrone Spracherkennungsanforderungen in der Cloud gespeichert. Für Ihren Disaster-Recovery-Plan müssen Sie auch diese Daten kennen, aufbewahren und auf eine Wiederherstellung vorbereiten. 

Die erneute Erstellung von angepassten Modellen aus gesicherten Daten kann besonders bei angepassten Akustikmodellen erheblich Zeit in Anspruch nehmen. Die Aufbewahrung paralleler Servicekonfigurationen eliminiert die mit der Disaster-Recovery verbundene Bearbeitungszeit.
{: note}

### Disaster-Recovery bei angepassten Sprachmodellen
{: #disaster-recovery-language}

Für angepasste Sprachmodelle müssen Sie die Modelle selbst sowie deren Korpora, Grammatiken und angepasste Wörter aufbewahren und auf eine erneute Erstellung und Wiederherstellung vorbereiten. Außerdem müssen Sie darauf vorbereitet sein, Ihre angepassten Sprachmodelle mit den zugehörigen Daten und Wörterressourcen erneut zu trainieren.

#### Angepasste Sprachmodelle sichern
{: #disaster-recovery-language-backup}

Bewahren Sie die folgenden Informationen zu Ihren angepassten Sprachmodellen auf:

-   Liste aller angepassten Sprachmodelle und ihrer Definitionen. So können Sie Informationen zu Ihren angepassten Modellen auflisten:
    -   Verwenden Sie die Methode `GET /v1/customizations`, um Informationen zu allen angepassten Modellen aufzulisten.
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}`, um Informationen zu einem angegebenen angepassten Modell aufzulisten.

Weitere Informationen finden Sie im Abschnitt  [Angepasste Sprachmodelle auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).
-   Kopien aller Korpustextdateien, die Sie zu Ihren angepassten Sprachmodellen hinzufügen. So können Sie Informationen zu den Korpora für Ihre angepassten Modelle auflisten:
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/corpora`, um alle Korpora für ein angepasstes Modell aufzulisten.
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/corpora/{corpus_name}`, um Informationen zu einem bestimmten Korpus für ein angepasstes Modell aufzulisten.

Weitere Informationen enthält der Abschnitt [Korpora für angepasstes Sprachmodell auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).
-   Kopien aller Grammatikdateien, die Sie zu Ihren angepassten Sprachmodellen hinzufügen. So können Sie Informationen zu den Grammatiken für Ihre angepassten Modelle auflisten:
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/grammars`, um Informationen zu allen Grammatiken für ein angepasstes Modell aufzulisten.
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/grammars/{grammar_name}`, um Informationen zu einer bestimmten Grammatik für ein angepasstes Modell aufzulisten.

    Weitere Informationen enthält der Abschnitt [Grammatiken für ein angepasstes Sprachmodell auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageGrammars#listGrammars).
-   Informationen zu allen angepassten Wörtern, die Sie direkt zu Ihren angepassten Sprachmodellen hinzufügen; hierzu gehören auch die Definitionen für die Klangähnlichkeit (sounds-like) und die optische Ausgabe (display-as). So können Sie Informationen zu den vokabularexternen Wörtern für Ihre angepassten Modelle auflisten:
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/words`, um Informationen zu allen Wörtern aus einem angepassten Modell aufzulisten. Mit dem Parameter `word_type` können Sie alle Wörter aus einem Modell (Wert `all`), vom Benutzer direkt hinzugefügte Wörter (Wert `user`), aus Korpora extrahierte Wörter (Wert `corpora`) oder durch Grammatiken erkannte Wörter (Wert `grammars`) auflisten.
    -   Verwenden Sie die Methode `GET /v1/customizations/{customization_id}/words/{word_name}`, um Informationen zu einem bestimmten Wort aus einem angepassten Modell aufzulisten.

    Weitere Informationen finden Sie im Abschnitt [Wörter aus angepasstem Sprachmodell auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).


Es hat sich bewährt, diese Informationen in einem Format aufzubewahren, das die erneute Erstellung Ihrer angepassten Sprachmodelle bei einem Fehler möglich macht. Wenn Sie die Informationen zu Ihren angepassten Modellen und ihren Daten aktiv verwalten und im Voraus die im folgenden Abschnitt aufgeführten Aufrufe vorbereiten, können Sie die Wiederherstellung so schnell wie möglich durchführen.

#### Angepasste Sprachmodelle wiederherstellen
{: #disaster-recovery-language-restore}

Falls eine Disaster-Recovery erforderlich werden sollte, können Sie Ihre angepassten Sprachmodelle und die zugehörigen Daten mithilfe der Sicherungsinformationen erneut erstellen:

1.  Verwenden Sie für die erneute Erstellung Ihrer angepassten Sprachmodelle die Methode `POST /v1/customizations`. Weitere Informationen hierzu finden Sie im Abschnitt [Angepasstes Sprachmodell erstellen](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language).
1.  Verwenden Sie zum Hinzufügen der Korpustextdateien zu Ihren angepassten Modellen die Methode `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`. Weitere Informationen finden Sie im Abschnitt [Korpus zum angepassten Sprachmodell hinzufügen](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addCorpus). 
1.  Verwenden Sie zum Hinzufügen der Grammatikdateien zu Ihren angepassten Modellen die Methode `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`. Weitere Informationen finden Sie im Abschnitt [Grammatik zu einem angepassten Sprachmodell hinzufügen](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
1.  Verwenden Sie zum Hinzufügen von mehreren Wörtern zu Ihren angepassten Modellen die Methode `POST /v1/customizations/{customization_id}/words`. Verwenden Sie zum Hinzufügen einzelner Wörter zu Ihren angepassten Modellen die Methode `PUT /v1/customizations/{customization_id}/words/{word_name}`. Weitere Informationen hierzu enthält der Abschnitt [Wörter zum angepassten Sprachmodell hinzufügen](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addWords).
1.  Verwenden Sie nach dem Wiederherstellen der Korpora, Grammatiken und angepassten Wörter zum Trainieren Ihrer angepassten Modelle die Methode `POST /v1/customizations/{customization_id}/train`. Weitere Informationen hierzu enthält der Abschnitt [Angepasstes Sprachmodell trainieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language).

Die Methoden, die Sie zum Hinzufügen von Korpora, Grammatiken und Wörtern sowie zum Trainieren eines angepassten Sprachmodells verwenden, werden asynchron ausgeführt. Sie müssen die Anforderungen überwachen, bis sie abgeschlossen sind.

Sie können nach und nach Daten hinzufügen und Ihre angepassten Sprachmodelle trainieren, statt alle Daten vor dem Trainieren der Modelle hinzuzufügen. Beispielsweise können Sie Ihre Korpora hinzufügen und anschließend Ihre Modelle trainieren, bevor Sie Grammatiken und einzelne Wörter hinzufügen. Sie können auch Schritt für Schritt einzelne Korpustextdateien, Grammatikdateien und Gruppen von angepassten Wörtern hinzufügen und Ihre Modelle damit trainieren.

### Disaster-Recovery bei angepassten Akustikmodellen
{: #disaster-recovery-acoustic}

Für angepasste Akustikmodelle müssen Sie die Modelle selbst sowie die zugehörigen Audioressourcen aufbewahren und auf eine erneute Erstellung und Wiederherstellung vorbereiten. Außerdem müssen Sie darauf vorbereitet sein, Ihre angepassten Akustikmodelle mit den zugehörigen Audioressourcen erneut zu trainieren.

#### Angepasste Akustikmodelle sichern
{: #disaster-recovery-acoustic-backup}

Bewahren Sie die folgenden Informationen zu Ihren angepassten Akustikmodellen auf:

-   Liste aller angepassten Akustikmodelle und ihrer Definitionen. So können Sie Informationen zu Ihren angepassten Modellen auflisten:
    -   Verwenden Sie die Methode `GET /v1/acoustic_customizations`, um Informationen zu allen angepassten Modellen aufzulisten.
    -   Verwenden Sie die Methode `GET /v1/acoustic_customizations/{customization_id}`, um Informationen zu einem angegebenen angepassten Modell aufzulisten.

Weitere Informationen finden Sie im Abschnitt [Angepasste Akustikmodelle auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic).
-   Kopien aller Audioressourcen (sowohl einzelne Audiodateien als auch Archivdateien), die Sie zu Ihren angepassten Akustikmodellen hinzufügen. So können Sie Informationen zu den Autioressourcen für Ihre angepassten Modelle auflisten:
    -   Verwenden Sie die Methode `GET /v1/acoustic_customizations/{customization_id}/audio`, um Informationen zu allen Audioressourcen für ein angepasstes Modell aufzulisten.
    -   Verwenden Sie die Methode `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`, um Informationen zu einer bestimmten Audioressource für ein angepasstes Modell aufzulisten.

    Weitere Informationen enthält der Abschnitt [Audioressourcen für ein angepasstes Akustikmodell auflisten](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

Es hat sich bewährt, diese Informationen in einem Format aufzubewahren, das die erneute Erstellung Ihrer angepassten Akustikmodelle bei einem Fehler möglich macht. Wenn Sie die Informationen zu Ihren angepassten Modellen und ihren Audioressourcen aktiv verwalten und im Voraus die im folgenden Abschnitt aufgeführten Aufrufe vorbereiten, können Sie die Wiederherstellung so schnell wie möglich durchführen.

#### Angepasste Akustikmodelle wiederherstellen
{: #disaster-recovery-acoustic-restore}

Falls eine Disaster-Recovery erforderlich werden sollte, können Sie Ihre angepassten Akustikmodelle und die zugehörigen Daten mithilfe der Sicherungsinformationen erneut erstellen:

1.  Verwenden Sie für die erneute Erstellung Ihrer angepassten Akustikmodelle die Methode `POST /v1/acoustic_customizations`. Weitere Informationen hierzu finden Sie im Abschnitt [Angepasstes Akustikmodell erstellen](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic).
1.  Verwenden Sie zum Hinzufügen der Audioressourcen zu Ihren angepassten Modellen die Methode `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`. Weitere Informationen hierzu enthält der Abschnitt [Audiodaten zum angepassten Akustikmodell hinzufügen](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio).
1.  Verwenden Sie nach dem Wiederherstellen der Audioressourcen die Methode `POST /v1/acoustic_customizations/{customization_id}/train`. Weitere Informationen finden Sie unter [Angepasstes Akustikmodell trainieren](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic).

Die Methoden, die Sie zum Hinzufügen von Audioressourcen und zum Trainieren eines angepassten Akustikmodells verwenden, werden asynchron ausgeführt. Sie müssen die Anforderungen überwachen, bis sie abgeschlossen sind.

Sie können nach und nach Audioressourcen hinzufügen und Ihre angepassten Akustikmodelle trainieren, statt alle Daten vor dem Trainieren der Modelle hinzuzufügen. Beispielsweise können Sie Ihre Audioressourcen einzeln nacheinander oder in Gruppen hinzufügen und Ihre Modelle mit Teilmengen der Audioressourcen statt gleichzeitig mit allen Audiodaten trainieren.

### Disaster-Recovery bei asynchronen Spracherkennungsjobs
{: #disaster-recovery-async}

Für die Spracherkennung mit der asynchronen HTTP-Schnittstelle müssen Sie die folgenden Informationen aufbewahren:

-   Alle Callback-URLs, die Sie zur Verwendung mit der asynchronen Schnittstelle in die Whitelist aufgenommen haben. Falls ein Fehler auftritt, müssen Sie möglicherweise die URLs mit der Methode `POST /v1/register_callback` erneut registrieren. Die Methode gibt eine entsprechende Antwort zurück, wenn eine URL bereits in eine Whitelist aufgenommen wurde.
-   Kopien der Audiodateien, die Sie zur Spracherkennung an die asynchrone Schnittstelle übergeben. Falls ein Fehler auftritt, bevor Sie die Ergebnisse eines abgeschlossenen asynchronen Jobs empfangen oder abgerufen haben, müssen Sie die Audiodateien mit der Methode `POST /v1/recognitions` erneut übergeben, nachdem der Service wiederhergestellt worden ist. Sobald Sie die Ergebnisse eines abgeschlossenen asynchronen Jobs erhalten haben, müssen Sie die Audiodateien nicht mehr aufbewahren.

Weitere Informationen enthält der Abschnitt [Asynchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-async). Wie bei den Sicherungsdaten für angepasste Modelle können Sie diese Informationen aktiv verwalten und sich so im Voraus auf die erneute Ausgabe der erforderlichen Anforderungen vorbereiten.
