---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-24"

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

# パラメーターの要約
{: #summary}

以下に示すのは、音声認識で利用可能なすべてのパラメーターの要約です。 {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} サービスのすべてのメソッドについて詳しくは、[API リファレンス](https://{DomainName}/apidocs/speech-to-text-data){: external}を参照してください。
{: shortdesc}

音声認識要求を行う場合は、次の基本要件を考慮してください。

-   メソッド名には大/小文字の区別があります。
-   HTTP 要求ヘッダーには大/小文字の区別はありません。
-   HTTP および WebSocket 照会パラメーターには大/小文字の区別があります。
-   JSON フィールド名には大/小文字の区別があります。
-   すべての JSON 応答コンテンツは UTF-8 文字セットになります。

以下のサービス固有の要件も考慮してください。

-   入力音声のみを指定する必要があります。 その他のすべてのパラメーターはオプションです。
-   入力の一部として無効なクエリー・パラメーターまたは JSON フィールドを指定した場合は、無効な引数について説明する `warnings` フィールドが応答に含められます。 警告に関係なく要求は成功します。

## access_token
{: #summary-access-token}

WebSocket インターフェースとの認証済み接続を確立するために使用するアクセス・トークン。詳しくは、[接続を開く](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets#WSopen)を参照してください。

<table>
  <caption>表 1. access_token パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:30%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      <code>/v1/recognize</code> 接続要求の照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      サポートされません
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      サポートされません
    </td>
  </tr>
</table>

## acoustic_customization_id
{: #summary-acoustic-customization-id}

環境やスピーカーの音響特性に合わせて調整されるカスタム音響モデルのカスタマイズ ID (オプション)。 デフォルトでは、カスタム・モデルは使用されません。 詳しくは、[カスタム・モデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input)を参照してください。

<table style="width:90%">
  <caption>表 2. acoustic_customization_id パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語でベータ
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      <code>/v1/recognize</code> 接続要求の照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## audio_metrics
{: #summary-audio-metrics}

サービスが入力音声の信号特性に関するメトリックを返すかどうかを指定するブール値 (オプション)。デフォルト (`false`) では、音声メトリックは返されません。詳しくは、[音声メトリック](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics)を参照してください。

<table style="width:90%">
  <caption>表 3. audio_metrics パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## base_model_version
{: #summary-base-model-version}

基本モデルのバージョン (オプション)。 このパラメーターは、主に、新規基本モデルのために更新されるカスタム・モデルで使用することを意図していますが、カスタム・モデル以外でも使用できます。 デフォルト値は、このパラメーターをカスタム・モデルと共に使用するかどうかによって異なります。 詳しくは、[基本モデルのバージョン](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#version)を参照してください。

<table style="width:90%">
  <caption>表 4. base_model_version パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      <code>/v1/recognize</code> 接続要求の照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## Content-Type
{: #summary-content-type}

サービスに渡す音声データのフォーマットを指定する音声フォーマット (MIME タイプ) (オプション)。 このサービスは、ほとんどの音声のフォーマットを自動的に検出できるため、ほとんどのフォーマットでこのパラメーターはオプションです。 このフィールドが必須となるフォーマットは、`audio/alaw`、 `audio/basic`、`audio/l16`、および `audio/mulaw` です。 詳しくは、[音声フォーマット](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats)を参照してください。

<table style="width:90%">
  <caption>表 5. Content-Type パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージの <code>content-type</code> パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの要求ヘッダー
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの要求ヘッダー
    </td>
  </tr>
</table>

## customization_weight
{: #summary-customization-weight}

サービスによってカスタム言語モデルの単語と基本語彙の単語に付与される相対的な重みづけを示す 0.0 から 1.0 までの double 値 (オプション)。 カスタム言語モデルがトレーニングされたときに別の重みづけが指定された場合を除き、デフォルトは 0.3 です。 詳しくは、[カスタム・モデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input)を参照してください。

<table style="width:90%">
  <caption>表 6. customization_weight パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語、英国英語、ブラジル・ポルトガル語、フランス語、ドイツ語、日本語、韓国語、およびスペイン語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## grammar_name
{: #summary-grammar-name}

音声認識に使用される文法を識別するストリング (オプション)。 サービスは、文法で定義されている文字列のみを認識します。 文法の名前と、その文法が定義されているカスタム言語モデルのカスタマイズ ID の両方を指定する必要があります。 詳しくは、[文法](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#grammars-input)を参照してください。

<table style="width:90%">
  <caption>表 7. grammar_name パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語、英国英語、ブラジル・ポルトガル語、フランス語、ドイツ語、日本語、韓国語、およびスペイン語でベータ
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## inactivity_timeout
{: #summary-inactivity-timeout}

サービスの非アクティブ・タイムアウトの秒数を指定する整数 (オプション)。 非アクティブとは、サービスがストリーミング・オーディオで音声を検出しないことを意味します。 デフォルトは 30 秒です。 無期限にする場合は、`-1` を使用します。 詳しくは、[非アクティブ・タイムアウト](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts-inactivity)を参照してください。

<table style="width:90%">
  <caption>表 8. inactivity_timeout パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## interim_results
{: #summary-interim-results}

最終トランスクリプトの前に変更される可能性が高い中間仮説を返すようにサービスに指示するブール値 (オプション)。 デフォルト (`false`) では、中間結果は返されません。 詳しくは、[中間結果](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim)を参照してください。

<table style="width:90%">
  <caption>表 9. interim_results パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      サポートされません
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      サポートされません
    </td>
  </tr>
</table>

## keywords
{: #summary-keywords}

サービスが入力オーディオで検出するキーワード文字列の配列 (オプション)。 デフォルトでは、キーワード検出は実行されません。 詳しくは、[キーワード検出](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting)を参照してください。

<table style="width:90%">
  <caption>表 10. keywords パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## keywords_threshold
{: #summary-keywords-threshold}

キーワードの肯定一致のための最小しきい値を示す、0.0 から 1.0 までの double (オプション)。 デフォルトでは、キーワード検出は実行されません。 詳しくは、[キーワード検出](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting)を参照してください。

<table style="width:90%">
  <caption>表 11. keywords_threshold パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## language_customization_id
{: #summary-language-customization-id}

使用するドメインの用語が含まれるカスタム言語モデルのカスタマイズ ID (オプション)。 デフォルトでは、カスタム・モデルは使用されません。 詳しくは、[カスタム・モデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input)を参照してください。

<table style="width:90%">
  <caption>表 12. language_customization_id パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語、英国英語、ブラジル・ポルトガル語、フランス語、ドイツ語、日本語、韓国語、およびスペイン語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      <code>/v1/recognize</code> 接続要求の照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## max_alternatives
{: #summary-max-alternatives}

サービスが返す仮説候補の最大数を指定する整数 (オプション)。 デフォルトでは、サービスは 1 つの最終的な仮説を返します。 詳しくは、[最大候補](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives)を参照してください。

<table style="width:90%">
  <caption>表 13. max_alternatives パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## model
{: #summary-model}

音声の発話言語とそのサンプリング・レート (広帯域または狭帯域) を指定するモデル (オプション)。 デフォルトでは、`en-US_BroadbandModel` が使用されます。 詳しくは、[言語とモデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-models)を参照してください。

<table style="width:90%">
  <caption>表 14. model パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      <code>/v1/recognize</code> 接続要求の照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## processing_metrics
{: #summary-processing-metrics}

サービスが入力音声の処理に関するメトリックを返すかどうかを指定するブール値 (オプション)。デフォルト (`false`) では、サービスは処理メトリックを返しません。詳しくは、[処理メトリック](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics)を参照してください。

<table style="width:90%">
  <caption>表 15. processing_metrics パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      サポートされません
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## processing_metrics_interval
{: #summary-processing-metrics-interval}

サービスが処理メトリックを返す間隔を指定する浮動小数点数 (オプション)。値は 0.1 以上です。`processing_metrics` パラメーターが `true` の場合、サービスはデフォルトで 1.0 秒ごとに処理メトリックを返します。詳しくは、[処理メトリック](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics)を参照してください。

<table style="width:90%">
  <caption>表 16. processing_metrics_interval パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      サポートされません
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## profanity_filter
{: #summary-profanity-filter}

サービスが書き起こしに含まれる禁止用語を検閲するかどうかを指定するブール値 (オプション)。 デフォルト (`true`) では、書き起こしから禁止用語がフィルタリングされます。 詳しくは、[禁止用語フィルター](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter)を参照してください。

<table style="width:90%">
  <caption>表 17. profanity_filter パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## redaction
{: #summary-redaction}

サービスが書き起こしに含まれる 3 桁以上の連続した数字からなる数値データを編集するかどうかを指定するブール値 (オプション)。 `redaction` パラメーターを `true` に設定した場合、サービスは自動的に `smart_formatting` パラメーターを `true` に強制設定します。 デフォルト (`false`) では、数値データは編集されません。 詳しくは、[数値の編集](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction)を参照してください。

<table style="width:90%">
  <caption>表 18. redaction パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語、日本語、および韓国語でベータ
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## smart_formatting
{: #summary-smart-formatting}

サービスが最終書き起こしで、日付、時刻、数字、通貨などの値を、より標準的な表現に変換するかどうかを指定するブール値 (オプション)。 米国英語では、この機能はさらに特定のキーワード句を句読点記号に変換します。 デフォルト (`false`) では、スマート・フォーマット設定は実行されません。 詳しくは、[スマート・フォーマット設定](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting)を参照してください。

<table style="width:90%">
  <caption>表 19. smart_formatting パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語、日本語、およびスペイン語でベータ
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## speaker_labels
{: #summary-speaker-labels}

複数参加者交換でどの個人がどの単語を話したかをサービスで識別するかどうかを指定するブール値 (オプション)。 `speaker_labels` パラメーターを `true` に設定した場合、サービスは自動的に `timestamps` パラメーターを `true` に強制設定します。 デフォルト (`false`) では、話者ラベルは返されません。 詳しくは、[話者ラベル](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels)を参照してください。

<table style="width:90%">
  <caption>表 20. speaker_labels パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      米国英語、日本語、およびスペイン語 (広帯域および狭帯域モデル) および英国英語 (狭帯域モデルのみ) でベータ
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## timestamps
{: #summary-timestamps}

サービスが書き起こしの単語のタイム・スタンプを生成するかどうかを指定するブール値 (オプション)。 デフォルト (`false`) では、タイム・スタンプは返されません。 詳しくは、[単語のタイム・スタンプ](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps)を参照してください。

<table style="width:90%">
  <caption>表 21. timestamps パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## Transfer-Encoding
{: #summary-transfer-encoding}

オーディオをサービスにストリームさせる `chunked` の値 (オプション)。 デフォルトでは、オーディオは 1 回限りの配信として一斉に送信されます。 詳しくは、[音声の伝送](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission)を参照してください。

<table style="width:90%">
  <caption>表 22. Transfer-Encoding パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      適用外、常にストリームされる
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの要求ヘッダー
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの要求ヘッダー
    </td>
  </tr>
</table>

## word_alternatives_threshold
{: #summary-word-alternatives-threshold}

サービスが入力音声の単語について音響的に類似した候補を報告するしきい値を指定する 0.0 から 1.0 までの double 値 (オプション)。 デフォルトでは、単語候補は返されません。 詳しくは、[単語候補](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives)を参照してください。

<table style="width:90%">
  <caption>表 23. word_alternatives_threshold パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## word_confidence
{: #summary-word-confidence}

サービスが書き起こしの単語の信頼度を提供するかどうかを指定するブール値 (オプション)。 デフォルト (`false`) では、信頼度は返されません。 詳しくは、[単語の信頼度](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence)を参照してください。

<table style="width:90%">
  <caption>表 24. word_confidence パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      JSON <code>start</code> メッセージのパラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognize</code> メソッドの照会パラメーター
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/recognitions</code> メソッドの照会パラメーター
    </td>
  </tr>
</table>

## X-Watson-Metadata
{: #summary-x-watson-metadata}

認識要求のために渡されたデータにカスタマー ID を関連付ける文字列 (オプション)。 このパラメーターは、引数 `customer_id={id}` を受け入れます。 デフォルトでは、データにカスタマー ID は関連付けられません。 詳しくは、[機密保護](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security)を参照してください。

<table style="width:90%">
  <caption>表 25. X-Watson-Metadata パラメーター</caption>
  <tr>
    <th>可用性および使用法</th>
    <th style="vertical-align:bottom">説明</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **可用性**
    </td>
    <td style="text-align:left">
      すべての言語で一般出荷可能
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      <code>/v1/recognize</code> 接続要求の <code>x-watson-metadata</code> 照会パラメーター (引数は URL エンコードにする必要があります。例: `customer_id%3dmy_customer_ID`)
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **同期 HTTP**
    </td>
    <td style="text-align:left">
      POST <code>/v1/recognize</code> メソッドの要求ヘッダー
</td>
  </tr>
  <tr>
    <td style="text-align:left">
      **非同期 HTTP**
    </td>
    <td style="text-align:left">
      <code>POST /v1/register_callback</code> および
      <code>POST /v1/recognitions</code> メソッドの要求ヘッダー
    </td>
  </tr>
</table>
