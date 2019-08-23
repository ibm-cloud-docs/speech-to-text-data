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

# Resumen de parámetros
{: #summary}

A continuación se muestra un resumen de todos los parámetros disponibles para el reconocimiento de voz. Para obtener más información sobre todos los métodos del servicio {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}, consulte la [Referencia de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
{: shortdesc}

Tenga en cuenta los siguientes requisitos básicos cuando realice una solicitud de reconocimiento de voz:

-   Los nombres de los métodos distinguen entre mayúsculas y minúsculas.
-   Las cabeceras de solicitudes HTTP no distinguen entre mayúsculas y minúsculas.
-   Los parámetros de consulta HTTP y WebSocket distinguen entre mayúsculas y minúsculas.
-   Los nombres de campos JSON distinguen entre mayúsculas y minúsculas.
-   Todo el contenido de la respuesta JSON está en el juego de caracteres UTF-8.

Tenga en cuenta también los siguientes requisitos específicos del servicio:

-   Solo es obligatorio especificar el audio de entrada. Todos los
demás parámetros son opcionales.
-   Si especifica un parámetro de consulta o un campo JSON no válido como parte de la entrada, la respuesta incluye un campo `warnings` que describe el argumento no válido. La solicitud tiene éxito a pesar de los avisos.

## access_token
{: #summary-access-token}

Una señal de acceso de IAM opcional que se utiliza para establecer una conexión autenticada con la interfaz WebSocket. Para obtener más información, consulte el apartado sobre cómo [Abrir una conexión](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets#WSopen).

<table>
  <caption>Tabla 1. El parámetro access_token</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:30%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro de consulta de la solicitud de conexión <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      No soportado
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      No soportado
    </td>
  </tr>
</table>

## acoustic_customization_id
{: #summary-acoustic-customization-id}

Un ID de personalización opcional para un modelo acústico personalizado que se adapta a las características acústicas de su entorno y de los oradores. De forma predeterminada, no se utiliza ningún modelo personalizado. Para obtener más información, consulte [Modelos personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabla 2. El parámetro acoustic_customization_id</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Beta para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro de consulta de la solicitud de conexión <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## audio_metrics
{: #summary-audio-metrics}

Un valor booleano opcional que indica si el servicio devuelve métricas sobre las características de señal del audio de entrada. De forma predeterminada, (`false`), el servicio no devuelve métricas de sonido. Para obtener más información, consulte [Métricas de audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics).

<table style="width:90%">
  <caption>Tabla 3. El parámetro audio_metrics</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## base_model_version
{: #summary-base-model-version}

Versión opcional de un modelo base. El parámetro está pensado principalmente para que se utilice con modelos personalizados que se actualizan para un nuevo modelo base, pero se puede utilizar sin un modelo personalizado. El valor predeterminado depende de si el parámetro se utiliza con o sin un modelo personalizado. Para obtener más información, consulte [Versión del modelo base](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#version).

<table style="width:90%">
  <caption>Tabla 4. El parámetro base_model_version</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro de consulta de la solicitud de conexión <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## Content-Type
{: #summary-content-type}

Un formato de audio opcional (tipo de MIME) que especifica el formato de los datos de audio que se pasan al servicio. El servicio puede detectar automáticamente el formato de la mayoría de audio, por lo que el parámetro es opcional para la mayoría de los formatos. Es obligatorio para los formatos `audio/alaw`, `audio/basic`, `audio/l16` y `audio/mulaw`. Para obtener más información, consulte [Formatos de audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).

<table style="width:90%">
  <caption>Tabla 5. El parámetro Content-Type</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro <code>content-type</code> del mensaje JSON <code>start</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Cabecera de solicitud del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Cabecera de solicitud del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## customization_weight
{: #summary-customization-weight}

Un valor opcional comprendido entre 0,0 y 1,0 que indica la ponderación relativa que otorga el servicio a las palabras de un modelo de lenguaje personalizado frente a las palabras del vocabulario base. El valor predeterminado es 0,3 a menos que se haya especificado una ponderación distinta al entrenar el modelo de lenguaje personalizado. Para obtener más información, consulte [Modelos personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabla 6. El parámetro personation_weight</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para inglés de EE. UU., inglés del Reino Unido, portugués de Brasil, francés, alemán, japonés, coreano y español
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## grammar_name
{: #summary-grammar-name}

Una serie opcional que identifica una gramática que se va a utilizar para el reconocimiento de voz. El servicio solo reconoce las series definidas por la gramática. Debe especificar tanto el nombre de la gramática como el ID de personalización del modelo de lenguaje personalizado para el que se define la gramática. Para obtener más información, consulte [Gramáticas](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#grammars-input).

<table style="width:90%">
  <caption>Tabla 7. El parámetro grammar_name</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Beta para inglés de EE. UU., inglés del Reino Unido, portugués de Brasil, francés, alemán, japonés, coreano y español
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## inactivity_timeout
{: #summary-inactivity-timeout}

Un número entero opcional que especifica el número de segundos correspondiente al tiempo de espera excedido de inactividad del servicio. Inactividad significa que el servicio no detecta voz en la secuencia de audio. El valor predeterminado es 30 segundos. Utilice `-1` para indicar un tiempo infinito. Para obtener más información, consulte [Tiempo de espera excedido de inactividad](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#timeouts-inactivity).

<table style="width:90%">
  <caption>Tabla 8. El parámetro inactivity_timeout</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## interim_results
{: #summary-interim-results}

Un valor booleano opcional que indica al servicio que devuelva hipótesis intermedias que es probable que cambien antes de la transcripción final. De forma predeterminada (`false`), no se devuelven resultados provisionales. Para obtener más información, consulte [Resultados provisionales](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#interim).

<table style="width:90%">
  <caption>Tabla 9. El parámetro interim_results</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      No soportado
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      No soportado
    </td>
  </tr>
</table>

## keywords
{: #summary-keywords}

Una matriz opcional de series de palabras clave que el servicio detecta en el audio de entrada. De forma predeterminada, no se lleva a cabo la detección de palabras clave. Para obtener más información, consulte [Detección de palabras clave](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting).

<table style="width:90%">
  <caption>Tabla 10. El parámetro keywords</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## keywords_threshold
{: #summary-keywords-threshold}

Un valor opcional comprendido entre 0,0 y 1,0 que indica el umbral mínimo para una coincidencia positiva de palabra clave. De forma predeterminada, no se lleva a cabo la detección de palabras clave. Para obtener más información, consulte [Detección de palabras clave](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#keyword_spotting).

<table style="width:90%">
  <caption>Tabla 11. El parámetro keywords_threshold</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## language_customization_id
{: #summary-language-customization-id}

Un ID de personalización opcional para un modelo de lenguaje personalizado que incluye terminología de su dominio. De forma predeterminada, no se utiliza ningún modelo personalizado. Para obtener más información, consulte [Modelos personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#custom-input).

<table style="width:90%">
  <caption>Tabla 12. El parámetro language_customization_id</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para inglés de EE. UU., inglés del Reino Unido, portugués de Brasil, francés, alemán, japonés, coreano y español
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro de consulta de la solicitud de conexión <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## max_alternatives
{: #summary-max-alternatives}

Un número entero opcional que especifica el número máximo de hipótesis alternativas que devuelve el servicio. De forma predeterminada, el servicio devuelve una sola hipótesis final. Para obtener más información, consulte [Número máximo de alternativas](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#max_alternatives).

<table style="width:90%">
  <caption>Tabla 13. El parámetro max_alternatives</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## model
{: #summary-model}

Un modelo opcional que especifica el idioma en el que se habla el audio y la velocidad a la que se ha muestreado: banda ancha o banda estrecha. De forma predeterminada, se utiliza `en-US_BroadbandModel`. Para obtener más información, consulte [Idiomas y modelos](/docs/services/speech-to-text-data?topic=speech-to-text-data-models).

<table style="width:90%">
  <caption>Tabla 14. El parámetro model</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro de consulta de la solicitud de conexión <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## processing_metrics
{: #summary-processing-metrics}

Un valor booleano opcional que indica si el servicio devuelve métricas sobre el proceso del audio de entrada. De forma predeterminada (`false`), el servicio no devuelve métricas de proceso. Para obtener más información, consulte [Métricas de proceso](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics).

<table style="width:90%">
  <caption>Tabla 15. El parámetro processing_metrics</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      No soportado
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## processing_metrics_interval
{: #summary-processing-metrics-interval}

Un valor flotante opcional de 0,1 como mínimo que indica el intervalo en que el servicio debe devolver las métricas de proceso. Si el parámetro `processing_metrics` es `true`, el servicio devuelve métricas de proceso cada segundo de forma predeterminada. Para obtener más información, consulte [Métricas de proceso](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics).

<table style="width:90%">
  <caption>Tabla 16. El parámetro processing_metrics_interval</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      No soportado
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## profanity_filter
{: #summary-profanity-filter}

Un valor booleano opcional que indica si el servicio censura de una transcripción el lenguaje obsceno. De forma predeterminada (`true`), se filtra el lenguaje obsceno de la transcripción. Para obtener más información, consulte [Filtrado de lenguaje obsceno](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#profanity_filter).

<table style="width:90%">
  <caption>Tabla 17. El parámetro profanity_filter</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para inglés de EE. UU.
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## redaction
{: #summary-redaction}

Un valor booleano opcional que indica si el servicio debe ocultar en una transcripción los datos numéricos con tres o más dígitos consecutivos. Si establece el parámetro `redaction` en `true`, el servicio impone automáticamente que el parámetro `smart_formatting` tenga el valor `true`. De forma predeterminada (`false`), los datos numéricos no se ocultan. Para obtener más información, consulte [Ocultación numérica](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#redaction).

<table style="width:90%">
  <caption>Tabla 18. El parámetro redaction</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Beta para inglés de EE. UU., japonés y coreano
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## smart_formatting
{: #summary-smart-formatting}

Un valor booleano opcional que indica si el servicio convierte fechas, horas, números, moneda y valores similares en representaciones más convencionales en la transcripción final. Para inglés de EE. UU., la característica también convierte determinadas frases con palabras clave en signos de puntuación. De forma predeterminada (`false`), no se lleva a cabo el formateo inteligente. Para obtener más información, consulte [Formateo inteligente](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#smart_formatting).

<table style="width:90%">
  <caption>Tabla 19. El parámetro smart_formatting</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Beta para inglés de EE. UU., japonés y español
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## speaker_labels
{: #summary-speaker-labels}

Un valor booleano opcional que indica si el servicio identifica las palabras que ha pronunciado cada persona en un intercambio con varios participantes. Si establece el parámetro `speaker_labels` en `true`, el servicio impone automáticamente que el parámetro `timestamps` tenga el valor `true`. De forma predeterminada (`false`), no se devuelven etiquetas de orador. Para obtener más información, consulte [Etiquetas de orador](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#speaker_labels).

<table style="width:90%">
  <caption>Tabla 20. El parámetro speaker_labels</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Beta para inglés de EE. UU., japonés y español (modelos de banda ancha y de banda estrecha) y para inglés del Reino Unido (solo modelo de banda estrecha)
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## timestamps
{: #summary-timestamps}

Un valor booleano opcional que indica si el servicio genera indicaciones de fecha y hora para las palabras de la transcripción. De forma predeterminada (`false`), no se devuelven indicaciones de fecha y hora. Para obtener más información, consulte [Indicaciones de fecha y hora de palabras](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_timestamps).

<table style="width:90%">
  <caption>Tabla 21. El parámetro timestamps</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## Transfer-Encoding
{: #summary-transfer-encoding}

Un valor opcional de `chunked` que hace que el audio se transmita en secuencia al servicio. De forma predeterminada, el audio se envía todo a la vez en una entrega única. Para obtener más información, consulte [Transmisión de audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-input#transmission).

<table style="width:90%">
  <caption>Tabla 22. El parámetro Transfer-Encoding</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      No se aplica; siempre se transmite en secuencia
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Cabecera de solicitud del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Cabecera de solicitud del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## word_alternatives_threshold
{: #summary-word-alternatives-threshold}

Un valor opcional comprendido entre 0,0 y 1,0 que especifica el umbral en el cual el servicio muestra alternativas acústicamente similares para las palabras del audio de entrada. De forma predeterminada, no se devuelven alternativas a palabras. Para obtener más información, consulte [Alternativas a palabras](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_alternatives).

<table style="width:90%">
  <caption>Tabla 23. El parámetro word_alternatives_threshold</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## word_confidence
{: #summary-word-confidence}

Un valor booleano opcional que indica si el servicio proporciona medidas de confianza para las palabras de la transcripción. De forma predeterminada (`false`), no se devuelven medidas de confianza. Para obtener más información, consulte [Confianza de palabras](/docs/services/speech-to-text-data?topic=speech-to-text-data-output#word_confidence).

<table style="width:90%">
  <caption>Tabla 24. El parámetro word_confidence</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro del mensaje <code>start</code> de JSON
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Parámetro de consulta del método <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>

## X-Watson-Metadata
{: #summary-x-watson-metadata}

Una serie opcional que asocia un ID de cliente con los datos que se pasan para las solicitudes de reconocimiento. El parámetro acepta el argumento `customer_id={id}`. De forma predeterminada, no se asocia ningún ID de cliente a los datos. Para obtener más información, consulte [Seguridad de la información](/docs/services/speech-to-text-data?topic=speech-to-text-data-information-security).

<table style="width:90%">
  <caption>Tabla 25. El parámetro X-Watson-Metadata</caption>
  <tr>
    <th>Disponibilidad y utilización</th>
    <th style="vertical-align:bottom">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left; width:35%">
      **Disponibilidad**
    </td>
    <td style="text-align:left">
      Disponible a nivel general para todos los idiomas
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **WebSocket**
    </td>
    <td style="text-align:left">
      Parámetro de consulta <code>x-watson-metadata</code> de la solicitud de conexión <code>/v1/recognize</code> (debe codificar el argumento en URL, por ejemplo `customer_id%3dmy_customer_ID`.)
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP síncrona**
    </td>
    <td style="text-align:left">
      Cabecera de solicitud del método POST <code>/v1/recognize</code>
    </td>
  </tr>
  <tr>
    <td style="text-align:left">
      **HTTP asíncrona**
    </td>
    <td style="text-align:left">
      Cabecera de solicitud del método <code>POST /v1/register_callback</code> y
      <code>POST /v1/recognitions</code>
    </td>
  </tr>
</table>
