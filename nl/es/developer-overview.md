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

# Visión general para los desarrolladores
{: #developerOverview}

Puede acceder a las prestaciones de {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} mediante una interfaz WebSocket y mediante las interfaces HTTP REST (Representational State Transfer) síncronas o asíncronas. También puede personalizar los modelos de lenguaje del servicio para que se ajusten a su dominio y entorno. Dispone de SDK para simplificar el desarrollo de aplicaciones en muchos lenguajes de programación.
{: shortdesc}

Se efectúa la autenticación en el servicio de {{site.data.keyword.speechtotextshort}} pasando un señal de acceso con cada solicitud. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} es una solución en la nube de multiarrendatario. Sus credenciales proporcionan acceso solamente a los datos y los datos están aislados de otros usuarios.

## Programación con el servicio
{: #programming}

El apartado sobre [Cómo realizar una solicitud de reconocimiento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request) le muestra cómo solicitar una transcripción básica con cada una de las interfaces de programación del servicio:

-   [La interfaz WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) ofrece una implementación eficiente, de baja latencia y de alto rendimiento a través de una conexión dúplex completa.
-   [La interfaz HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) proporciona una interfaz básica para transcribir el audio con solicitudes de bloqueo.
-   [La interfaz HTTP asíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) proporciona una interfaz de no bloqueo que le permite registrar un URL de devolución de llamada para recibir notificaciones o para sondear el servicio para ver el estado y los resultados del trabajo.

Las interfaces ofrecen funciones similares de reconocimiento de voz, pero puede especificar el mismo parámetro como una cabecera de solicitud, un parámetro de consulta o un parámetro de un objeto JSON, en función de la interfaz que utilice.

Las interfaces WebSocket y HTTP síncrona aceptan un máximo de 100 MB de datos de audio con una sola solicitud. La interfaz HTTP asíncrona acepta un máximo de 1 GB de datos de audio con una solicitud.

-   Para obtener más información sobre cómo realizar solicitudes con cada una de las interfaces de {{site.data.keyword.speechtotextshort}}, consulte [Cómo realizar solicitudes al servicio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests).
-   Para ver ejemplos de solicitudes básicas de reconocimiento de voz con cada una de las interfaces del servicio, consulte [Cómo realizar una solicitud de reconocimiento](/docs/services/speech-to-text-data?topic=speech-to-text-data-basic-request).
-   Para ver descripciones de todos los parámetros de reconocimiento de voz disponibles, consulte el [Resumen de parámetros](/docs/services/speech-to-text-data?topic=speech-to-text-data-summary).
-   Para ver descripciones de todos los métodos y sus parámetros, junto con ejemplos, consulte la [Referencia de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.

## Ventajas de la interfaz WebSocket
{: #advantages}

La interfaz WebSocket ofrece varias ventajas sobre la interfaz HTTP:

-   La interfaz WebSocket proporciona un canal de comunicación de un solo socket y dúplex completo. La interfaz permite que el cliente envíe solicitudes y audio al servicio y reciba resultados a través de una sola conexión en forma asíncrona.
-   Proporciona una experiencia de programación mucho más sencilla y potente. El servicio envía respuestas controladas por sucesos a los mensajes del cliente, eliminando la necesidad de que el cliente sondee el servidor.
-   Le permite establecer y utilizar una sola conexión autenticada de forma indefinida. Las interfaces HTTP requieren que autentique cada llamada al servicio.
-   Reduce la latencia. Los resultados de reconocimiento llegan más rápido porque el servicio los envía directamente al cliente. La interfaz HTTP requiere cuatro solicitudes y conexiones distintas para lograr los mismos resultados.
-   Reduce la utilización de la red. El protocolo WebSocket es ligero. Solo requiere una única conexión para realizar el reconocimiento de voz en directo.
-   Permite que el audio se transmita directamente desde navegadores (clientes de WebSocket HTML5) al servicio.

## Personalización del servicio
{: #customizing}

[La interfaz de personalización](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization) le permite crear modelos personalizados para mejorar las prestaciones de reconocimiento de voz del servicio:

-   Los [modelos de lenguaje personalizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate) le permite definir palabras específicas del dominio para un modelo base. Los modelos de lenguaje personalizado amplían el vocabulario base del servicio con terminología específica de dominios, como la medicina y el ámbito legal.
-   Los [modelos acústicos personalizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic) le permiten adaptar un modelo base a las características acústicas de su entorno y de los oradores. Los modelos acústicos personalizados mejoran la capacidad del servicio de reconocer voz con características acústicas específicas.
-   La [Gramática](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammars) le permite restringir las frases que el servicio puede reconocer a las definidas en las reglas de la gramática. Al limitar el espacio de búsqueda de series válidas, el servicio puede ofrecer resultados más rápido y con mayor precisión. Las gramáticas reciben soporte con modelos de lenguaje personalizados.

Puede utilizar un modelo de lenguaje personalizado, un modelo acústico personalizado o ambos para el reconocimiento de voz con cualquiera de las interfaces del servicio.

## Obtención de métricas
{: #overview-metrics}

El servicio ofrece dos tipos de métricas opcionales para solicitudes de reconocimiento de voz:

-   Las [métricas de proceso](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#processing_metrics) proporcionan información de temporización detallada sobre el análisis del servicio del audio de entrada. El servicio devuelve las métricas a intervalos específicos y con sucesos de transcripción como, por ejemplo, resultados provisionales y finales. Puede utilizar las métricas para medir el progreso de servicio transcribiendo el audio.
-   Las [métricas de audio](/docs/services/speech-to-text-data?topic=speech-to-text-data-metrics#audio_metrics) proporcionan información detallada sobre las características de señal del audio de entrada. Los resultados proporcionan métricas de agregación para todo el audio de entrada en la conclusión del proceso de habla. Puede utilizar las métricas para determinar las características y la calidad del audio.

Puede solicitar métricas de proceso con las interfaces WebSocket y HTTP asíncrona. Puede solicitar métricas de audio con cualquiera de las interfaces del servicio. De forma predeterminada, el servicio no devuelve ninguna métrica.

## Soporte de CORS
{: #cors}

El servicio da soporte a CORS (Cross-Origin Resource Sharing). Con el uso de CORS, las páginas web pueden solicitar recursos directamente desde un dominio externo. CORS elude la política de seguridad de mismo origen, que de otro modo impediría tales solicitudes. Puesto que el servicio da soporte a CORS, una página web puede comunicarse directamente con el servicio sin pasar la solicitud a través del servidor web que aloja la página.

Por ejemplo, una página web que se carga desde un servidor en {{site.data.keyword.cloud}} puede llamar directamente a la API de personalización, pasando por alto el servidor de {{site.data.keyword.cloud_notm}}. Para obtener más información, consulte [enable-cors.org](https://enable-cors.org/){: external}.

## Utilización de kits de desarrollo de software (SDK)
{: #sdks}

Dispone de SDK para el servicio {{site.data.keyword.speechtotextshort}}, que simplifican el desarrollo de aplicaciones de voz. Los SDK de {{site.data.keyword.ibmwatson}} están disponibles para muchos lenguajes de programación y plataformas ampliamente utilizados.

-   Para ver una lista completa de los SDK y los enlaces a los SDK de GitHub, consulte [Utilización de SDK](/docs/services/watson?topic=watson-using-sdks).
-   Para obtener información detallada sobre todos los métodos de los SDK de Node, Java&trade;, Python, Ruby y Go para el servicio {{site.data.keyword.speechtotextshort}}, consulte la [Referencia de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
