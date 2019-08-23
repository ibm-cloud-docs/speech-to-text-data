---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-19"

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

# Cómo trabajar con recursos de audio
{: #audioResources}

Puede añadir archivos de audio individuales o archivos archivadores que contengan varios archivos de audio a un modelo acústico personalizado. El medio recomendado para añadir recursos de audio es mediante la adición de archivos archivadores. Crear y añadir un solo archivo archivador resulta mucho más eficaz que añadir varios archivos de audio individualmente. También puede enviar solicitudes para añadir varios recursos de audio diferentes a la vez.
{: shortdesc}

## Adición de un recurso de audio
{: #addAudioResource}

Utilice el método `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` para añadir cualquier tipo de recurso de audio a un modelo acústico personalizado. El recurso de audio se pasa como cuerpo de la solicitud e incluye los siguientes parámetros:

-   El parámetro de vía de acceso `customization_id` para especificar el ID de personalización del modelo.
-   El parámetro de vía de acceso `audio_name` para especificar un nombre para el recurso de audio.
    -   Utilice un nombre en el idioma del modelo personalizado que refleje el contenido del recurso.
    -   El nombre puede tener un máximo de 128 caracteres.
    -   No utilice caracteres que se tengan que codificar en URL. Por ejemplo, en el nombre no utilice espacios, barras inclinadas, barras inclinadas invertidas, ampersands, comillas dobles, signos más, signos de igual, interrogaciones, etc. (El servicio no impide el uso de estos caracteres. Pero como se tienen que codificar en URL siempre que se utilicen, se desaconseja utilizarlos.)
    -   No utilice el nombre de un recurso de audio que ya se haya añadido al modelo personalizado.

Cuando actualice los recursos de audio de un modelo, debe entrenar el modelo para que los cambios entren en vigor durante la transcripción. Para obtener más información, consulte [Entrenamiento del modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic).

## Adición de un archivo de audio
{: #addAudioType}

Para añadir un archivo de audio individual a un modelo acústico personalizado, debe especificar el formato (tipo de MIME) del audio con la cabecera `Content-Type`. Puede añadir audio con cualquier formato que se pueda utilizar con solicitudes de reconocimiento. Incluya los parámetros `rate`, `channels` y `endianness` con la especificación de los formatos que los requieran. Para obtener más información acerca de los formatos de audio admitidos, consulte [Formatos de audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats).

La especificación `application/octet-stream` para un formato de audio no recibe soporte para los recursos de audio.
{: note}

El ejemplo siguiente del apartado [Adición de audio al modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio) añade un archivo `audio/wav`:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: audio/wav"
--data-binary @audio1.wav
"{url}/v1/acoustic_customizations/{customization_id}/audio/audio1"
```
{: pre}

## Adición de un archivo archivador
{: #addArchiveType}

El medio recomendado para añadir audio a un modelo acústico personalizado es añadir un archivo archivador que incluya varios archivos de audio. Puede añadir los siguientes tipos de archivos archivadores especificando el tipo de archivador con la cabecera de solicitud `Content-Type`:

-   Un archivo **.zip**, especificando `application/zip`
-   Un archivo **.tar.gz**, especificando `application/gzip`

Es posible que también tenga que especificar la cabecera `Contained-Content-Type`, en función del formato de los archivos que está añadiendo:

-   Para los archivos de audio de tipo `audio/basic`, `audio/l16` o `audio/mulaw`, debe utilizar la cabecera `Contained-Content-Type` para especificar el formato de los archivos de audio. Incluya los parámetros `rate`, `channels` y `endianness` donde sea necesario. En este caso, todos los archivos de audio contenidos en el archivo archivador deben tener el mismo formato de audio.
-   Para archivos de audio de todos los demás tipos, puede omitir la cabecera `Contained-Content-Type`. En este caso, los archivos de audio contenidos en el archivo archivador pueden tener cualquiera de los formatos que no aparecen listados en el punto anterior. No es necesario que tengan el mismo formato.

No utilice la cabecera `Contained-Content-Type` cuando añada un recurso de tipo de audio.
{: note}

El nombre de un archivo de audio que esté incluido en un recurso de tipo archivador puede incluir 128 caracteres como máximo. Aquí se incluye la extensión del archivo y todos los elementos del nombre (por ejemplo, barras inclinadas).

El siguiente ejemplo del apartado [Adición de audio al modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio) añade un archivo `application/zip` que contiene archivos de audio en formato `audio/l16` que se han muestreado a 16 kHz:

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/zip"
--header "Contained-Content-Type: audio/l16;rate=16000"
--data-binary @audio2.zip
"{url}/v1/acoustic_customizations/{customization_id}/audio/audio2"
```
{: pre}

## Directrices para añadir recursos de audio
{: #audioGuidelines}

La mejora en la precisión del reconocimiento que se puede esperar de utilizar un modelo acústico personalizado depende de una serie de factores. Estos factores incluyen la cantidad de datos de audio que contiene el modelo acústico personalizado y el grado de similitud entre dichos datos y el audio que se está transcribiendo. La mejora también depende de si el modelo acústico personalizado se entrena con un modelo de lenguaje personalizado correspondiente.

Siga estas directrices cuando añada recursos de audio a un modelo acústico personalizado:

-   Añada al menos 10 minutos y no más de 200 horas de audio a un modelo acústico personalizado. El audio debe incluir voz, no silencio.

    La calidad del audio marca la diferencia cuando se determina la cantidad que hay que añadir. Cuanto mejor refleje el audio del modelo las características del audio que se va a reconocer, mejor será la calidad del modelo personalizado para el reconocimiento de voz. Si el audio es de buena calidad, la adición de más audio puede mejorar la precisión de la transcripción. Pero añadir incluso de cinco a diez horas de audio de buena calidad puede marcar una diferencia positiva.
-   Añada recursos de audio que no tengan más de 100 MB. Todos los recursos de tipo de audio y archivador están limitados a un tamaño máximo de 100 MB.

    Para maximizar la cantidad de audio que puede añadir con un solo recurso, tenga en cuenta la posibilidad de utilizar un formato de audio que permita compresión. Para obtener más información, consulte [Límites de datos y compresión](/docs/services/speech-to-text-data?topic=speech-to-text-data-audio-formats#limits).
-   Divida los archivos de audio grandes en varios archivos más pequeños. Asegúrese de dividir el audio entre palabras en puntos de silencio.

    Como es posible enviar varias solicitudes simultáneas para añadir diferentes recursos de audio, puede añadir archivos más pequeños a la vez. Este método en paralelo para añadir recursos de audio puede acelerar el análisis del servicio de su audio.
-   Añadir contenido de audio que refleje las condiciones del canal acústico del audio que tiene previsto transcribir. Por ejemplo, si la aplicación maneja audio que tiene ruido de fondo de un vehículo en movimiento, utilice el mismo tipo de datos para crear el modelo personalizado.
-   Asegúrese de que la frecuencia de muestreo de un archivo de audio coincide con la frecuencia de muestreo del modelo base para el modelo acústico personalizado:
    -   Para los modelos de banda ancha, la frecuencia de muestreo debe ser al menos de 16 kHz (16.000 muestras por segundo).
    -   Para los modelos de banda estrecha, la frecuencia de muestreo debe ser al menos de 8 kHz (8000 muestras por segundo).

    Si la frecuencia de muestreo del audio es superior a la frecuencia de muestreo mínima necesaria, el servicio reduce las muestras de audio hasta la frecuencia adecuada. Si la frecuencia de muestreo del audio es inferior a la frecuencia mínima necesaria, el servicio etiqueta el archivo de audio como `invalid` (no válido). Si algún archivo de audio contenido en un archivo archivador no es válido, el servicio considera que todo el archivador no es válido.
-   Cree un modelo de lenguaje personalizado para utilizarlo con el modelo acústico personalizado en los casos siguientes:
    -   Si el audio dura menos de una hora, cree un modelo de lenguaje personalizado basado en transcripciones del audio para conseguir mejores resultados.
    -   Si el audio es específico de un dominio y contiene palabras que no están en el vocabulario base del servicio, utilice la personalización del modelo de lenguaje para ampliar el vocabulario base del servicio. La personalización del modelo acústico por sí sola no puede generar estas palabras durante la transcripción.

    Para obtener más información, consulte [Utilización conjunta del modelo acústico personalizado y modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-useBoth).
