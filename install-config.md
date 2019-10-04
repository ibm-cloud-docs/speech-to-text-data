---

copyright:
  years: 2018, 2019
lastupdated: "2019-10-03"

subcollection: speech-to-text-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:gif: data-image-type='gif'}

# Installing the service
{: #install}

Use this installation method to install {{site.data.keyword.texttospeechdatafull}} if you do not have an {{site.data.keyword.icp4dfull}} cluster. These instructions describe how to install {{site.data.keyword.icp4dfull}} as a stand-alone deployment or as a Red Hat Openshift V3.11 deployment. You then install {{site.data.keyword.speechtotextshort}} to the deployment as an add-on.
{: shortdesc}

## Installation
{: #installation-pointer}

To install and configure {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, see [Installing the Watson Speech to Text add-on](https://www.ibm.com/support/producthub/icpdata/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/watson/speech-to-text-install.html){: external}.

## Application details
{: #app-details}

### Microservices
{: #microservices}

Microservices are individual components that together comprise a service. {{site.data.keyword.speechtotextshort}} consists of the following microservices:

  - **sttRuntime**: The {{site.data.keyword.speechtotextshort}} runtime.
  - **sttAMPatcher**: The {{site.data.keyword.speechtotextshort}} acoustic model (AM) patcher.
  - **sttCustomization**: Enables {{site.data.keyword.speechtotextshort}} customization.
  - **sttAsync**: Provides asynchronous operation support for {{site.data.keyword.speechtotextshort}}.

In addition to these service-specific microservices, the Helm chart installs the following resources:

  - **PostgreSQL**: Provides storage for customizations and asynchronous operations.
  - **RabbitMQ**: Provides storage for asynchronous operations.
  - **Minio**: Provides storage for the {{site.data.keyword.speechtotextshort}} runtime and AM patcher.
  - **GDPR data deletion**: Enables deletion of specific customer data following a GDPR request as described in [Information security](/docs/speech-to-text-data?topic=information-security).

