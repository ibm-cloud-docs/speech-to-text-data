---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

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

# Notas del release
{: #release-notes}

Están disponibles las versiones siguientes de {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. La información incluye funciones y cambios nuevos para cada versión del producto y para las limitaciones conocidas.
{: shortdesc}

## Limitaciones conocidas
{: #limitations}

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} no tiene ninguna limitación conocida.

## Versión 1.0.0 (junio de 2019)
{: #v100}

El release inicial del servicio. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} se basa en el servicio {{site.data.keyword.speechtotextfull}} en {{site.data.keyword.cloud_notm}} público. Para obtener más información sobre el servicio público, consulte
[Acerca de {{site.data.keyword.speechtotextshort}}](https://{DomainName}/docs/services/speech-to-text?topic=speech-to-text-about#about){: external}.

{{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} difiere del servicio público de {{site.data.keyword.speechtotextshort}} en lo que se indica a continuación. Es posible que encuentre útil esta información si está familiarizado con el servicio de {{site.data.keyword.speechtotextshort}} en {{site.data.keyword.cloud_notm}} público.

-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} utiliza señales de acceso para la autenticación. Para obtener más información, consulte [Cómo realizar solicitudes al servicio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) y la [Referencia de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   Los puntos finales de {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} son específicos del clúster de {{site.data.keyword.icp4dfull_notm}}. Para obtener más información, consulte [Cómo realizar solicitudes al servicio](/docs/services/speech-to-text-data?topic=speech-to-text-data-making-requests) y la [Referencia de API](https://{DomainName}/apidocs/speech-to-text-data){: external}.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} no efectúa ningún registro de solicitudes. No es necesario que utilice la cabecera de solicitud `X-Watson-Learning-Opt-Out`.
-   {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} no da soporte a señales Watson. No puede utilizar la cabecera de solicitud `X-Watson-Authorization-Token` para autenticarse con el servicio.
