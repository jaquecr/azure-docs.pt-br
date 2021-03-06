---
title: Como usar o SDK de fala para avaliação de pronúncia
titleSuffix: Azure Cognitive Services
description: O SDK de fala dá suporte à avaliação de pronúncia, que avalia a qualidade de pronúncia da entrada de fala, com indicadores de precisão, fluência, integridade, etc.
services: cognitive-services
author: yulin-li
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 09/29/2020
ms.author: yulili
ms.custom: references_regions
zone_pivot_groups: programming-languages-set-nineteen
ms.openlocfilehash: 245a00acb07d1c0e769a243413fccdf64d544f5a
ms.sourcegitcommit: 857859267e0820d0c555f5438dc415fc861d9a6b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2020
ms.locfileid: "93133490"
---
# <a name="pronunciation-assessment"></a>Avaliação de pronúncia

A avaliação de pronúncia avalia a pronúncia de fala e dá aos palestrantes os comentários sobre a precisão e a fluência de áudio falado.
Com a avaliação de pronúncia, os aprendizes de linguagem podem praticar, obter comentários instantâneos e melhorar sua pronúncia para que eles possam falar e apresentar confiança.
Os educadores podem usar a capacidade de avaliar a pronúncia de vários alto-falantes em tempo real.

Neste artigo, você aprenderá a configurar `PronunciationAssessmentConfig` e recuperar o `PronunciationAssessmentResult` usando o SDK de fala.

> [!NOTE]
> Atualmente, o recurso de avaliação de pronúncia está disponível apenas em regiões `westus` `eastasia` e e `centralindia` só dá suporte a idioma `en-US` .

## <a name="pronunciation-assessment-with-the-speech-sdk"></a>Avaliação de pronúncia com o SDK de fala

Nos exemplos abaixo, você criará um `PronunciationAssessmentConfig` e o aplicará a um `SpeechRecognizer` .

Os trechos de código a seguir ilustram como usar a detecção automática de idioma em seus aplicativos:

::: zone pivot="programming-language-csharp"

```csharp
var pronunciationAssessmentConfig = new PronunciationAssessmentConfig(
    "reference text", GradingSystem.HundredMark, Granularity.Phoneme);

using (var recognizer = new SpeechRecognizer(
    speechConfig,
    audioConfig))
{
    // apply the pronunciation assessment configuration to the speech recognizer
    pronunciationAssessmentConfig.ApplyTo(recognizer);
    var speechRecognitionResult = await recognizer.RecognizeOnceAsync();
    var pronunciationAssessmentResult =
        PronunciationAssessmentResult.FromResult(speechRecognitionResult);
    var pronunciationScore = pronunciationAssessmentResult.PronunciationScore;
}
```

::: zone-end

::: zone pivot="programming-language-cpp"

```cpp
auto pronunciationAssessmentConfig =
    PronunciationAssessmentConfig::Create("reference text",
        PronunciationAssessmentGradingSystem::HundredMark,
        PronunciationAssessmentGranularity::Phoneme);

auto recognizer = SpeechRecognizer::FromConfig(
    speechConfig,
    audioConfig);

// apply the pronunciation assessment configuration to the speech recognizer
pronunciationAssessmentConfig->ApplyTo(recognizer);
speechRecognitionResult = recognizer->RecognizeOnceAsync().get();
auto pronunciationAssessmentResult =
    PronunciationAssessmentResult::FromResult(speechRecognitionResult);
auto pronunciationScore = pronunciationAssessmentResult->PronunciationScore;
```

::: zone-end

::: zone pivot="programming-language-java"

```java
PronunciationAssessmentConfig pronunciationAssessmentConfig =
    new PronunciationAssessmentConfig("reference text", 
        PronunciationAssessmentGradingSystem.HundredMark,
        PronunciationAssessmentGranularity.Phoneme);

SpeechRecognizer recognizer = new SpeechRecognizer(
    speechConfig,
    audioConfig);

// apply the pronunciation assessment configuration to the speech recognizer
pronunciationAssessmentConfig.applyTo(recognizer);
Future<SpeechRecognitionResult> future = recognizer.recognizeOnceAsync();
SpeechRecognitionResult result = future.get(30, TimeUnit.SECONDS);
PronunciationAssessmentResult pronunciationAssessmentResult =
    PronunciationAssessmentResult.fromResult(result);
Double pronunciationScore = pronunciationAssessmentResult.getPronunciationScore();

recognizer.close();
speechConfig.close();
audioConfig.close();
pronunciationAssessmentConfig.close();
result.close();
```

::: zone-end

::: zone pivot="programming-language-python"

```Python
pronunciation_assessment_config = \
        speechsdk.PronunciationAssessmentConfig(reference_text='reference text',
                grading_system=msspeech.PronunciationAssessmentGradingSystem.HundredMark,
                granularity=msspeech.PronunciationAssessmentGranularity.Phoneme)
speech_recognizer = speechsdk.SpeechRecognizer(
        speech_config=speech_config, \
        audio_config=audio_config)

# apply the pronunciation assessment configuration to the speech recognizer
pronunciation_assessment_config.apply_to(speech_recognizer)
result = speech_recognizer.recognize_once()
pronunciation_assessment_result = speechsdk.PronunciationAssessmentResult(result)
pronunciation_score = pronunciation_assessment_result.pronunciation_score
```

::: zone-end

::: zone pivot="programming-language-objectivec"

```Objective-C
SPXPronunciationAssessmentConfiguration* pronunciationAssessmentConfig =
    [[SPXPronunciationAssessmentConfiguration alloc]init:@"reference text"
                                           gradingSystem:SPXPronunciationAssessmentGradingSystem_HundredMark
                                             granularity:SPXPronunciationAssessmentGranularity_Phoneme];

SPXSpeechRecognizer* speechRecognizer = \
        [[SPXSpeechRecognizer alloc] initWithSpeechConfiguration:speechConfig
                                              audioConfiguration:audioConfig];

// apply the pronunciation assessment configuration to the speech recognizer
[pronunciationAssessmentConfig applyToRecognizer:speechRecognizer];

SPXSpeechRecognitionResult *result = [speechRecognizer recognizeOnce];
SPXPronunciationAssessmentResult* pronunciationAssessmentResult = [[SPXPronunciationAssessmentResult alloc] init:result];
double pronunciationScore = pronunciationAssessmentResult.pronunciationScore;
```

::: zone-end

### <a name="pronunciation-assessment-configuration-parameters"></a>Parâmetros de configuração de avaliação de pronúncia

Esta tabela lista os parâmetros de configuração para avaliação de pronúncia.

| Parâmetro | Descrição | Obrigatório/Opcional |
|-----------|-------------|---------------------|
| ReferenceText | O texto em relação ao qual a pronúncia será avaliada. | Obrigatório |
| GradingSystem | O sistema de ponto para a calibragem de pontuação. Os valores aceitos são `FivePoint` e `HundredMark`. A configuração padrão é `FivePoint`. | Opcional |
| Granularidade | A granularidade da avaliação. Os valores aceitos são `Phoneme` , que mostra a pontuação no nível de texto completo, Word e fonema, `Word` , que mostra a pontuação no texto completo e no nível de palavra, `FullText` , que mostra a pontuação somente no nível de texto completo. A configuração padrão é `Phoneme`. | Opcional |
| EnableMiscue | Habilita o cálculo de miscue. Com isso habilitado, as palavras pronunciadas serão comparadas ao texto de referência e serão marcadas com omissão/inserção com base na comparação. Os valores aceitos são `False` e `True`. A configuração padrão é `False`. | Opcional |
| Scenarioid | Um GUID que indica um sistema de ponto personalizado. | Opcional |

### <a name="pronunciation-assessment-result-parameters"></a>Parâmetros de resultado da avaliação de pronúncia

Esta tabela lista os parâmetros de resultado da avaliação de pronúncia.

| Parâmetro | Descrição |
|-----------|-------------|
| `AccuracyScore` | Precisão da pronúncia da fala. A precisão indica o quão próximo os fonemas correspondem à pronúncia de um orador nativo. A pontuação de precisão de nível de texto completo e de palavra é agregada da Pontuação de precisão de nível de fonema. |
| `FluencyScore` | Fluência da fala determinada. Fluência indica a precisão com que a fala corresponde ao uso silencioso de quebras silenciosas entre palavras do orador nativo. |
| `CompletenessScore` | Integridade da fala, determinada pelo cálculo da proporção de palavras pronunciadas para fazer referência à entrada de texto. |
| `PronunciationScore` | Pontuação geral que indica a qualidade da pronúncia da fala determinada. Isso é agregado de `AccuracyScore` `FluencyScore` e `CompletenessScore` com peso. |
| `ErrorType` | Esse valor indica se uma palavra é omitida, inserida ou pronunciada incorretamente, em comparação com `ReferenceText` . Os valores possíveis são `None` (ou seja, nenhum erro nesta palavra), `Omission` `Insertion` e `Mispronunciation` . |

## <a name="next-steps"></a>Próximas etapas

<!-- TODO: update the sample links after release -->

<!-- ::: zone pivot="programming-language-csharp"
* See the [sample code](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/csharp/sharedcontent/console/speech_recognition_samples.cs#L741) on GitHub for automatic language detection
::: zone-end

::: zone pivot="programming-language-cpp"
* See the [sample code](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/cpp/windows/console/samples/speech_recognition_samples.cpp#L507) on GitHub for automatic language detection
::: zone-end

::: zone pivot="programming-language-java"
* See the [sample code](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/java/jre/console/src/com/microsoft/cognitiveservices/speech/samples/console/SpeechRecognitionSamples.java#L521) on GitHub for automatic language detection
::: zone-end

::: zone pivot="programming-language-python"
* See the [sample code](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/python/console/speech_synthesis_sample.py#L434) on GitHub for automatic language detection
::: zone-end

::: zone pivot="programming-language-objectivec"
* See the [sample code](https://github.com/Azure-Samples/cognitive-services-speech-sdk/blob/master/samples/objective-c/ios/speech-samples/speech-samples/ViewController.m#L494) on GitHub for automatic language detection
::: zone-end -->

* [Documentação de referência do SDK de fala](speech-sdk.md)
