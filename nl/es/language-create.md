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

# Creación de un modelo de lenguaje personalizado
{: #languageCreate}

Siga estos pasos para crear un modelo de lenguaje personalizado para {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}:
{: shortdesc}

1.  [Cree un modelo de lenguaje personalizado](#createModel-language). Puede crear varios modelos personalizados para los mismos dominios o para dominios diferentes. El proceso es el mismo para cualquier modelo que cree. Sin embargo, solo puede especificar un único modelo personalizado a la vez con una solicitud de reconocimiento.
1.  [Añada un corpus al modelo de lenguaje personalizado](#addCorpus). Un corpus es un documento de texto sin formato que utiliza terminología del dominio en el contexto. El servicio crea un vocabulario para un modelo personalizado mediante la extracción de términos del corpus que no existen en su vocabulario base. Puede añadir varios corpus a un modelo personalizado.
1.  [Añada palabras al modelo de lenguaje personalizado](#addWords). También puede añadir palabras personalizadas a un modelo individualmente. Además, puede utilizar los mismos métodos para modificar las palabras personalizadas que se extraen de los corpus. Los métodos le permiten especificar la pronunciación de palabras y cómo se visualizan las palabras en una transcripción de voz.
1.  [Entrene el modelo de lenguaje personalizado](#trainModel-language). Una vez que haya añadido palabras al modelo personalizado, debe entrenar el modelo con las palabras. El entrenamiento prepara el modelo personalizado para que se utilice en el reconocimiento de voz. El modelo no utiliza palabras nuevas o modificadas hasta que lo entrena.
1.  Después de entrenar el modelo personalizado, puede utilizarlo con las solicitudes de reconocimiento. Si el audio que se pasa para la transcripción contiene palabras específicas del dominio que están definidas en el modelo personalizado, los resultados de la solicitud reflejan el vocabulario mejorado del modelo. Para obtener más información, consulte el apartado sobre [Utilización de un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse).

Los pasos para la creación de un modelo de lenguaje personalizado son iterativos. Puede añadir corpus, añadir palabras y entrenar o volver a entrenar un modelo tantas veces como sea necesario.

También puede añadir gramáticas a un modelo de lenguaje personalizado. Las gramáticas restringen la respuesta del servicio a aquellas palabras que la gramática reconoce. Para obtener más información, consulte [Utilización de gramáticas con modelos de lenguaje personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars).

La personalización del modelo de lenguaje está disponible para la mayoría de idiomas. Para obtener más información, consulte [Soporte de idiomas para la personalización](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
{: note}

## Creación de un modelo de lenguaje personalizado
{: #createModel-language}

Para crear un nuevo modelo de lenguaje personalizado se utiliza el método `POST /v1/customizations`. Puede crear tantos modelos de lenguaje personalizados como desee, pero solo puede utilizar un modelo a la vez con una solicitud de reconocimiento de voz. El método acepta un objeto JSON que define los atributos del nuevo modelo personalizado como el cuerpo de la solicitud.

<table>
  <caption>Tabla 1. Atributos de un nuevo modelo de lenguaje personalizado</caption>
  <tr>
    <th style="width:20%; text-align:left">Parámetro</th>
    <th style="width:12%; text-align:center">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Un nombre definido por el usuario para el nuevo modelo personalizado. Utilice un nombre que describa el dominio del modelo personalizado, como por ejemplo <code>Modelo personalizado médico</code> o <code>Modelo personalizado legal</code>. Utilice un nombre que sea exclusivo entre todos sus modelos de lenguaje personalizado.
      Utilice un nombre en el idioma del modelo personalizado.
    </td>
  </tr>
  <tr>
    <td><code>base_model_name</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      El nombre del modelo de lenguaje que se va a personalizar mediante el nuevo modelo personalizado. Especifique uno de los modelos de lenguaje soportados que se devuelven mediante el método <code>GET /v1/models</code>. El nuevo modelo solo se puede utilizar con el modelo base que personaliza.
    </td>
  </tr>
  <tr>
    <td><code>dialect</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      El dialecto del idioma especificado que se va a utilizar con el modelo personalizado. De forma predeterminada, el dialecto coincide con el idioma del modelo base; por ejemplo, el dialecto es <code>en-US</code> para los modelos de idioma en inglés de EE. UU., <code>en-US_BroadbandModel</code> o
      <code>en-US_NarrowbandModel</code>.<br/></br>
      El parámetro solo tiene sentido para los modelos en español, para los que el servicio crea un modelo personalizado que se adapta al habla del dialecto indicado:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-ES</code> para español castellano (valor predeterminado)
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-LA</code> para español de Latinoamérica
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <code>es-US</code> para español de Norteamérica (México)
        </li>
      </ul>
      Si especifica un dialecto, debe ser válido para el modelo base.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Una descripción del nuevo modelo. Utilice una descripción en el idioma del modelo personalizado.
    </td>
  </tr>
</table>

En el ejemplo siguiente se crea un nuevo modelo de lenguaje personalizado denominado `Modelo de ejemplo`. El modelo se crea para el modelo base `en-US_BroadbandModel` y su descripción es `Modelo de lenguaje personalizado de ejemplo`. La cabecera `Content-Type` especifica que se pasan datos JSON al método.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/json"
--data "{\"name\": \"Modelo de ejemplo\",
  \"base_model_name\": \"en-US_BroadbandModel\",
  \"description\": \"Modelo de lenguaje personalizado de ejemplo\"}"
"{url}/v1/customizations"
```
{: pre}

El ejemplo devuelve el ID de personalización del nuevo modelo. Cada modelo personalizado se identifica mediante un ID de personalización exclusivo, que es un GUID (identificador global exclusivo). El GUID del modelo personalizado se especifica con el parámetro `customization_id` de las llamadas que están asociadas con el modelo.

```javascript
{
  "customization_id": "74f4807e-b5ff-4866-824e-6bba1a84fe96"
}
```
{: codeblock}

El modelo personalizado nuevo propiedad de la instancia del servicio cuyas credenciales se utilizan para crearlo. Para obtener más información, consulte [Propiedad de modelos personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#customOwner).

## Adición de un corpus al modelo de lenguaje personalizado
{: #addCorpus}

Una vez que se crea el modelo de lenguaje personalizado, el paso siguiente consiste en añadir datos (palabras específicas del dominio) al modelo. El método recomendado para cumplimentar un modelo personalizado con palabras nuevas consiste en añadir uno o varios corpus.

Un corpus es un archivo de texto sin formato que contiene frases de ejemplo del dominio. El servicio analiza el contenido de un archivo de corpus y extrae las palabras que no están en su vocabulario base. Estas palabras reciben el nombre de palabras no definidas en el vocabulario (OOV).

-   Para obtener más información sobre el uso de corpus, consulte [Cómo trabajar con corpus](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingCorpora).
-   Para obtener más información sobre la forma en que el servicio añade corpus a un modelo, consulte [¿Qué ocurre cuando añado un archivo de corpus?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseCorpus)

Al proporcionar frases que incluyen palabras nuevas, los corpus permiten al servicio aprender las palabras en su contexto. Luego puede aumentar o modificar las palabras del modelo de forma individual. El entrenamiento de un modelo solo con palabras individuales, en contraposición con las palabras que añade el corpus, requiere más tiempo y puede producir resultados menos efectivos.
{: tip}

Utilice el método `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` para añadir un corpus a un modelo personalizado:

-   Especifique el ID de personalización del modelo personalizado con el parámetro de vía de acceso `customization_id`.
-   Especifique un nombre para el corpus con el parámetro de vía de acceso `corpus_name`. Utilice un nombre en el idioma del modelo personalizado que refleje el contenido del corpus.
    -   El nombre puede tener un máximo de 128 caracteres.
    -   No utilice caracteres que se tengan que codificar en URL. Por ejemplo, en el nombre no utilice espacios, barras inclinadas, barras inclinadas invertidas, ampersands, comillas dobles, signos más, signos de igual, interrogaciones, etc. (El servicio no impide el uso de estos caracteres. Pero como se tienen que codificar en URL siempre que se utilicen, se desaconseja utilizarlos.)
    -   No utilice el nombre de un corpus o gramática que ya se haya añadido al modelo personalizado.
    -   No utilice el nombre `user`, que está reservado por el servicio para indicar las palabras personalizadas que el usuario añade o modifica.
    -   No utilice el nombre `base_lm` ni `default_lm`. Ambos nombres se reservan para un posterior uso por parte del servicio.
-   Pase el archivo de texto del corpus como el cuerpo de la solicitud.

Puede añadir un máximo de 90 mil palabras OOV y 10 millones de palabras en total de todas las fuentes combinadas. Esto incluye las palabras de los corpus y de las gramáticas, y las palabras que añade directamente. Para obtener más información, consulte [¿Cuántos datos necesito?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#wordsResourceAmount)
{: note}

En el ejemplo siguiente se añade el archivo de texto de corpus `healthcare.txt` al modelo personalizado con el ID especificado. En el ejemplo se utiliza el corpus `healthcare`.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--data-binary @healthcare.txt
"{url}/v1/customizations/{customization_id}/corpora/healthcare"
```
{: pre}

El método también acepta un parámetro de consulta opcional `allow_overwrite` que sobrescribe un corpus existente para un modelo personalizado. Utilice el parámetro si tiene que actualizar un archivo de corpus después de añadirlo a un modelo.

Este método es asíncrono. Puede tardar uno o dos minutos en completarse. La duración de la operación depende del número total de palabras del corpus, del número de palabras nuevas que el servicio encuentra en el corpus y de la carga actual del servicio. Para obtener más información sobre cómo comprobar el estado de un corpus, consulte [Supervisión de la solicitud de añadir un corpus](#monitorCorpus).

Puede añadir el número de corpus que desee a un modelo personalizado llamando al método una vez para cada archivo de texto de corpus. La adición de un corpus debe haber finalizado para poder añadir otro. Después de añadir un corpus a un modelo personalizado, examine las nuevas palabras personalizadas para comprobar si hay errores tipográficos y de otro tipo. Para obtener más información, consulte [Validación de un recurso de palabras](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).

### Supervisión de la solicitud de añadir un corpus
{: #monitorCorpus}

El servicio devuelve un código de respuesta 201 si el corpus es válido. Luego procesa de forma asíncrona el contenido del corpus y extrae automáticamente las palabras nuevas. No puede enviar solicitudes para añadir datos al modelo personalizado ni para entrenar el modelo hasta que el servicio termine de analizar el corpus para la solicitud actual.

Para determinar el estado del análisis, utilice el método `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` para sondear el estado del corpus. El método acepta el ID del modelo y el nombre del corpus, tal como se muestra en el ejemplo siguiente:

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/corpora/corpus1"
```
{: pre}

La respuesta incluye el estado del corpus:

```javascript
{
  "name": "corpus1",
  "total_words": 5037,
  "out_of_vocabulary_words": 401,
  "status": "analyzed"
}
```
{: codeblock}

El campo `status` tiene uno de los valores siguientes:

-   `analyzed` indica que el servicio ha analizado correctamente el corpus.
-   `being_processed` indica que el servicio todavía está analizando el corpus.
-   `undetermined` indica que el servicio ha encontrado un error al procesar el corpus.

Utilice un bucle para consultar el estado del corpus cada 10 segundos hasta que esté en el estado `analyzed`. Para obtener más información sobre cómo consultar el estado de los corpus de un modelo, consulte [Listado de corpus para un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).

## Adición de palabras al modelo de lenguaje personalizado
{: #addWords}

Aunque la adición de corpus es el método recomendado para añadir palabras a un modelo de lenguaje personalizado, también puede añadir directamente palabras personalizados individuales al modelo. El servicio añade las palabras personalizadas al modelo personalizado tal y como lo hace con las palabras OOV que descubre en los corpus.

Si solo tiene una o unas pocas palabras que añadir a un modelo, el uso de corpus para añadir las palabras podría no resultar práctico o incluso viable. La forma más sencilla de hacerlo es mediante la adición de una palabra con solo su ortografía. Pero también puede proporcionar varias pronunciaciones para la palabra e indicar cómo se debe mostrar.

-   Para obtener más información sobre cómo añadir palabras directamente, consulte [Cómo trabajar con palabras personalizadas](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#workingWords).
-   Para obtener más información acerca de la forma en que el servicio añade palabras personalizadas a un modelo, consulte [¿Qué ocurre cuando añado o modifico una palabra personalizada?](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#parseWord)

Puede utilizar los métodos siguientes para añadir palabras a un modelo personalizado:

-   El método `POST /v1/customizations/{customization_id}/words` añade varias palabras a la vez. Debe pasar un objeto JSON que contenga información sobre cada palabra con el cuerpo de la solicitud. En el ejemplo siguiente se añaden dos palabras personalizadas, `HHonors` e `IEEE`, al modelo personalizado con el ID especificado. La cabecera `Content-Type` especifica que se pasan datos JSON al método.

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

    También puede añadir las palabras desde un archivo. Por ejemplo, el archivo `words.json` define las mismas dos palabras personalizadas.

    ```
    {"words":
      [
        {"word": "HHonors", "sounds_like": ["hilton honors", "H. honors"], "display_as": "HHonors"},
        {"word": "IEEE", "sounds_like": ["I. triple E."]}
      ]
    }
    ```
    {: codeblock}

    El mandato siguiente añade las palabras del archivo:

    ```bash
    curl -X POST
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data-binary @words.json
    "{url}/v1/customizations/{customization_id}/words"
    ```
    {: pre}

    Este método es asíncrono. El tiempo que tarda en completarse depende del número de palabras que añade y de la carga actual del servicio. Para obtener más información sobre cómo comprobar el estado de la operación, consulte [Supervisión de la solicitud de añadir palabras](#monitorWords).
-   El método `PUT /v1/customizations/{customization_id}/words/{word_name}` añade palabras individuales. Debe pasar un objeto JSON que contenga información sobre la palabra. En el ejemplo siguiente se añade la palabra `NCAA` al modelo con el ID especificado. Como siempre, la cabecera `Content-Type` especifica que se pasan datos JSON al método.

    ```bash
    curl -X PUT
    --header "Authorization: Bearer {token}"
    --header "Content-Type: application/json"
    --data "{\"sounds_like\": [\"N. C. A. A.\", \"N. C. double A.\"]}"
    "{url}/v1/customizations/{customization_id}/words/NCAA"
    ```
    {: pre}

    Este método es síncrono. El servicio devuelve un código de respuesta que muestra de forma inmediata si se ha ejecutado correctamente o no.

Al igual que sucede con la adición de corpus, examine las nuevas palabras personalizadas para comprobar si hay errores tipográficos y de otro tipo. Esta comprobación es especialmente importante cuando se añaden varias palabras a la vez. Para obtener más información, consulte [Validación de un recurso de palabras](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).

### Supervisión de la solicitud de añadir palabras
{: #monitorWords}

Cuando se utiliza el método `POST /v1/customizations/{customization_id}/words`, el servicio devuelve el código de respuesta 201 si los datos de entrada son válidos. Luego procesa de forma asíncrona las palabras para añadirlas al modelo. La operación suele ser más rápida que la adición de un corpus o que el entrenamiento de un modelo, pero su duración depende del número de palabras nuevas que se añaden y de la carga actual del servicio. No puede enviar solicitudes para añadir datos al modelo personalizado ni para entrenar el modelo hasta que el servicio complete la solicitud de añadir palabras nuevas.

Para determinar el estado de la solicitud. utilice el método `GET /v1/customizations/{customization_id}` para sondear el estado del modelo. El método acepta el ID de personalización del modelo y devuelve información que incluye el estado del modelo, como en el ejemplo siguiente:

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
  "name": "Modelo de ejemplo",
  "description": "Modelo del idioma personalizado de ejemplo",
  "base_model_name": "en-US_BroadbandModel",
  "status": "pending",
  "progress": 0
}
```
{: codeblock}

El campo `status` muestra el estado actual del modelo. Mientras el servicio está procesando palabras nuevas, el estado es `pending`. Utilice un bucle para consultar el estado cada 10 segundos hasta que esté en el estado `ready`, que indica que la operación se ha completado. Para obtener información sobre los valores posibles de `status`, consulte [Supervisión de la solicitud de entrenamiento del modelo](#monitorTraining-language).

### Modificación de las palabras de un modelo personalizado
{: #modifyWord}

También puede utilizar los métodos `POST /v1/customizations/{customization_id}/words` y `PUT /v1/customizations/{customization_id}/words/{word_name}` para modificar o aumentar una palabra en un modelo personalizado. Es posible que tenga que utilizar los métodos para corregir un error tipográfico u otro error que se haya cometido al añadir una palabra al modelo. También es posible que tenga que añadir definiciones de pronunciaciones para una palabra existente.

Los métodos para modificar la definición de una palabra existente se utilizan del mismo modo que los utilizados para añadir una palabra. Los nuevos datos que se proporcionan para la palabra sobrescriben la definición existente de la palabra.

## Entrenamiento del modelo de lenguaje personalizado
{: #trainModel-language}

Una vez que haya cumplimentado un modelo de lenguaje personalizado con palabras nuevas (mediante la adición de corpus, de gramáticas y de palabras directamente), debe entrenar el modelo con los nuevos datos. El proceso de entrenamiento prepara el modelo personalizado para que utilice los datos en el reconocimiento de voz. El modelo no utiliza las palabras que se añaden a través de cualquier método hasta que lo entrena con los datos.

Utilice el método `POST /v1/customizations/{customization_id}/train` para entrenar un modelo personalizado. Debe pasar al método el ID de personalización del modelo que desea entrenar, como en el ejemplo siguiente:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}/train"
```
{: pre}

Este método es asíncrono. La formación puede tardar unos minutos en completarse en función del número de palabras nuevas con las que se está entrenando el modelo y de la carga actual del servicio. Para obtener más información sobre cómo consultar el estado de una operación de entrenamiento, consulte [Supervisión de la solicitud de entrenamiento del modelo](#monitorTraining-language).

El método incluye los siguientes parámetros de consulta opcionales:

-   El parámetro `word_type_to_add` especifica las palabras con las que se va a entrenar el modelo personalizado:
    -   Especifique `all` o bien omita el parámetro para entrenar el modelo con todas sus palabras, independientemente de su origen.
    -   Especifique `user` para entrenar el modelo solo con las palabras que el usuario ha añadido o modificado, sin tener en cuenta las palabras que solo se han extraído de corpus o de gramáticas.

    Esta opción resulta útil si añade corpus con datos incorrectos, como palabras que contienen errores tipográficos. Antes de entrenar el modelo con este tipo de datos, puede utilizar el parámetro de consulta `word_type` del método `GET /v1/customizations/{customization_id}/words` para revisar las palabras que se extraen de corpus y de gramáticas. Para obtener más información, consulte [Listado de las palabras de un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).
-   El parámetro `customization_weight` especifica la ponderación relativa que se otorga a las palabras del modelo personalizado en comparación con las palabras del vocabulario base cuando se utiliza el modelo personalizado para el reconocimiento de voz. También puede especificar una ponderación de personalización con cualquier solicitud de reconocimiento que utilice el modelo personalizado. Para obtener más información, consulte [Utilización de ponderaciones de personalización](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageUse#weight).
-   El parámetro `strict` indica si el entrenamiento debe continuar si un modelo personalizado contiene una mezcla de recursos válidos y no válidos (corpus, gramáticas y palabras). De forma predeterminada, el entrenamiento falla si el modelo contiene uno o más recursos no válidos. Establezca el parámetro `false` para permitir que el entrenamiento continúe siempre que el modelo contenga como mínimo un recurso válido. El servicio excluye del entrenamiento los recursos que no son válidos. Para obtener más información, consulte [Errores de entrenamiento](#failedTraining-language).

### Supervisión de la solicitud de entrenamiento del modelo
{: #monitorTraining-language}

El servicio devuelve el código de respuesta 200 si inicia correctamente el proceso de entrenamiento. El servicio no acepta otras solicitudes de entrenamiento, ni solicitudes para añadir nuevos corpus, gramáticas o palabras, hasta que finaliza la solicitud actual.

Para determinar el estado de una solicitud de entrenamiento, utilice el método `GET /v1/customizations/{customization_id}` para sondear el estado del modelo. El método acepta el ID de personalización del modelo y devuelve información sobre el modelo.

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
  "name": "Modelo de ejemplo",
  "description": "Modelo del idioma personalizado de ejemplo",
  "base_model_name": "en-US_BroadbandModel",
  "status": "training",
  "progress": 0
}
```
{: codeblock}

La respuesta incluye los campos `status` y `progress` que muestran el estado del modelo personalizado. El significado del campo `progress` depende del estado del modelo. El campo `status` puede tener uno de los valores siguientes:

-   `pending` indica que el modelo se ha creado pero está a la espera de que se añadan datos de entrenamiento válidos o que el servicio termine de analizar los datos que se han añadido. El campo `progress` es `0`.
-   `ready` indica que el modelo contiene datos válidos y que está listo para ser entrenado. El campo `progress` es `0`.

    Si el modelo contiene una mezcla de recursos válidos y no válidos (por ejemplo, ambas palabras personalizadas válida y no válida), el entrenamiento del modelo falla a menos que establezca el parámetro de consulta `strict` en `false`. Para obtener más información, consulte [Errores de entrenamiento](#failedTraining-language).
-   `training` indica que el modelo se está entrenando. El campo `progress` pasa de `0` a `100` cuando termina el entrenamiento. <!-- The `progress` field indicates the progress of the training as a percentage complete. -->
-   `available` indica que el modelo está entrenado y listo para su uso. El campo `progress` es `100`.
-   `upgrading` indica que el modelo se está actualizando. El campo `progress` es `0`.
-   `failed` indica que el entrenamiento del modelo ha fallado. El campo `progress` es `0`. Para obtener más información, consulte [Errores de entrenamiento](#failedTraining-language).

Utilice un bucle para consultar el estado cada 10 segundos hasta que esté en el estado `available`. Para obtener más información sobre cómo comprobar el estado de un modelo personalizado, consulte [Listado de modelos de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).

### Errores de entrenamiento
{: #failedTraining-language}

El entrenamiento no se puede iniciar si el servicio está gestionando otra solicitud para el modelo de lenguaje personalizado. Por ejemplo, una solicitud de entrenamiento no se puede iniciar con un código de estado de 409 si el servicio está

-   Procesando un corpus o una gramática para generar una lista de palabras OOV
-   Procesando palabras personalizadas para validar o generar automáticamente pronunciaciones
-   Gestionando de otra solicitud de entrenamiento

El entrenamiento tampoco se puede iniciar con un código de estado de 400 si el modelo personalizado

-   No contiene datos de entrenamiento válidos nuevos (corpus, gramáticas o palabras) desde que se creó o desde que se entrenó por última vez
-   Contiene un corpus, una gramática o una palabra (o varios), por ejemplo, una palabra personalizada tiene una pronunciación 'suena como' no válida

Si falla la solicitud de entrenamiento con un código de estado de 400, el servicio establece el estado de modelo personalizado en `failed`. Efectúe
una de las acciones siguientes:

-   Utilice métodos de la interfaz de personalización para examinar los recursos de los modelos y corrija los posibles errores que encuentre:
    -   Para un corpus no válido, puede corregir el archivo de texto del corpus y utilizar el parámetro `allow_overwrite` del método `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` para añadir el archivo corregido al modelo. Para obtener más información, consulte [Adición de un corpus al modelo de lenguaje personalizado](#addCorpus).
    -   Para una gramática no válida, puede corregir el archivo de gramática y utilizar el parámetro `allow_overwrite` del método `POST /v1/customizations/{customization_id}/grammars/{grammar_name}` para añadir el archivo corregido al modelo. Para obtener más información, consulte [Adición de una gramática al modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
    -   Para una palabra personalizada no válida, puede utilizar el método `POST /v1/customizations/{customization_id}/words` o `PUT /v1/customizations/{customization_id}/words/{word_name}` para modificar la palabra directamente en el recurso de palabras del modelo. Para obtener más información, consulte [Modificación de las palabras de un modelo personalizado](#modifyWord).

    Para obtener más información sobre la validación de las palabras en un modelo de lenguaje personalizado, consulte [Validación de un recurso de palabras](/docs/services/speech-to-text-data?topic=speech-to-text-data-corporaWords#validateModel).
-   Establezca el parámetro `strict` del método `POST /v1/customizations/{customization_id}/train` en `false` para excluir los recursos no válidos del entrenamiento. El modelo debe contener al menos un recurso válido (corpus, grammar o palabra) para que el entrenamiento tenga éxito. El parámetro `strict` es útil para entrenar un modelo personalizado que contiene una mezcla de recursos válidos y no válidos.
