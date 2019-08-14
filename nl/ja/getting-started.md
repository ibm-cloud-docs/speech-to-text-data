---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-25"

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

# 入門チュートリアル
{: #gettingStarted}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} は音声をテキストに書き起こすことで、さまざまな用途に音声書き起こし機能を使用できるようにします。このチュートリアルでは curl コマンドを活用して、サービスを素早く使用開始することを支援します。さまざまな事例を通じて、サービスの `POST /v1/recognize` メソッドを呼び出して書き起こしを要求する方法を示します。
{: shortdesc}

## 始めに
{: #before-you-begin}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} を使用するには、まず以下の手順を実行する必要があります。

1.  {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} のインスタンスをプロビジョンします。プロビジョニングについて詳しくは、[サービスのインストール](/docs/services/speech-to-text-data?topic=speech-to-text-data-install)を参照してください。
1.  {{site.data.keyword.icp4dfull_notm}} Web クライアントのメニューから、**「マイ・インスタンス」**を選択します。
1.  {{site.data.keyword.speechtotextshort}} インスタンスをクリックして、概要ページを開きます。`{token}` および `{URL}` 資格情報値をコピーします。

### curl の使用例
{: #getting-started-curl}

このチュートリアルでは、`curl` コマンドを使用して、サービスの HTTP インターフェースのメソッドを呼び出します。ご使用のシステムに `curl` コマンドがインストールされていることを確認してください。

1.  `curl` がインストールされているかどうかをテストするには、コマンド・ラインで次のコマンドを実行します。Secure Sockets Layer (SSL) をサポートする `curl` のバージョンが出力にリストされたら、チュートリアルの準備ができています。

    ```bash
    curl -V
    ```
    {: pre}

1.  必要であれば、ご使用のオペレーティング・システムに合った SSL 対応バージョンの `curl` を [curl.haxx.se](https://curl.haxx.se/){: external} からインストールします。

例で使用されている中括弧は省略してください。それらは可変値を表しています。
{: tip}

## ステップ 1: オプションを使用せずに音声を書き起こす
{: #transcribe}

追加の要求パラメーターなしで `POST /v1/recognize` メソッドを呼び出して、FLAC 音声ファイルの基本的な書き起こしを要求します。

1.  サンプル音声ファイル <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a> をダウンロードします。
1.  次のコマンドを実行して、基本的な書き起こしを実行するためのサービスの `/v1/recognize` メソッドをパラメーターなしで呼び出します。 この例では、`Content-Type` ヘッダーを使用して `audio/flac` という音声タイプを指定しています。 この例では、デフォルトの言語モデル `en-US_BroadbandModel` を書き起こし用に使用しています。
    -   `{token}` をサービス・インスタンスのアクセス・トークンに置き換えます。
    -   `{url}` をサービス・インスタンスの URL に置き換えます。
    -   `{path_to_file}` は、`audio-file.flac` ファイルの場所を指定するように変更します。

    *Windows ユーザーは、*各行末の円記号 (``&#xa5;`) をキャレット (``^`) に置き換えてください。末尾にスペースが入らないように注意してください。
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize"
    ```
    {: pre}

    サービスから以下の書き起こし結果が返されます。

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

## ステップ 2: オプションを使用して音声を書き起こす
{: #transcribeOptions}

`POST /v1/recognize` メソッドを呼び出して同じ FLAC 音声ファイルを書き起こしますが、ここでは 2 つの書き起こしパラメーターを指定します。

1.  必要に応じて、サンプル音声ファイル <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン" title="外部リンク・アイコン"></a> をダウンロードします。
1.  次のコマンドを実行して、サービスの `/v1/recognize` メソッドを 2 つの追加パラメーター付きで呼び出します。 `timestamps` パラメーターを `true` に設定して、音声ストリーム内の各単語の始まりと終わりを示します。 `max_alternatives` パラメーターを `3` に設定して、最も可能性が高い代替の書き起こし結果を 3 つ受け取るようにします。 この例では、`Content-Type` ヘッダーを使用して `audio/flac` という音声タイプを指定しており、この要求ではデフォルト・モデル `en-US_BroadbandModel` を使用しています。
    -   `{token}` をサービス・インスタンスのアクセス・トークンに置き換えます。
    -   `{url}` をサービス・インスタンスの URL に置き換えます。
    -   `{path_to_file}` は、`audio-file.flac` ファイルの場所を指定するように変更します。

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: audio/flac" \
    --data-binary @{path_to_file}audio-file.flac \
    "{url}/v1/recognize?timestamps=true&max_alternatives=3"
    ```
    {: pre}

    サービスから返される次の結果には、タイム・スタンプと 3 つの代替書き起こし内容が含まれています。

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
              "transcript": "several tornadoes touched down as a line of
severe thunderstorms swept through Colorado on Sunday "
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

## 次のステップ

-   音声認識要求を発行するために使用できるインターフェースと SDK について詳しくは、[開発者向けの概要](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview)を参照してください。
-   サービスに対して要求を行う方法について詳しくは、[サービスに対する要求を行う](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests)を参照してください。
-   サービスの各インターフェースで使用する基本的な音声認識要求については、[認識要求の実行](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request)を参照してください。
-   サービスのインターフェースのすべてのメソッドについて詳しくは、[API リファレンス](https://{DomainName}/apidocs/speech-to-text-data){: external}を参照してください。
