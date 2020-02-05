---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-04"

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

# Input features
{: #input}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} offers the following features to specify how the service is to perform a speech recognition request. All of the input parameters that are described in the following sections are optional. Only the input audio is required.
{: shortdesc}

-   For examples of simple speech recognition requests for each of the service's interfaces, see [Making a recognition request](/docs/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   For an alphabetized list of all available speech recognition parameters, including their status (generally available or beta), supported languages, and supported interfaces, see the [Parameter summary](/docs/speech-to-text-data?topic=speech-to-text-data-summary).

## Custom models
{: #custom-input}

Language and acoustic model customization are available at different levels of support (generally available or beta). For more information, see [Language support for customization](/docs/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
{: note}

All interfaces accept a custom model for use in a recognition request:

-   *Custom language models* expand the service's base vocabulary with terminology from specific domains. Use the `language_customization_id` parameter to include a custom language model with a request. You can also specify an optional `customization_weight` parameter. The parameter indicates the relative weight that is given to words from the custom model as opposed to words from the base vocabulary.

    For more information, see [Using a custom language model](/docs/speech-to-text-data?topic=speech-to-text-data-languageUse).
-   *Custom acoustic models* adapt the service's base acoustic model for the acoustic characteristics of your environment and speakers. Use the `acoustic_customization_id` parameter to include a custom acoustic model with a request. You can specify both a custom language model and a custom acoustic model with a request.

    For more information, see [Using a custom acoustic model](/docs/speech-to-text-data?topic=speech-to-text-data-acousticUse).

Custom models are based on one of the language models that are described in [Languages and models](/docs/speech-to-text-data?topic=speech-to-text-data-models). A custom model can be used only with the base model for which it is created. If your custom model is based on a model other than `en-US_BroadbandModel`, the default, you must also specify the name of the model with the request. To use a custom model, you must issue the request with credentials for the instance of the service that owns the custom model.

For an introduction to customization, see [The customization interface](/docs/speech-to-text-data?topic=speech-to-text-data-customization).

### Custom model examples
{: #customExample}

The following example request includes the `language_customization_id` parameter to use the custom language model with the specified ID. It includes the `customization_weight` parameter to indicate that words from the custom model are to be given a relative weight of `0.5`.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognize?language_customization_id={customization_id}&customization_weight=0.5"
```
{: pre}

The following example request uses both a custom language model and a custom acoustic model. The former is identified with the `language_customization_id` parameter, the latter with the `acoustic_customization_id` parameter.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file1.flac
"{url}/v1/recognize?language_customization_id={customization_id}&acoustic_customization_id={customization_id}"
```
{: pre}

For examples that use custom models with each of the service's interfaces, see

-   [Using a custom language model](/docs/speech-to-text-data?topic=speech-to-text-data-languageUse)
-   [Using a custom acoustic model](/docs/speech-to-text-data?topic=speech-to-text-data-acousticUse)

## Grammars
{: #grammars-input}

You can add grammars to a custom language model and use them for speech recognition. Grammars use a formal language specification to define a set of production rules for transcribing strings. The rules specify how to form valid strings from the language's alphabet.

When you use a grammar for speech recognition, the service recognizes only phrases that are recognized by the grammar. By limiting the search space for valid strings, the service can deliver results faster and more accurately.

All interfaces accept the following parameters for a recognition request:

-   The `language_customization_id` parameter identifies the custom language model for which the grammar is defined. You must issue the request with credentials for the instance of the service that owns the model.
-   The `grammar_name` parameter specifies the grammar that you want to use. You can specify only a single grammar with a request.

For more information, see [Using grammars with custom language models](/docs/speech-to-text-data?topic=speech-to-text-data-grammars).

### Grammars example
{: #grammarsExample}

The following example request includes the `language_customization_id` and `grammar_name` parameters to restrict the service's response to strings that are defined in the grammar named `list-abnf`.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file.flac
"{url}/v1/recognize?language_customization_id={customization_id}&grammar_name=list-abnf"
```
{: pre}

For examples that use grammars with each of the service's interfaces, see [Using a grammar for speech recognition](/docs/speech-to-text-data?topic=speech-to-text-data-grammarUse).

## Base model version
{: #version}

To improve the quality of speech recognition, the service occasionally updates the base language models described in [Languages and models](/docs/speech-to-text-data?topic=speech-to-text-data-models). The base models for languages are independent of each other, as are the broadband and narrowband models for a language. Therefore, updates to base models occur independently of each other and have no effect on other models.

When multiple versions of a base model exist, the optional `base_model_version` parameter specifies the version of the model to be used with a recognition request. The parameter is intended primarily for use with custom models that are updated for a new base model, but it can be used without a custom model. The version of a base model that is used for a request depends on whether you pass the `base_model_version` parameter. It also depends on whether you specify a custom model (language, acoustic, or both) with the request.

-   *If you do not specify a custom model with the request*

    -   Omit the `base_model_version` parameter to use the latest version of the base model.
    -   Specify the `base_model_version` parameter to use a specific version of the base model.

-   *If you specify a custom model with the request*

    -   Omit the `base_model_version` parameter to use the latest version of the base model to which the custom model is upgraded. For example, if the custom model is upgraded to the latest version of the base model, the service uses the latest versions of the base and custom models.
    -   Specify the `base_model_version` parameter to use the specified versions of both the base and custom models.

The parameter is intended for use with custom models. Therefore, you can learn about the available versions of a base model only by listing information about a custom model that is based on it.

-   For more information about upgrading custom models, see [Upgrading custom models](/docs/speech-to-text-data?topic=speech-to-text-data-customUpgrade).
-   For more information about using different versions of base and custom models for speech recognition, see [Making recognition requests with upgraded custom models](/docs/speech-to-text-data?topic=speech-to-text-data-customUpgrade#upgradeRecognition).

## Audio transmission
{: #transmission}

*With the WebSocket interface,* audio data is always streamed to the service over the connection. You can pass data through the socket all at once, or you can pass data for the live-use case as it becomes available. The service returns results as they become available.

*With the synchronous and asynchronous HTTP interfaces,* you can transmit audio to the service in either of the following ways:

-   *One-shot delivery* - You omit the `Transfer-Encoding` header and pass all of the audio data to the service at one time as a single delivery.
-   *Streaming* - You set the `Transfer-Encoding` request header to the value `chunked` and stream the data over a persistent connection. The data does not need to exist fully before you stream it to the service. You can stream the data as it becomes available. The service sends results only when it receives the final chunk, which you indicate by sending an empty chunk.

    For more information about streaming chunked audio with the `Transfer-Encoding` header, see
    -   [Chunked transfer encoding](https://wikipedia.org/wiki/Chunked_transfer_encoding){: external}
    -   [Transfer Codings](https://tools.ietf.org/html/rfc7230#section-4){: external} in *IETF RFC 7320 HTTP/1.1: Message Syntax and Routing*

With the HTTP interfaces, the service always transcribes the entire audio stream before sending any results. The results can include multiple `transcript` elements to indicate phrases that are separated by pauses. Concatenate the `transcript` elements to assemble the complete transcript.

The service enforces timeouts on a streaming session. It can terminate a streaming session if it detects an extended period of silence or receives no audio during a 30-second period. For more information about timeouts and how to avoid them, see [Timeouts](#timeouts).

### Audio transmission example
{: #transmissionExample}

The following example request specifies `chunked` for the `Transfer-Encoding` header to use streaming mode. The connection remains open to accept additional chunks of audio.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--header "Transfer-Encoding: chunked"
--data-binary @{path}audio-file1.flac
"{url}/v1/recognize"
```
{: pre}

## Timeouts
{: #timeouts}

When you initiate a streaming session with the HTTP or WebSocket speech recognition methods, the service enforces inactivity and session timeouts. If a timeout lapses during a streaming session, the service closes the connection. Your application must recover gracefully from possible closed connections.

When you stream audio over HTTP, the service sends a space character in its response every 20 seconds. The service does this to improve usability by avoiding the 30-second HTTP REST inactivity timeout. To keep the connection alive while recognition is ongoing, the service continues to send this space character until it completes its transcription. The space character has no effect on JSON-encoded response data.

This HTTP inactivity timeout is different from the service's inactivity timeout. The WebSocket interface is not subject to this HTTP timeout.
{: note}

### Inactivity timeout
{: #timeouts-inactivity}

An *inactivity timeout* (HTTP status code 400) occurs when the service is receiving audio but detects only continuous silence or non-speech activity (no speech) for 30 seconds. The service sends the error message `No speech detected for 30s`. The inactivity timeout is useful, for example, for terminating a session when a user simply walks away from a live microphone.

The default inactivity timeout is 30 seconds. You can override this value by using the `inactivity_timeout` parameter. Specify a larger value to increase the inactivity timeout. Specify a value of `-1` to set the inactivity timeout to infinity. You are charged for all audio that you send to the service, including silence, so increasing the inactivity timeout can incur additional charges for a streaming session that sends only silence.

The following example request sets the inactivity timeout to 60 seconds. The request sends an initial file to begin the streaming session.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Transfer-Encoding: chunked"
--header "Content-Type: audio/flac"
--data-binary @{path}audio-file1.flac
"{url}/v1/recognize?inactivity_timeout=60"
```
{: pre}

### Session timeout
{: #timeouts-session}

A *session timeout* (HTTP status code 408) occurs when you fail to send sufficient audio to keep a streaming session active. The service can consider a session idle and trigger a session timeout for the following reasons:

-   You fail to send at least 15 seconds of audio to the service in any 30-second window.

    Until you send the last chunk to indicate the end of the stream, you must send at least 15 seconds of audio within any 30-second period. The audio can be silence if you set the `inactivity_timeout` parameter to a larger value or to `-1`. You are charged for the duration of any audio that you send to the service, including silence.
-   You stream audio at a rate that is much slower than real-time.

    Ideally, you would initiate a request to establish a session just before you obtain audio for transcription. You would then maintain the session by sending audio at a rate that is close to real-time.

You do not need to worry about the session timeout after you send the last chunk to indicate the end of the stream. The service continues to process the audio until it returns the final transcription results.

When you transcribe a long audio stream, the service can take more than 30 seconds to process the audio and generate a response. The service does not begin to calculate the session timeout until it finishes processing all audio that it has received. The service's processing time cannot cause the session to exceed the 30-second session timeout.

For example, if you send one hour of audio in the first 10 seconds of a session, the service might take 300 seconds to process the audio.  To keep this session alive, you would need to send at least 15 more seconds of some audio, including silence, no later than 340 seconds into the session.

In this example, if you were to send another 15 seconds of audio at the 100-second mark of the session, the service might spend an additional two seconds processing this audio. In this case, you would need to send 15 more seconds of audio no later 342 seconds into the session.

Do not rely on processing time or on whether you have received results to determine whether a streaming session is idle. Assume that the service can process all audio instantly, and send data to the service accordingly. If you stream audio in real-time, do not fall behind in sending audio at one-half real-time (15 seconds of audio) in any 30-second window. This rate is typically sufficient to accommodate network latency and delays.
{: important}

## Information security
{: #security-input}

*Information security* includes features to associate a customer ID with data that is passed to the service with a request. You associate a customer ID with the data by passing the `X-Watson-Metadata` header with the request. If necessary, you can then delete the data by using the `DELETE /v1/user_data` method. For more information, see [Information security](/docs/speech-to-text-data?topic=speech-to-text-data-information-security).
