---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

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

# Fazendo uma solicitação de reconhecimento
{: #basic-request}

Para solicitar reconhecimento de voz com o {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}, é necessário fornecer apenas o áudio que deve ser transcrito. O serviço oferece os mesmos recursos de transcrição básica com cada uma de suas interfaces.
{: shortdesc}

As seções a seguir mostram solicitações de transcrição básica para cada uma das interfaces do serviço:

-   Os exemplos apresentam um breve arquivo FLAC denominado <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/speech-to-text/audio-file.flac" download="audio-file.flac">audio-file.flac <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo" title="Ícone de link externo"></a>.
-   Os exemplos usam o modelo de idioma padrão, `en-US_BroadbandModel`.

[Entendendo os resultados do reconhecimento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-response) descreve a resposta do serviço para esses exemplos.

Se você usar um certificado autoassinado, será necessário desativar a verificação de SSL para que uma solicitação para o serviço seja bem-sucedida. Para obter mais informações, consulte [Desativando a verificação de SSL](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests#SSLverification).
{: important}

## Enviando áudio com uma solicitação
{: #basic-request-audio}

O áudio que você transmite para o serviço deve estar em um dos formatos suportados do serviço. Para a maioria dos áudios, o serviço pode detectar automaticamente o formato. Para alguns áudios, deve-se especificar o formato com o `Content-Type` ou parâmetro equivalente. Para obter mais informações, consulte [Formatos de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats). (Para clareza, os exemplos a seguir especificam o formato de áudio com todas as solicitações).

As interfaces do serviço aceitam quantias máximas de áudio diferentes. Deve-se enviar pelo menos 100 bytes de áudio com qualquer solicitação.

-   Com as interfaces do WebSocket e HTTP síncrona, é possível passar um máximo de 100 MB de dados de áudio com uma única solicitação.
-   Com a interface de HTTP assíncrona, é possível passar um máximo de 1 GB de dados de áudio com uma solicitação.

Se você estiver reconhecendo grandes quantidades de áudio, será possível dividir manualmente o áudio em chunks menores. Mas, geralmente, é mais eficiente e conveniente converter o áudio em um formato compactado com perdas. A compactação pode maximizar a quantia de dados que você pode enviar com uma única solicitação. Especialmente se o áudio estiver no formato WAV ou FLAC, convertê-lo para um formato com perdas pode fazer uma diferença significativa.

-   Para obter mais informações sobre os formatos de áudio que usam compactação, consulte [Formatos de áudio suportados](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#formats).
-   Para obter mais informações sobre os efeitos da compactação e sobre como converter seu áudio em um formato que a use, consulte [Limites de dados e compactação](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#limits) e [Conversão de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#conversion).

## Usando a interface do WebSocket
{: #basic-request-websocket}

[A interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) oferece uma implementação eficiente que fornece baixa latência e rendimento alto por meio de uma conexão full duplex. Todas as solicitações e respostas são enviadas por meio da mesma conexão do WebSocket. Por causa de suas vantagens, os WebSockets são o mecanismo preferencial para reconhecimento de voz. Para obter mais informações, consulte [Vantagens da interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-developerOverview#advantages).

Para usar a interface do WebSocket, primeiro use o método `/v1/recognize` para estabelecer uma conexão com o serviço. Especifique parâmetros como o modelo de idioma e qualquer modelo customizado que deve ser usado para solicitações enviadas por meio da conexão. Em seguida, registre os listeners de eventos para manipular respostas do serviço. Para fazer uma solicitação, envie uma mensagem de texto JSON que inclui o formato de áudio e qualquer parâmetro adicional. Passe o áudio como uma mensagem binária (BLOB) e, em seguida, envia uma mensagem de texto para sinalizar o fim do áudio.

O exemplo a seguir fornece o código JavaScript que estabelece uma conexão e envia as mensagens de texto e binárias para uma solicitação de reconhecimento. O exemplo não inclui o código para instalar os manipuladores de eventos.

```javascript
var my_access_token = '{token}';
var wsURI = '{ws_url}/v1/recognize'
  + '?access_token=' + my_access_token;
var websocket = new WebSocket(wsURI);

websocket.send(JSON.stringify({
  action: 'start',
  content-type: 'audio/flac'
}));
websocket.send(blob);
websocket.send(JSON.stringify({'action': 'stop'}));
```
{: codeblock}

## Usando a interface de HTTP síncrona
{: #basic-request-http}

[A interface de HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fornece a maneira mais simples de fazer uma solicitação de reconhecimento. Use o método `POST /v1/recognize` para fazer uma solicitação para o serviço. Passe o áudio e todos os parâmetros com a solicitação única.

O `curl` de exemplo a seguir mostra uma solicitação de reconhecimento básico de HTTP:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @audio-file.flac
"{url}/v1/recognize"
```
{: pre}

## Usando a interface de HTTP assíncrona
{: #basic-request-async}

[A interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fornece uma interface sem bloqueio para transcrição de áudio. É possível usar a interface registrando ou não primeiro uma URL de retorno de chamada com o serviço. Com uma URL de retorno de chamada, o serviço envia notificações de retorno de chamada com status de tarefa e resultados de reconhecimento.

A interface usa assinaturas HMAC-SHA1 com base em um segredo especificado pelo usuário para fornecer autenticação e integridade de dados para suas notificações. Sem uma URL de retorno de chamada, deve-se pesquisar o serviço para obter o status e os resultados da tarefa. Com qualquer abordagem, use o método `POST /v1/recognitions` para fazer uma solicitação de reconhecimento.

O `curl` de exemplo a seguir mostra uma solicitação de reconhecimento de HTTP assíncrona simples. A solicitação não inclui uma URL de retorno de chamada, portanto, deve-se pesquisar o serviço para obter o status da tarefa e a transcrição resultante.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/flac"
--data-binary @audio-file.flac
"{url}/v1/recognitions"
```
{: pre}
