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

# Sobre
{: #about}

O {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} fornece recursos de reconhecimento de voz para seus aplicativos. O serviço aproveita o aprendizado de máquina para combinar o conhecimento da gramática, a estrutura do idioma e a composição de sinais de áudio e voz para transcrever com precisão a voz humana. Ele atualiza continuamente e refina sua transcrição à medida que recebe mais fala.
{: shortdesc}

O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} fornece várias interfaces que fazem com que ele seja adequado para qualquer aplicativo em que a fala é a entrada e uma transcrição textual é a saída. Exemplos de aplicativos incluem

-   Controle de voz de aplicativos, dispositivos integrados e acessórios de veículo
-   Transcrições de reuniões e conferências telefônicas
-   Ditado de notas e mensagens de e-mail

O serviço é ideal para clientes que precisam extrair transcrições de fala de alta qualidade do áudio da central de atendimento. Clientes em segmentos de mercado como serviços financeiros, assistência médica, seguro e telecomunicações podem desenvolver aplicativos nativos em nuvem para atendimento ao cliente, voz do cliente, assistência do agente e outras soluções.

Para obter informações sobre como instalar e configurar o {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}}, consulte [Instalando o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-install).

O {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} baseia-se no serviço {{site.data.keyword.speechtotextfull}} no {{site.data.keyword.cloud_notm}} público. Para obter mais informações sobre o serviço público, consulte [Sobre o {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.
{: note}

## Interfaces Suportadas
{: #interfaces}

O serviço {{site.data.keyword.speechtotextshort}} oferece múltiplas interfaces para reconhecimento de voz:

-   Uma [interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) para estabelecer conexões persistentes, full duplex e de baixa latência com o serviço. É possível passar um máximo de 100 MB de dados de áudio para o serviço com uma única solicitação.
-   Uma [interface de HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) para chamadas HTTP básicas para o serviço. É possível passar um máximo de 100 MB de dados de áudio com uma solicitação.
-   Uma [interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) para chamadas sem bloqueio para o serviço. É possível passar o máximo de 1 GB de dados de áudio com uma solicitação.

O serviço também fornece uma [interface de customização](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) que você pode usar para ajustar o reconhecimento de voz para seu idioma e requisitos acústicos. É possível expandir o vocabulário de um modelo com a terminologia específica do domínio ou adaptar um modelo para as características acústicas de seu áudio. Também é possível incluir [gramáticas](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) para restringir as frases que o serviço pode reconhecer.

-   Para obter informações sobre como fazer solicitações com cada uma das interfaces do {{site.data.keyword.speechtotextshort}}, consulte [Fazendo solicitações para o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Para obter exemplos de solicitações de reconhecimento de voz básica com cada uma das interfaces do serviço, consulte [Fazendo uma solicitação de reconhecimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Para obter uma descrição de alto nível do desenvolvimento do aplicativo com o serviço, consulte [Visão geral para desenvolvedores](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview).

Os SDKs estão disponíveis em muitas linguagens de programação para simplificar seu uso do serviço. Para obter mais informações, consulte a [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Recursos de entrada
{: #inputFeatures}

As interfaces do serviço compartilham muitos recursos de entrada comuns para transcrever a voz para texto:

-   [Formatos de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats) - É possível transcrever o áudio Ogg ou Web Media (WebM) com o codec Opus ou Vorbis, MP3 (ou MPEG), Waveform Audio File Format (WAV), Free Lossless Audio Codec (FLAC), Pulse-Code Modulation (PCM) linear de 16 bits, G.729, A-law, mu-law (ou u-law) e áudio básico. Usando um formato que suporta compactação, é possível maximizar a quantia de dados de áudio que podem ser enviados com uma solicitação.
-   [Idiomas e modelos](/docs/services/speech-to-text-data?topic=speech-to-text-data-models) - É possível transcrever o áudio usando modelos de banda larga ou de banda estreita. Use a banda larga para áudio amostrado a uma taxa mínima de 16 kHz. Use uma banda estreita para áudio amostrado em uma taxa mínima de 8 kHz.
-   [Transmissão de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission) - É possível passar áudio como um fluxo contínuo de chunks de dados ou como uma entrega única que passa todos os dados de uma vez. Com o fluxo, o serviço força a inatividade e os [tempos limites de sessão](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts)da sessão.

## Recursos de saída
{: #outputFeatures}

A maioria das interfaces também suporta os recursos de saída comuns a seguir:

-   Os [Rótulos do falante](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels) reconhecem diferentes falantes do áudio em inglês dos EUA, japonês ou espanhol. A transcrição rotula as contribuições de cada falante em uma conversa com múltiplos participantes. (Funcionalidade beta.)
-   [Marcação de palavra-chave](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting) identifica frases faladas que correspondem às sequências de palavras-chave especificadas com um nível de confiança definido pelo usuário. A marcação de palavra-chave é especialmente útil quando frases individuais do áudio são mais importantes do que a transcrição completa. Por exemplo, um sistema de suporte ao cliente pode identificar palavras-chave para determinar como rotear as solicitações do usuário.
-   Os [resultados provisórios](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim) retornam hipóteses continuamente refinadas à medida que a transcrição progride. O serviço retorna os resultados finais quando a transcrição é concluída. Os resultados provisórios estão disponíveis somente com a interface do WebSocket.
-   [Alternativas máximas](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives) fornecem possíveis transcrições alternativas. O serviço indica os resultados finais nos quais ele tem a maior confiança.
-   [Alternativas de palavra](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives) solicitam palavras alternativas que são acusticamente semelhantes às palavras de uma transcrição.
-   [Confiança de palavra](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence) retorna os níveis de confiança para cada palavra de uma transcrição.
-   [Registros de data e hora da palavra](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps) retornam registros de data e hora para o início e o término de cada palavra de uma transcrição.
-   [Formatação inteligente](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting) converte datas, horas, números, valores de moeda, números de telefone e endereços da Internet em formulários mais legíveis e convencionais nas transcrições finais. Para inglês dos EUA, também é possível fornecer frases de palavra-chave para incluir determinados símbolos de pontuação em transcrições finais. A formatação inteligente é suportada para áudio em inglês dos EUA, japonês e espanhol. (Funcionalidade beta.)
-   [A edição de dados numéricos](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction) edita, ou mascara, dados numéricos de uma transcrição final. A edição de dados destina-se a remover das transcrições as informações pessoais sensíveis, como números de cartão de crédito. O recurso é suportado para áudio em inglês dos EUA, japonês e coreano. (Funcionalidade beta.)
-   [Filtragem de profanidade](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter) censura a profanidade da transcrições em inglês dos EUA.
-   As [Métricas de processamento](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) fornecem informações de sincronização detalhadas sobre a análise do áudio de entrada do serviço.
-   As [Métricas de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) fornecem informações detalhadas sobre as características de sinal do áudio de entrada.

## Suporte ao idioma
{: #languages}

O serviço oferece modelos para os seguintes idiomas: português do Brasil, francês, alemão, japonês, coreano, chinês mandarim, árabe padrão moderno, espanhol, inglês do Reino Unido e inglês dos EUA. O serviço não suporta todos os recursos para todos os idiomas. Além disso, ele suporta alguns recursos como geralmente disponíveis (GA) para uso de produção e outros como ofertas beta para diferentes idiomas.

-   As interfaces do WebSocket e de HTTP síncrona e assíncrona estão em disponibilidade geral para todos os idiomas.
-   O serviço oferece modelos de banda larga e modelos de banda estreita para todos os idiomas. Para obter mais informações, consulte [Idiomas e modelos](/docs/services/speech-to-text-data?topic=speech-to-text-data-models).
-   Alguns recursos de reconhecimento de voz estão disponíveis apenas para alguns idiomas e apenas com algumas interfaces. Para obter mais informações, consulte o [Resumo de parâmetro](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   A interface de customização do modelo de idioma está em disponibilidade geral para todos os idiomas. A interface de customização do modelo acústico está disponível como funcionalidade beta para todos os idiomas. Para obter mais informações, consulte [Suporte ao idioma para customização](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).

## Experimente o serviço
{: #tryOut}

Para obter exemplos do serviço {{site.data.keyword.speechtotextshort}} em ação, consulte

-   Uma [demo rápida](https://speech-to-text-demo.ng.bluemix.net/){: external} que transcreve texto da entrada de áudio do fluxo ou de um arquivo que você transferiu por upload.
-   Os aplicativos no {{site.data.keyword.ibmwatson}}[Kits do iniciador](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} que demonstram o serviço.
-   A postagem do blog do {{site.data.keyword.watson}} [Fazendo robôs atenderem: usando o serviço {{site.data.keyword.speechtotextshort}} do {{site.data.keyword.watson}}](https://www.ibm.com/blogs/watson/2016/07/getting-robots-listen-using-watsons-speech-text-service/){: external} que mostra como usar a interface WebSocket do serviço com Python para extrair a fala do áudio. O post fornece um tutorial completo que demonstra o código e as etapas envolvidos.
