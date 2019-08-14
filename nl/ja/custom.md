---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-24"

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

# カスタマイズ・インターフェース
{: #customization}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} で提供されるカスタマイズ・インターフェースを使用して、このサービスの音声認識機能を拡張できます。カスタマイズ機能を使用して、対象の分野と音声に合わせて基本モデルをカスタマイズすることで音声認識要求の正確度を高めることができます。 言語モデルのカスタマイズは、すべての言語で一般出荷可能な機能となります。音響モデルのカスタマイズは、すべての言語でベータ版機能として利用できます。詳しくは、[各言語でのカスタマイズのサポート](#languageSupport)を参照してください。
{: shortdesc}

カスタマイズ・インターフェースは、カスタム言語モデルとカスタム音響モデルの両方をサポートしています。 両タイプのカスタム・モデル用のインターフェースは似ており、簡単に使用できます。 いずれかのタイプのカスタム・モデルを認識要求で使用することも簡単であり、そのためにはモデルのカスタマイズ ID を要求で指定します。

音声認識は、カスタム・モデルを使用するかどうかに関わらず、同じように機能します。 カスタム・モデルを音声認識用に使用する場合は、認識要求で通常使用できるすべての入力パラメーターと出力パラメーターを使用できます。 使用可能なすべてのパラメーターについて詳しくは、[パラメーターの要約](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary)を参照してください。

## 言語モデルのカスタマイズ
{: #customLanguage-intro}

このサービスは、幅広い一般の対象者を念頭に開発されています。 このサービスの基本語彙には、日常的な会話で使用される多数の単語が含まれています。 このサービスのモデルは、多くの用途で十分な正確度の音声認識を実現します。 ただしこれらのモデルでは、特定の分野に関連する特定の用語の知識が不足している場合があります。

*言語モデルのカスタマイズ*・インターフェースを使用すると、医療、法律、情報技術などの分野で音声認識の正確度を向上させることができます。 言語モデルのカスタマイズを使用することで、基本モデルの語彙を拡張および調整して分野固有の用語を追加できます。

カスタム言語モデルを作成して、対象の分野固有のコーパスと単語を追加します。 拡張された語彙に基づいてカスタム言語モデルをトレーニングしたら、そのモデルをカスタマイズされた音声認識用に使用できます。 このサービスは、一般にどのようなカスタム・モデルも数分間でトレーニングできます。 モデルを作成するために要する労力のレベルは、そのモデルに対して使用できるデータに依存します。

詳しくは、以下を参照してください。

-   [カスタム言語モデルの作成](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate)
-   [カスタム言語モデルの使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse)

## 音響モデルのカスタマイズ
{: #customAcoustic-intro}

同様に、このサービスはさまざまな音声特性に適応した基本音響モデルを使用して開発されました。 ただし次のような場合は、基本モデルをカスタマイズしてご使用の音声に適合させることで、音声認識を向上させることができます。

-   ご使用の音響チャネル環境に固有の問題がある場合。 例えば、環境にノイズが多いか、マイクロフォンの品質や配置が最適ではないか、音声が遠方場効果の影響を受ける場合などです。
-   話者の話し方が標準的でない場合。 例えば、話者の話す速度が異常に速いか、音声に砕けた会話が含まれている場合などです。
-   話者のなまりが発音されている場合。 例えば、非母国語や第二言語で話している話者が音声に含まれている場合などです。

*音響モデルのカスタマイズ*・インターフェースを使用すると、基本モデルをカスタマイズして対象の環境と話者に適合させることができます。 カスタム音響モデルを作成して、書き起こそうとしている音声の音響的特性にほぼ一致する音声データ (音声リソース) を追加します。 音声リソースを使用してカスタム音響モデルをトレーニングしたら、そのモデルをカスタマイズされた音声認識用に使用できます。

サービスによってカスタム・モデルをトレーニングするのにかかる時間は、そのモデルに含まれている音声データの量に依存します。 一般に、累積音声の長さの 2 倍のトレーニング時間がかかります。 モデルを作成するために要する労力のレベルは、そのモデルに対して使用できる音声データに依存します。 また、音声の書き起こしを使用するかどうかにも依存します。

詳しくは、以下を参照してください。

-   [カスタム音響モデルの作成](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic)
-   [カスタム音響モデルの使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-acousticUse)

## 文法
{: #grammars-intro}

カスタム言語モデルを使用すると、サービスの基本語彙を拡張できます。 *文法* を使用すると、サービスがこの語彙から認識できる単語を制限できます。 音声認識のためにカスタム言語モデルで文法を使用する場合、サービスはその文法によって認識される単語、句、およびストリングのみを認識できます。 文法では、有効な一致対象を探すための限定された検索スペースが定義されるため、サービスは通常より高速かつ正確に結果を返すことができます。

コーパスの場合と同様に、文法をカスタム言語モデルに追加して、このモデルをトレーニングします。 ただしコーパスとは異なり、音声認識時にカスタム・モデルで文法を使用することを明示的に指定する必要があります。

詳しくは、以下を参照してください。

-   [カスタム言語モデルでの文法の使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars)
-   [カスタム言語モデルへの文法の追加](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd)
-   [音声認識での文法の使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarUse)

## 音響と言語のカスタマイズの併用
{: #combined}

カスタム音響モデルのみを使用して、サービスの認識機能を向上させることができます。 ただし、サンプル音声の書き起こしまたは関連コーパスがある場合は、そのデータを使用して、カスタム音響モデルに基づいて音声認識の質をさらに高めることができます。

カスタム音響モデルを補完するカスタム言語モデルを作成することで、これら 2 つのモデルを併用して音声認識を強化できます。 カスタム音響モデルをトレーニングする際は、音声リソースの書き起こしが含まれたカスタム言語モデルを指定したり、それらのリソース内の分野固有の単語の語彙を指定したりできます。 同様に、音声を書き起こす場合、サービスはカスタム言語モデル、カスタム音響モデル、またはその両方のモデルを受け付けます。 ご使用のカスタム言語モデルに文法が含まれている場合は、そのモデルと文法をカスタム音響モデルとともに音声認識用に使用できます。

詳しくは、[カスタム音響モデルとカスタム言語モデルの併用](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth)を参照してください。

## 各言語でのカスタマイズのサポート
{: #languageSupport}

言語モデルと音響モデルのカスタマイズ機能は一部の言語でのみ使用できます。 次の表では、サービスが各言語についてカスタマイズをサポートしているレベルを示しています。

-   *GA* は、そのインターフェースを実動使用向けに一般出荷可能であることを示します。
-   *ベータ* は、そのインターフェースをベータ版として使用可能であることを示します。
-   *サポート対象外* は、そのインターフェースをその言語で使用できないことを意味します。

広帯域モデルと狭帯域モデルのどちらも、それらのモデルを使用可能な任意のサポート対象言語で使用できます。 言語モデルのカスタマイズをサポートしている言語は、文法もサポートしています。 すべての使用可能なモデルのリストについては、[サポートされている言語モデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-models#modelsList)を参照してください。

<table>
  <caption>表 1. 各言語でのカスタマイズのサポート</caption>
  <tr>
    <th style="text-align:left; vertical-align:bottom; width 24%">
      言語
    </th>
    <th style="text-align:center; vertical-align:bottom; width 37%">
      言語モデルのカスタマイズのサポート
    </th>
    <th style="text-align:center; vertical-align:bottom; width 37%">
      音響モデルのカスタマイズのサポート
    </th>
  </tr>
  <tr>
    <td>ブラジル・ポルトガル語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>フランス語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>ドイツ語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>日本語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>韓国語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>北京語</td>
    <td style="text-align:center">サポートされません</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>現代標準アラビア語</td>
    <td style="text-align:center">サポートされません</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>スペイン語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>英国英語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
  <tr>
    <td>米国英語</td>
    <td style="text-align:center">GA</td>
    <td style="text-align:center">ベータ</td>
  </tr>
</table>

`GET /v1/models` メソッドと `GET /v1/models/{model_id}` メソッドを使用して、任意の言語モデルが言語モデルのカスタマイズをサポートしているかどうかを確認できます。 基本モデルで言語モデルのカスタマイズがサポートされている場合は、このモデルに対するこれらのメソッドの出力の `supported_features` フィールドでは、`custom_language_model` フィールドが `true` に設定されます。

## カスタマイズの使用上の注意
{: #customUsage}

以下の使用上の注意は、言語モデルのカスタマイズと音響モデルのカスタマイズの両方に当てはまります。

### カスタム・モデルの所有権
{: #customOwner}

カスタム・モデルの所有元は、そのモデルを作成するために使用された資格情報を持つ {{site.data.keyword.speechtotextshort}} サービスのインスタンスです。 カスタム・モデルに対して何らかの操作を行うには、そのサービス・インスタンスの資格情報を、カスタマイズ・インターフェースのメソッドで使用する必要があります。他のサービス・インスタンス用に作成された資格情報を使用して、そのカスタム・モデルを表示したりそのカスタム・モデルにアクセスしたりすることはできません。

同じ {{site.data.keyword.speechtotextshort}} サービス・インスタンス用に取得されたすべての資格情報は、そのサービス・インスタンス用に作成されたすべてのカスタム・モデルに対するアクセス権を共有します。 カスタム・モデルへのアクセスを制限するには、別個のサービス・インスタンスを作成して、そのサービス・インスタンスの資格情報のみを使用して、そのモデルを作成して操作してください。 他のサービス・インスタンスの資格情報を使用して、このカスタム・モデルを操作することはできません。

同一サービス・インスタンスの複数の資格情報の間で所有権を共有する利点は、例えば一連の資格情報が漏えいした場合に、それらの資格情報を取り消し可能であることです。 その後、同じサービス・インスタンスの新しい資格情報を作成することで、元の資格情報を使用して作成されたカスタム・モデルの所有権を保持したまま、それらのカスタム・モデルにアクセスできます。

### 機密保護
{: #customSecurity}

カスタム言語モデルとカスタム音響モデルについて追加または更新されたデータに、顧客 ID を関連付けることができます。 顧客 ID をコーパス、カスタム単語、文法、および音声リソースに関連付けるには、次のメソッドを使用して `X-Watson-Metadata` ヘッダーを渡します。

-   `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word_name}`
-   `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`
-   `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`

必要に応じて、後で `DELETE /v1/user_data` メソッドを使用してデータを削除できます。 詳しくは、[機密保護](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security)を参照してください。
