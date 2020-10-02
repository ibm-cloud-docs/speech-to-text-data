---

copyright:
  years: 2015, 2020
lastupdated: "2020-10-02"

subcollection: speech-to-text-data

---

{:faq: data-hd-content-type='faq'}
{:support: data-reuse='support'}
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

# Usage FAQs
{: #faq-usage}

FAQs for {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} include questions about speech recognition, audio transmission, customization, and other topics.

## How much audio data can I submit to the service?
{: #faq-usage-two}
{: faq}
{: support}

The amount of audio that you can submit with a single speech recognition request depends on the interface that you are using:

-   The WebSocket and synchronous HTTP interfaces accept a maximum of 100 MB of audio data.
-   The asynchronous HTTP interface accepts a maximum of 1 GB of audio data.

For more information, see [Supported interfaces](/docs/speech-to-text-data?topic=speech-to-text-data-about#interfaces).

## How can I improve transcription accuracy?
{: #faq-usage-three}
{: faq}
{: support}

The {{site.data.keyword.speechtotextdatafull}} service offers a customization interface that provides many features and options to improve the speech recognition capabilities of the supported base language models:

-   If you are transcribing audio for a specific domain, you can create custom language models to expand and tailor a base model's vocabulary to include domain-specific terminology. When you use custom language models, you can also create and incorporate custom grammars to restrict the words that the service can recognize from your model's vocabulary. For more information, see [Creating a custom language model](/docs/speech-to-text-data?topic=speech-to-text-data-languageCreate) and [Adding a grammar to a custom language model](/docs/speech-to-text-data?topic=speech-to-text-data-grammarAdd).
-   If you are transcribing audio with unique characteristics (such as speaker accents, telephone conversations, or background noise), you can create a custom acoustic model to adapt a base model for your environment and speakers. For more information, see [Creating a custom acoustic model](/docs/speech-to-text-data?topic=speech-to-text-data-acoustic).
-   You can also use custom acoustic and custom language models together. If transcriptions or related corpora are available for your audio, you can use that data to create a complementary custom language model to further improve the quality of speech recognition based on your custom acoustic model. For more information, see [Using custom acoustic and custom language models together](/docs/speech-to-text-data?topic=speech-to-text-data-useBoth).

## How many words can I add to a custom language model?
{: #faq-usage-four}
{: faq}
{: support}

You can add a maximum of 90 thousand out-of-vocabulary (OOV) words to a custom language model from all sources. You can add a maximum of 10 million total words to a custom language model from all sources. But many factors contribute to the amount of data that you need for an effective custom language model. Although it is not possible to provide the exact number of words that you need to add for any custom model or application, even adding a few words to a custom model can improve speech recognition. For more information about limits on the number of words that you can add and for other factors that affect the amount of data that you need, see [How much data do I need?](/docs/speech-to-text-data?topic=speech-to-text-data-corporaWords#wordsResourceAmount).

## How does custom model upgrading work?
{: #faq-usage-five}
{: faq}
{: support}

When a new version of a base model is released to improve the quality of speech recognition, you must upgrade any custom language and custom acoustic models that are built on the base model to take advantage of the updates. For more information, see [Upgrading custom models](/docs/speech-to-text-data?topic=speech-to-text-data-customUpgrade).

## Can the {{site.data.keyword.speechtotextshort}} service transcribe numbers as digits instead of strings?
{: #faq-usage-six}
{: faq}
{: support}

For US English, Japanese, and Spanish audio, you can use smart formatting to convert certain strings, such as digits and numbers, to more conventional representations. Smart formatting is beta functionality. For more information, see [Smart formatting](/docs/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting).
