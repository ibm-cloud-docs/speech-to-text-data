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

# Nota sobre a Liberação
{: #release-notes}

As versões a seguir do {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} estão disponíveis. As informações incluem novos recursos e mudanças para cada versão do produto e quaisquer limitações conhecidas.
{: shortdesc}

## Limitações Conhecidas
{: #limitations}

O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} não tem limitações conhecidas.

## Versão 1.0.0 (junho de 2019)
{: #v100}

A liberação inicial do serviço. O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} baseia-se no serviço {{site.data.keyword.speechtotextfull}} no {{site.data.keyword.cloud_notm}} público. Para obter mais informações sobre o serviço público, consulte [Sobre o {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.

O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} difere do serviço público do {{site.data.keyword.speechtotextshort}} das maneiras a seguir. Essas informações poderão ser úteis caso você já esteja familiarizado com o serviço {{site.data.keyword.speechtotextshort}} no {{site.data.keyword.cloud_notm}} público.

-   O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} usa tokens de acesso para autenticação. Para obter mais informações, consulte [Fazendo solicitações para o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) e a [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   Os terminais para o {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} são específicos para o cluster do {{site.data.keyword.icp4dfull_notm}}. Para obter mais informações, consulte [Fazendo solicitações para o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) e a [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} não executa nenhuma criação de log de solicitação. Não é necessário usar o cabeçalho da solicitação `X-Watson-Learning-Opt-Out`.
-   O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} não suporta tokens do Watson. Não é possível usar o cabeçalho da solicitação `X-Watson-Authorization-Token` para se autenticar no serviço.
