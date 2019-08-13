---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-24"

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

# Usando gramáticas com modelos de idioma customizados
{: #grammars}

O {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} suporta o uso de gramática com modelos de idioma customizados. É possível incluir gramáticas em um modelo de idioma customizado e usá-las para reconhecimento de voz. Gramáticas restringem o conjunto de frases que o serviço pode reconhecer do áudio.
{: shortdesc}

Uma gramática usa uma especificação de idioma formal para definir um conjunto de regras de produção para as sequências de transcrição. As regras especificam como formar sequências válidas por meio do alfabeto do idioma. Quando você aplica uma gramática ao reconhecimento de voz, o serviço pode retornar apenas uma ou mais frases que são geradas pela gramática.

Por exemplo, quando você precisa reconhecer palavras ou frases específicas, como *sim* ou *não*, letras ou números individuais, ou uma lista de nomes, usar gramáticas pode ser mais eficiente do que examinar palavras e transcrições alternativas. Além disso, ao limitar o espaço de procura para sequências válidas, o serviço pode entregar resultados mais rapidamente e com mais precisão.

Quando você usa um modelo de idioma customizado e uma gramática para reconhecimento de voz, o serviço pode retornar uma frase válida da gramática ou um resultado vazio. Se o resultado não estiver vazio, o serviço incluirá uma pontuação de confiança com a transcrição final, como ele faz para todas as solicitações de reconhecimento. Para as gramáticas, a pontuação indica a probabilidade de que a resposta correspondeu à gramática. Falsos positivos são sempre possíveis, especialmente para gramáticas simples, portanto, deve-se sempre considerar a confiança dos resultados do serviço ao avaliar sua resposta.

O recurso de gramáticas é funcionalidade beta. O serviço suporta as gramáticas para todos os idiomas para os quais ele suporta a customização do modelo de idioma. Para obter mais informações, consulte [Suporte ao idioma para customização](/docs/services/speech-to-text-data?topic=speech-to-text-data-customization#languageSupport).
{: note}

## Formatos de gramática suportados
{: #grammarFormats}

O serviço {{site.data.keyword.speechtotextshort}} suporta gramáticas que são definidas nos formatos padrão a seguir:

-   *Augmented Backus-Naur Form (ABNF)*, que usa uma representação de texto simples que é semelhante à gramática BNF tradicional. O tipo de mídia para esse formato é `application/srgs`.
-   *Formulário XML*, que usa elementos XML para representar a gramática. O tipo de mídia para esse formato é `application/srgs+xml`.

Os dois formatos de gramática têm o poder expressivo de uma gramática com contexto livre (CFG). No entanto, o serviço pode decodificar apenas as gramáticas regulares do tipo 3 na hierarquia Chomsky. Essas gramáticas representam a automata do estado finito.

Para obter informações gerais sobre gramáticas, consulte as páginas da Wikipédia a seguir:

-   [Speech Recognition Grammar Specification](https://wikipedia.org/wiki/Speech_Recognition_Grammar_Specification){: external}
-   [Formulário Backus-Naur aumentado](https://wikipedia.org/wiki/Augmented_Backus%E2%80%93Naur_form){: external}
-   [Hierarquia Chomsky](https://wikipedia.org/wiki/Chomsky_hierarchy){: external}

## A Speech Recognition Grammar Specification
{: #grammarSpecification}

O serviço {{site.data.keyword.speechtotextshort}} suporta gramáticas, conforme definido pelo W3C [Speech Recognition Grammar Specification Versão 1.0](https://www.w3.org/TR/speech-grammar/){: external}. A especificação fornece informações detalhadas sobre os formatos suportados e sobre como definir uma gramática. Para obter informações sobre os tipos de mídia suportados, consulte [Apêndice G. Tipos de mídia e sufixo de arquivo](https://www.w3.org/TR/speech-grammar/#AppG){: external} da especificação.

O serviço *não* suporta atualmente todos os recursos da Speech Recognition Grammar Specification. Especificamente, o serviço não suporta os recursos descritos nas seções a seguir da especificação:

-   [Seção 1.4 Interpretação de semântica](https://www.w3.org/TR/speech-grammar/#S1.4){: external}. O{{site.data.keyword.IBM_notm}} está trabalhando para suportar esse recurso em uma liberação futura do serviço.
-   [Seção 1.5 Gramáticas integradas](https://www.w3.org/TR/speech-grammar/#S1.5){: external}. O{{site.data.keyword.IBM_notm}} está trabalhando para suportar esse recurso em uma liberação futura do serviço.
-   [Seção 2.2.2 Referência externa por URI](https://www.w3.org/TR/speech-grammar/#S2.2.2){: external}. O serviço suporta apenas referências locais, conforme descrito na [Seção 2.2.1 Referências locais](https://www.w3.org/TR/speech-grammar/#S2.2.1){: external}. Em outras palavras, uma gramática deve ser autocontida.
-   [Seção 2.2.3 Regras especiais](https://www.w3.org/TR/speech-grammar/#S2.2.3){: external}.
-   [Seção 2.2.4 Referenciando documentos de N-gram (Informativo)](https://www.w3.org/TR/speech-grammar/#S2.2.4){: external}.
-   [Seção 2.7 Idioma](https://www.w3.org/TR/speech-grammar/#S2.7){: external}. O serviço não suporta a comutação de idioma. O serviço suporta apenas um idioma global por gramática.

Palavras na gramática devem estar na codificação UTF-8 (ASCII é um subconjunto de UTF-8). Usar qualquer outra codificação pode levar a problemas ao compilar a gramática ou resultados inesperados na decodificação. O serviço ignora uma codificação especificada no cabeçalho da gramática.
{: note}
