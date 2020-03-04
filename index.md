---

Copyright:
  years: 2018, 2020
lastupdated: "2020-03-04"

subcollection: speech-to-text-data

---

{:support: data-reuse='support'}
{:help: .help}
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

# About
{: #about}

**Service update:** *{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} was updated on 28 February 2020. You can now specify the pause interval at which the service splits a transcript into multiple final results. You can also direct the service to split the transcript into multiple final results for semantic features such as sentences. For more information, see the [Version 1.1.3 service update](/docs/speech-to-text-data?topic=speech-to-text-data-release-notes#v113) in the release notes.*

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} provides speech recognition capabilities for your applications. The service leverages machine learning to combine knowledge of grammar, language structure, and the composition of audio and voice signals to accurately transcribe the human voice. It continuously updates and refines its transcription as it receives more speech.
{: shortdesc}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} provides various interfaces that make it suitable for any application where speech is the input and a textual transcript is the output. Example applications include

-   Voice control of applications, embedded devices, and vehicle accessories
-   Transcribing meetings and conference calls
-   Dictating email messages and notes

The service is ideal for clients who need to extract high-quality speech transcripts from call center audio. Clients in industries such as financial services, healthcare, insurance, and telecommunication can develop cloud-native applications for customer care, customer voice, agent assistance, and other solutions.

For information about installing and configuring {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, see [Installing the Watson Speech to Text add-on](/docs/speech-to-text-data?topic=speech-to-text-data-stt-installing).

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} is based on the {{site.data.keyword.speechtotextfull}} service on the public {{site.data.keyword.cloud_notm}}. For more information about the public service, see [About {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/speech-to-text?topic=speech-to-text-about#about){: external}.
{: note}

## Supported interfaces
{: #interfaces}
{: help}
{: support}

The {{site.data.keyword.speechtotextshort}} service offers multiple interfaces for speech recognition:

-   A [WebSocket interface](/docs/speech-to-text-data?topic=speech-to-text-data-websockets) for establishing persistent, full-duplex, low-latency connections with the service. You can pass a maximum of 100 MB of audio data to the service with a single request.
-   A [synchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-http) for basic HTTP calls to the service. You can pass a maximum of 100 MB of audio data with a request.
-   An [asynchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-async) for non-blocking calls to the service. You can pass as much as 1 GB of audio data with a request.

The service also provides a [customization interface](/docs/speech-to-text-data?topic=speech-to-text-data-customization) that you can use to tune speech recognition for your language and acoustic requirements. You can expand the vocabulary of a model with domain-specific terminology or adapt a model for the acoustic characteristics of your audio. You can also add [grammars](/docs/speech-to-text-data?topic=speech-to-text-data-grammars) to restrict the phrases that the service can recognize.

-   For information about making requests with each of the {{site.data.keyword.speechtotextshort}} interfaces, see [Making requests to the service](/docs/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   For examples of basic speech recognition requests with each of the service's interfaces, see [Making a recognition request](/docs/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   For a high-level description of application development with the service, see [Overview for developers](/docs/speech-to-text-data?topic=speech-to-text-data-developerOverview).

SDKs are available in many programming languages to simplify your use of the service. For more information, see the [API reference](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Input features
{: #inputFeatures}
{: help}
{: support}

The service's interfaces share many common input features for transcribing speech to text:

-   [Audio formats](/docs/speech-to-text-data?topic=speech-to-text-data-audio-formats) - You can transcribe Ogg or Web Media (WebM) audio with the Opus or Vorbis codec, MP3 (or MPEG), Waveform Audio File Format (WAV), Free Lossless Audio Codec (FLAC), Linear 16-bit Pulse-Code Modulation (PCM), G.729, A-law, mu-law (or u-law), and basic audio. By using a format that supports compression, you can maximize the amount of audio data that you can send with a request.
-   [Languages and models](/docs/speech-to-text-data?topic=speech-to-text-data-models) - You can transcribe audio by using broadband or narrowband models. Use broadband for audio that is sampled at a minimum rate of 16 kHz. Use narrowband for audio that is sampled at a minimum rate of 8 kHz.
-   [Audio transmission](/docs/speech-to-text-data?topic=speech-to-text-data-input#transmission) - You can pass audio as a continuous stream of data chunks or as a one-shot delivery that passes all of the data at one time. With streaming, the service enforces inactivity and session [timeouts](/docs/speech-to-text-data?topic=speech-to-text-data-input#timeouts).

## Output features
{: #outputFeatures}
{: help}
{: support}

Most interfaces also support the following common output features:

-   [Speaker labels](/docs/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels) recognize different speakers from US English, Japanese, or Spanish audio. The transcription labels each speaker's contributions to a multi-participant conversation. (Beta functionality.)
-   [Keyword spotting](/docs/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting) identifies spoken phrases that match specified keyword strings with a user-defined level of confidence. Keyword spotting is especially useful when individual phrases from the audio are more important than the full transcription. For example, a customer support system might identify keywords to determine how to route user requests.
-   [Interim results](/docs/speech-to-text-data?topic=speech-to-text-data-output#interim) return continually refined hypotheses as transcription progresses. The service returns final results when transcription is complete. Interim results are available only with the WebSocket interface.
-   [Maximum alternatives](/docs/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives) provide possible alternative transcripts. The service indicates final results in which it has the greatest confidence.
-   [Word alternatives](/docs/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives) request alternative words that are acoustically similar to the words of a transcript.
-   [Word confidence](/docs/speech-to-text-data?topic=speech-to-text-data-output#word_confidence) returns confidence levels for each word of a transcript.
-   [Word timestamps](/docs/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps) return timestamps for the start and end of each word of a transcript.
-   [Smart formatting](/docs/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting) converts dates, times, numbers, currency values, phone numbers, and internet addresses into more readable, conventional forms in final transcripts. For US English, you can also provide keyword phrases to include certain punctuation symbols in final transcripts. Smart formatting is supported for US English, Japanese, and Spanish audio. (Beta functionality.)
-   [Numeric redaction](/docs/speech-to-text-data?topic=speech-to-text-data-output#redaction) redacts, or masks, numeric data from a final transcript. Redaction is intended to remove sensitive personal information, such as credit card numbers, from transcripts. The feature is supported for US English, Japanese, and Korean audio. (Beta functionality.)
-   [Profanity filtering](/docs/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter) censors profanity from US English transcripts.
-   [End of phrase silence time](/docs/speech-to-text-data?topic=speech-to-text-data-output#silence_time) specifies the duration of the pause interval at which the service splits a transcript into multiple final results in response to silence.
-   [Split transcript at phrase end](/docs/speech-to-text-data?topic=speech-to-text-data-output#split_transcript) directs the services to split a transcript into multiple final results for semantic features such as sentences. The service bases its understanding of semantic features on the base language model that you use with a request. Custom language models and grammars can also influence how and where the service splits a transcript.
-   [Processing metrics](/docs/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) provide detailed timing information about the service's analysis of the input audio.
-   [Audio metrics](/docs/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) provide detailed information about the signal characteristics of the input audio.

## Language support
{: #languages}
{: help}
{: support}

The service offers models for the following languages and dialects:

-   Arabic (Modern Standard)
-   Brazilian Portuguese
-   Chinese (Mandarin)
-   English (United Kingdom and United States)
-   French
-   German
-   Japanese
-   Korean
-   Spanish (Argentinian, Castilian, Chilean, Colombian, Mexican, and Peruvian)

The service does not support all features for all languages. Moreover, it supports some features as generally available (GA) for production use and others as beta offerings for different languages.

-   The Spanish Castilian dialect is generally available. The other five Spanish dialects are beta.
-   The WebSocket and synchronous and asynchronous HTTP interfaces are generally available for all languages.
-   The service offers both broadband models and narrowband models for all languages. For more information, see [Languages and models](/docs/speech-to-text-data?topic=speech-to-text-data-models).
-   Some speech recognition features are available only for some languages and only with some interfaces. For more information, see the [Parameter summary](/docs/speech-to-text-data?topic=speech-to-text-data-summary).
-   The language model customization interface is generally available for all languages. The acoustic model customization interface is available as beta functionality for all languages. For more information, see [Language support for customization](/docs/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).

## FISMA support
{: #fisma}

Federal Information Security Management Act (FISMA) support is available for {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} offerings purchased on or after August 30, 2019 (version 1.0.1). {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} is FISMA High Ready.

## Try out the service
{: #tryOut}

For examples of the {{site.data.keyword.speechtotextshort}} service in action, see

-   A [quick demo](https://speech-to-text-demo.ng.bluemix.net/){: external} that transcribes text from streaming audio input or from a file that you upload.
-   Applications in the {{site.data.keyword.ibmwatson}} [Starter Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} that demonstrate the service.
-   The {{site.data.keyword.watson}} blog post [Getting robots to listen: Using {{site.data.keyword.watson}}'s {{site.data.keyword.speechtotextshort}} service](https://www.ibm.com/blogs/watson/2016/07/getting-robots-listen-using-watsons-speech-text-service/){: external} that shows how to use the service's WebSocket interface with Python to extract speech from audio. The post provides a thorough tutorial that demonstrates the code and steps involved.
