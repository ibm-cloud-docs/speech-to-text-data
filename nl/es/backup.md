---

copyright:
  years: 2019
lastupdated: "2019-06-22"

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

# Copia de seguridad y restauración
{: #backup}

Para llevar a cabo una recuperación tras posibles desastres, debe realizar una copia de seguridad y estar preparado para restaurar {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. Usted es el responsable de comprender la configuración, la personalización y el uso del servicio. También es responsable de estar preparado para recrear una instancia del servicio y restaurar sus datos.
{: shortdesc}

La recuperación tras desastre puede convertirse en un problema si su solución en la nube sufre un fallo significativo que incluye la pérdida potencial de datos. En caso de pérdida de datos, deberá que restaurar los datos para devolver la instancia de servicio a su estado más reciente.

Para el servicio {{site.data.keyword.speechtotextshort}}, los datos de modelos de lenguaje personalizados, modelos acústicos personalizados y solicitudes de reconocimiento de voz asíncronas se almacenan en la nube. El plan de recuperación tras desastre incluye el conocimiento, la conservación y la preparación para restaurar estos datos.

La recreación de modelos personalizados, especialmente de modelos acústicos personalizados, a partir de los datos guardados puede tardar bastante tiempo. El mantenimiento de las configuraciones de servicio en paralelo puede eliminar el tiempo de recuperación asociado con la recuperación tras desastre.
{: note}

### Recuperación tras desastre para modelos de lenguaje personalizado
{: #disaster-recovery-language}

En el caso de modelos de lenguaje personalizado, debe mantener y estar preparado para volver a crear y restaurar los modelos de lenguaje personalizado y sus corpus, sus gramáticas y sus palabras personalizadas. También debe estar preparado para volver a entrenar los modelos de lenguaje personalizado con sus recursos de datos y palabras.

#### Copia de seguridad de modelos de lenguaje personalizado
{: #disaster-recovery-language-backup}

Conserve la siguiente información acerca de los modelos de lenguaje personalizado:

-   Una lista de todos los modelos de lenguaje personalizado y sus definiciones. Para ver información acerca de los modelos personalizados:
    -   Utilice el método `GET /v1/customizations` para ver información sobre todos los modelos personalizados.
    -   Utilice el método `GET /v1/customizations/{customization_id}` para ver información sobre un modelo personalizado específico.

    Para obtener más información, consulte [Listado de modelos de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).
-   Copias de todos los archivos de texto del corpus que haya añadido a los modelos de lenguaje personalizado. Para ver información acerca de los corpus de los modelos personalizados:
    -   Utilice el método `GET /v1/customizations/{customization_id}/corpora` para ver una lista de los corpus de un modelo personalizado.
    -   Utilice el método `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` para ver información sobre los corpus especificados para un modelo personalizado.

    Para obtener más información, consulte [Listado de los corpus de un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).
-   Copias de todos los archivos de gramática que haya añadido a los modelos de lenguaje personalizado. Para ver información acerca de las gramáticas de los modelos personalizados:
    -   Utilice el método `GET /v1/customizations/{customization_id}/grammars` para ver información sobre todas las gramáticas de un modelo personalizado.
    -   Utilice el método `GET /v1/customizations/{customization_id}/grammars/{grammar_name}` para ver información sobre una gramática especificada de un modelo personalizado.

    Para obtener más información, consulte [Listado de las gramáticas de un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageGrammars#listGrammars).
-   Información sobre todas las palabras personalizadas, incluidas sus definiciones de pronunciación y de visualización, que se añaden directamente a los modelos de lenguaje personalizados. Para ver información acerca de las palabras no definidas en el vocabulario (OOV) de los modelos personalizados:
    -   Utilice el método `GET /v1/customizations/{customization_id}/words` para ver información sobre las palabras de un modelo personalizado. Puede utilizar el parámetro `word_type` para ver una lista de `todas` las palabras de un modelo, las palabras añadidas directamente por el `usuario`, palabras extraídas del `corpus` o palabras reconocidas por `gramáticas`.
    -   Utilice el método `GET /v1/customizations/{customization_id}/words/{word_name}` para ver información sobre una palabra especificada de un modelo personalizado.

    Para obtener más información, consulte [Listado de las palabras de un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).

Se recomienda conservar esta información en un formato que pueda utilizar para recrear los modelos de lenguaje personalizado en el caso de que se produzca un error. El mantenimiento activo de la información sobre los modelos personalizados y sus datos y la preparación de las llamadas que se muestran en la siguiente sección le pueden permitirle recuperarse lo más rápido posible.

#### Restauración de modelos de lenguaje personalizado
{: #disaster-recovery-language-restore}

Si tiene que recuperarse de un desastre, puede utilizar la información de copia de seguridad para volver a crear los modelos de lenguaje personalizado y sus datos:

1.  Para volver a crear los modelos de lenguaje personalizado, utilice el método `POST /v1/customizations`. Para obtener más información, consulte el apartado sobre [Creación de un modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language).
1.  Para añadir los archivos de texto del corpus a los modelos personalizados, utilice el método `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`. Para obtener más información, consulte [Adición de un corpus al modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addCorpus).
1.  Para añadir los archivos de gramática a los modelos personalizados, utilice el método `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`. Para obtener más información, consulte [Adición de una gramática al modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
1.  Para añadir varias palabras a los modelos personalizados, utilice el método `POST /v1/customizations/{customization_id}/words`. Para añadir palabras individuales a los modelos personalizados, utilice el método `PUT /v1/customizations/{customization_id}/words/{word_name}`. Para obtener más información, consulte [Adición de palabras al modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addWords).
1.  Para entrenar los modelos personalizados después de restaurar los corpus, las gramáticas y las palabras personalizadas, utilice el método `POST /v1/customizations/{customization_id}/train`. Para obtener más información, consulte [Entrenamiento del modelo de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language).

Los métodos que se utilizan para añadir corpus, gramáticas y palabras y para entrenar un modelo de lenguaje personalizado son asíncronos. Es necesario que supervise las solicitudes hasta que finalicen.

Puede añadir datos de forma incremental y entrenar los modelos de lenguaje personalizado en lugar de añadir todos los datos antes de entrenar los modelos. Por ejemplo, puede añadir el corpus y luego entrenar el modelo antes de añadir gramáticas y palabras individuales. También puede añadir y entrenar de forma incremental los modelos con archivos de texto de corpus individuales, archivos de gramática y grupos de palabras personalizadas.

### Recuperación tras desastre para modelos de lenguaje personalizado
{: #disaster-recovery-acoustic}

Para los modelos acústicos personalizados, tiene que mantener y estar preparado para volver a crear y restaurar los modelos acústicos personalizados y sus recursos de audio. También tiene que estar preparado para volver a entrenar sus modelos acústicos personalizados con sus recursos de audio.

#### Copia de seguridad de modelos acústicos personalizados
{: #disaster-recovery-acoustic-backup}

Conserve la siguiente información acerca de los modelos acústicos personalizados:

-   Una lista de todos los modelos acústicos personalizados y sus definiciones. Para ver información acerca de los modelos personalizados:
    -   Utilice el método `GET /v1/acoustic_customizations` para ver información sobre todos los modelos personalizados.
    -   Utilice el método `GET /v1/acoustic_customizations/{customization_id}` para ver información sobre un modelo personalizado específico.

    Para obtener más información, consulte [Listado de modelos acústicos personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic).
-   Copias de todos los recursos de audio, tanto archivos de audio individuales como archivos archivadores, que han añadido a los modelos acústicos personalizados. Para ver información acerca de los recursos de audio de los modelos personalizados:
    -   Utilice el método `GET /v1/acoustic_customizations/{customization_id}/audio` para ver información sobre todos los recursos de audio correspondientes a un modelo personalizado.
    -   Utilice el método `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` para ver información sobre un recurso de audio especificado de un modelo personalizado.

    Para obtener más información, consulte [Listado de recursos de audio para un modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

Se recomienda conservar esta información en un formato que pueda utilizar para recrear los modelos acústicos personalizados en el caso de que se produzca un error. El mantenimiento activo de la información sobre los modelos personalizados y sus recursos de audio y la preparación de las llamadas que se muestran en la siguiente sección le pueden permitirle recuperarse lo más rápido posible.

#### Restauración de modelos acústicos personalizados
{: #disaster-recovery-acoustic-restore}

Si tiene que recuperarse de un desastre, puede utilizar la información de copia de seguridad para volver a crear los modelos acústicos personalizados y sus datos:

1.  Para volver a crear los modelos acústicos personalizados, utilice el método `POST /v1/acoustic_customizations`. Para obtener más información, consulte el apartado sobre [Creación de un modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic).
1.  Para añadir recursos de audio a los modelos personalizados, utilice el método `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`. Para obtener más información, consulte [Adición de audio al modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio).
1.  Para entrenar los modelos personalizados después de restaurar los recursos de audio, utilice el método `POST /v1/acoustic_customizations/{customization_id}/train`. Para obtener más información, consulte [Entrenamiento del modelo acústico personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic).

Los métodos que se utilizan para añadir recursos de audio y para entrenar un modelo acústico personalizado son asíncronos. Es necesario que supervise las solicitudes hasta que finalicen.

Puede añadir recursos de audio de forma incremental y entrenar los modelos acústicos personalizados en lugar de añadir todos los datos antes de entrenar los modelos. Por ejemplo, puede añadir recursos de audio de uno en uno o en grupos, entrenando los modelos con subconjuntos de los recursos de audio en lugar de hacerlo con todo el audio a la vez.

### Recuperación tras desastre para trabajos de reconocimiento de voz asíncronos
{: #disaster-recovery-async}

Para el reconocimiento de voz con la interfaz HTTP asíncrona, debe mantener la información siguiente:

-   Todos los URL de devolución de llamada que ha colocado en la lista blanca para utilizarlos con la interfaz asíncrona. Si se produce una anomalía, es posible que tenga que utilizar el método `POST /v1/register_callback` para volver a registrar los URL. El método devuelve una respuesta adecuada si un URL ya está en la lista blanca.
-   Copias de los archivos de audio que envíe a la interfaz asíncrona para el reconocimiento de voz. Si se produce una anomalía antes de recibir o de recuperar los resultados de un trabajo asíncrono completado, tiene que utilizar el método `POST /v1/recognitions` para volver a enviar los archivos de audio cuando se restaure el servicio. Una vez que tenga los resultados de un trabajo asíncrono completado, ya no tendrá que mantener los archivos de audio.

Para obtener más información, consulte [La interfaz HTTP asíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async). Al igual que sucede con los datos de copia de seguridad de los modelos personalizados, puede conservar de forma activa esta información y estar preparado para volver a emitir las solicitudes necesarias por anticipado.
