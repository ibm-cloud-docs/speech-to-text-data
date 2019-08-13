---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-26"

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

# Visão geral para desenvolvedores
{: #developerOverview}

É possível acessar os recursos do {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} usando uma interface do WebSocket e usando interfaces Representational State Transfer (REST) de HTTP síncronas ou assíncronas. Também é possível customizar os modelos de idioma do serviço para se adequarem ao seu domínio e ambiente. Os SDKs estão disponíveis para simplificar o desenvolvimento de aplicativos em várias linguagens de programação.
{: shortdesc}

Você pode se autenticar no serviço {{site.data.keyword.speechtotextshort}} transmitindo um token de acesso com cada solicitação. O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} é uma solução de nuvem com diversos locatários. Suas credenciais fornecem acesso somente aos seus dados e seus dados são isolados de outros usuários.


## Programando com o serviço
{: #programming}

[Fazendo uma solicitação de reconhecimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request) mostra como solicitar transcrição básica com cada uma das interfaces de programação do serviço:

-   [A interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) oferece uma implementação eficiente, de baixa latência e de alto rendimento por meio de uma conexão full duplex.
-   [A interface de HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fornece uma interface básica para transcrever áudio com solicitações de bloqueio.
-   [A interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fornece uma interface sem bloqueio que permite registrar uma URL de retorno de chamada para receber notificações ou para pesquisar o status e os resultados da tarefa.

As interfaces fornecem recursos de reconhecimento de voz semelhantes, mas é possível especificar o mesmo parâmetro que um cabeçalho de solicitação, um parâmetro de consulta ou um parâmetro de um objeto JSON, dependendo da interface usada.

As interfaces do WebSocket e de HTTP síncrona aceitam um máximo de 100 MB de dados de áudio com uma única solicitação. A interface de HTTP assíncrona aceita um máximo de 1 GB de dados de áudio com uma solicitação.

-   Para obter informações sobre como fazer solicitações com cada uma das interfaces do {{site.data.keyword.speechtotextshort}}, consulte [Fazendo solicitações para o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Para obter exemplos de solicitações de reconhecimento de voz básica com cada uma das interfaces do serviço, consulte [Fazendo uma solicitação de reconhecimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Para obter descrições de todos os parâmetros de reconhecimento de voz disponíveis, consulte o [Resumo de parâmetro](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   Para obter descrições de todos os métodos e seus parâmetros, juntamente com exemplos, consulte a [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Vantagens da interface do WebSocket
{: #advantages}

A interface do WebSocket tem várias vantagens sobre a interface de HTTP:

-   A interface do WebSocket fornece um canal de comunicação single socket, full duplex. A interface permite que o cliente envie solicitações e áudio para o serviço e receba resultados por meio de uma única conexão em um modo assíncrono.
-   Ela fornece uma experiência de programação muito mais simples e mais poderosa. O serviço envia respostas acionadas por evento para as mensagens do cliente, eliminando a necessidade de o cliente pesquisar o servidor.
-   Ela permite estabelecer e usar uma única conexão autenticada indefinidamente. As interfaces HTTP requerem que você autentique cada chamada para o serviço.
-   Isso reduz a latência. Os resultados do reconhecimento chegam mais rapidamente porque o serviço os envia diretamente para o cliente. A interface de HTTP requer quatro solicitações e conexões distintas para alcançar os mesmos resultados.
-   Reduz a utilização da rede. O protocolo WebSocket é leve. Ele requer apenas uma única conexão para executar reconhecimento de voz em tempo real.
-   Ele ativa o áudio a ser transmitido diretamente dos navegadores (clientes HTML5 WebSocket) para o serviço.

## Customizando o serviço
{: #customizing}

[A interface de customização](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) permite que você crie modelos customizados para melhorar os recursos de reconhecimento de voz do serviço:

-   [Modelos de idioma customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate) permitem definir palavras específicas do domínio para um modelo base. Os modelos de idioma customizados expandem o vocabulário base do serviço com a terminologia específica para domínios como medicina e direito.
-   Os [modelos acústicos customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic) permitem que você adapte um modelo base para as características acústicas de seu ambiente e dos falantes. Os modelos acústicos customizados melhoram a capacidade do serviço de reconhecer a fala para características acústicas específicas.
-   As [gramáticas](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) permitem que você restrinja as frases que o serviço pode reconhecer para aquelas definidas nas regras da gramática. Ao limitar o espaço de procura para sequências válidas, o serviço pode entregar resultados mais rapidamente e com mais precisão. Gramáticas são suportadas com modelos de idioma customizados.

É possível usar um modelo de idioma customizado, um modelo acústico customizado, ou ambos, para o reconhecimento de voz com qualquer uma das interfaces do serviço.

## Obtendo métricas
{: #overview-metrics}

O serviço oferece dois tipos de métricas opcionais para solicitações de reconhecimento de voz:

-   As [Métricas de processamento](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) fornecem informações de sincronização detalhadas sobre a análise do áudio de entrada do serviço. O serviço retorna as métricas em intervalos especificados e com eventos de transcrição, tais como resultados temporários e finais. É possível usar as métricas para calibrar o progresso do serviço na transcrição do áudio.
-   As [Métricas de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) fornecem informações detalhadas sobre as características de sinal do áudio de entrada. Os resultados fornecem métricas agregadas para o áudio de entrada inteiro na conclusão do processamento da fala. É possível usar as métricas para determinar as características e a qualidade do áudio.

É possível solicitar métricas de processamento com o WebSocket e as interfaces HTTP assíncronas. É possível solicitar métricas de áudio com qualquer uma das interfaces do serviço. Por padrão, o serviço não retorna nenhuma métrica.

## Suporte ao CORS
{: #cors}

O serviço suporta o Cross-Origin Resource Sharing (CORS). Usando o CORS, as páginas da web podem solicitar recursos diretamente de um domínio externo. O CORS evita a política de segurança da mesma origem, que, de outra maneira, impede essas solicitações. Como o serviço suporta CORS, uma página da web pode se comunicar diretamente com o serviço sem passar a solicitação por meio do servidor da web que hospeda a página.

Por exemplo, uma página da web que é carregada por meio de um servidor no {{site.data.keyword.cloud}} pode chamar a API de customização diretamente, ignorando o servidor {{site.data.keyword.cloud_notm}}. Para obter mais informações, consulte [enable-cors.org](https://enable-cors.org/){: external}.

## Usando kits de desenvolvimento de software
{: #sdks}

Os SDKs estão disponíveis para o serviço {{site.data.keyword.speechtotextshort}} para simplificar o desenvolvimento de aplicativos de fala. Os SDKs do {{site.data.keyword.ibmwatson}} estão disponíveis para muitas linguagens de programação e plataformas populares.

-   Para obter uma lista completa de SDKs e links para os SDKs no GitHub, consulte [Usando SDKs](/docs/services/watson?topic=watson-using-sdks).
-   Para obter informações detalhadas sobre todos os métodos dos SDKs do Node, do Java&trade;, do Python, do Ruby e do Go do serviço {{site.data.keyword.speechtotextshort}}, consulte a [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
