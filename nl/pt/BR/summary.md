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

# Resumo de parâmetro
{: #summary}

A seguir está um resumo de todos os parâmetros disponíveis para reconhecimento de voz. Para obter mais informações sobre todos os métodos do serviço {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}, consulte a [Referência de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
{: shortdesc}

Considere os requisitos básicos a seguir ao fazer uma solicitação de reconhecimento de voz:

-   Os nomes dos métodos fazem distinção entre maiúsculas e minúsculas.
-   Cabeçalhos da solicitação de HTTP não fazem distinção entre maiúsculas e minúsculas.
-   Os parâmetros de consulta HTTP e WebSocket fazem distinção entre maiúsculas e minúsculas.
-   Os nomes de campo JSON fazem distinção entre maiúsculas e minúsculas.
-   Todo o conteúdo de resposta JSON está no conjunto de caracteres UTF-8.

Considere também os requisitos específicos do serviço a seguir:

-   É necessário especificar apenas o áudio de entrada. Todos os outros parâmetros são opcionais.
-   Se você especificar um parâmetro de consulta ou um campo JSON inválido como parte da entrada, a resposta incluirá um campo `warnings` que descreva o argumento inválido. A solicitação é bem-sucedida, apesar de qualquer aviso.

## access_token
{: #summary-access-token}

Um token de acesso usado para estabelecer uma conexão autenticada com a interface do WebSocket. Para obter mais informações, consulte [Abrir uma conexão](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets#WSopen).

<table>
  <caption>Tabela 1. O parâmetro access_token</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:30%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta da solicitação de conexão <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Sem suporte
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Sem suporte
    </td>
  </tr>
</table>

## acoustic_customization_id
{: #summary-acoustic-customization-id}

Um ID de customização opcional para um modelo acústico customizado que é adaptado para as características acústicas do ambiente e dos falantes. Por padrão, nenhum modelo customizado é usado. Para obter mais informações, consulte [Modelos customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabela 2. O parâmetro acoustic_customization_id</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Beta para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta da solicitação de conexão <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## audio_metrics
{: #summary-audio-metrics}

Um booleano opcional que indica se o serviço retorna métricas sobre as características de sinal do áudio de entrada. Por padrão (`false`), o serviço não retorna nenhuma métrica de áudio. Para obter mais informações, consulte [Métricas de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics).

<table style="width:90%">
  <caption>Tabela 3. O parâmetro audio_metrics</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## base_model_version
{: #summary-base-model-version}

Uma versão opcional de um modelo base. O parâmetro é destinado principalmente para uso com modelos customizados que são atualizados para um novo modelo base, mas ele pode ser usado sem um modelo customizado. O valor padrão depende de o parâmetro ser usado com ou sem um modelo customizado. Para obter mais informações, consulte [Versão do modelo base](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#version).

<table style="width:90%">
  <caption>Tabela 4. O parâmetro base_model_version</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta da solicitação de conexão <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## Conteúdo-tipo
{: #summary-content-type}

Um formato de áudio opcional (tipo MIME) que especifica o formato dos dados de áudio que você transmite para o serviço. O serviço pode detectar automaticamente o formato da maioria dos áudios, portanto, o parâmetro é opcional para a maioria dos formatos. Ele é necessário para os formatos `audio/alaw`, `audio/basic`, `audio/l16` e `audio/mulaw`. Para obter mais informações, consulte [Formatos de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).

<table style="width:90%">
  <caption>Tabela 5. O parâmetro Content-Type</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro <code>content-type</code> da mensagem JSON <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Cabeçalho da solicitação do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Cabeçalho de solicitação do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## customization_weight
{: #summary-customization-weight}

Um duplo opcional entre 0,0 e 1,0 que indica o peso relativo que o serviço fornece para palavras de um modelo de idioma customizado versus palavras do vocabulário base. O padrão é 0,3, a menos que um peso diferente tenha sido especificado quando o modelo de idioma customizado foi treinado. Para obter mais informações, consulte [Modelos customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabela 6. O parâmetro customization_weight</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para inglês dos EUA, inglês do Reino Unido, português do Brasil, francês, alemão, japonês, coreano e espanhol.
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## grammar_name
{: #summary-grammar-name}

Uma sequência opcional que identifica uma gramática que deve ser usada para reconhecimento de voz. O serviço reconhece apenas as sequências que são definidas pela gramática. Deve-se especificar o nome da gramática e o ID de customização do modelo de idioma customizado para o qual a gramática está definida. Para obter mais informações, consulte [Gramáticas](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#grammars-input).

<table style="width:90%">
  <caption>Tabela 7. O parâmetro grammar_name</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Beta para inglês dos EUA, inglês do Reino Unido, português do Brasil, francês, alemão, japonês, coreano e espanhol
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## inactivity_timeout
{: #summary-inactivity-timeout}

Um número inteiro opcional que especifica o número de segundos para o tempo limite de inatividade do serviço. A inatividade significa que o serviço não detecta nenhuma fala no áudio do fluxo. O padrão é 30 segundos. Use `-1` para indicar infinito. Para obter mais informações, consulte [Tempo limite de inatividade](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts-inactivity).

<table style="width:90%">
  <caption>Tabela 8. O parâmetro inactivity_timeout</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## interim_results
{: #summary-interim-results}

Um booleano opcional que direciona o serviço para retornar hipóteses intermediárias que provavelmente mudarão antes da transcrição final. Por padrão (`false`), os resultados provisórios não são retornados. Para obter mais informações, consulte [Resultados provisórios](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim).

<table style="width:90%">
  <caption>Tabela 9. O parâmetro interim_results</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Sem suporte
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Sem suporte
    </td>
  </tr>
</table>

## palavras-chave
{: #summary-keywords}

Uma matriz opcional de sequências de palavras-chave que o serviço marca no áudio de entrada. Por padrão, a marcação de palavra-chave não é executada. Para obter mais informações, consulte [Marcação de palavra-chave](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting).

<table style="width:90%">
  <caption>Tabela 10. O parâmetro keywords</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## keywords_threshold
{: #summary-keywords-threshold}

Um duplo opcional entre 0,0 e 1,0 que indica o limite mínimo para uma correspondência de palavra-chave positiva. Por padrão, a marcação de palavra-chave não é executada. Para obter mais informações, consulte [Marcação de palavra-chave](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting).

<table style="width:90%">
  <caption>Tabela 11. O parâmetro keywords_threshold</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## language_customization_id
{: #summary-language-customization-id}

Um ID de customização opcional para um modelo de idioma customizado que inclui terminologia do seu domínio. Por padrão, nenhum modelo customizado é usado. Para obter mais informações, consulte [Modelos customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabela 12. O parâmetro language_customization_id</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para inglês dos EUA, inglês do Reino Unido, português do Brasil, francês, alemão, japonês, coreano e espanhol.
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta da solicitação de conexão <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## max_alternatives
{: #summary-max-alternatives}

Um número inteiro opcional que especifica o número máximo de hipóteses alternativas que o serviço retorna. Por padrão, o serviço retorna uma única hipótese final. Para obter mais informações, consulte [Alternativas máximas](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives).

<table style="width:90%">
  <caption>Tabela 13. O parâmetro max_alternatives</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## modelo
{: #summary-model}

Um modelo opcional que especifica o idioma no qual o áudio é falado e a taxa na qual ele foi amostrado: banda larga ou banda estreita. Por padrão, `en-US_BroadbandModel` é usado. Para obter mais informações, consulte [Idiomas e modelos](/docs/services/speech-to-text-data?topic=speech-to-text-data-models).

<table style="width:90%">
  <caption>Tabela 14. O parâmetro model</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta da solicitação de conexão <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## processing_metrics
{: #summary-processing-metrics}

Um booleano opcional que indica se o serviço retorna as métricas sobre seu processamento do áudio de entrada. Por padrão (`false`), o serviço não retorna nenhuma métrica de processamento. Para obter mais informações, consulte [Métricas de processamento](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics).

<table style="width:90%">
  <caption>Tabela 15. O parâmetro processing_metrics</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Sem suporte
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## processing_metrics_interval
{: #summary-processing-metrics-interval}

Um flutuação opcional de pelo menos 0,1 que indica o intervalo no qual o serviço deve retornar as métricas de processamento. Se o parâmetro `processing_metrics` for `true`, o serviço retornará as métricas de processamento a cada 1,0 segundos por padrão. Para obter mais informações, consulte [Métricas de processamento](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics).

<table style="width:90%">
  <caption>Tabela 16. O parâmetro processing_metrics_interval</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Sem suporte
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## profanity_filter
{: #summary-profanity-filter}

Um booleano opcional que indica se o serviço censura profanidade de uma transcrição. Por padrão (`true`), a profanidade é filtrada da transcrição. Para obter mais informações, consulte [Filtragem de profanidade](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter).

<table style="width:90%">
  <caption>Tabela 17. O parâmetro profanity_filter</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para inglês dos EUA
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## redaction
{: #summary-redaction}

Um booleano opcional que indica se o serviço edita os dados numéricos com três ou mais dígitos consecutivos de uma transcrição. Se você configurar o parâmetro `redaction` como `true`, o serviço forçará automaticamente o parâmetro `smart_formatting` para ser `true`. Por padrão (`false`), os dados numéricos não são editados. Para obter mais informações, consulte [Edição de dados numéricos](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction).

<table style="width:90%">
  <caption>Tabela 18. O parâmetro redaction</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Beta para inglês dos EUA, japonês e coreano
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## smart_formatting
{: #summary-smart-formatting}

Um booleano opcional que indica se o serviço converte datas, horas, números, moeda e valores semelhantes em representações mais convencionais na transcrição final. Para inglês dos EUA, o recurso também converte algumas frases de palavra-chave em símbolos de pontuação. Por padrão (`false`), a formatação inteligente não é executada. Para obter mais informações, consulte [Formatação inteligente](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting).

<table style="width:90%">
  <caption>Tabela 19. O parâmetro smart_formatting</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Beta para inglês dos EUA, japonês e espanhol
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## speaker_labels
{: #summary-speaker-labels}

Um booleano opcional que indica se o serviço identifica as palavras ditas por cada indivíduo em uma interação com múltiplos participantes. Se você configurar o parâmetro `speaker_labels` como `true`, o serviço forçará automaticamente o parâmetro `timestamps` para que seja `true`. Por padrão (`false`), os rótulos do falante não são retornados. Para obter mais informações, consulte [Rótulos do falante](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels).

<table style="width:90%">
  <caption>Tabela 20. O parâmetro speaker_labels</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Beta para inglês dos EUA, japonês e espanhol (modelos de banda larga e de banda estreita) e inglês do Reino Unido (somente modelo de banda estreita)
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## timestamps
{: #summary-timestamps}

Um booleano opcional que indica se o serviço produz registros de data e hora para as palavras da transcrição. Por padrão (`false`), os registros de data e hora não são retornados. Para obter mais informações, consulte [Registros de data e hora de palavra](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps).

<table style="width:90%">
  <caption>Tabela 21. O parâmetro timestamps</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## Transfer-Encoding
{: #summary-transfer-encoding}

Um valor opcional de `chunked` que faz com que o áudio seja transmitido para o serviço. Por padrão, o áudio é enviado todo de uma vez como uma entrega única. Para obter mais informações, consulte [Transmissão de áudio](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission).

<table style="width:90%">
  <caption>Tabela 22. O parâmetro Transfer-Encoding</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Não aplicável. É sempre transmitido
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Cabeçalho da solicitação do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Cabeçalho de solicitação do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## word_alternatives_threshold
{: #summary-word-alternatives-threshold}

Um duplo opcional entre 0,0 e 1,0 que especifica o limite no qual o serviço relata alternativas acusticamente semelhantes para palavras do áudio de entrada. Por padrão, as alternativas de palavra não são retornadas. Para obter mais informações, consulte [Alternativas de palavra](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives).

<table style="width:90%">
  <caption>Tabela 23. O parâmetro word_alternatives_threshold</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## word_confidence
{: #summary-word-confidence}

Um booleano opcional que indica se o serviço fornece medidas de confiança para as palavras da transcrição. Por padrão (`false`), as medidas de confiança de palavra não são retornadas. Para obter mais informações, consulte [Confiança de palavra](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence).

<table style="width:90%">
  <caption>Tabela 24. O parâmetro word_confidence</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro da mensagem <code>start</code> do JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta do método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## X-Watson-Metadata
{: #summary-x-watson-metadata}

Uma sequência opcional que associa um ID do cliente aos dados que são transmitidos para solicitações de reconhecimento. O parâmetro aceita o argumento `customer_id={id}`. Por padrão, nenhum ID do cliente está associado aos dados. Para obter mais informações, consulte [Segurança de informações](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security).

<table style="width:90%">
  <caption>Tabela 25. O parâmetro X-Watson-Metadata</caption>
  <tr>
    <th>Disponibilidade e uso</th>
    <th style="vertical-align:bottom">Descrição</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidade**
    </td>
    <td style="text-align:left">
      Geralmente disponível para todos os idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parâmetro de consulta<code>x-watson-metadata</code> da solicitação de conexão <code>/v1/recognize</code> (deve-se codificar a URL do argumento, por exemplo, `customer_id%3dmy_customer_ID`.)
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrono**
    </td>
    <td style="text-align:left">
      Cabeçalho da solicitação do método POST <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP assíncrono**
    </td>
    <td style="text-align:left">
      Cabeçalho da solicitação dos métodos <code>POST /v1/register_callback</code> e
      <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>
