---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-20"

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

# Release notes
{: #release-notes}

The following versions of {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} are available. Information includes new features and changes for each version of the product and any known limitations.
{: shortdesc}

## Known limitations
{: #limitations}

No known limitations at this time.

## Version 1.1.4 (19 June 2020)
{: #v114}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.4 is now available. Installation and administration of the service include many changes. This version supports {{site.data.keyword.icp4dfull_notm}} versions 2.5 and 3.0.1, and Red Hat OpenShift versions 3.11 and 4.3. For more information about installing and managing the service, see [Installing {{site.data.keyword.watson}} {{site.data.keyword.speechtotextshort}} version 1.1.4](/docs/speech-to-text-data?topic=speech-to-text-data-speech-install).

The release includes the following functional changes and enhancements:

-   The service now offers greatly improved backup and restore procedures. Utilities are now available to back up data from your datastores, so you no longer need to re-create all of your data in the event of a disaster. For more information, see [Backing up and restoring your data](/docs/speech-to-text-data?topic=speech-to-text-data-speech-backup).
-   The service now offers two new optional parameters for controlling the level of speech activity detection. The parameters can help ensure that only relevant audio is processed for speech recognition.
    -   The `speech_detector_sensitivity` parameter adjusts the sensitivity of speech activity detection. You can use the parameter to suppress word insertions from music, coughing, and other non-speech events.
    -   The `background_audio_suppression` parameter suppresses background audio based on its volume to prevent it from being transcribed or otherwise interfering with speech recognition. You can use the parameter to suppress side conversations or background noise.

    You can use the parameters individually or together. They are available for all interfaces and for most language models. For more information about the parameters, their allowable values, and their effect on the quality and latency of speech recognition, see [Speech activity detection](/docs/speech-to-text-data?topic=speech-to-text-data-input#detection).
-   The service now supports broadband and narrowband models for the Dutch and Italian languages:
    -   Dutch broadband model (`nl-NL_BroadbandModel`)
    -   Dutch narrowband model (`nl-NL_NarrowbandModel`)
    -   Italian broadband model (`it-IT_BroadbandModel`)
    -   Italian narrowband model (`it-IT_NarrowbandModel`)

    Dutch and Italian language models are generally available (GA) for speech recognition and for language model and acoustic model customization. For more information about all available language models, see
    -   [Supported language models](/docs/speech-to-text-data?topic=speech-to-text-data-models#modelsList)
    -   [Language support for customization](/docs/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport)
-   The service now supports speaker labels (the `speaker_labels` parameter) for German and Korean language models. Speaker labels identify which individuals spoke which words in a multi-participant exchange. For more information, see [Speaker labels](/docs/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels).
-   The Japanese narrowband model (`ja-JP_NarrowbandModel`) now includes some multigram word units for digits and decimal fractions. The service returns these multigram units regardless of whether you enable smart formatting. The smart formatting feature understands and returns the multigram units that the model generates. If you apply your own post-processing to transcription results, you need to handle these units appropriately. For more information, see [Japanese](/docs/speech-to-text-data?topic=speech-to-text-data-output#smartFormattingJapanese) in the smart formatting documentation.
-   The backup and restore procedures are greatly simplified. They now back up data from the datastores, so you no longer need to re-create the operations you have run. For more information, see [Backing up and restoring your data](/docs/speech-to-text-data?topic=speech-to-text-data-speech-backup).

## Version 1.1.3 (28 February 2020)
{: #v113}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.3 is now available. The release includes the following changes:

-   **As of 1 April 2020,** acoustic model customization is now generally available (GA) for all supported languages. For more information about support for individual language models, see [Language support for customization](/docs/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
-   For speech recognition, the service now supports the `end_of_phrase_silence_time` parameter. The parameter specifies the duration of the pause interval at which the service splits a transcript into multiple final results. Each final result indicates a pause or extended silence that exceeds the pause interval. For most languages, the default pause interval is 0.8 seconds; for Chinese the default interval is 0.6 seconds.

    You can use the parameter to effect a trade-off between how often a final result is produced and the accuracy of the transcription. Increase the interval when accuracy is more important than latency. Decrease the interval when the speaker is expected to say short phrases or single words.

    For more information, see [End of phrase silence time](/docs/speech-to-text-data?topic=speech-to-text-data-output#silence_time).
-   For speech recognition, the service now supports the `split_transcript_at_phrase_end` parameter. The parameter directs the service to split the transcript into multiple final results based on semantic features of the input, such as at the conclusion of sentences. The service bases its understanding of semantic features on the base language model that you use with a request. Custom language models and grammars can also influence how and where the service splits a transcript.

    The parameter causes the service to add an `end_of_utterance` field to each final result to indicate the motivation for the split: `full_stop`, `silence`, `end_of_data`, or `reset`.

    For more information, see [Split transcript at phrase end](/docs/speech-to-text-data?topic=speech-to-text-data-output#split_transcript).

## Version 1.1.2 (27 November 2019)
{: #v112}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.1.2 is now available. The release includes the following change:

-   You can create no more than 1024 custom language models and no more than 1024 custom acoustic models per owning credentials. For more information, see [Maximum number of custom models](/docs/speech-to-text-data?topic=speech-to-text-data-customization#customMaximum).

## Version 1.0.1 (30 August 2019)
{: #v101}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} version 1.0.1 is now available. The service now works with {{site.data.keyword.icp4dfull_notm}} 2.1.0.1. The release includes the following changes:

-   The service now supports installing {{site.data.keyword.icp4dfull_notm}} with Red Hat OpenShift.
-   The service now offers broadband and narrowband language models in six Spanish dialects:

    -   Argentinian Spanish (`es-AR_BroadbandModel` and `es-AR_NarrowbandModel`)
    -   Castilian Spanish (`es-ES_BroadbandModel` and `es-ES_NarrowbandModel`)
    -   Chilean Spanish (`es-CL_BroadbandModel` and `es-CL_NarrowbandModel`)
    -   Colombian Spanish (`es-CO_BroadbandModel` and `es-CO_NarrowbandModel`)
    -   Mexican Spanish (`es-MX_BroadbandModel` and `es-MX_NarrowbandModel`)
    -   Peruvian Spanish (`es-PE_BroadbandModel` and `es-PE_NarrowbandModel`)

    The Castilian Spanish models are not new. They are generally available for speech recognition and language model customization, and beta for acoustic model customization.

    The models for the other five dialects are new and are beta for all uses. Because they are beta, these additional dialects might not be ready for production use and are subject to change. They are initial offerings that are expected to improve in quality with time and usage.

    For more information, see the following sections:

    -   [Supported language models](/docs/speech-to-text-data?topic=speech-to-text-data-models#modelsList)
    -   [Language support for customization](/docs/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport)
-   Federal Information Security Management Act (FISMA) support is now available for {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}. The service is FISMA High Ready.

## Version 1.0.0 (28 June 2019)
{: #v100}

The initial release of the service. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} is based on the {{site.data.keyword.speechtotextfull}} service on the public {{site.data.keyword.cloud_notm}}. For more information about the public service, see [About {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/speech-to-text?topic=speech-to-text-about){: external}.

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} differs from the public {{site.data.keyword.speechtotextshort}} service in the following ways. You might find this information helpful if you are already familiar with the {{site.data.keyword.speechtotextshort}} service on the public {{site.data.keyword.cloud_notm}}.

-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} uses access tokens for authentication. For more information, see [Making requests to the service](/docs/speech-to-text-data?topic=speech-to-text-data-making-requests) and the [API reference](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   The endpoints for {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} are specific to your {{site.data.keyword.icp4dfull_notm}} cluster. For more information, see [Making requests to the service](/docs/speech-to-text-data?topic=speech-to-text-data-making-requests) and the [API reference](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} does not perform any request logging. You do not need to use the `X-Watson-Learning-Opt-Out` request header.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} does not support Watson tokens. You cannot use the `X-Watson-Authorization-Token` request header to authenticate with the service.
