---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

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

# リリース・ノート
{: #release-notes}

以下のバージョンの {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} を使用できます。情報には、製品の各バージョンの新機能と変更点、および既知の制限が含まれます。
{: shortdesc}

## 既知の制限事項
{: #limitations}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} には既知の制限はありません。

## バージョン 1.0.0 (2019 年 6 月)
{: #v100}

サービスの初期リリース。{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} は、パブリック {{site.data.keyword.speechtotextfull}} 上の {{site.data.keyword.cloud_notm}} サービスに基づいています。パブリック・サービスについて詳しくは、[{{site.data.keyword.speechtotextshort}} について](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external} を参照してください。


{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} は、以下の点でパブリック {{site.data.keyword.speechtotextshort}} サービスとは異なります。パブリック {{site.data.keyword.cloud_notm}} 上の {{site.data.keyword.speechtotextshort}} サービスを既によく知っている場合、この情報が役立つことがあります。

-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} は認証のためにアクセス・トークンを使用します。詳しくは、[サービスに対する要求を行う](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests)および [API リファレンス](https://{DomainName}/apidocs/speech-to-text-data){: external}を参照してください。
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} のエンドポイントは、使用する {{site.data.keyword.icp4dfull_notm}} クラスターに固有のものです。詳しくは、[サービスに対する要求を行う](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests)および [API リファレンス](https://{DomainName}/apidocs/speech-to-text-data){: external}を参照してください。
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} は、要求ロギングを実行しません。`X-Watson-Learning-Opt-Out` 要求ヘッダーを使用する必要はありません。
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} は Watson トークンをサポートしていません。`X-Watson-Authorization-Token` 要求ヘッダーを使用してサービスで認証することはできません。
