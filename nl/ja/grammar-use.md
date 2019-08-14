---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# 音声認識での文法の使用
{: #grammarUse}

カスタム言語モデルを作成し、文法を使用してそのカスタム言語モデルをトレーニングしたら、サービスの WebSocket インターフェースおよび同期と非同期の HTTP インターフェースを通じて、その文法を音声認識要求で使用できます。
{: shortdesc}

-   `language_customization_id` パラメーターを使用して、文法を定義する対象であるカスタム言語モデルのカスタマイズ ID (GUID) を指定します。要求は、モデルを所有するサービス・インスタンスの資格情報を使用して行う必要があります。
-   `grammar_name` パラメーターを使用して、文法の名前を指定します。 1 つの要求で指定できるのは、単一の文法のみです。

文法を使用する際は、指定された文法内の単語のみがサービスで認識されます。 サービスでは、コーパスから追加されたカスタム単語、個別に追加または変更されたカスタム単語、および他の文法によって認識されるカスタム単語は使用されません。

-   [WebSocket インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets)の場合は、まず `/v1/recognize` メソッドの `language_customization_id` パラメーターを使用してカスタマイズ ID を指定します。 このメソッドを使用して、サービスとの WebSocket 接続を確立します。

    ```javascript
    var my_access_token = '{token}';
    var wsURI = '{ws_url}/v1/recognize'
      + '?access_token=' + my_access_token
      + '&language_customization_id={customization_id}';
    var websocket = new WebSocket(wsURI);
    ```
    {: codeblock}

    次に、アクティブな接続の JSON `start` メッセージで、`grammar_name` パラメーターを使用して文法の名前を指定します。 この値を `start` メッセージを通じて渡すことで、この接続を介して送信する要求ごとに文法を動的に変更できます。

    ```javascript
    function onOpen(evt) {
      var message = {
        action: 'start',
        content-type: 'audio/l16;rate=22050',
        grammar_name: '{grammar_name}'
      };
      websocket.send(JSON.stringify(message));
      websocket.send(blob);
    }
    ```
    {: codeblock}
-   [同期 HTTP インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-http)の場合は、`POST /v1/recognize` メソッドを通じて両方のパラメーターを渡します。

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognize?language_customization_id={customization_id}&grammar_name={grammar_name}"
    ```
    {: pre}
-   [非同期 HTTP インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-async)の場合は、`POST /v1/recognitions` メソッドを通じて両方のパラメーターを渡します。

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: audio/flac"
    --data-binary @audio-file.flac
    "{url}/v1/recognitions?language_customization_id={customization_id}&grammar_name={grammar_name}"
    ```
    {: pre}
