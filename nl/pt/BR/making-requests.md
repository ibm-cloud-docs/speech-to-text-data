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

# Fazendo solicitações para o serviço
{: #making-requests}

Para fazer solicitações autenticadas para o {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}, provisione uma instância do serviço e obtenha credenciais. Use uma URL diferente para as interfaces de HTTP e de WebSocket do serviço. Se você usar um certificado autoassinado, será necessário desativar a verificação de SSL de solicitações para o serviço.
{: shortdesc}

## Provisionando uma instância e obtendo credenciais
{: #making-requests-provisioning}

Antes de usar o serviço {{site.data.keyword.speechtotextshort}}, deve-se provisionar uma instância do serviço e obter suas credenciais. Para obter mais informações, consulte [Antes de iniciar](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#before-you-begin). Na última etapa desse procedimento, copie o `{token}` e a `{URL}` para sua instância de serviço:

-   O `{token}` fornece seu token de acesso para autenticar o serviço. É possível usar o token de acesso exibido no Web client do {{site.data.keyword.icp4dfull_notm}}. No entanto, em um ambiente de produção, use um token gerado programaticamente para sua instância de serviço. Para obter mais informações e exemplos, consulte *Autenticação* na [Referência de API](https://{DomainName}/apidocs/speech-to-text-data#authentication){: external}.

    Você pode se autenticar no serviço {{site.data.keyword.speechtotextshort}} transmitindo seu token de acesso com cada solicitação. O {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} é uma solução de nuvem com diversos locatários. Suas credenciais fornecem acesso somente aos seus dados e seus dados são isolados de outros usuários.
-   A `{URL}` fornece o terminal base usado para chamar métodos do serviço.

A URL contém os componentes a seguir:

```
https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api
```
{: codeblock}

Os valores de variáveis entre `{}` (chaves) fornecem as informações a seguir:

-   `{icp4d_cluster_host}` é o nome ou o endereço IP do host no qual o cluster do {{site.data.keyword.icp4dfull_notm}} é implementado.
-   `{:port}` é o número da porta na qual o serviço atende a solicitações no host especificado. Deve-se preceder o número da porta com `:` (dois pontos).
-   `{release}` é o nome da liberação especificado quando o gráfico do Helm foi instalado.
-   `{instance_id}` é o identificador de sua instância de serviço.

As chaves indicam sequências de variáveis que devem ser substituídas por valores literais. Não inclua as chaves em chamadas reais para o serviço.
{: note}

## Fazendo uma solicitação de HTTP autenticada
{: #httpRequest}

O serviço {{site.data.keyword.speechtotextshort}} oferece duas interfaces de HTTP:

-   A [interface de HTTP síncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) fornece acesso a todas as funcionalidades do serviço, incluindo as interfaces de customização.
-   A [interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) fornece métodos somente para reconhecimento de voz.

Ambas as interfaces de HTTP aceitam solicitações por meio do protocolo HTTP Seguro, que, por sua vez, depende do protocolo Secure Sockets Layer (SSL) (ou Segurança da Camada de Transporte [TLS]). Todas as URLs para solicitações para uma interface de HTTP iniciam com a especificação de protocolo `https`.

Os exemplos nesta documentação usam o comando `curl` para chamar as interfaces de HTTP do serviço. Para obter mais informações, consulte [Usando os exemplos de curl](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#getting-started-curl). O formato básico de uma solicitação de HTTP com `curl` inclui os componentes a seguir:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Os valores de variáveis entre chaves fornecem as informações a seguir:

-   `{http_method}` especifica o método de solicitação de HTTP para o exemplo: `POST`, `PUT`, `GET` ou `DELETE`. O método de solicitação é necessário com `curl` para qualquer coisa diferente de `GET`.
-   `{token}` fornece o token de acesso para sua instância de serviço. Deve-se usar o token de acesso para fazer uma solicitação segura para o serviço.
-   `{method}` é o método do serviço que você está chamando. Por exemplo, use o método `recognize` para fazer uma solicitação de HTTP síncrona para o serviço.

Os valores de variáveis restantes fornecem as informações descritas anteriormente. Muitos métodos têm nomes mais longos e incluem parâmetros de caminho que devem ser especificados como parte da solicitação. A maioria dos exemplos também incluem cabeçalhos de solicitação, parâmetros de consulta e outros valores.

Os exemplos mostram a URL para chamadas para as interfaces de HTTP como `{url}/v1/{method}`. Substitua `{url}` pelos valores recém-descritos.
{: note}

## Fazendo uma solicitação autenticada do WebSocket
{: #websocketRequest}

O serviço {{site.data.keyword.speechtotextshort}} oferece uma [interface do WebSocket](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets) que fornece somente reconhecimento de voz. O serviço aceita solicitações por meio do protocolo WebSocket Secure, que, novamente, depende do protocolo Secure Sockets Layer (SSL) (ou Segurança da Camada de Transporte [TLS]). Todas as URLs para solicitações para a interface do WebSocket iniciam com a especificação do protocolo `wss`.

É possível chamar a interface do WebSocket somente por meio do código do aplicativo. Não é possível chamar a interface do WebSocket por meio da linha de comandos. Estabeleça uma conexão do WebSocket com o serviço no terminal a seguir.

```
wss://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/recognize
```
{: codeblock}

Os valores de variáveis fornecem as informações que foram descritas anteriormente. O token de acesso é passado por meio do parâmetro de consulta `access_token` do método.

Os exemplos mostram a URL para chamadas para a interface do WebSocket como `{ws_url}/v1/recognize`. Substitua `{ws_url}` pelos valores recém-descritos.
{: note}

## Desativando a verificação de SSL
{: #SSLverification}

Todos os serviços do Watson usam SSL (ou TLS) para conexões e comunicações seguras entre o cliente e o servidor. A conexão é verificada com relação ao armazenamento de certificados locais para assegurar autenticação, integridade e confidencialidade.

O {{site.data.keyword.icp4dfull_notm}} instala um certificado autoassinado. Esse certificado não pode ser verificado com êxito por padrão. É possível executar um dos procedimentos a seguir para se conectar com êxito a uma instância de serviço:

-   Incluir o certificado autoassinado no armazenamento confiável para seu agente do usuário.

    Por exemplo, para fazer solicitações seguras com `curl`, inclua o certificado no armazenamento confiável para `curl`. Para fazer solicitações seguras por meio do navegador, inclua o certificado no armazenamento confiável do navegador.
-   Desativar a verificação de SSL.

    A desativação da verificação de SSL compromete a segurança da conexão e dos dados. É altamente desaconselhável. Desative o SSL apenas se for absolutamente necessário e execute as etapas para ativá-lo assim que possível.
    {: important}

    -   Para desativar a verificação de SSL para uma solicitação `curl`, use a opção `--insecure` (`-k`) com a solicitação. Essa opção direciona o comando para efetuar bypass da verificação de certificados SSL da ferramenta.
    -   Para desativar a verificação de SSL para uma solicitação do WebSocket, use a abordagem apropriada para sua biblioteca do cliente ou use um dos SDKs de {{site.data.keyword.speechtotextshort}} do {{site.data.keyword.ibmwatson}}.

Para obter mais informações sobre como desativar a verificação de SSL de chamadas para o serviço, consulte *Desativando a verificação de SSL* na [Referência de API](https://{DomainName}/apidocs/speech-to-text-data#disabling-ssl){: external}. As informações incluem exemplos para `curl` e para todos os SDKs.
