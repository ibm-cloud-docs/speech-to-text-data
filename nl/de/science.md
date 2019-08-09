---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

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

# Der wissenschaftliche Hintergrund für den Service
{: #science}

{{site.data.keyword.IBM}} war schon in den frühen Sechzigerjahren ein Wegbereiter für die Forschung im Bereich der Spracherkennung (siehe [Pioneering Speech Recognition](https://www.ibm.com/ibm/history/ibm100/us/en/icons/speechreco/){: external}). Beispielsweise beschreiben [Bahl, Jelinek und Mercer (1983)](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#bahl1983) den grundlegenden mathematischen Ansatz für die Spracherkennung, der von fast allen modernen Spracherkennungssystemen verwendet wird. [Jelinek (1985)](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#jelinek1985) beschreibt die Erstellung des ersten Echtzeit-Spracherkennungssystems für umfangreiche Wörterbestände aus Diktaten. Darüber hinaus werden in dieser Veröffentlichung Probleme beschrieben, die auch beim heutigen Stand der Forschung weiterhin ungelöst sind.
{: shortdesc}

{{site.data.keyword.IBM_notm}} knüpft jetzt mit {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} an diese traditionsreiche Forschung und Entwicklung an. {{site.data.keyword.IBM_notm}} hat eine Spracherkennungsgenauigkeit bei den öffentlichen Vergleichsdaten für Conversational Telephone Speech (CTS) ([Saon und andere, 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#saon2017)) und Broadcast News-Transkription (BN) ([Thomas und andere, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#thomas2019)) demonstriert, die einen Branchenrekord darstellt. {{site.data.keyword.IBM_notm}} hat nicht nur die Effektivität akustischer Modellierung demonstriert, sondern auch neuronale Netze für die Sprachmodellierung eingesetzt ([Kurata und andere, 2017a](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2017a) und [Kurata und andere, 2017b](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2017a)). 

In den folgenden Mitteilungen sind die jüngsten Errungenschaften von {{site.data.keyword.IBM_notm}} im Bereich der Spracherkennung zusammengefasst: 

-   [Reaching new records in speech recognition](https://www.ibm.com/blogs/watson/2017/03/reaching-new-records-in-speech-recognition/){: external}
-   [{{site.data.keyword.IBM_notm}} Breaks Industry Record for Conversational Speech Recognition by Extending Deep Learning Technologies](https://www-03.ibm.com/press/us/en/pressrelease/51790.wss){: external}
-   [{{site.data.keyword.IBM_notm}} Sets New Transcription Performance Milestone on Automatic Broadcast News Captioning](https://www.ibm.com/blogs/research/2019/05/automatic-broadcast-news-captioning/){: external}

Diese Errungenschaften tragen dazu bei, die {{site.data.keyword.IBM_notm}} Speech-Services weiter voranzubringen. Aktuelle Ideen, die dem cloudbasierten {{site.data.keyword.speechtotextshort}}-Service am besten entsprechen: 

-   *Für die Sprachmodellierung* setzt {{site.data.keyword.IBM_notm}} ein auf neuronalen Netzen basierendes Sprachmodell ein, um Trainingtext zu generieren ([Suzuki und andere, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#suzuki2019)). 
-   *Für die akustische Modellierung* verwendet {{site.data.keyword.IBM_notm}} wegen der Ressourcenbeschränkungen der Cloud ein relativ kompaktes Modell. Für das Training dieses kompakten Modells verwendet {{site.data.keyword.IBM_notm}} "Teacher-Student Training / Knowledge Distillation", d. h. Training in Form von Lehrer und Schüler sowie Destillation von Wissen. Große und starke neuronale Netze, z. B. Long Short-Term Memory (LSTM), VGG und Residual Network (ResNet), werden zuerst trainiert. Die Ausgabe dieser Netze wird dann als Lehrersignale zum Trainieren eines kompakten Modells für die tatsächliche Implementierung verwendet ([Fukuda und andere, 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#fukuda2017)). 

Darüber hinaus konzentriert sich {{site.data.keyword.IBM_notm}} zusätzlich auf End-to-End-Modellierung. Beispielsweise wurde eine leistungsstarke Modellierungspipeline für direkte Akustik-Wort-Modelle eingerichtet ([Audhkhasi und andere, 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#audhkhasi2017) und [Audhkhasi und andere, 2018](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#audhkhasi2018)), die derzeit weiter verbessert wird ([Saon und andere, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#saon2019)). Darüber hinaus gibt es Bemühungen zur Erstellung kompakter End-to-End-Modelle für eine spätere Implementierung in der Cloud ([Kurata und Audhkhasi, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2019)). 

Weitere Informationen zu der wissenschaftlichen Forschung, die hinter dem Service steht, finden Sie in den Dokumenten, die im Abschnitt [Referenzinformationen zur Forschung](/docs/services/speech-to-text-data?topic=speech-to-text-data-references) aufgelistet sind. 
