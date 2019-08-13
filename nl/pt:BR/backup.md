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

# Backup e restauração
{: #backup}

Para se recuperar de possíveis desastres, deve-se fazer backup e estar preparado para restaurar o {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}}. Você é responsável por entender sua configuração, customização e uso do serviço. Você também é responsável por estar preparado para recriar uma instância do serviço e para restaurar seus dados.
{: shortdesc}

A recuperação de desastre poderá se tornar um problema se sua solução de nuvem tiver uma falha significativa que inclua a perda potencial de dados. No caso de perda de dados, é necessário restaurar os seus dados para fazer com que a instância de serviço volte para seu estado mais recente.

Para o serviço {{site.data.keyword.speechtotextshort}}, os dados para modelos de idioma customizados, modelos acústicos customizados e solicitações de reconhecimento de voz assíncrona são armazenados na nuvem. Seu plano de recuperação de desastre inclui saber, preservar e estar preparado para restaurar esses dados.

Recriar modelos customizados, especialmente modelos acústicos customizados, por meio de dados salvos pode levar um período de tempo significativo. A manutenção das configurações de serviços paralelos pode eliminar o tempo de retorno associado à recuperação de desastre.
{: note}

### Recuperação de desastre para modelos de idioma customizados
{: #disaster-recovery-language}

Para modelos de idioma customizados, é necessário manter e estar preparado para recriar e restaurar seus modelos de idioma customizados e sua corpora, gramáticas e palavras customizadas. Também é necessário estar preparado para retreinar seus modelos de idioma customizados em seus dados e recursos de palavras.

#### Fazendo backup de modelos de idioma customizados
{: #disaster-recovery-language-backup}

Preserve as informações a seguir sobre os modelos de idioma customizados:

-   Uma lista de todos os seus modelos de idioma customizados e suas definições. Para listar informações sobre seus modelos customizados:
    -   Use o método `GET /v1/customizations` para listar informações sobre todos os modelos customizados.
    -   Use o método `GET /v1/customizations/{customization_id}` para listar informações sobre um modelo customizado especificado.

    Para obter mais informações, consulte [Listando modelos de idioma customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language).
-   Copia todos os arquivos de texto do corpus que você inclui em seus modelos de idiomas customizados. Para listar informações sobre os corpora para seus modelos customizados:
    -   Use o método `GET /v1/customizations/{customization_id}/corpora` para listar todos os corpora para um modelo customizado.
    -   Use o método `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` para listar informações sobre um corpus especificado para um modelo customizado.

    Para obter mais informações, consulte [Listando os corpora para um modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora).
-   Cópias de todos os arquivos de gramática que você inclui em seus modelos de idioma customizados. Para listar informações sobre as gramáticas para seus modelos customizados:
    -   Use o método `GET /v1/customizations/{customization_id}/grammars` para listar informações sobre todas as gramáticas para um modelo customizado.
    -   Use o método `GET /v1/customizations/{customization_id}/grammars/{grammar_name}` para listar informações sobre uma gramática especificada para um modelo customizado.

    Para obter mais informações, consulte [Listando gramáticas para um modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageGrammars#listGrammars).
-   Informações sobre todas as palavras customizadas, incluindo suas definições de pronúncia e exibição, que você inclui diretamente em seus modelos de idioma customizados. Para listar informações sobre as palavras fora do vocabulário (OOV) para os modelos customizados:
    -   Use o método `GET /v1/customizations/{customization_id}/words` para listar informações sobre as palavras de um modelo customizado. É possível usar o parâmetro `word_type` para listar `all` as palavras de um modelo, as palavras incluídas diretamente pelo `user`, as palavras extraídas dos `corpora` ou as palavras reconhecidas pelas `grammars`.
    -   Use o método `GET /v1/customizations/{customization_id}/words/{word_name}` para listar informações sobre uma palavra especificada de um modelo customizado.

    Para obter mais informações, consulte [Listando palavras de um modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords).

É uma melhor prática preservar essas informações em um formato que pode ser usado para recriar os modelos de idioma customizados no caso de uma falha. Manter ativamente as informações sobre seus modelos customizados e seus dados e preparar as chamadas listadas na seção a seguir antecipadamente, pode permitir que você se recupere o mais rapidamente possível.

#### Restaurando modelos de idioma customizados
{: #disaster-recovery-language-restore}

Se você precisar se recuperar de um desastre, será possível usar as informações de backup para recriar seus modelos de idioma customizados e seus dados:

1.  Para recriar seus modelos de idioma customizados, use o método `POST /v1/customizations`. Para obter mais informações, consulte [Criar um modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language).
1.  Para incluir os arquivos de texto do corpus em seus modelos customizados, use o método `POST /v1/customizations/{customization_id}/corpora/{corpus_name}`. Para obter mais informações, consulte [Incluir um corpus no modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addCorpus).
1.  Para incluir os arquivos de gramática em seus modelos customizados, use o método `POST /v1/customizations/{customization_id}/grammars/{grammar_name}`. Para obter mais informações, consulte [Incluir uma gramática no modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar).
1.  Para incluir múltiplas palavras em seus modelos customizados, use o método `POST /v1/customizations/{customization_id}/words`. Para incluir palavras únicas em seus modelos customizados, use o método `PUT /v1/customizations/{customization_id}/words/{word_name}`. Para obter mais informações, consulte [Incluir palavras no modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addWords).
1.  Para treinar seus modelos customizados assim que você restaurar seus corpora, gramáticas e palavras customizadas, use o método `POST /v1/customizations/{customization_id}/train`. Para obter mais informações, consulte [Treinar o modelo de idioma customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language).

Os métodos que você usa para incluir corpora, gramáticas e palavras e para treinar um modelo de idioma customizado são assíncronos. É necessário monitorar as solicitações até que elas sejam concluídas.

É possível incluir dados e treinar seus modelos de idioma customizados de forma incremental em vez de incluir todos os dados antes de treinar os modelos. Por exemplo, é possível incluir seu corpus e, em seguida, treinar seus modelos antes de incluir gramáticas e palavras individuais. Também é possível incluir e treinar incrementalmente seus modelos em arquivos de texto de corpus individuais, arquivos de gramática e grupos de palavras customizadas.

### Recuperação de desastre para modelos acústicos customizados
{: #disaster-recovery-acoustic}

Para modelos acústicos customizados, é necessário manter e estar preparado para recriar e restaurar seus modelos acústicos customizados e seus recursos de áudio. Também é necessário estar preparado para retreinar seus modelos acústicos customizados em seus recursos de áudio.

#### Fazendo backup de modelos acústicos customizados
{: #disaster-recovery-acoustic-backup}

Preserve as informações a seguir sobre seus modelos acústicos customizados:

-   Uma lista de todos os seus modelos acústicos customizados e suas definições. Para listar informações sobre seus modelos customizados:
    -   Use o método `GET /v1/acoustic_customizations` para listar informações sobre todos os modelos customizados.
    -   Use o método `GET /v1/acoustic_customizations/{customization_id}` para listar informações sobre um modelo customizado especificado.

    Para obter mais informações, consulte [Listando modelos acústicos customizados](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic).
-   Cópias de todos os recursos de áudio, tanto os arquivos de áudio individuais quanto os archives, que você inclui em seus modelos acústicos customizados. Para listar informações sobre os recursos de áudio para seus modelos customizados:
    -   Use o método `GET /v1/acoustic_customizations/{customization_id}/audio` para listar informações sobre todos os recursos de áudio para um modelo customizado.
    -   Use o método `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` para listar informações sobre um recurso de áudio especificado para um modelo customizado.

    Para obter mais informações, consulte [Listando recursos de áudio para um modelo acústico customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio).

É uma melhor prática preservar essas informações em um formato que pode ser usado para recriar seus modelos acústicos customizados no caso de uma falha. Manter ativamente as informações sobre os seus modelos customizados e seus recursos de áudio e preparar as chamadas listadas na seção a seguir antecipadamente, pode permitir que você se recupere o mais rapidamente possível.

#### Restaurando modelos acústicos customizados
{: #disaster-recovery-acoustic-restore}

Se você precisar se recuperar de um desastre, será possível usar as informações de backup para recriar seus modelos acústicos customizados e seus dados:

1.  Para recriar seus modelos acústicos customizados, use o método `POST /v1/acoustic_customizations`. Para obter mais informações, consulte [Criar um modelo acústico customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic).
1.  Para incluir os recursos de áudio em seus modelos customizados, use o método `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}`. Para obter mais informações, consulte [Incluir áudio no modelo acústico customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio).
1.  Para treinar seus modelos customizados assim que você restaurar seus recursos de áudio, use o método `POST /v1/acoustic_customizations/{customization_id}/train`. Para obter mais informações, consulte [Treinar o modelo acústico customizado](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic).

Os métodos que você usa para incluir recursos de áudio e para treinar um modelo acústico customizado são assíncronos. É necessário monitorar as solicitações até que elas sejam concluídas.

É possível incluir os recursos de áudio e treinar seus modelos acústicos customizados de maneira incremental em vez de incluir todos os dados antes de treinar os modelos. Por exemplo, é possível incluir os recursos de áudio um de cada vez ou em grupos, treinando seus modelos em subconjuntos de recursos de áudio em vez de em todo o áudio de uma vez.

### Recuperação de desastre para tarefas de reconhecimento de voz assíncronas
{: #disaster-recovery-async}

Para reconhecimento de voz com a interface de HTTP assíncrona, é necessário manter as informações a seguir:

-   Todas as URLs de retorno de chamada que você insere na lista de desbloqueio para uso com a interface assíncrona. Se ocorrer uma falha, talvez seja necessário usar o método `POST /v1/register_callback` para registrar novamente as URLs. O método retornará uma resposta apropriada se uma URL já estiver na lista de desbloqueio.
-   Cópias dos arquivos de áudio que você envia para a interface assíncrona para reconhecimento de voz. Se ocorrer uma falha antes de você receber ou recuperar os resultados de uma tarefa assíncrona concluída, será necessário usar o método `POST /v1/recognitions` para reenviar os arquivos de áudio quando o serviço for restaurado. Quando você tiver os resultados de uma tarefa assíncrona concluída, não será mais necessário manter os arquivos de áudio.

Para obter mais informações, consulte [A interface de HTTP assíncrona](/docs/services/speech-to-text-data?topic=speech-to-text-data-async). Assim como ocorre com os dados de backup para modelos customizados, é possível preservar ativamente essas informações e estar preparado para emitir novamente as solicitações necessárias antecipadamente.
