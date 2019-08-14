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

# カスタム言語モデルの作成
{: #languageCreate}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} のカスタム言語モデルを作成するには、以下の手順に従います。
{: shortdesc}

1.  [カスタム言語モデルを作成します](#createModel-language)。 同じ分野または異なる分野を対象とした複数のカスタム・モデルを作成できます。 そのプロセスは、作成するすべてのモデルで同一です。 ただし、認識要求で一度に指定できるカスタム・モデルは 1 つに限られます。
1.  [カスタム言語モデルにコーパスを追加します](#addCorpus)。 コーパスとは、特定の分野の用語をコンテキストに応じて使用する、プレーン・テキスト形式の文書のことです。 このサービスは、基本語彙には含まれていない用語をコーパスから抽出して、カスタム・モデルの語彙を構築します。 1 つのカスタム・モデルに複数のコーパスを追加することができます。
1.  [カスタム言語モデルに単語を追加します](#addWords)。 カスタム単語を個別にモデルに追加することもできます。 また、同じメソッドを使用して、コーパスから抽出されたカスタム単語を変更することもできます。 これらのメソッドでは、単語の発音や、音声書き起こしで単語を表示する方法を指定できます。
1.  [カスタム言語モデルをトレーニングします](#trainModel-language)。 カスタム・モデルに単語を追加した後は、それらの単語に関してモデルをトレーニングする必要があります。 トレーニングによって、カスタム・モデルを音声認識で使用できる状態に準備します。 トレーニングされるまでは、モデルで新規単語または変更された単語は使用されません。
1.  カスタム・モデルのトレーニングが完了した後、そのモデルを認識要求で使用できます。 書き起こしのために渡される音声に、カスタム・モデルで定義されている分野固有の単語が含まれている場合、要求の結果にはモデルの拡張語彙が反映されます。 詳しくは、[カスタム言語モデルの使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse)を参照してください。

カスタム言語モデルを作成する手順は、反復的なものです。 必要に応じて何度でも、コーパスの追加、単語の追加、モデルのトレーニングまたはリトレーニングを行うことができます。

カスタム言語モデルに文法も追加できます。 文法を追加すると、サービスの応答が、文法によって認識される単語のみに制限されます。 詳しくは、[カスタム言語モデルでの文法の使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars)を参照してください。

言語モデル・カスタマイズは、ほとんどの言語で有効です。 詳しくは、[各言語でのカスタマイズのサポート](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport)を参照してください。
{: note}

## カスタム言語モデルの作成
{: #createModel-language}

新しいカスタム言語モデルを作成するには、`POST /v1/customizations` メソッドを使用します。 作成できるカスタム言語モデルの数に制限はありませんが、音声認識要求で一度に使用できるモデルは 1 つに限られます。 このメソッドは、新しいカスタム・モデルの属性を定義する JSON オブジェクトを、要求の本体として受け入れます。

<table>
  <caption>表 1. 新規カスタム言語モデルの属性</caption>
  <tr>
    <th style="width:20%; text-align:left">パラメーター</th>
    <th style="width:12%; text-align:center">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>必須</em></td>
    <td style="text-align:center">String</td>
    <td>
      新規カスタム・モデルのユーザー定義の名前。 カスタム・モデルの分野を表す名前を使用してください (例えば、<code>Medical custom model</code>、<code>Legal custom model</code> など)。 ユーザーが
      所有するすべてのカスタム言語モデルの間で一意となる名前を使用します。
      カスタム・モデルの言語と一致するローカライズされた名前を使用します。
    </td>
  </tr>
  <tr>
    <td><code>base_model_name</code><br/><em>必須</em></td>
    <td style="text-align:center">String</td>
    <td>
      新規カスタム・モデルによってカスタマイズする
      言語モデルの名前。 <code>GET /v1/models</code> メソッドによって返される、
      サポートされる言語モデルのいずれかを指定します。 新規モデルは、
      カスタマイズ対象の基本モデルでのみ使用できます。
    </td>
  </tr>
  <tr>
    <td><code>dialect</code><br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td>
      カスタム・モデルで使用される指定の言語の
      方言。 デフォルトで、方言は基本モデルの言語と一致します。
      例えば、米国英語言語モデルの <code>en-US_BroadbandModel</code>
      または <code>en-US_NarrowbandModel</code>
      のいずれかの場合、方言は
      <code>en-US</code> です。<br/></br>
      このパラメーターは、スペイン語モデルの場合にのみ意味があります。
      サービスでは、スペイン語モデルに対して、以下に示された方言での音声に適合する
      カスタム・モデルが作成されます。
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          カスティリャ・スペイン語の場合は <code>es-ES</code> (デフォルト)
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          ラテンアメリカ・スペイン語の場合は <code>es-LA</code>
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          北米 (メキシコ) スペイン語の場合は <code>es-US</code>
        </li>
      </ul>
      方言を指定する場合、それが基本モデルで有効である必要があります。
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td>
      新規モデルの説明。 カスタム・モデルの言語と一致するローカライズされた説明を使用します。
    </td>
  </tr>
</table>

以下に、`Example model` という名前の新規カスタム・モデルを作成する例を示します。 このモデルは基本モデル `en-US-BroadbandModel` を対象に作成され、`Example custom language model` という説明が指定されています。 `Content-Type` ヘッダーで、メソッドに JSON データが渡されることを指定します。

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/json"
--data "{\"name\": \"Example model\",
  \"base_model_name\": \"en-US_BroadbandModel\",
  \"description\": \"Example custom language model\"}"
"{url}/v1/customizations"
```
{: pre}

この例では、新規モデルのカスタマイズ ID が返されます。 各カスタムモデルは、GUID (Globally Unique Identifier) で表されるカスタマイズ ID によって識別されます。 カスタム・モデルに関連する呼び出しで、そのモデルの GUID を指定するには、`customization_id` パラメーターを使用します。

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96"
}
```
{: codeblock}

新規カスタム・モデルの所有元は、そのモデルを作成するために使用された資格情報を持つサービスのインスタンスです。詳しくは、[カスタム・モデルの所有権](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#customOwner)を参照してください。

## カスタム言語モデルへのコーパスの追加
{: #addCorpus}

カスタム言語モデルを作成した後は、次のステップとして、そのモデルにデータ (分野固有の単語) を追加します。 カスタム・モデルに新規単語を追加する方法として推奨されるのは、1 つ以上のコーパスを追加することです。

コーパスは、理想的には、対象分野で使用される例文が含まれる、プレーン・テキスト・ファイルです。 サービスでは、コーパスのファイル内容が解析され、基本語彙に含まれていないすべての単語が抽出されます。 このような単語は、未知 (OOV) 語と呼ばれます。

-   コーパスの使用について詳しくは、[コーパスの処理](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingCorpora)を参照してください。
-   サービスによってコーパスがモデルに追加される方法について詳しくは、[コーパス・ファイル追加時の動作](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseCorpus)を参照してください。

コーパスで新規単語を含む文が提供されることにより、サービスはコンテキストで単語を学習できるようになります。 その後、モデルの単語を個別に追加または変更できます。 コーパスから追加した単語に関してモデルをトレーニングするのではなく、個々の単語に関してのみモデルをトレーニングすると、トレーニングに時間がかかるだけでなく、得られる結果の有効性が低くなる可能性があります。
{: tip}

コーパスをカスタム・モデルに追加するには、`POST /v1/customizations/{customization_id}/corpora/{corpus_name}` メソッドを使用します。

-   `customization_id` パス・パラメーターにカスタム・モデルのカスタマイズ ID を指定します。
-   `corpus_name` パス・パラメーターにコーパスの名前を指定します。 カスタム・モデルの言語と一致し、コーパスの内容を反映する、ローカライズされた名前を使用します。
    -   名前の最大文字数は 128 文字です。
    -   URL エンコードする必要のある文字は使用しないでください。例えば、スペース、スラッシュ、円記号、コロン、アンパーサンド、二重引用符、正符号、等号、疑問符などは、名前に使用しないでください。(これらの文字の使用がサービスによって禁止されているわけではありません。ただし、これらの文字を使用するときには常に URL エンコードする必要があるため、使用は推奨されません。)
    -   カスタム・モデルに既に追加されているコーパスや文法の名前を使用しないでください。
    -   名前 `user` を使用しないでください。これは、ユーザーによって追加または変更されるカスタム単語を表すためにサービスによって予約されています。
    -   `base_lm` および `default_lm` という名前は使用しないでください。いずれの名前も、サービスで将来使用するために予約されています。
-   要求の本体としてコーパス・テキスト・ファイルを渡します。

すべてのソースから合わせて最大で 9 万の OOV 語および合計 1000 万の単語を追加できます。 これには、コーパスおよび文法からの単語、および直接追加する単語が含まれます。 詳しくは、[必要なデータ量](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#wordsResourceAmount)を参照してください。
{: note}

以下に、指定の ID を持つカスタム・モデルに、コーパス・テキスト・ファイル `healthcare.txt` を追加する例を示します。 例では、コーパス `healthcare` が指定されています。

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--data-binary @healthcare.txt
"{url}/v1/customizations/{customization_id}/corpora/healthcare"
```
{: pre}

このメソッドでは、カスタム・モデルの既存のコーパスを上書きする、オプションの `allow_overwrite` クエリー・パラメーターも受け入れられます。 コーパス・ファイルをモデルに追加した後で、コーパス・ファイルの更新が必要になった場合、このパラメーターを使用します。

このメソッドは非同期です。 完了するまでに約 1、2 分かかる場合があります。 操作の所要時間は、コーパスに含まれる単語の総数、サービスがコーパスから検出する新規単語の数、およびサービスに現在かかっている負荷に応じて変わります。 コーパスのステータスを確認する方法について詳しくは、[コーパスの追加要求のモニタリング](#monitorCorpus)を参照してください。

コーパス・テキスト・ファイルごとにメソッドを呼び出すことによって、1 つのカスタム・モデルに任意の数のコーパスを追加することができます。 1 つのコーパスが完全に追加されてから、別のコーパスを追加する必要があります。 カスタム・モデルにコーパスを追加した後、新規カスタム単語を調べて、タイプミスやその他の誤りがないことを確認します。 詳しくは、[単語リソースの検証](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel)を参照してください。

### コーパスの追加要求のモニタリング
{: #monitorCorpus}

コーパスが有効な場合、サービスは 201 応答コードを返します。 その後、コーパスの内容を非同期で処理して、自動的に新規単語を抽出します。 現在の要求に対してサービスによるコーパスの分析が完了するまでは、カスタム・モデルにデータを追加する要求やモデルをトレーニングする要求を実行依頼することはできません。

分析のステータスを判別するには、`GET /v1/customizations/{customization_id}/corpora/{corpus_name}` メソッドを使用して、コーパスのステータスをポーリングします。 以下の例に示すように、メソッドではモデルの ID およびコーパスの名前が受け入れられます。

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/corpora/corpus1"
```
{: pre}

応答にはコーパスのステータスが含まれます。

```javascript
{
  "name": "corpus1",
         "total_words": 5037,
         "out_of_vocabulary_words": 401,
         "status": "analyzed"
}
```
{: codeblock}

`status` フィールドには、以下のいずれかの値が設定されます。

-   `analyzed` は、サービスによるコーパスの分析が正常に完了したことを意味します。
-   `being_processed` は、サービスによるコーパスの分析がまだ進行中であることを意味します。
-   `undetermined` は、コーパスの処理中にサービスでエラーが発生したことを意味します。

コーパスのステータスが `analyzed` になるまで、ループを使用して 10 秒間隔でステータスを確認します。 モデルのコーパスのステータスを確認する方法について詳しくは、[カスタム言語モデルのコーパスのリスト](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora)を参照してください。

## カスタム言語モデルへの単語の追加
{: #addWords}

カスタム言語モデルに単語を追加する方法としてコーパスを追加することが推奨されますが、個別のカスタム単語をモデルに直接追加することもできます。 サービスはコーパスで検出した OOV 語を追加する場合と同じように、カスタム単語をカスタム・モデルに追加します。

モデルに追加する単語が 1 つのみまたは少数の場合は、コーパスを使用して単語を追加することは、実践的でも実行可能でもない場合があります。 最も単純な方法は、つづりだけを指定して単語を追加することです。 ただし、単語に複数の発音を指定したり、単語の表示方法を指定したりすることもできます。

-   単語を直接追加する方法について詳しくは、[カスタム単語の処理](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingWords)を参照してください。
-   サービスによってカスタム単語がモデルに追加される方法について詳しくは、[カスタム単語の追加または変更時の動作](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseWord)を参照してください。

単語をカスタム・モデルに追加するには、以下のメソッドを使用できます。

-   `POST /v1/customizations/{customization_id}/words` メソッドを使用すると、複数の単語が一度に追加されます。 要求本体で、各単語に関する情報を提供する JSON オブジェクトを渡します。 以下に、指定の ID を持つカスタム・モデルに、`HHonors` および `IEEE` という 2 つのカスタム単語を追加する例を示します。 `Content-Type` ヘッダーで、メソッドに JSON データが渡されることを指定します。

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data "{\"words\": [
      {\"word\": \"HHonors\", \"sounds_like\": [\"hilton honors\", \"H. honors\"], \"display_as\": \"HHonors\"},
      {\"word\": \"IEEE\", \"sounds_like\": [\"I. triple E.\"]}]}"
    "{url}/v1/customizations/{customization_id}/words"
    ```
    {: pre}

    ファイルから単語を追加することもできます。 例えば、ファイル `words.json` で上記と同じ 2 つのカスタム単語が定義されています。

    ```
    {"words":
      [
        {"word": "HHonors", "sounds_like": ["hilton honors", "H. honors"], "display_as": "HHonors"},
        {"word": "IEEE", "sounds_like": ["I. triple E."]}
      ]
    }
    ```
    {: codeblock}

    以下のコマンドによって、ファイルから単語を追加します。

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data-binary @words.json
    "{url}/v1/customizations/{customization_id}/words"
    ```
    {: pre}

    このメソッドは非同期です。 完了するまでの時間は、追加する単語の数およびサービスに現在かかっている負荷に応じて変わります。 操作のステータスを確認する方法について詳しくは、[単語の追加要求のモニタリング](#monitorWords)を参照してください。
-   `PUT /v1/customizations/{customization_id}/words/{word_name}` メソッドを使用すると、個別の単語が追加されます。 単語に関する情報を提供する JSON オブジェクトを渡します。 以下に、指定の ID のモデルに単語 `NCAA` を追加する例を示します。 この場合も、`Content-Type` ヘッダーで、メソッドに JSON データが渡されることを指定します。

    ```bash
    curl -X PUT
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data "{\"sounds_like\": [\"N. C. A. A.\", \"N. C. double A.\"]}"
    "{url}/v1/customizations/{customization_id}/words/NCAA"
    ```
    {: pre}

    このメソッドは同期処理です。 サービスは、要求の成功または失敗を報告する応答コードを直ちに返します。

コーパスを追加する場合と同様に、新規カスタム単語を調べて、タイプミスやその他の誤りがないことを確認します。 この確認は、複数の単語を一度に追加する場合は特に重要です。 詳しくは、[単語リソースの検証](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel)を参照してください。

### 単語の追加要求のモニタリング
{: #monitorWords}

`POST /v1/customizations/{customization_id}/words` メソッドを使用したときに、入力データが有効な場合、サービスは 201 応答コードを返します。 その後、単語を非同期で処理してモデルに追加します。 この操作は通常、コーパスを追加したりモデルをトレーニングしたりする場合よりも迅速ですが、所要時間は、追加する新規単語の数およびサービスに現在かかっている負荷に応じて変わります。 サービスが新規単語の追加要求を完了するまでは、カスタム・モデルにデータを追加する要求やモデルをトレーニングする要求は実行依頼できません。

要求のステータスを判別するには、`GET /v1/customizations/{customization_id}` メソッドを使用して、モデルのステータスをポーリングします。 以下の例に示すように、メソッドではモデルのカスタマイズ ID が受け入れられ、そのモデルのステータスを含む情報が返されます。

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
  "created": "2016-06-01T18:42:25.324Z",
  "updated": "2016-06-01T18:45:11.737Z",
  "language": "en-US",
  "dialect": "en-US",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model",
  "description": "Example custom language model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "pending",
  "progress": 0
}
```
{: codeblock}

`status` フィールドで、モデルの現在の状態が報告されます。 サービスが新規単語を処理している間は、ステータスは `pending` のままです。 ステータスが `ready` になり操作の完了が示されるまで、ループを使用して 10 秒間隔でステータスを確認します。 有効な `status` 値について詳しくは、[モデルのトレーニング要求のモニタリング](#monitorTraining-language)を参照してください。

### カスタム・モデルの単語の変更
{: #modifyWord}

`POST /v1/customizations/{customization_id}/words` メソッドおよび `PUT /v1/customizations/{customization_id}/words/{word_name}` メソッドを使用して、カスタム・モデルの単語を変更または拡張することもできます。 モデルに単語を追加したときに発生したタイプミスやその他の誤りを修正するために、これらのメソッドを使用しなければならない場合があります。 また、既存の単語に同音異字の定義を追加しなければならない場合もあります。

既存の単語の定義を変更するには、単語を追加する場合とまったく同じようにこれらのメソッドを使用します。 単語に指定する新規データによって、その単語の既存の定義が上書きされます。

## カスタム言語モデルのトレーニング
{: #trainModel-language}

コーパスの追加、文法の追加、または単語の直接追加により、カスタム言語モデルに新規単語を取り込んだ後は、新規データに関してモデルをトレーニングする必要があります。 トレーニングにより、音声認識においてカスタム・モデルでそれらのデータが使用されるように準備します。 データに関してトレーニングされるまでは、どのような方法によって追加した単語であってもモデルでは使用されません。

カスタム・モデルをトレーニングするには、`POST /v1/customizations/{customization_id}/train` メソッドを使用します。 以下の例に示すように、トレーニングするモデルのカスタマイズ ID をこのメソッドに渡します。

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/train"
```
{: pre}

このメソッドは非同期です。 モデルをトレーニングする対象の新規単語の数およびサービスに現在かかっている負荷によっては、トレーニングが完了するまでに数分かかる場合があります。 トレーニング操作のステータスを確認する方法について詳しくは、[モデルのトレーニング要求のモニタリング](#monitorTraining-language)を参照してください。

このメソッドには、以下のオプションのクエリー・パラメーターが含まれています。

-   `word_type_to_add` パラメーターは、カスタム・モデルをトレーニングする対象の単語を指定します。
    -   単語の取得元にかかわらず、すべての単語に関してモデルをトレーニングするには、`all` を指定するか、このパラメーターを省略します。
    -   ユーザーによって追加または変更された単語に関してのみモデルをトレーニングし、コーパスまたは文法からのみ抽出された単語を無視するには、`user` を指定します。

    タイプミスが含まれる単語など、データにノイズがあるコーパスを追加する場合は、このオプションが役立ちます。 そのようなデータに関してモデルをトレーニングする前に、`GET /v1/customizations/{customization_id}/words` メソッドの `word_type` クエリー・パラメーターを使用して、コーパスおよび文法から抽出された単語を確認できます。 詳しくは、[カスタム言語モデルの単語のリスト](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords)を参照してください。
-   カスタム・モデルが音声認識で使用される場合、`customization_weight` パラメーターによって、基本語彙の単語と対比してカスタム・モデルの単語に付与される相対的な重みを指定します。カスタム・モデルを使用する認識要求であればカスタマイズの重みを指定できます。 詳しくは、[カスタマイズの重み付けの使用](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse#weight)を参照してください。
-   `strict` パラメーターは、カスタム・モデルに有効なリソースと無効なリソース (コーパス、文法、単語) が混在している場合にトレーニングを進めるかどうかを示します。デフォルトでは、モデルに 1 つ以上の無効なリソースが含まれている場合、トレーニングは失敗します。モデルに少なくとも 1 つの有効なリソースが含まれている場合にトレーニングを続行できるようにするには、このパラメーターを `false` に設定します。サービスにより無効なリソースはトレーニングから除外されます。詳しくは、[トレーニングの失敗](#failedTraining-language)を参照してください。

### モデルのトレーニング要求のモニタリング
{: #monitorTraining-language}

トレーニング・プロセスが正常に開始されると、サービスは 200 応答コードを返します。 既存の要求が完了するまで、サービスは以降のトレーニング要求や、コーパス、文法、または単語を新規に追加する要求を受け入れることはできません。

トレーニング要求のステータスを判別するには、`GET /v1/customizations/{customization_id}` メソッドを使用して、モデルのステータスをポーリングします。 このメソッドではモデルのカスタマイズ ID が受け入れられ、そのモデルに関する情報が返されます。

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96",
  "created": "2016-06-01T18:42:25.324Z",
  "updated": "2016-06-01T18:45:11.737Z",
  "language": "en-US",
  "dialect": "en-US",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "name": "Example model",
  "description": "Example custom language model",
  "base_model_name": "en-US_BroadbandModel",
  "status": "training",
  "progress": 0
}
```
{: codeblock}

応答には、カスタム・モデルの状態を報告する `status` フィールドおよび `progress` フィールドが含まれます。 `progress` フィールドの意味は、モデルのステータスに応じて異なります。 `status` フィールドには、以下のいずれかの値が設定されます。

-   `pending` は、モデルは作成されたが、有効なトレーニング・データの追加を待機しているか、サービスによる追加データの分析完了を待機していることを意味します。 この場合、`progress`
フィールドは `0` になります。
-   `ready` は、モデルに有効なデータが取り込まれ、モデルのトレーニングを開始できる状態になっていることを意味します。 この場合、`progress`
フィールドは `0` になります。

モデルに有効なリソースと無効なリソース (有効なカスタム単語と無効なカスタム単語の両方など) が混在している場合は、`strict` 照会パラメーターを `false` に設定していない限り、モデルのトレーニングが失敗します。詳しくは、[トレーニングの失敗](#failedTraining-language)を参照してください。
-   `training` は、モデルがトレーニング中であることを意味します。 トレーニングが完了した時点で、`progress` フィールドの値は `0` から `100` に変わります。<!-- The `progress` field indicates the progress of the training as a percentage complete. -->
-   `available` は、モデルのトレーニングが完了し、モデルが使用可能な状態になっていることを意味します。 この場合、`progress`
フィールドは `100` になります。
-   `upgrading` は、モデルがアップグレード中であることを意味します。 この場合、`progress`
フィールドは `0` になります。
-   `failed` は、モデルのトレーニングが失敗したことを意味します。 `progress` フィールドは `0` です。詳しくは、[トレーニングの失敗](#failedTraining-language)を参照してください。

ステータスが `available` になるまで、ループを使用して 10 秒間隔でステータスを確認します。 カスタム・モデルのステータスを確認する方法について詳しくは、[カスタム言語モデルのリスト](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language)を参照してください。

### トレーニングの失敗
{: #failedTraining-language}

サービスがカスタム言語モデルの別の要求を処理している場合、トレーニングの開始は失敗します。 例えば、サービスが以下のような場合、状況コード 409 でトレーニング要求の開始が失敗します。

-   OOV 語のリストを生成するためにコーパスまたは文法を処理している
-   同音異字発音を検証または自動生成するためにカスタム単語を処理している
-   別のトレーニング要求を処理している

また、カスタム・モデルが以下のような場合、状況コード 400 でトレーニングの開始が失敗します。

-   カスタム・モデルが作成または最後にトレーニングされた時点以降、モデルに新しい有効なトレーニング・データ (コーパス、文法、または単語) が含まれていない。
-   1 つ以上の無効なコーパス、文法、または単語が含まれている (例えばカスタム単語に無効な発音が含まれている場合など)。

トレーニング要求が状況コード 400 で失敗した場合、このサービスによりカスタム・モデルの状況が `failed` に設定されます。以下のいずれかのアクションを実行してください。

-   カスタマイズ・インターフェースのメソッドを使用して、モデルのリソースを調べ、見つかったエラーをすべて修正します。
    -   無効なコーパスについては、コーパスのテキスト・ファイルを修正し、`POST /v1/customizations/{customization_id}/corpora/{corpus_name}` メソッドの `allow_overwrite` パラメーターを使用して、修正したファイルをモデルに追加できます。詳しくは、[カスタム言語モデルへのコーパスの追加](#addCorpus)を参照してください。
    -   無効な文法については、文法ファイルを修正し、`POST /v1/customizations/{customization_id}/grammars/{grammar_name}` メソッドの `allow_overwrite` パラメーターを使用して、修正したファイルをモデルに追加できます。詳しくは、[カスタム言語モデルへの文法の追加](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar)を参照してください。
    -   無効なカスタム単語については、`POST /v1/customizations/{customization_id}/words` または `PUT /v1/customizations/{customization_id}/words/{word_name}` メソッドを使用して、モデルの単語リソース内でその単語を直接修正できます。詳しくは、[カスタム・モデルの単語の変更](#modifyWord)を参照してください。

カスタム言語モデルでの単語の検証について詳しくは、[単語リソースの検証](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel)を参照してください。
-   トレーニングから無効なリソースを除外するには、`POST /v1/customizations/{customization_id}/train` メソッドの `strict` パラメーターを `false` に設定します。トレーニングが成功するためには、モデルに少なくとも 1 つの有効なリソース (コーパス、文法、または単語) が含まれている必要があります。`strict` パラメーターは、有効なリソースと無効なリソースが混在するカスタム・モデルをトレーニングする際に役立ちます。
