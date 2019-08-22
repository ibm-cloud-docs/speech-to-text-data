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

# 백업 및 복원
{: #backup}

잠재적인 재해로부터 복구하려면 백업을 수행하고 {{site.data.keyword.speechtotextdatafull}} for {{site.data.keyword.icp4dfull}} 복원을 준비해야 합니다. 사용자는 서비스의 구성, 사용자 정의 및 사용법을 이해해야 합니다. 또한 서비스 인스턴스를 다시 작성하고 데이터를 복원할 준비가 되어 있어야 합니다.
{: shortdesc}

클라우드 솔루션에서 잠재적인 데이터 손실을 포함하는 중대한 장애가 발생하는 경우 재해 복구가 문제가 될 수 있습니다. 데이터 손실의 경우 서비스 인스턴스를 최신 상태로 되돌리려면 데이터를 복원해야 합니다.

{{site.data.keyword.speechtotextshort}} 서비스의 경우, 사용자 정의 언어 모델, 사용자 정의 음향 모델 및 비동기 음성 인식 요청에 대한 데이터가 클라우드에 저장됩니다. 재해 복구 플랜에는 데이터 파악, 보존 및 복원 준비가 포함됩니다.

저장된 데이터에서 사용자 정의 모델, 특히 사용자 정의 음향 모델을 다시 작성하는 데 상당한 시간이 걸릴 수 있습니다. 병렬 서비스 구성을 유지보수하면 재해 복구와 연관된 소요 시간이 제거될 수 있습니다.
{: note}

### 사용자 정의 언어 모델에 대한 재해 복구
{: #disaster-recovery-language}

사용자 정의 언어 모델의 경우 사용자 정의 언어 모델과 해당 말뭉치, 문법 및 사용자 정의 단어를 유지보수해야 하며 다시 작성하고 복원할 준비가 되어 있어야 합니다. 또한 사용자 정의 언어 모델을 해당 데이터 및 오디오 리소스에 대해 재훈련할 준비가 되어 있어야 합니다.

#### 사용자 정의 언어 모델 백업
{: #disaster-recovery-language-backup}

사용자 정의 언어 모델에 대한 다음 정보를 보존하십시오.

-   모든 사용자 정의 언어 모델 및 해당 정의의 목록. 사용자 정의 모델에 대한 정보를 나열하려면 다음을 수행하십시오.
    -   모든 사용자 정의 모델에 대한 정보를 나열하려면 `GET /v1/customizations` 메소드를 사용하십시오.
    -   지정된 사용자 정의 모델에 대한 정보를 나열하려면 `GET /v1/customizations/{customization_id}` 메소드를 사용하십시오.

자세한 정보는 [사용자 정의 언어 모델 나열](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageLanguageModels#listModels-language)을 참조하십시오.
-   사용자 정의 언어 모델에 추가하는 모든 말뭉치 텍스트 파일의 사본. 사용자 정의 모델의 말뭉치에 대한 정보를 나열하려면 다음을 수행하십시오.
    -   사용자 정의 모델의 모든 말뭉치를 나열하려면 `GET /v1/customizations/{customization_id}/corpora` 메소드를 사용하십시오.
    -   사용자 정의 모델의 지정된 말뭉치에 대한 정보를 나열하려면 `GET /v1/customizations/{customization_id}/corpora/{corpus_name}` 메소드를 사용하십시오.

자세한 정보는 [사용자 정의 언어 모델의 말뭉치 나열](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageCorpora#listCorpora)을 참조하십시오.
-   사용자 정의 언어 모델에 추가하는 모든 문법 파일의 사본. 사용자 정의 모델의 문법에 대한 정보를 나열하려면 다음을 수행하십시오.
    -   사용자 정의 모델의 모든 문법에 대한 정보를 나열하려면 `GET /v1/customizations/{customization_id}/grammars` 메소드를 사용하십시오.
    -   사용자 정의 모델의 지정된 문법에 대한 정보를 나열하려면 `GET /v1/customizations/{customization_id}/grammars/{grammar_name}` 메소드를 사용하십시오.

자세한 정보는 [사용자 정의 언어 모델의 문법 나열](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageGrammars#listGrammars)을 참조하십시오.
-   사용자 정의 언어 모델에 직접 추가하는 모든 사용자 정의 단어에 대한 정보(해당 sounds-like 및 display-as 정의 포함). 사용자 정의 모델의 OOV(Out Of Vocabulary) 단어에 대한 정보를 나열하려면 다음을 수행하십시오.
    -   사용자 정의 모델의 단어에 대한 정보를 나열하려면 `GET /v1/customizations/{customization_id}/words` 메소드를 사용하십시오. `word_type` 매개변수를 사용하여 모델의 모든 단어(`all`), 사용자가 직접 추가한 단어(`user`), 말뭉치에서 추출된 단어(`corpora`) 또는 문법에서 인식된 단어(`grammars`)를 나열할 수 있습니다.
    -   사용자 정의 모델의 지정된 단어에 대한 정보를 나열하려면 `GET /v1/customizations/{customization_id}/words/{word_name}` 메소드를 사용하십시오.

    자세한 정보는 [사용자 정의 언어 모델의 단어 나열](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageWords#listWords)을 참조하십시오.

장애 발생 시 사용자 정의 언어 모델을 다시 작성하는 데 사용할 수 있는 형식으로 이 정보를 보존하는 것이 좋습니다. 사용자 정의 모델 및 해당 데이터에 대한 정보를 적극적으로 유지보수하고 다음 섹션에 나열된 요구사항을 미리 준비하면 가능한 빠르게 복구할 수 있습니다.

#### 사용자 정의 언어 모델 복원
{: #disaster-recovery-language-restore}

재해에서 복구해야 하는 경우 백업 정보를 사용하여 사용자 정의 언어 모델과 해당 데이터를 다시 작성할 수 있습니다.

1.  사용자 정의 언어 모델을 다시 작성하려면 `POST /v1/customizations` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 언어 모델 작성](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#createModel-language)을 참조하십시오.
1.  사용자 정의 모델에 말뭉치 텍스트 파일을 추가하려면 `POST /v1/customizations/{customization_id}/corpora/{corpus_name}` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 언어 모델에 말뭉치 추가](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addCorpus)를 참조하십시오.
1.  사용자 정의 모델에 문법 파일을 추가하려면 `POST /v1/customizations/{customization_id}/grammars/{grammar_name}` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 언어 모델에 문법 추가](/docs/services/speech-to-text-data?topic=speech-to-text-data-grammarAdd#addGrammar)를 참조하십시오.
1.  여러 단어를 사용자 정의 모델에 추가하려면 `POST /v1/customizations/{customization_id}/words` 메소드를 사용하십시오. 단일 단어를 사용자 정의 모델에 추가하려면 `PUT /v1/customizations/{customization_id}/words/{word_name}` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 언어 모델에 단어 추가](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#addWords)를 참조하십시오.
1.  말뭉치, 문법 및 사용자 정의 단어를 복원한 후 사용자 정의 모델을 훈련하려면 `POST /v1/customizations/{customization_id}/train` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 언어 모델 훈련](/docs/services/speech-to-text-data?topic=speech-to-text-data-languageCreate#trainModel-language)을 참조하십시오.

말뭉치, 문법 및 단어를 사용자 정의 언어 모델에 추가하고 사용자 정의 언어 모델을 훈련하는 데 사용하는 메소드는 비동기식입니다. 완료될 때까지 요청을 모니터해야 합니다.

모델을 훈련하기 전에 모든 데이터를 추가하는 대신 증분식으로 모델을 추가하고 사용자 정의 언어 모델을 훈련할 수 있습니다. 예를 들어, 문법 및 개별 단어를 추가하기 전에 말뭉치를 추가한 다음 모델을 훈련할 수 있습니다. 개별 말뭉치 텍스트 파일, 문법 파일 및 사용자 정의 단어 그룹을 증분식으로 추가하고 이에 대해 모델을 훈련할 수도 있습니다.

### 사용자 정의 음향 모델의 재해 복구
{: #disaster-recovery-acoustic}

사용자 정의 음향 모델의 경우 사용자 정의 음향 모델과 해당 오디오 리소스를 유지보수해야 하며 다시 작성하고 복원할 준비가 되어 있어야 합니다. 또한 사용자 정의 음향 모델을 해당 오디오 리소스에 대해 재훈련할 준비가 되어 있어야 합니다.

#### 사용자 정의 음향 모델 백업
{: #disaster-recovery-acoustic-backup}

사용자 정의 음향 모델에 대한 다음 정보를 보존하십시오.

-   모든 사용자 정의 음향 모델 및 해당 정의의 목록. 사용자 정의 모델에 대한 정보를 나열하려면 다음을 수행하십시오.
    -   모든 사용자 정의 모델에 대한 정보를 나열하려면 `GET /v1/acoustic_customizations` 메소드를 사용하십시오.
    -   지정된 사용자 정의 모델에 대한 정보를 나열하려면 `GET /v1/acoustic_customizations/{customization_id}` 메소드를 사용하십시오.

자세한 정보는 [사용자 정의 음향 모델 나열](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAcousticModels#listModels-acoustic)을 참조하십시오.
-   사용자 정의 음향 모델에 추가하는 모든 오디오 리소스(개별 오디오 파일 및 아카이브 파일 모두)의 사본. 사용자 정의 모델의 오디오 리소스에 대한 정보를 나열하려면 다음을 수행하십시오.
    -   사용자 정의 모델의 모든 오디오 리소스에 대한 정보를 나열하려면 `GET /v1/acoustic_customizations/{customization_id}/audio` 메소드를 사용하십시오.
    -   사용자 정의 모델의 지정된 오디오 리소스에 대한 정보를 나열하려면 `GET /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` 메소드를 사용하십시오.

    자세한 정보는 [사용자 정의 음향 모델에 대한 오디오 리소스 나열](/docs/services/speech-to-text-data?topic=speech-to-text-data-manageAudio#listAudio)을 참조하십시오.

장애 발생 시 사용자 정의 음향 모델을 다시 작성하는 데 사용할 수 있는 형식으로 이 정보를 보존하는 것이 좋습니다. 사용자 정의 모델 및 해당 오디오 리소스에 대한 정보를 적극적으로 유지보수하고 다음 섹션에 나열된 요구사항을 미리 준비하면 가능한 빠르게 복구할 수 있습니다.

#### 사용자 정의 음향 모델 복원
{: #disaster-recovery-acoustic-restore}

재해에서 복구해야 하는 경우 백업 정보를 사용하여 사용자 정의 음향 모델과 해당 데이터를 다시 작성할 수 있습니다.

1.  사용자 정의 음향 모델을 다시 작성하려면 `POST /v1/acoustic_customizations` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 음향 모델 작성](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#createModel-acoustic)을 참조하십시오.
1.  사용자 정의 모델에 오디오 리소스를 추가하려면 `POST /v1/acoustic_customizations/{customization_id}/audio/{audio_name}` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 음향 모델에 오디오 추가](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#addAudio)를 참조하십시오.
1.  오디오 리소스를 복원한 후 사용자 정의 모델을 훈련하려면 `POST /v1/acoustic_customizations/{customization_id}/train` 메소드를 사용하십시오. 자세한 정보는 [사용자 정의 음향 모델 훈련](/docs/services/speech-to-text-data?topic=speech-to-text-data-acoustic#trainModel-acoustic)을 참조하십시오.

오디오 리소스를 추가하고 사용자 정의 음향 모델을 훈련하는 데 사용하는 메소드는 비동기식입니다. 완료될 때까지 요청을 모니터해야 합니다.

모델을 훈련하기 전에 모든 데이터를 추가하는 대신 증분식으로 오디오 리소스를 추가하고 사용자 정의 음향 모델을 훈련할 수 있습니다. 예를 들어, 오디오 리소스를 한 번에 하나씩 또는 그룹으로 추가하여 한 번에 모든 오디오에 대해 모델을 훈련하는 대신 오디오 리소스의 서브세트에 대해 훈련할 수 있습니다.

### 비동기 음성 인식 작업에 대한 재해 복구
{: #disaster-recovery-async}

비동기 HTTP 인터페이스를 사용하는 음성 인식의 경우 다음 정보를 유지보수해야 합니다.

-   비동기 인터페이스에 사용하도록 화이트리스트에 추가하는 모든 콜백 URL. 장애가 발생하는 경우 `POST /v1/register_callback` 메소드를 사용하여 URL을 다시 등록해야 할 수 있습니다. URL이 이미 화이트리스트에 있는 경우 이 메소드가 적절한 응답을 리턴합니다.
-   음성 인식을 위해 비동기 인터페이스에 제출하는 오디오 파일의 사본. 완료된 비동기 작업의 결과를 수신하거나 검색하기 전에 장애가 발생하는 경우 서비스가 복원될 때 `POST /v1/recognitions` 메소드를 사용하여 오디오 파일을 다시 제출해야 합니다. 완료된 비동기 작업의 결과를 얻은 후에는 더 이상 오디오 파일을 유지보수할 필요가 없습니다.

자세한 정보는 [비동기 HTTP 인터페이스](/docs/services/speech-to-text-data?topic=speech-to-text-data-async)를 참조하십시오. 사용자 정의 모델의 백업 데이터와 마찬가지로 이 정보를 적극적으로 보존하고 필요한 요청을 미리 재발행하도록 준비할 수 있습니다.
