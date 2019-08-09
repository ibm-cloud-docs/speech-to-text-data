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

# Anforderungen an den Service ausgeben
{: #making-requests}

Um authentifizierte Anforderungen an {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} ausgeben zu können, müssen Sie eine Instanz des Service bereitstellen und Berechtigungsnachweise anfordern. Für die HTTP- und WebSocket-Schnittstellen des Service verwenden Sie eine andere URL. Wenn Sie ein selbst signiertes Zertifikat verwenden, müssen Sie die SSL-Verifizierung für Anforderungen an den Service inaktivieren.
{: shortdesc}

## Instanz bereitstellen und Berechtigungsnachweise anfordern
{: #making-requests-provisioning}

Bevor Sie den {{site.data.keyword.speechtotextshort}}-Service verwenden, müssen Sie eine Instanz des Service bereitstellen und Ihre Berechtigungsnachweise anfordern. Weitere Informationen finden Sie unter [Vorbereitende Schritte](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#before-you-begin). Im letzten Schritt dieser Prozedur kopieren Sie das `{token}` und die `{URL}` für Ihre Serviceinstanz: 

-   Das `{token}` stellt Ihr Zugriffstoken für die Authentifizierung beim Service bereit. Sie können das Zugriffstoken verwenden, das im Web-Client von {{site.data.keyword.icp4dfull_notm}} angezeigt wird. In einer Produktionsumgebung müssen Sie jedoch ein Token verwenden, das Sie programmgesteuert für Ihre Serviceinstanz generieren. Weitere Informationen und Beispiele finden Sie in dem Abschnitt über die *Authentifizierung* in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data#authentication){: external}. 

Für die Authentifizierung beim {{site.data.keyword.speechtotextshort}}-Service übergeben Sie mit jeder Anforderung Ihr Zugriffstoken. {{site.data.keyword.speechtotextshort}} for {{site.data.keyword.icp4dfull_notm}} ist eine Multi-Tenant-Cloudlösung. Mit Ihren Berechtigungsnachweisen ist nur Zugriff auf Ihre Daten möglich, und Ihre Daten werden von anderen Benutzern isoliert.
-   Die `{URL}` stellt den Basisendpunkt bereit, den Sie zum Aufrufen von Methoden des Service verwenden. 

Die URL enthält die folgenden Komponenten: 

```
https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api
```
{: codeblock}

Die Variablenwerte in geschweiften Klammern (`{}`) geben Folgendes an: 

-   `{icp4d_cluster_host}` ist der Name oder die IP-Adresse des Hosts, auf dem Ihr {{site.data.keyword.icp4dfull_notm}}-Cluster implementiert ist. 
-   `{:port}` ist die Portnummer, an der der Service für Anforderungen auf dem angegebenen Host empfangsbereit ist. Sie müssen der Portnummer einen Doppelpunkt (`:`) voranstellen. 
-   `{release}` ist der Releasename, der bei der Installation des Helm-Diagramms angegeben wurde. 
-   `{instance_id}` ist die ID Ihrer Serviceinstanz. 

Die geschweiften Klammern kennzeichnen Variablenzeichenfolgen, die Sie durch Literalwerte ersetzen müssen. In tatsächlichen Aufrufen an den Service dürfen Sie die geschweiften Klammern nicht angeben.
{: note}

## Authentifizierte HTTP-Anforderung ausgeben
{: #httpRequest}

Der {{site.data.keyword.speechtotextshort}}-Service bietet zwei HTTP-Schnittstellen: 

-   Die [synchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-http) ermöglicht den Zugriff auf alle Funktionen des Service, einschließlich Anpassungsschnittstellen. 
-   Die [asynchrone HTTP-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-async) stellt ausschließlich Methoden für die Spracherkennung bereit. 

Beide HTTP-Schnittstellen akzeptieren Anforderungen über das HTTPS-Protokoll, das wiederum auf das SSL-Protokoll (Secure Sockets Layer) oder das TLS-Protokoll (Transport Layer Security) zurückgreift. Alle URLs für Anforderungen an eine HTTP-Schnittstelle beginnen mit der Protokollspezifikation `https`. 

In den Beispielen dieser Dokumentation werden die HTTP-Schnittstellen des Service mit dem Befehl `curl` aufgerufen. Weitere Informationen finden Sie unter [curl-Beispiele verwenden](/docs/services/speech-to-text-data?topic=speech-to-text-data-gettingStarted#getting-started-curl). Das Basisformat einer HTTP-Anforderung mit `curl` besteht aus den folgenden Komponenten: 

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

Die Variablenwerte in geschweiften Klammern geben Folgendes an: 

-   `{http_method}` gibt die HTTP-Anforderungsmethode für das Beispiel an: `POST`, `PUT`, `GET` oder `DELETE`. Mit Ausnahme von `GET` ist die Anforderungsmethode bei `curl` erforderlich. 
-   `{token}` gibt das Zugriffstoken für Ihre Serviceinstanz an. Sie müssen das Zugriffstoken verwenden, um eine sichere Anforderung an den Service auszugeben. 
-   `{method}` ist die Methode des Service, die Sie aufrufen wollen. Zum Beispiel verwenden Sie die Methode `recognize`, um eine synchrone HTTP-Anforderung an den Service auszugeben. 

Die übrigen Variablenwerte geben die Informationen an, die bereits beschrieben wurden. Viele Methoden haben längere Namen und enthalten Pfadparameter, die Sie in der Anforderung angeben müssen. Die meisten Beispiele enthalten darüber hinaus auch Anforderungsheader, Abfrageparameter und andere Werte. 

In den Beispielen wird die URL für Aufrufe der HTTP-Schnittstellen wie folgt dargestellt: `{url}/v1/{method}`. Ersetzen Sie `{url}` durch die gerade beschriebenen Werte.
{: note}

## Authentifizierte WebSocket-Anforderung ausgeben
{: #websocketRequest}

Der {{site.data.keyword.speechtotextshort}}-Service bietet eine [WebSocket-Schnittstelle](/docs/services/speech-to-text-data?topic=speech-to-text-data-websockets), die nur Spracherkennung bereitstellt. Der Service akzeptiert Anforderungen über das WSS-Protokoll (WebSocket Secure), das wiederum auf das SSL-Protokoll (Secure Sockets Layer) oder das TLS-Protokoll (Transport Layer Security) zurückgreift. Alle URLs für Anforderungen an eine WebSocket-Schnittstelle beginnen mit der Protokollspezifikation `wss`. 

Sie können die WebSocket-Schnittstelle nur über den Anwendungscode aufrufen. Sie können die WebSocket-Schnittstelle nicht über die Befehlszeile aufrufen. Sie erstellen eine WebSocket-Verbindung zum Service an dem folgenden Endpunkt. 

```
wss://{icp4d_cluster_host}{:port}/speech-to-text/{release}/instances/{instance_id}/api/v1/recognize
```
{: codeblock}

Die Variablenwerte geben die Informationen an, die bereits beschrieben wurden. Sie übergeben Ihr Zugriffstoken über den Abfrageparameter `access_token` der Methode. 

In den Beispielen wird die URL für Aufrufe der WebSocket-Schnittstelle wie folgt dargestellt: `{ws_url}/v1/recognize`. Ersetzen Sie `{ws_url}` durch die gerade beschriebenen Werte.
{: note}

## SSL-Verifizierung inaktivieren
{: #SSLverification}

Bei allen Watson-Services wird SSL (oder TLS) für sichere Verbindungen und sichere Kommunikation zwischen dem Client und dem Server verwendet. Die Verifizierung der Verbindung erfolgt mithilfe des lokalen Zertifikatsspeichers, um die Authentifizierung, Integrität und Vertraulichkeit zu gewährleisten. 

{{site.data.keyword.icp4dfull_notm}} installiert ein selbst signiertes Zertifikat. Eine erfolgreiche Verifizierung dieses Zertifikats ist nicht ohne Weiteres möglich. Sie können einen der folgenden Schritte ausführen, damit eine Verbindung zu einer Serviceinstanz erfolgreich hergestellt werden kann: 

-   Fügen Sie das selbst signierte Zertifikat dem Truststore für Ihren Benutzeragenten hinzu. 

Sollen beispielsweise sichere Anforderungen mit `curl` ausgegeben werden, fügen Sie das Zertifikat dem Truststore für `curl` hinzu. Sollen sichere Anforderungen über Ihren Browser ausgegeben werden, fügen Sie das Zertifikat dem Truststore für den Browser hinzu.
-   Inaktivieren Sie die SSL-Verifizierung. 

    Durch die Inaktivierung der SSL-Verifizierung wird die Sicherheit der Verbindung und der Daten beeinträchtigt. Es wird ausdrücklich davon abgeraten. SSL darf nur inaktiviert werden, wenn dies unbedingt erforderlich ist. Ergreifen Sie in diesem Fall Maßnahmen, um SSL so bald wie möglich wieder zu aktivieren.
    {: important}

    -   Zur Inaktivierung der SSL-Verifizierung für eine `curl`-Anforderung verwenden Sie die Option `--insecure` (`-k`) in der Anforderung. Diese Option bewirkt, dass der Befehl die Verifizierung von SSL-Zertifikaten durch das Tool umgeht. 
    -   Zur Inaktivierung der SSL-Verifizierung für eine  WebSocket-Anforderung verwenden Sie die entsprechende Methode für Ihre Clientbibliothek oder eines der {{site.data.keyword.ibmwatson}} {{site.data.keyword.speechtotextshort}}-SDKs. 

Weitere Informationen zur Inaktivierung der SSL-Verifizierung für Aufrufe des Service finden Sie in dem Abschnitt über die *Inaktivierung der SSL-Verifizierung* in der [API-Referenz](https://{DomainName}/apidocs/speech-to-text-data#disabling-ssl){: external}. Die Informationen enthalten Beispiele für `curl` und für alle SDKs. 
