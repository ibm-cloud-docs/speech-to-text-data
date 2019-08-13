---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# A interface do WebSocket
{: #websockets}

A interface do WebSocket do {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} é a maneira mais natural para um cliente interagir com o serviço. Para usar a interface do WebSocket para reconhecimento de voz, use primeiro o método `/v1/recognize` para estabelecer uma conexão persistente com o serviço. Em seguida, envie mensagens de texto e binárias por meio da conexão para iniciar e gerenciar as solicitações de reconhecimento.
{: shortdesc}

A solicitação de reconhecimento e o ciclo de resposta têm as etapas a seguir:

1.  [Abrir uma conexão](#WSopen)
1.  [Iniciar uma solicitação de reconhecimento](#WSstart)
1.  [Enviar áudio e receber os resultados do reconhecimento](#WSaudio)
1.  [Terminar uma solicitação de reconhecimento](#WSstop)
1.  [Enviar solicitações adicionais e modificar parâmetros de solicitação](#WSmore)
1.  [Manter uma conexão ativa](#WSkeep)
1.  [Fechar uma conexão](#WSclose)

Quando o cliente envia dados para o serviço, ele *deve* transmitir todas as mensagens JSON como mensagens de texto e todos os dados de áudio como mensagens binárias.

Os fragmentos de código de exemplo a seguir são gravados em JavaScript e são baseados na API do HTML5 WebSocket. Para obter mais informações sobre o protocolo WebSocket, consulte o Internet Engineering Task Force (IETF) [Solicitação de comentários (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
{: note}

## Abrir uma conexão
{: #WSopen}

O {{site.data.keyword.speechtotextshort}} usa o protocolo WebSocket Secure (WSS) para disponibilizar o método `/v1/recognize` no terminal a seguir. Para obter mais informações sobre os componentes da URL, consulte [Fazendo solicitações para o serviço](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).

```
wss://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/recognize
```
{: codeblock}

Os exemplos na documentação referem-se a esse terminal como `{ws_url}`.
{: note}

Um cliente WebSocket chama esse método com os parâmetros de consulta a seguir para estabelecer uma conexão autenticada com o serviço.

<table>
  <caption>Tabela 1. Parâmetros do método <code>/v1/recognize</code></caption>
  <tr>
    <th style="width:23%; text-align:left">Parâmetros</th>
    <th style="width:12%; text-align:center">Tipo de Dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>      Necessárias
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Passe um token de acesso válido para estabelecer uma conexão autenticada
      com o serviço. Deve-se estabelecer a conexão antes que o token de acesso expire.<br/><br/>
      Você passa um token de acesso apenas para estabelecer uma conexão autenticada.
      Depois de estabelecer uma conexão, é possível mantê-la ativa indefinidamente.
      Você permanece autenticado pelo tempo que mantém a conexão aberta.
      Não é necessário atualizar o token de acesso para uma conexão ativa que dure além do prazo de expiração do token. Uma conexão pode permanecer
      ativa mesmo após a exclusão do token.
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>modelo</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Especifica o modelo de idioma a ser usado para transcrição.
      Se você não especificar um modelo, o serviço usará o modelo <code>en-US_BroadbandModel</code> por padrão. Para obter mais informações, consulte [Idiomas e modelos](/docs/services/speech-to-text-data?topic=speech-to-text-data-models).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>language_customization_id</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Especifica o Identificador Exclusivo Global (GUID) de um modelo de idioma customizado que deve ser usado para todas as solicitações que são enviadas por meio da conexão. O modelo base do modelo de idioma customizado deve corresponder ao valor do parâmetro <code>model</code>. Se você incluir um ID de customização, deverá fazer a solicitação com credenciais para a instância do serviço que tem o modelo customizado. Por padrão, nenhum modelo de idioma customizado é usado. Para obter mais informações, consulte [A interface de customização](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>acoustic_customization_id</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Especifica o Identificador Exclusivo Global (GUID) de um modelo acústico customizado que deve ser usado para todas as solicitações que são enviadas por meio da conexão. O modelo base do modelo acústico customizado deve corresponder ao valor do parâmetro <code>model</code>. Se você incluir um ID de customização, deverá fazer a solicitação com credenciais para a instância do serviço que tem o modelo customizado. Por padrão, nenhum modelo acústico customizado é usado. Para obter mais informações, consulte [A interface de customização](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>base_model_version</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Especifica a versão do `model` base que deve ser usada para todas as solicitações que são enviadas por meio da conexão. O parâmetro é destinado principalmente para o uso com modelos customizados que passaram por upgrade para um novo modelo base. O valor padrão depende de o parâmetro ser usado com ou sem um modelo customizado. Para obter mais informações, consulte [Versão do modelo base](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#version).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Associa um ID do cliente a todos os dados que são passados por meio da conexão. O parâmetro aceita o argumento <code>customer_id={id}</code>, em que <code>id</code> é uma sequência aleatória ou genérica que deve ser associada aos dados. Deve-se codificar a URL do argumento para o parâmetro, por exemplo, `customer_id%3dmy_customer_ID`. Por padrão, nenhum ID do cliente está associado aos dados. Para obter mais informações, consulte [Segurança de informações](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security).
    </td>
  </tr>
</table>

O fragmento do código JavaScript a seguir abre uma conexão com o serviço. A chamada para o método `/v1/recognize` passa os parâmetros de consulta `access_token` e `model`. O último para direcionar o serviço para usar o modelo de banda larga de espanhol. Após estabelecer a conexão, o cliente define os listeners de eventos (`onOpen`, `onClose` e assim por diante) para responder a eventos do serviço. O cliente pode usar a conexão para múltiplas solicitações de reconhecimento.

```javascript
var my_access_token = '{token}';
var wsURI = '{ws_url}/v1/recognize'
  + '?access_token=' + my_access_token
  + '&model=es-ES_BroadbandModel';
var websocket = new WebSocket(wsURI);

websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

O cliente pode abrir múltiplas conexões simultâneas do WebSocket com o serviço. O número de conexões simultâneas é limitado apenas pela capacidade do serviço, que geralmente não apresenta problemas para os usuários.

## Iniciar uma solicitação de reconhecimento
{: #WSstart}

Para iniciar uma solicitação de reconhecimento, o cliente envia uma mensagem de texto JSON para o serviço por meio da conexão estabelecida. O cliente deve enviar essa mensagem antes de enviar qualquer áudio para transcrição. A mensagem deve incluir o parâmetro `action`, mas geralmente pode omitir o parâmetro `content-type`.

<table>
  <caption>Tabela 2. Parâmetros da mensagem de texto do JSON</caption>
  <tr>
    <th style="width:23%; text-align:left">Parâmetros</th>
    <th style="width:12%; text-align:center">Tipo de Dados</th>
    <th style="text-align:left">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>ação</code><br/><em>      Necessárias
    </em></td>
    <td style="text-align:center">Sequência de caracteres</td>
    <td style="text-align:left">
      Especifica a ação a ser executada:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <code>start</code> inicia uma solicitação de reconhecimento ou especifica novos parâmetros para solicitações subsequentes. Para obter mais informações, consulte [Enviar solicitações adicionais e modificar parâmetros de solicitação](#WSmore).
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>stop</code> sinaliza que todo o áudio para uma solicitação foi enviado. Para obter mais informações, consulte [Encerrar uma solicitação de reconhecimento](#WSstop).
        </li>
      </ul>
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>content-type</code><br/><em>      Opcional
    </em></td>
    <td style="text-align:center">Seqüência de caracteres</td>
    <td style="text-align:left">
      Identifica o formato (tipo MIME) dos dados de áudio para a solicitação.
      O parâmetro é necessário para os formatos `audio/alaw`, `audio/basic`, `audio/l16` e `audio/mulaw`. Para obter mais informações, consulte [Formatos de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).
    </td>
  </tr>
</table>

A mensagem também pode incluir parâmetros opcionais para especificar outros aspectos de como a solicitação deve ser processada e as informações que devem ser retornadas. Para obter informações sobre todos os recursos de entrada e saída, consulte o [Resumo de parâmetro](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary). É possível especificar um modelo de idioma, um modelo de idioma customizado e um modelo acústico customizado apenas como parâmetros de consulta da URL do WebSocket.

O fragmento do código JavaScript a seguir envia parâmetros de inicialização para a solicitação de reconhecimento por meio da conexão WebSocket. As chamadas são incluídas na função `onOpen` do cliente para assegurar que elas sejam enviadas somente depois que a conexão for estabelecida.

```javascript
function onOpen(evt) {
  var message = {
    action: 'start',
    content-type: 'audio/l16;rate=22050'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Se ele receber a solicitação com êxito, o serviço retornará a mensagem de texto a seguir para indicar que ele está `listening`:

```javascript
{'state': 'listening'}
```
{: codeblock}

O estado `listening` indica que a instância de serviço está configurada (sua mensagem `start` do JSON era válida) e está pronta para processar uma nova elocução para uma solicitação de reconhecimento. Quando ele começa a atender, o serviço processa qualquer áudio que foi enviado antes da mensagem `listening`.

Se o cliente especificar um parâmetro de consulta ou um campo JSON inválido para a solicitação de reconhecimento, a resposta JSON do serviço incluirá um campo `warnings`. O campo descreve cada argumento inválido. A solicitação é bem-sucedida, apesar dos avisos.

## Enviar áudio e receber os resultados do reconhecimento
{: #WSaudio}

Depois que a mensagem inicial `start` é enviada, o cliente pode começar a enviar dados de áudio para o serviço. O cliente não precisa esperar que o serviço responda à mensagem `start` com a mensagem `listening`. O serviço retorna os resultados da transcrição assincronamente no mesmo formato que ele retorna os resultados para as interfaces de HTTP.

O cliente deve enviar o áudio como dados binários. O cliente pode enviar um máximo de 100 MB de dados de áudio com uma única elocução (por solicitação de `send`). Ele deve enviar pelo menos 100 bytes de áudio para qualquer solicitação. O cliente pode enviar múltiplas elocuções por meio de uma única conexão WebSocket. Para obter informações sobre como usar a compactação para maximizar a quantia de áudio que você pode passar para o serviço com uma solicitação, consulte [Formatos de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).

A interface do WebSocket impõe um tamanho máximo do quadro de 4 MB. O cliente pode configurar o tamanho máximo do quadro para menos de 4 MB. Se não for prático configurar o tamanho do quadro, o cliente poderá configurar o tamanho máximo da mensagem para menos de 4 MB e enviar os dados de áudio como uma sequência de mensagens. Para obter mais informações sobre os quadros do WebSocket, consulte [IETF RFC 6455](http://tools.ietf.org/html/rfc6455){: external}.

O fragmento do código JavaScript a seguir envia dados de áudio para o serviço como uma mensagem binária (blob):

```javascript
websocket.send(blob);
```
{: codeblock}

O fragmento a seguir recebe hipóteses de reconhecimento que o serviço retorna de forma assíncrona. Os resultados são manipulados pela função `onMessage` do cliente.

```javascript
function onMessage(evt) {
  console.log(evt.data);
}
```
{: codeblock}

## Terminar uma solicitação de reconhecimento
{: #WSstop}

Ao terminar o envio dos dados de áudio para uma solicitação para o serviço, o cliente *deve* sinalizar o término da transmissão de áudio binário para o serviço de uma das maneiras a seguir:

-   Enviando uma mensagem de texto do JSON com o parâmetro `action` configurado para o valor `stop`:

    ```javascript
    {action: 'stop'}
    ```
    {: codeblock}

-   Enviando uma mensagem binária vazia, uma na qual o blob especificado está vazio:

    ```javascript
    websocket.send(blob)
    ```
    {: codeblock}

O serviço não envia os resultados finais até que receba a confirmação de que a transmissão de áudio está completa. Se você falhar ao sinalizar que a transmissão está concluída, a conexão poderá atingir o tempo limite sem que o serviço envie os resultados finais.

Para receber resultados finais entre múltiplas solicitações de reconhecimento, o cliente deve sinalizar o final da transmissão para a solicitação anterior antes de enviar uma solicitação subsequente. Depois de retornar os resultados finais para a primeira solicitação, o serviço retornará outra mensagem `{"state":"listening"}` para o cliente. Essa mensagem indica que o serviço está pronto para receber outra solicitação.

## Enviar solicitações adicionais e modificar parâmetros de solicitação
{: #WSmore}

Enquanto a conexão do WebSocket permanecer ativa, o cliente poderá continuar a usar a conexão para enviar solicitações de reconhecimento adicionais com novo áudio. Por padrão, o serviço continua a usar os parâmetros que foram enviados com a mensagem `start` anterior para todas as solicitações subsequentes que são enviadas por meio da mesma conexão.

Para mudar os parâmetros para solicitações subsequentes, o cliente pode enviar outra mensagem `start` com os novos parâmetros após receber os resultados finais do reconhecimento e a mensagem `{"state":"listening"}` do serviço. O cliente pode mudar qualquer parâmetro, exceto aqueles parâmetros especificados quando a conexão é aberta (`model`, `language_customization_id` e assim por diante).

O exemplo a seguir envia uma mensagem `start` com novos parâmetros para solicitações de reconhecimento subsequentes que são enviadas por meio da conexão. A mensagem especifica o mesmo `content-type` como o exemplo anterior, mas ela direciona o serviço para retornar as medidas de confiança e os registros de data e hora para as palavras da transcrição.

```javascript
var message = {
  action: 'start',
  content-type: 'audio/l16;rate=22050',
  word_confidence: true,
  timestamps: true
};
websocket.send(JSON.stringify(message));
```
{: codeblock}

## Manter uma conexão ativa
{: #WSkeep}

O serviço finalizará a sessão e fechará a conexão se ocorrer um tempo limite de inatividade ou de sessão:

-   Um *tempo limite de inatividade* ocorre se o áudio está sendo enviado pelo cliente, mas o serviço não detecta nenhuma fala. O tempo limite de inatividade é 30 segundos por padrão. É possível usar o parâmetro `inactivity_timeout` para especificar um valor diferente, incluindo `-1` para configurar o tempo limite para infinito. Para obter mais informações, consulte [Tempo limite de inatividade](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts-inactivity).
-   Um *tempo limite da sessão* ocorre se o serviço não recebe dados do cliente ou não envia resultados provisórios por 30 segundos. Não é possível mudar a duração desse tempo limite, mas é possível estender a sessão enviando ao serviço qualquer dado de áudio, incluindo apenas silêncio, antes que o tempo limite ocorra. Também deve-se configurar `inactivity_timeout` como `-1`. Você é cobrado pela duração de qualquer dado que envia para o serviço, incluindo o silêncio enviado para estender uma sessão. Para obter mais informações, consulte [Tempo limite de sessão](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts-session).

Os clientes e os servidores do WebSocket também podem trocar *quadros de ping-pong* para evitar tempos limites de leitura trocando pequenas quantidades de dados periodicamente. Muitos quadros do WebSocket trocam quadros de ping-pong, mas alguns não. Para determinar se a sua implementação usa quadros de ping-pong, verifique sua lista de recursos. Não é possível determinar ou gerenciar programaticamente quadros de ping-pong.

Se a sua pilha do WebSocket não implementar quadros de ping-pong e você estiver enviando arquivos de áudio longos, a sua conexão poderá atingir um tempo limite de leitura. Para evitar esses tempos limites, envie continuamente o áudio para o serviço ou solicite resultados temporários do serviço. Qualquer uma das abordagens pode assegurar que a falta de quadros de ping-pong não faça com que sua conexão seja fechada.

Para obter mais informações sobre quadros de ping-pong, consulte a [Seção 5.5.2 Ping](http://tools.ietf.org/html/rfc6455#section-5.5.2){: external} e a [Seção 5.5.3 Pong](http://tools.ietf.org/html/rfc6455#section-5.5.3){: external} do IETF RFC 6455.

## Fechar uma conexão
{: #WSclose}

Quando o cliente terminar de interagir com o serviço, ele poderá fechar a conexão do WebSocket. Quando a conexão é fechada, o cliente não pode mais usá-la para enviar solicitações ou receber resultados. Feche a conexão somente depois de receber todos os resultados para uma solicitação. Posteriormente, a conexão atingirá o tempo limite e fechará se você não a fechar explicitamente.

O fragmento a seguir do código JavaScript fecha uma conexão aberta:

```javascript
websocket.close();
```
{: codeblock}

## Códigos de retorno do WebSocket
{: #WSreturn}

O serviço pode enviar os códigos de retorno a seguir para o cliente por meio da conexão do WebSocket:

-   `1000` indica encerramento normal da conexão, o que significa que o propósito para o qual a conexão foi estabelecida foi atendido.
-   `1002` indica que o serviço está fechando a conexão devido a um erro de protocolo.
-   `1006` indica que a conexão foi fechada anormalmente.
-   `1009` indica que o tamanho do quadro excedeu o limite de 4 MB.
-   `1011` indica que o serviço está finalizando a conexão porque encontrou uma condição inesperada que o impede de preencher a solicitação.

Se o soquete fechar com um erro, o cliente receberá uma mensagem informativa do formulário `{"error":"{message}"}` antes que o soquete seja fechado. Para obter mais informações sobre os códigos de retorno do WebSocket, consulte [IETF RFC 6455](http://tools.ietf.org/html/rfc6455){: external}.

## Exemplo de sessão do WebSocket
{: #WSexample}

O exemplo a seguir mostra uma sessão do WebSocket entre um cliente e o {{site.data.keyword.speechtotextshort}}. A sessão é mostrada como três interações separadas para facilitar o acompanhamento. Mas todas as três interações são parte de uma única sessão com o serviço. O exemplo concentra-se na troca de mensagens; ele não mostra a abertura e o fechamento da conexão.

### Primeira interação de exemplo
{: #firstExample}

Na primeira interação, o cliente envia áudio que contém a sequência `Name the Mayflower`. O cliente envia uma mensagem binária com um único chunk de dados de áudio PCM (`audio/l16`), para os quais ele indica a taxa de amostragem necessária. O cliente não aguarda a resposta `{"state":"listening"}` do serviço para começar a enviar os dados de áudio e para sinalizar o término da solicitação. O envio dos dados reduz imediatamente a latência porque o áudio se torna disponível para o serviço assim que está pronto para manipular uma solicitação de reconhecimento.

-   O *cliente* envia:

    ```javascript
    {
      "action": "start",
      "content-type": "audio/l16;rate=22050"
    }
    <binary audio data>
    {
      "action": "stop"
    }
    ```
    {: codeblock}

-   O *serviço* responde:

    ```javascript
    {"state": "listening"}
    {"results": [{"alternatives": [{"transcript": "name the mayflower "}],
                  "final": true}], "result_index": 0}
    {"state":"listening"}
    ```
    {: codeblock}

### Segunda interação de exemplo
{: #secondExample}

Na segunda interação, o cliente envia áudio que contém a sequência `Second audio transcript`. O cliente envia o áudio em uma única mensagem binária e usa os mesmos parâmetros que especificou na primeira solicitação.

-   O *cliente* envia:

    ```javascript
    <binary audio data>
    {
      "action": "stop"
    }
    ```
    {: codeblock}

-   O *serviço* responde:

    ```javascript
    {"results": [{"alternatives": [{"transcript": "second audio transcript "}],
                  "final": true}], "result_index": 0}
    {"state":"listening"}
    ```
    {: codeblock}

### Terceira interação de exemplo
{: #thirdExample}

Na terceira interação, o cliente novamente envia áudio que contém a sequência `Name the Mayflower`. O cliente novamente envia uma mensagem binária com um único chunk de dados de áudio PCM. Mas dessa vez, o cliente solicita resultados provisórios com a transcrição.

-   O *cliente* envia:

    ```javascript
    {
      "action": "start",
      "content-type": "audio/l16;rate=22050",
      "interim_results": true
    }
    <binary audio data>
    {
      "action": "stop"
    }
    ```
    {: codeblock}

-   O *serviço* responde:

    ```javascript
    {"state":"listening"}
    {"results": [{"alternatives": [{"transcript": "name "}],
                  "final": false}], "result_index": 0}
    {"results": [{"alternatives": [{"transcript": "name may "}],
                  "final": false}], "result_index": 0}
    {"results": [{"alternatives": [{"transcript": "name may flour "}],
                  "final": false}], "result_index": 0}
    {"results": [{"alternatives": [{"transcript": "name the mayflower "}],
                  "final": true}], "result_index": 0}
    {"state":"listening"}
    ```
    {: codeblock}
