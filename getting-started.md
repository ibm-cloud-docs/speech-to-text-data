---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-19"

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

# Getting started with {{site.data.keyword.speechtotextshort}}
{: #gettingStarted}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} transcribes audio to text to enable speech transcription capabilities for applications. This curl-based tutorial can help you get started quickly with the service. The examples show you how to call the service's `POST /v1/recognize` method to request a transcript.
{: shortdesc}

## Before you begin
{: #before-you-begin}

To use {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, you must first complete the following steps:

1.  Provision an instance of {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}. For more information about provisioning, see [Installing the service](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).
1.  From the {{site.data.keyword.icp4dfull_notm}} web client menu, choose **My Instances**.
1.  Click the {{site.data.keyword.speechtotextshort}} instance to open the overview page. Copy the `{token}` and `{URL}` credential values.

### Using the curl examples
{: #getting-started-curl}

This tutorial uses the `curl` command to call methods of the service's HTTP interface. Make sure that you have the `curl` command installed on your system.

1.  To test whether `curl` is installed, run the following command on the command line. If the output lists the `curl` version that supports Secure Sockets Layer (SSL), you are set for the tutorial.

    ```bash
    curl -V
    ```
    {: pre}

1.  If necessary, install the version of `curl` with SSL enabled for your operating system from [curl.haxx.se](https://curl.haxx.se/){: external}.

Omit the braces from the examples. They indicate variable values.
{: tip}

## Step 1: Transcribe audio with no options
{: #transcribe}

Call the `POST /v1/recognize` method to request a basic transcript of a FLAC audio file with no additional request parameters.

1.  Download the sample audio file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
1.  Issue the following command to call the service's `/v1/recognize` method for basic transcription with no parameters. The example uses the `Content-Type` header to indicate the type of the audio, `audio/flac`. The example uses the default language model, `en-US_BroadbandModel`, for transcription.
    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.
    -   Modify `{path_to_file}` to specify the location of the `audio-file.flac` file.

    *Windows users,* replace the backslash (`\`) at the end of each line with a caret (`^`). Make sure there are no trailing spaces.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize"
    ```
    {: pre}

    The service returns the following transcription results:

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

## Step 2: Transcribe audio with options
{: #transcribeOptions}

Call the `POST /v1/recognize` method to transcribe the same FLAC audio file, but specify two transcription parameters.

1.  If necessary, download the sample audio file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>.
1.  Issue the following command to call the service's `/v1/recognize` method with two extra parameters. Set the `timestamps` parameter to `true` to indicate the beginning and end of each word in the audio stream. Set the `max_alternatives` parameter to `3` to receive the three most likely alternatives for the transcription. The example uses the `Content-Type` header to indicate the type of the audio, `audio/flac`, and the request uses the default model, `en-US_BroadbandModel`.
    -   Replace `{token}` with the access token for your service instance.
    -   Replace `{url}` with the URL for your service instance.
    -   Modify `{path_to_file}` to specify the location of the `audio-file.flac` file.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize?timestamps=true&max_alternatives=3"
    ```
    {: pre}

    The service returns the following results, which include timestamps and three alternative transcriptions:

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
              "transcript": "several tornadoes touch down as a line
of severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touched down as a line
of severe thunderstorms swept through Colorado on Sunday "
            },
            {
              "transcript": "several tornadoes touch down as a line
of severe thunderstorms swept through Colorado and Sunday "
            }
          ],
          "final": true
        }
      ],
      "result_index": 0
    }
    ```
    {: codeblock}

## Next steps

-   Learn more about the interfaces and SDKs that are available for making speech recognition requests in the [Overview for developers](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).
-   Learn about making requests to the service in [Making requests to the service](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   See basic speech recognition requests for each of the service's interfaces in [Making a recognition request](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Find detailed information about all methods of the service's interfaces in the [API reference](https://{DomainName}/apidocs/speech-to-text-data){: external}.
