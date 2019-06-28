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

# Languages and models
{: #models}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} supports speech recognition in many languages. For all interfaces, you can use the `model` parameter to specify the model for a speech recognition request. The model indicates the language in which the audio is spoken and the rate at which it is sampled.
{: shortdesc}

## Supported language models
{: #modelsList}

For most languages, the service supports both broadband and narrowband models:

-   *Broadband models* are for audio that is sampled at greater than or equal to 16 kHz. Use broadband models for responsive, real-time applications, for example, for live-speech applications.
-   *Narrowband models* are for audio that is sampled at 8 kHz. Use narrowband models for offline decoding of telephone speech, which is the typical use for this sampling rate.

Choosing the correct model for your application is important. Use the model that matches the sampling rate (and language) of your audio. The service automatically adjusts the sampling rate of your audio to match the model that you specify. For more information, see [Sampling rate](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#samplingRate).

To achieve the best recognition accuracy, you also need to consider the frequency content of your audio. For more information, see [Audio frequency](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#frequency).
{: tip}

Table 1 lists the supported models for each language. If you omit the `model` parameter from a request, the service uses the US English broadband model, `en-US_BroadbandModel`, by default.

<table>
  <caption>Table 1. Supported language models</caption>
  <tr>
    <th style="text-align:left">Language</th>
    <th style="text-align:center">Broadband model</th>
    <th style="text-align:center">Narrowband model</th>
  </tr>
  <tr>
    <td>French</td>
    <td style="text-align:center"><code>fr-FR_BroadbandModel</code></td>
    <td style="text-align:center"><code>fr-FR_NarrowbandModel</code></td>
  </tr>
  <tr>
    <td>Japanese</td>
    <td style="text-align:center"><code>ja-JP_BroadbandModel</code></td>
    <td style="text-align:center"><code>ja-JP_NarrowbandModel</code></td>
  </tr>
  <tr>
    <td>Korean</td>
    <td style="text-align:center"><code>ko-KR_BroadbandModel</code></td>
    <td style="text-align:center"><code>ko-KR_NarrowbandModel</code></td>
  </tr>
  <tr>
    <td>Spanish</td>
    <td style="text-align:center"><code>es-ES_BroadbandModel</code></td>
    <td style="text-align:center"><code>es-ES_NarrowbandModel</code></td>
  </tr>
  <tr>
    <td>US English</td>
    <td style="text-align:center"><code>en-US_BroadbandModel</code></td>
    <td style="text-align:center"><code>en-US_NarrowbandModel</code></br>
      <code>en-US_ShortForm_NarrowbandModel</code></td>
  </tr>
</table>

### The US English short-form model
{: #modelsShortForm}

The US English short-form model, `en-US_ShortForm_NarrowbandModel`, can improve speech recognition for Interactive Voice Response (IVR) and Automated Customer Support solutions. The short-form model is trained to recognize the short utterances that are frequently expressed in customer support settings like automated and human support call centers. The model is tuned, for example, for precise utterances such as digits, single-character word and name spellings, and yes-no responses. Using a grammar in combination with the short-form model can further improve recognition results.

As with all models, noisy environments can adversely impact the results. For example, background acoustic noise from airports, moving vehicles, conference rooms, and multiple speakers can reduce transcription accuracy.  Audio from speaker phones can also reduce accuracy due to the echo common to such devices. Using a custom acoustic model with the short-form model can counteract such effects.

-   For more information about language model and acoustic model customization, see [The customization interface](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization).
-   For more information about grammars, see [Using grammars with custom language models](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars).

### Language model example
{: #modelsExample}

The following example HTTP request uses the model `en-US-NarrowbandModel` for speech recognition:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognize?model=en-US_NarrowbandModel"
```
{: pre}

## Listing models
{: #listModels}

The HTTP interface provides two methods for listing information about the supported models:

-   The `GET /v1/models` method lists information about all available models.
-   The `GET /v1/models/{model_id}` method lists information about a specified model.

Both methods return the following information about a model:

-   `name` is the name of the model that you use in a request.
-   `language` is the language identifier of the model (for example, `en-US`).
-   `rate` identifies the sampling rate (minimum acceptable rate for audio) that is used by the model in Hertz.
-   `url` is the URI for the model.
-   `description` provides a brief description of the model.
-   `supported_features` describes the additional service features that are supported with the model:
    -   `custom_language_model` is a boolean that indicates whether you can create custom language models that are based on the model.
    -   `speaker_labels` indicates whether you can use the `speaker_labels` parameter with the model.

### Example requests and responses
{: #listExample}

The following example lists all models that are supported by the service:

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/models"
```
{: pre}

```javascript
{
  "models": [
    {
      "name": "en-US_BroadbandModel",
      "language": "en-US",
      "url": "{url}/v1/models/en-US_BroadbandModel",
      "rate": 16000,
      "supported_features": {
        "custom_language_model": true,
        "speaker_labels": true
      },
      "description": "US English broadband model."
    },
    {
      "name": "ko-KR_BroadbandModel",
      "language": "ko-KR",
      "url": "{url}/v1/models/ko-KR_BroadbandModel",
      "rate": 16000,
      "supported_features": {
        "custom_language_model": true,
        "speaker_labels": false
      },
      "description": "Korean broadband model."
    },
    . . .
  ]
}
```
{: codeblock}

The following example shows information about the US English broadband model. The model supports both language model customization and speakers labels.

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/models/en-US_BroadbandModel"
```
{: pre}

```javascript
{
  "rate": 16000,
  "name": "en-US_BroadbandModel",
  "language": "en-US",
  "url": "{url}/v1/models/en-US_BroadbandModel",
  "supported_features": {
    "custom_language_model": true,
    "speaker_labels": true
  },
  "description": "US English broadband model."
}
```
{: codeblock}
