---

Copyright:
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

# 製品について
{: #about}

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} は、ユーザーのアプリケーションで使用できる音声認識機能を提供します。このサービスは機械学習を活用して、文法、言語構造、および音声シグナルの構成に関する知識を組み合わせることで、人間の音声を正確に書き起こします。このサービスは繰り返し更新されて、受け取る音声データが増えるほど書き起こし機能が向上します。
{: shortdesc}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} は各種のインターフェースを提供しているため、音声を入力して書き起こしテキストを出力するどのような用途にも対応できます。例えば、次のような用途に使用できます。

-   アプリケーション、埋め込みデバイス、および車両装備品の音声制御
-   会議や電話会議の書き起こし
-   E メール・メッセージやメモの口述筆記

このサービスは、コールセンターの音声から高品質の音声書き起こしを抽出する必要があるお客様に理想的なサービスです。金融サービス、医療、保険、通信などの業界のお客様は、カスタマー・ケア、カスタマー・ボイス、エージェント・アシスタンス、その他のソリューション用のクラウド・ネイティブ・アプリケーションを開発できます。

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} のインストールおよび構成について詳しくは、[サービスのインストール](/docs/services/speech-to-text-data?topic=speech-to-text-data-install)を参照してください。

{{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} は、パブリック {{site.data.keyword.speechtotextfull}} 上の {{site.data.keyword.cloud_notm}} サービスに基づいています。パブリック・サービスについて詳しくは、[{{site.data.keyword.speechtotextshort}} について](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external} を参照してください。
{: note}

## サポートされているインターフェース
{: #interfaces}

{{site.data.keyword.speechtotextshort}} サービスでは、音声認識用に以下の複数のインターフェースが提供されています。

-   [WebSocket インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets)では、永続的な低遅延の全二重接続をサービスとの間で確立できます。単一の要求で最大 100 MB の音声データをサービスに渡すことができます。
-   [同期 HTTP インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-http)では、サービスに対して基本的な HTTP 呼び出しを発行できます。 単一の要求で最大 100 MB の音声データを渡すことができます。
-   [非同期 HTTP インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-async)では、サービスに対して非ブロッキング呼び出しを発行できます。 単一の要求で最大 1 GB の音声データを渡すことができます。

このサービスでさらに提供されている[カスタマイズ・インターフェース](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization)を使用して、対象の言語や音響上の要件に合わせて音声認識を調整できます。 分野固有の用語を追加してモデルの語彙を拡張することも、モデルをカスタマイズして対象の音声の音響特性に適合させることもできます。 [文法](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars)を追加することで、サービスで認識できる句を制限することもできます。

-   各 {{site.data.keyword.speechtotextshort}}インターフェースを使用して要求を行う方法については、[サービスに対する要求を行う](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests)を参照してください。
-   サービスの各インターフェースで使用する基本的な音声認識要求の例については、[認識要求の実行](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request)を参照してください。
-   サービスを使用したアプリケーション開発の概要については、[開発者向けの概要](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview)を参照してください。

サービスの使用を簡素化するための SDK が多くのプログラミング言語用に提供されています。 詳しくは、[API リファレンス](https://{DomainName}/apidocs/speech-to-text-data){: external}を参照してください。

## 入力機能
{: #inputFeatures}

サービスの各インターフェースでは、音声をテキストに書き起こすための多数の共通の入力機能が共有されています。

-   [音声フォーマット](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats) - 書き起こし可能な対象は、Opus または Vorbis コーデックを使用した Ogg または Web Media (WebM) 音声、MP3 (または MPEG)、Waveform Audio File Format (WAV)、Free Lossless Audio Codec (FLAC)、線形 16 ビット・パルス符号変調 (PCM)、G.729、A-law、mu-law (または u-law)、および基本的な音声です。圧縮をサポートしているフォーマットを使用することで、単一の要求で送信できる音声データの量を最大化できます。
-   [言語とモデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-models) - 広帯域モデルまたは狭帯域モデルを使用して音声を書き起こすことができます。 最低サンプリング・レートが 16 kHz である音声には広帯域モデルを使用してください。 最低サンプリング・レートが 8 kHz である音声には狭帯域モデルを使用してください。
-   [音声の伝送](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission) - データ・チャンクの連続ストリームとして音声を渡すことも、1 回限りの送信としてすべての音声データを同時に渡すこともできます。 ストリーミングの場合は、非アクティブとセッションの[タイムアウト](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts)が適用されます。

## 出力機能
{: #outputFeatures}

ほとんどのインターフェースでは、以下の共通の出力機能もサポートされています。

-   [話者ラベル](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels)によって、米国英語、日本語、またはスペイン語の音声で個別の話者が識別されます。書き起こし結果では、複数の人物が参加している会話における各話者の発言がラベル付けされます (ベータ機能)。
-   [キーワード検出](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting)では、ユーザー定義の信頼度レベルに基づいて、指定されたキーワード・ストリングに一致する発話句が識別されます。 キーワード検出が特に役に立つのは、書き起こし内容全体よりも音声に含まれる個別の句の方が重要な場合です。 例えば、お客様サポート・システムでは、識別されたキーワードに基づいてユーザーの要望の転送先を決定できます。
-   [中間結果](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim)では、書き起こしの進行に伴って継続的に洗練される仮説が返されます。書き起こしが完了した時点で、最終結果が返されます。中間結果を提供できるのは、WebSocket インターフェースのみです。
-   [最大候補数](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives)では、可能性のある書き起こし候補が返されます。 サービスでは、信頼度が最も高い最終結果が提示されます。
-   [単語候補](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives)では、書き起こし結果に含まれる単語に音響的に類似している単語候補が提示されます。
-   [単語の信頼度](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence)では、書き起こし結果に含まれる各単語の信頼度レベルが返されます。
-   [単語のタイム・スタンプ](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps)では、書き起こし結果に含まれる各単語の開始と終了のタイム・スタンプが返されます
-   [スマート・フォーマット設定](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting)では、日付、時刻、数値、金額、電話番号、およびインターネット・アドレスが、読みやすい標準的形式に変換されて、最終書き起こし結果に出力されます。 米国英語の場合は、最終書き起こし結果で特定の句読点記号を追加するキーワード句を指定することもできます。 スマート・フォーマット設定がサポートされているのは、米国英語、日本語、およびスペイン語の音声です (ベータ機能)。
-   [数値編集](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction)では、最終書き起こし結果で数値データを編集 (伏せ字) します。 編集機能の目的は、クレジット・カード番号などの機密性の高い個人情報を書き起こし結果から削除することです。 この機能がサポートされているのは、米国英語、日本語、および韓国語の音声です (ベータ機能)。
-   [禁止用語フィルター](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter)では、米国英語の書き起こし結果に含まれる禁止用語が検閲されます。
-   [処理メトリック](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics)は、このサービスによる入力音声分析に関する詳細なタイミング情報を提供します。
-   [音声メトリック](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics)は、入力音声の信号特性に関する詳細情報を提供します。

## 言語サポート
{: #languages}

このサービスで提供されるモデルでサポートされている言語は、ブラジル・ポルトガル語、フランス語、ドイツ語、日本語、韓国語、北京語、現代標準アラビア語、スペイン語、英国英語、および米国英語です。 サービスは、すべての言語ですべての機能をサポートしているわけではありません。 さらにサービスは、一部の機能を一般出荷可能 (GA) として実動使用向けにサポートしている一方で、他の機能をベータ版としてさまざまな言語向けにサポートしています。

-   WebSocket インターフェースおよび同期と非同期の HTTP インターフェースは、すべての言語で一般出荷可能です。
-   すべての言語で、サービスには広帯域モデルと狭帯域モデルの両方が用意されています。詳しくは、[言語とモデル](/docs/services/speech-to-text-data?topic=speech-to-text-data-models)を参照してください。
-   一部の音声認識機能は、特定の言語のみ、および特定のインターフェースのみで使用できます。詳しくは、[パラメーターの要約](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary)を参照してください。
-   言語モデル・カスタマイズ・インターフェースは、すべての言語で一般出荷可能です。音響モデル・カスタマイズ・インターフェースは、すべての言語でベータ機能として使用できます。 詳しくは、[各言語でのカスタマイズのサポート](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport)を参照してください。

## サービスの試用
{: #tryOut}

{{site.data.keyword.speechtotextshort}} サービスの実際の動作の例については、以下を参照してください。

-   [クイック・デモ](https://speech-to-text-demo.ng.bluemix.net/){: external}では、ストリーミング入力された音声またはアップロード・ファイルに含まれる音声をテキストに書き起こすことができます。
-   {{site.data.keyword.ibmwatson}}[Starter Kit](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} に含まれるアプリケーションによって、サービスの使用法が示されます。
-   {{site.data.keyword.watson}} ブログ投稿 [Getting robots to listen: Using {{site.data.keyword.watson}}'s {{site.data.keyword.speechtotextshort}} service](https://www.ibm.com/blogs/watson/2016/07/getting-robots-listen-using-watsons-speech-text-service/){: external} では、サービスの WebSocket インターフェースを Python と組み合わせて使用して、音声から発話を抽出する方法を説明しています。 この投稿は、必要なコードと手順を紹介する詳細なチュートリアルになっています。
