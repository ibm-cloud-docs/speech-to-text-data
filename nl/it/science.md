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

# La scienza dietro il servizio
{: #science}

Come descritto da [Pioneering Speech Recognition](https://www.ibm.com/ibm/history/ibm100/us/en/icons/speechreco/){: external}, {{site.data.keyword.IBM}} è stata una pioniera della ricerca nel campo del riconoscimento vocale fin dai primi anni '60. Ad esempio, [Bahl, Jelinek, and Mercer (1983)](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#bahl1983) descrive l'approccio matematico di base al riconoscimento vocale impiegato praticamente in tutti i sistemi di riconoscimento vocale moderni. E [Jelinek (1985)](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#jelinek1985) descrive la creazione del primo sistema di riconoscimento vocale con un ampio vocabolario e in tempo reale per la dettatura. Questo documento descrive anche problemi che sono ancora oggi argomenti di ricerca irrisolti.
{: shortdesc}

{{site.data.keyword.IBM_notm}} continua questa ricca tradizione di ricerca e sviluppo con {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. {{site.data.keyword.IBM_notm}} ha dimostrato l'accuratezza del riconoscimento vocale della registrazione del settore sui dataset di riferimento pubblico per Conversational Telephone Speech (CTS) ([Saon and others, 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#saon2017)) e la trascrizione Broadcast News (BN) ([Thomas and others, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#thomas2019)). {{site.data.keyword.IBM_notm}} ha utilizzato reti neurali per la modellazione della lingua ([Kurata and others, 2017a](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2017a) e [Kurata and others, 2017b](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2017a)), oltre a dimostrare l'efficacia della modellazione acustica. 

I seguenti annunci riepilogano i risultati sul riconoscimento vocale più recenti di {{site.data.keyword.IBM_notm}}: 

-   [Reaching new records in speech recognition](https://www.ibm.com/blogs/watson/2017/03/reaching-new-records-in-speech-recognition/){: external}
-   [{{site.data.keyword.IBM_notm}} Breaks Industry Record for Conversational Speech Recognition by Extending Deep Learning Technologies](https://www-03.ibm.com/press/us/en/pressrelease/51790.wss){: external}
-   [{{site.data.keyword.IBM_notm}} Sets New Transcription Performance Milestone on Automatic Broadcast News Captioning](https://www.ibm.com/blogs/research/2019/05/automatic-broadcast-news-captioning/){: external}

Questi risultati contribuiscono a migliorare ulteriormente i servizi vocali di {{site.data.keyword.IBM_notm}}. Le idee recenti che meglio si adattano al servizio {{site.data.keyword.speechtotextshort}} basato su cloud includono

-   *Per la modellazione della lingua,* {{site.data.keyword.IBM_notm}} utilizza un modello di lingua basato sulla rete neurale per generare testo di addestramento ([Suzuki and others, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#suzuki2019)).
-   *Per la modellazione acustica,* {{site.data.keyword.IBM_notm}} utilizza un modello abbastanza compatto per conformarsi alle limitazioni delle risorse del cloud. Per addestrare questo modello compatto, {{site.data.keyword.IBM_notm}} utilizza un approccio "addestramento insegnante-studente/distillazione della conoscenza." Le reti neurali grandi e complesse come Long Short-Term Memory (LSTM), VGG e Residual Network (ResNet) vengono addestrate per prime. L'output di queste reti viene poi utilizzato come segnali insegnante per addestrare un modello compatto per la distribuzione effettiva ([Fukuda and others, 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#fukuda2017)).

Per superare ulteriormente i limiti, {{site.data.keyword.IBM_notm}} si concentra anche sulla modellazione end-to-end. Ad esempio, è stata stabilita una pipeline di modellazione complessa per i modelli Direct Acoustic-to-Word ([Audhkhasi and others, 2017](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#audhkhasi2017) e [Audhkhasi and others, 2018](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#audhkhasi2018)) che ora sta ulteriormente migliorando ([Saon and others, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#saon2019)). Sta inoltre compiendo ulteriori sforzi per creare modelli end-to-end compatti per la distribuzione futura nel cloud ([Kurata and Audhkhasi, 2019](/docs/services/speech-to-text-data?topic=speech-to-text-data-references#kurata2019)).

Per ulteriori informazioni sulla ricerca scientifica alla base del servizio, vedi i documenti elencati in [Riferimenti di ricerca](/docs/services/speech-to-text-data?topic=speech-to-text-data-references).
