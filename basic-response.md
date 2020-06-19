---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-08"

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

# Understanding recognition results
{: #basic-response}

Regardless of the interface that you use, {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} returns transcription results that reflect the input and output parameters that you specify. The service returns all JSON response content in the UTF-8 character set.
{: shortdesc}

## Basic transcription response
{: #response}

The service returns the following response for the examples in [Making a recognition request](/docs/speech-to-text-data?topic=speech-to-text-data-basic-request). The examples pass only an audio file and its content type. The audio speaks a single sentence with no noticeable pauses between words.

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

The service returns a `SpeechRecognitionResults` object, which is the top-level response object. For these simple requests, the object includes one `results` field and and one `result_index` field:

-   The `results` field provides an array of information about the transcription results. For this example, the `alternatives` field includes the `transcript` and the service's `confidence` in the results. The `final` field has a value of `true` to indicate that these results will not change.
-   The `result_index` field provides a unique identifier for the results. The example shows final results for a request with a single audio file that has no pauses, and the request includes no additional parameters. So the service returns a single `result_index` field with a value of `0`, which is always the initial index.

If the input audio is more complex or the request includes additional parameters, the results can contain much more information.

### The alternatives field
{: #responseAlternatives}

The `alternatives` field provides an array of transcription results. For this request, the array includes a single element.

-   The `confidence` field is a score that indicates the service's confidence in the transcript, which for this example approaches 90 percent.
-   The `transcript` field provides the results of the transcription.

The `final` and `result_index` fields qualify the meaning of these fields.

### The final field
{: #responseFinal}

The `final` field indicates whether the transcript shows final transcription results:

-   The field is `true` for final results, which are guaranteed not to change. The service sends no further updates for transcripts that it returns as final results.
-   The field is `false` for interim results, which are subject to change. If you use the `interim_results` parameter with the WebSocket interface, the service returns evolving interim hypotheses in the form of multiple `results` fields as it transcribes the audio. The `final` field is always `false` for interim results. The service sets the field to `true` for the final results for the audio. The service sends no further updates for the transcription of that audio.

To obtain interim results, use the WebSocket interface and set the `interim_results` parameter to `true`. For more information, see [Interim results](/docs/speech-to-text-data?topic=speech-to-text-data-output#interim).

### The result_index field
{: #responseResultIndex}

The `result_index` field provides an identifier for the results that is unique for that request. If you request interim results, the service sends multiple `results` fields for evolving hypotheses of the input audio. The indexes for interim results for the same audio always have the same value, as do the final results for the same audio.

Once you receive final results for any audio, the service sends no further results with that index for the remainder of the request. The index for any further results is incremented by one.

Regardless of whether you request interim results, the service can return multiple final results with different indexes if your audio includes pauses or extended periods of silence. For more information, see [Pauses and silence](#pauses-silence).

If your audio produces multiple final results, concatenate the `transcript` elements of the final results to assemble the complete transcription of the audio. Assemble the results in order by `result_index`. You can ignore interim results for which the `final` field is `false`.

### Additional response content
{: #responseAdditional}

Many of the output parameters that are available for speech recognition impact the contents of the service's response. For example, the following parameters cause the service to return additional information about the audio:

-   The `max_alternatives` parameter requests multiple alternative transcripts. The `alternatives` array includes a separate element for each alternative. Each element of the array includes a `transcript` field. Only the most likely alternative includes a `confidence` field.
-   The `word_confidence` and `timestamps` parameters request additional information about individual words of the transcript. The `alternatives` array includes additional fields with those names.
-   The `keywords` and `keywords_threshold` parameters request keyword spotting. The `results` array includes a `keywords_result` field.
-   The `word_alternatives_threshold` parameter requests acoustically similar results for individual words. The `results` array includes a `word_alternatives` field.
-   The `interim_results` parameter of the WebSocket interface requests interim transcription hypotheses. As mentioned previously, the service sends multiple responses as it transcribes the audio.
-   The `speaker_labels` parameter identifies the individual speakers of a multi-participant exchange. The response includes a `speaker_labels` field at the same level as the `results` and `results_index` fields.
-   The `split_transcript_at_phrase_end` parameter directs the service to split a transcript into multiple final results for semantic features of the input such as sentences. Each `final_result` includes an additional `end_of_utterance` field to indicate why the service split the transcript at that point.

For more information about these and other parameters that can affect the service's response, see [Output features](/docs/speech-to-text-data?topic=speech-to-text-data-output). For more information about all available parameters, see the [Parameter summary](/docs/speech-to-text-data?topic=speech-to-text-data-summary).

## Pauses and silence
{: #pauses-silence}

The service transcribes an entire audio stream until either the stream ends or a timeout occurs. However, if the audio includes pauses or extended silence between spoken words or phrases, recognition results can include multiple final results.

For most languages, the default pause interval that the service uses to determine separate final results is 0.8 seconds; for Chinese the default interval is 0.6 seconds. You can use the `end_of_phrase_silence_time` parameter to change the duration of the interval. For more information, see [End of phrase silence time](/docs/speech-to-text-data?topic=speech-to-text-data-output#silence_time).

How the service returns the results depends on the interface that you use. The following examples show responses with two final results from the HTTP and WebSocket interfaces. The same input audio is used in both cases. The audio speaks the phrase "one two three four five six," with a one-second pause between the words "three" and "four." The examples use the default pause interval for speech recognition.

-   *For the HTTP interfaces,* the service sends a single `SpeechRecognitionResults` object. The `alternatives` array has a separate element for each final result. The response has a single `result_index` field with a value of `0`.

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "confidence": 0.99,
              "transcript": "one two three "
            }
          ],
          "final": true
        },
        {
          "alternatives": [
            {
              "confidence": 0.99,
              "transcript": "four five six "
            }
          ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

-   *For the WebSocket interface,* the service sends two separate responses with two different `SpeechRecognitionResults` objects. Each response object has a different `result_index` field, which has a value of `0` for the first response and `1` for the second response.

    ```javascript
    {
      "results": [
        {
          "alternatives": [
            {
              "confidence": 0.99,
              "transcript": "one two three "
            }
          ],
          "final": true
        },
      ]
      "result_index": 0
    }
    {
      "results": [
        {
          "alternatives": [
            {
              "confidence": 0.99,
              "transcript": "four five six "
            }
          ],
          "final": true
        }
      ],
      "result_index": 1
    }
    ```
    {: codeblock}

If your results include multiple final results, concatenate the `transcript` elements of the final results to assemble the complete transcription of the audio.

Silence of 30 seconds in streamed audio can result in an [inactivity timeout](/docs/speech-to-text-data?topic=speech-to-text-data-input#timeouts-inactivity).
{: note}

## Hesitation markers
{: #hesitation}

The service can include hesitation markers in transcription results when it discovers brief fillers or pauses in speech. Also referred to as disfluencies, such pauses can include fillers such as "uhm", "uh", "hmm", and related non-lexical utterances. Unless you need to use them for your application, you can safely filter hesitation markers from a transcript.

In English, the service uses the hesitation token `%HESITATION`, as shown in the following example. Other languages can use different markers. Hesitation markers can appear in both interim and final results.

```javascript
{
  "results": [
    {
      "alternatives": [
        {
          "confidence": 0.99,
          "transcript": ". . . that %HESITATION that's a . . ."
        }
      ],
      "final": true
    }
  ],
  "result_index": 0
}
```
{: codeblock}

Hesitation markers can also appear in other fields of a transcript. For example, if you request [Word timestamps](/docs/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps) for the individual words of a transcript, the service reports the start and end time of each hesitation marker.

```javascript
{
  "results": [
    {
      "alternatives": [
        {
          "timestamps": [
            . . .
            [
              "that",
              7.31,
              7.69
            ],
            [
              "%HESITATION",
              7.69,
              7.98
            ],
            [
              "that's",
              7.98,
              8.41
            ],
            [
              "a",
              8.41,
              8.48
            ],
            . . .
          ],
          "confidence": 0.99,
          "transcript": ". . . that %HESITATION that's a . . ."
        }
      ],
      "final": true
    }
  ],
  "result_index": 0
}
```
{: codeblock}

Enabling smart formatting prevents hesitation markers from appearing in final transcription results. For more information, see [Smart formatting](/docs/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting).
{: note}

## Capitalization
{: #capitalization}

For most languages, the service does not use capitalization in response transcripts. If capitalization is important for your application, you must capitalize the first word of each sentence and any other terms for which capitalization is appropriate.

*For US English only,* the service does capitalize many proper nouns. For example, the service returns the following text for the specified phrase:

```
Barack Obama graduated from Columbia University
```
{: codeblock}

For other languages, the service returns the following text:

```
barack obama graduated from columbia university
```
{: codeblock}

The service always applies this capitalization to US English, regardless of whether you use smart formatting.

## Punctuation
{: #punctuation}

The service does not insert punctuation in response transcripts by default. You must add any punctuation that you need to the service's results.

For some languages, you can use smart formatting to direct the service to substitute punctuation symbols, such as commas, periods, question marks, and exclamation points, for certain keyword strings. For more information, see [smart formatting](/docs/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting).
