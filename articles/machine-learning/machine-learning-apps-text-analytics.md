---
title: "API-интерфейсы машинного обучения — текстовая аналитика | Документация Майкрософт"
description: "Интерфейсы API аналитики корпорации Майкрософт машины обучения текст может быть используется tooanalyze неструктурированных текстовых для анализа мнений, извлечения ключевой фразы, обнаруженный язык и разделе обнаружения."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API-интерфейсы машинного обучения: текстовая аналитика для мнений, извлечение ключевой фразы, определение языка и определение темы
> [!NOTE]
> Это руководство предназначено для версии 1 hello API. Для версии 2 [ **см. документ toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Версия 2 — теперь hello предпочтительную версию этого API.
> 
> 

## <a name="overview"></a>Обзор
Hello API текст аналитики — это набор анализа текста [веб-службы](https://datamarket.azure.com/dataset/amla/text-analytics) с использованием машинного обучения Azure. Hello API можно использовать tooanalyze неструктурированных текстовых для задач, таких как анализ мнений, извлечения ключевой фразы, обнаруженный язык и разделе обнаружения. Нет обучающие данные необходимости toouse этот интерфейс API: просто Оживите свои данные текста. Этот API использует расширенный естественный язык, наилучшим образом обработки toodeliver методы в классе прогнозов.

Аналитика текста в действии можно увидеть на наш [сайта](https://text-analytics-demo.azurewebsites.net/), где вы также найдете [образцы](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) о том, как анализа текста tooimplement в C# и Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Анализ мнений
Hello API возвращает численный показатель между 0 и 1. Закрыть too1 оценки указывать положительных отзывов, тогда закрыть too0 оценки отрицательное мнений. Оценка тональности создается с помощью методов классификации. Классификатор toohello входных признаков Hello включают n грамм, функции, сформированный на основе тегов частей речи и внедряемые объекты word. В настоящее время английский — hello поддерживается только язык.

## <a name="key-phrase-extraction"></a>Извлечение ключевой фразы
Hello API возвращает список строк, обозначающих ключа разговора hello с введенным текстом hello. Мы используем методы из высокотехнологичного набора средств для обработки естественных языков Microsoft Office. В настоящее время английский — hello поддерживается только язык.

## <a name="language-detection"></a>Определение языка
Hello API возвращает hello обнаружил язык и численный показатель между 0 и 1. Закрыть too1 оценки указывают точностью 100%, чтобы идентифицировать hello языка задано значение true. Поддерживается всего 120 языков.

## <a name="topic-detection"></a>Определение темы
Это выпущенном API, который возвращает hello разделы верхнего обнаруженных список записи текста. Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов. Данный API требует не менее 100 текста записывает toobe отправлен, но является спроектированный toodetect разделы сотен toothousands записей. Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи. Hello API — спроектированный toowork подходит для short, отдела, записать текст, например рецензии и отзывов пользователей.

- - -
## <a name="api-definition"></a>Определение интерфейса API
### <a name="headers"></a>Заголовки
Убедитесь, что включены hello правильные заголовки в запросе, который должен иметь следующий вид:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Ключ учетной записи из вашей учетной записи можно найти в hello [Azure Data Market](https://datamarket.azure.com/account/keys). Обратите внимание, что в настоящее время в качества формата входных и выходных данных принимается только JSON. XML не поддерживается.

- - -
## <a name="single-response-apis"></a>API-интерфейсы отдельного ответа
### <a name="getsentiment"></a>GetSentiment
**URL-адрес**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Пример запроса**

В вызове hello ниже запрашивающих анализ мнений hello фразу «Hello World»:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Возвращается следующий ответ:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Пример запроса**

В вызове hello ниже мы запрашиваете hello ключевых фраз, найденных в тексте hello «Был замечательных toostay гостиницы в, с декоративных уникальное и понятное персонал»:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Возвращается следующий ответ:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Пример запроса**

В вызове GET hello ниже, мы запрашивается для hello мнения по hello ключевых фраз в тексте hello *Здравствуй, мир!*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Возвращается следующий ответ:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**Необязательные параметры**

`NumberOfLanguagesToDetect` является необязательным параметром. по умолчанию Hello — 1.

- - -
## <a name="batch-apis"></a>API-интерфейсы пакетной службы
службы анализа текста Hello позволяет toodo мнений и извлечения ключа фразы в пакетном режиме. Обратите внимание, что в каждой из записей hello счетчики оценивается как одна транзакция. Таким образом, при получении тональности для 1000 записей в одном запросе будет вычтено 1000 транзакций.

Обратите внимание, что идентификаторы hello введенные в системе hello используются идентификаторы hello, возвращаемого системной hello. Hello веб-службы не проверяет, что эти идентификаторы уникальны. Это hello ответственность за уникальность tooverify hello вызывающего объекта. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL-адрес**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Пример запроса**

В hello POST вызовите ниже, мы запрашивается для hello sentiments фраз hello, «Hello World», «"Hello World Foo» и «Hello Мои World» в тексте hello hello запроса:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Тело запроса:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

В ответе hello ниже вы получаете список hello показатели, связанные с текстом идентификаторы:

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Пример запроса**

В этом примере мы запрашиваете hello перечень sentiments для hello ключевых фраз в hello следующий текст: 

* «Была замечательных toostay гостиницы на, декоративных уникальное и понятное персонала»
* "It was an amazing build conference, with very interesting talks";
* «hello трафика существовала, я потратил три часа будет toohello аэропорт»

Этот запрос выполняется как конечную точку toohello вызов POST:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Тело запроса:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

В ответе hello ниже вы получаете hello список ключевых фраз, связанных с текстом идентификаторов:

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

В вызове процедуры POST hello ниже запрашивающих определения языка для двух входных значений текста:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Тело запроса:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Возвращает следующий ответ, когда обнаруживается английского языка в первых входных данных hello и французский языки в вторую входную строку hello hello:

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>Интерфейсы API определения темы
Это выпущенном API, который возвращает hello разделы верхнего обнаруженных список записи текста. Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов. Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи.

Данный API требует не менее 100 текста записывает toobe отправлен, но является спроектированный toodetect разделы сотен toothousands записей.

### <a name="topics--submit-job"></a>Темы — отправить задание
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Пример запроса**

В вызове процедуры POST hello ниже запрашивающих разделы для набора 100 статей, где hello и фамилии ввода показываются статьи и два StopPhrases включены.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Тело запроса:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

В ответе hello ниже вы получаете hello JobId hello отправленного задания:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Список из слов или фраз, которые не нужно возвращать в качестве темы. Может быть используется toofilter out очень универсальным разделах. Например, в наборе данных об обзорах отелей разумно использовать стоповые фразы "отель" и "хостел".  

### <a name="topics--poll-for-job-results"></a>Темы — опрос результатов задания
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Пример запроса**

Передайте приветствия JobId возвращенные hello «отправить» шаг toofetch hello результаты задания. Рекомендуется вызывать эту конечную точку каждую минуту, пока состояние = «Завершено» в ответ hello. Он займет около 10 минут toocomplete задания или более заданий с нескольких тысяч записей.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Во время обработки, hello ответа будет выглядеть следующим образом:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Hello API возвращает выходные данные в формате JSON в hello следующий формат:

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


Hello свойства для каждой части ответа hello выглядят следующим образом:

**Свойства TopicInfo**

| Ключ | Описание |
|:--- |:--- |
| TopicId |Уникальный идентификатор каждой темы. |
| Оценка |Количество записей назначить tootopic. |
| KeyPhrase |Суммирование слово или фразу для раздела hello. Может состоять из одного или нескольких слов. |

**Свойства TopicAssignment**

| Ключ | Описание |
|:--- |:--- |
| Идентификатор |Идентификатор записи hello. Указывает идентификатор toohello, включенные во входном файле hello. |
| TopicId |Идентификатор раздела Hello назначены какие записи hello. |
| Distance |Уверенность, что hello запись принадлежит toohello раздела. Расстояние ближе toozero указывает достоверности выше. |

