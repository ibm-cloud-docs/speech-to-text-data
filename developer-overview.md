---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-04"

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

# Overview for developers
{: #developerOverview}

You can access the capabilities of {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} by using a WebSocket interface and by using synchronous or asynchronous HTTP Representational State Transfer (REST) interfaces. You can also customize the service's language models to suit your domain and environment. SDKs are available to simplify application development in many programming languages.
{: shortdesc}

You authenticate to the {{site.data.keyword.speechtotextshort}} service by passing an access token with each request. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} is a multi-tenant cloud solution. Your credentials provide access only to your data, and your data is isolated from other users.

## Programming with the service
{: #programming}

[Making a recognition request](/docs/speech-to-text-data?topic=speech-to-text-data-basic-request) shows you how to request basic transcription with each of the service's programming interfaces:

-   [The WebSocket interface](/docs/speech-to-text-data?topic=speech-to-text-data-websockets) offers an efficient, low-latency, and high-throughput implementation over a full-duplex connection.
-   [The synchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-http) provides a basic interface to transcribe audio with blocking requests.
-   [The asynchronous HTTP interface](/docs/speech-to-text-data?topic=speech-to-text-data-async) provides a non-blocking interface that lets you register a callback URL to receive notifications or to poll the service for job status and results.

The interfaces provide similar speech recognition capabilities, but you might specify the same parameter as a request header, a query parameter, or a parameter of a JSON object depending on the interface that you use.

The WebSocket and synchronous HTTP interfaces accept a maximum of 100 MB of audio data with a single request. The asynchronous HTTP interface accepts a maximum of 1 GB of audio data with a request.

-   For information about making requests with each of the {{site.data.keyword.speechtotextshort}} interfaces, see [Making requests to the service](/docs/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   For examples of basic speech recognition requests with each of the service's interfaces, see [Making a recognition request](/docs/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   For descriptions of all available speech recognition parameters, see the [Parameter summary](/docs/speech-to-text-data?topic=speech-to-text-data-summary).
-   For descriptions of all methods and their parameters, along with examples, see the [API reference](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Advantages of the WebSocket interface
{: #advantages}

The WebSocket interface has a number of advantages over the HTTP interface:

-   The WebSocket interface provides a single-socket, full-duplex communication channel. The interface lets the client send requests and audio to the service and receive results over a single connection in an asynchronous fashion.
-   It provides a much simpler and more powerful programming experience. The service sends event-driven responses to the client's messages, eliminating the need for the client to poll the server.
-   It allows you to establish and use a single authenticated connection indefinitely. The HTTP interfaces require you to authenticate each call to the service.
-   It reduces latency. Recognition results arrive faster because the service sends them directly to the client. The HTTP interface requires four distinct requests and connections to achieve the same results.
-   It reduces network utilization. The WebSocket protocol is lightweight. It requires only a single connection to perform live-speech recognition.
-   It enables audio to be streamed directly from browsers (HTML5 WebSocket clients) to the service.

## Customizing the service
{: #customizing}

[The customization interface](/docs/speech-to-text-data?topic=speech-to-text-data-customization) lets you create custom models to improve the service's speech recognition capabilities:

-   [Custom language models](/docs/speech-to-text-data?topic=speech-to-text-data-languageCreate) let you define domain-specific words for a base model. Custom language models expand the service's base vocabulary with terminology specific to domains such as medicine and law.
-   [Custom acoustic models](/docs/speech-to-text-data?topic=speech-to-text-data-acoustic) let you adapt a base model for the acoustic characteristics of your environment and speakers. Custom acoustic models improve the service's ability to recognize speech for specific acoustic characteristics.
-   [Grammars](/docs/speech-to-text-data?topic=speech-to-text-data-grammars) let you restrict the phrases that the service can recognize to those defined in the grammar's rules. By limiting the search space for valid strings, the service can deliver results faster and more accurately. Grammars are supported with custom language models.

You can use a custom language model, a custom acoustic model, or both for speech recognition with any of the service's interfaces.

## Obtaining metrics
{: #overview-metrics}

The service offers two types of optional metrics for speech recognition requests:

-   [Processing metrics](/docs/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) provide detailed timing information about the service's analysis of the input audio. The service returns the metrics at specified intervals and with transcription events, such as interim and final results. You can use the metrics to gauge the service's progress in transcribing the audio.
-   [Audio metrics](/docs/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) provide detailed information about the signal characteristics of the input audio. The results provide aggregated metrics for the entire input audio at the conclusion of speech processing. You can use the metrics to determine the characteristics and quality of the audio.

You can request processing metrics with the WebSocket and asynchronous HTTP interfaces. You can request audio metrics with any of the service's interfaces. By default, the service returns no metrics.

## CORS support
{: #cors}

The service supports Cross-Origin Resource Sharing (CORS). By using CORS, web pages can request resources directly from a foreign domain. CORS circumvents the same-origin security policy, which otherwise prevents such requests. Because the service supports CORS, a web page can communicate directly with the service without passing the request through the web server that hosts the page.

For instance, a web page that is loaded from a server in {{site.data.keyword.cloud}} can call the customization API directly, bypassing the {{site.data.keyword.cloud_notm}} server. For more information, see [enable-cors.org](https://enable-cors.org/){: external}.

## Using Software Development Kits
{: #sdks}

SDKs are available for the {{site.data.keyword.speechtotextshort}} service to simplify the development of speech applications. {{site.data.keyword.ibmwatson}} SDKs are available for many popular programming languages and platforms.

-   For a complete list of SDKs and links to the SDKs on GitHub, see [Using SDKs](/docs/speech-to-text-data?topic=watson-using-sdks).
-   For detailed information about all methods of the Node, Java&trade;, Python, Ruby, and Go SDKs for the {{site.data.keyword.speechtotextshort}} service, see the [API reference](https://{DomainName}/apidocs/speech-to-text-data){: external}.
