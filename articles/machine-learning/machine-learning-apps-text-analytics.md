---
title: "API-интерфейсы машинного обучения — текстовая аналитика | Документация Майкрософт"
description: "Интерфейсы API текстовой аналитики машинного обучения Microsoft можно использовать для анализа неструктурированного текста в таких задачах, как анализ мнений, извлечение ключевой фразы, определение языка и определение темы."
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
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>API-интерфейсы машинного обучения: текстовая аналитика для мнений, извлечение ключевой фразы, определение языка и определение темы
> [!NOTE]
> Это руководство предназначено для API версии 1. Руководство для версии 2 см. [**здесь**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Теперь версия 2 является предпочтительной версией этого API.
> 
> 

## <a name="overview"></a>Обзор
API анализа текста — это набор [веб-служб](https://datamarket.azure.com/dataset/amla/text-analytics) для анализа текста, созданный с помощью машинного обучения Azure. API можно использовать для анализа неструктурированного текста в таких задачах, как анализ мнений, извлечение ключевой фразы, определение языка и определение темы. Для работы с этим API данные для обучения не нужны, поэтому можно просто использовать свои текстовые данные. Для обеспечения лучшего в своем классе прогнозирования этот API применяет собственные расширенные методы обработки естественного языка.

Анализ текста в действии можно увидеть на нашем [демонстрационном сайте](https://text-analytics-demo.azurewebsites.net/), где также находятся [примеры](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) реализации анализа текста в C# и Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Анализ мнений
API возвращает численную оценку между 0 и 1. Если оценка приближается к 1, то у текста позитивная тональность, а если к 0, то негативная. Оценка тональности создается с помощью методов классификации. Входные признаки, поступающие в классификатор, включают n-граммы, признаки, созданные на основе частеречной разметки, и векторное представление слов. В настоящее время поддерживается только английский язык.

## <a name="key-phrase-extraction"></a>Извлечение ключевой фразы
API возвращает список строк с обозначением ключевых тем разговора во входном тексте. Мы используем методы из высокотехнологичного набора средств для обработки естественных языков Microsoft Office. В настоящее время поддерживается только английский язык.

## <a name="language-detection"></a>Определение языка
API возвращает определенный язык и численную оценку между 0 и 1. Если оценка приближается к 1, существует стопроцентная уверенность, что язык определен правильно. Поддерживается всего 120 языков.

## <a name="topic-detection"></a>Определение темы
Это только что выпущенный API, который определяет основные темы для списка отправленных текстовых записей. Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов. Этот интерфейс API позволяет определять темы для количества текстовых записей от нескольких сотен до тысяч. При этом минимальное количество текстовых записей равно 100. Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи. Этот API-интерфейс хорошо работает с короткими, написанными человеком текстами, такими как обзоры и отзывы пользователей.

- - -
## <a name="api-definition"></a>Определение интерфейса API
### <a name="headers"></a>Заголовки
Убедитесь, что в запрос, который должен иметь следующий вид, включены правильные заголовки:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Ключ учетной записи можно найти в вашей учетной записи в [Azure Data Market](https://datamarket.azure.com/account/keys). Обратите внимание, что в настоящее время в качества формата входных и выходных данных принимается только JSON. XML не поддерживается.

- - -
## <a name="single-response-apis"></a>API-интерфейсы отдельного ответа
### <a name="getsentiment"></a>GetSentiment
**URL-адрес**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Пример запроса**

В приведенном ниже вызове запрашивается тональность фразы "Hello World".

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

В приведенном ниже вызове запрашиваются ключевые фразы в тексте "It was a wonderful hotel to stay at, with unique decor and friendly staff".

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

В приведенном ниже вызове GET запрашивается тональность ключевых фраз в тексте *Hello World*

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

`NumberOfLanguagesToDetect` является необязательным параметром. Значение по умолчанию — 1.

- - -
## <a name="batch-apis"></a>API-интерфейсы пакетной службы
Служба текстовой аналитики позволяет выполнять поиск на основе тональности и ключевых фраз в пакетном режиме. Обратите внимание, что каждая из записей считается как одна транзакция. Таким образом, при получении тональности для 1000 записей в одном запросе будет вычтено 1000 транзакций.

Обратите внимание, что введенные в систему идентификаторы — это идентификаторы, возвращенные системой. Веб-служба не проверяет уникальность идентификаторов. Ответственность за проверку уникальности несет вызывающий объект. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL-адрес**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Пример запроса**

В приведенном ниже вызове POST запрашивается тональность следующих ключевых фраз в тексте запроса: "Hello World", "Hello Foo World" и "Hello My World".

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

Тело запроса:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

В приведенном ниже ответе отображается список показателей, связанных с идентификаторами текста:

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

В приведенном ниже вызове запрашивается список тональностей ключевых фраз в следующих текстах: 

* "It was a wonderful hotel to stay at, with unique decor and friendly staff";
* "It was an amazing build conference, with very interesting talks";
* "The traffic was terrible, I spent three hours going to the airport".

Этот запрос выполняется как вызов метода POST в конечную точку:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

Тело запроса:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

В приведенном ниже ответе можно получить список ключевых фраз, связанных с идентификаторами текста:

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

В приведенном ниже вызове POST запрашивается определение языка для двух входных значений текста:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

Тело запроса:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Возвращается следующий ответ, где в первом наборе входных данных определен английский язык, а в втором — французский.

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
Это только что выпущенный API, который определяет основные темы для списка отправленных текстовых записей. Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов. Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи.

Этот интерфейс API позволяет определять темы для количества текстовых записей от нескольких сотен до тысяч. При этом минимальное количество текстовых записей равно 100.

### <a name="topics--submit-job"></a>Темы — отправить задание
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Пример запроса**

В приведенном ниже вызове POST запрашиваются темы для набора 100 статей, отображаются первая и последняя статьи, и включены две стоповые фразы.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

Тело запроса:

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

В приведенном ниже ответе вы получаете JobId для отправленного задания:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Список из слов или фраз, которые не нужно возвращать в качестве темы. Можно использовать для исключения слишком общих тем. Например, в наборе данных об обзорах отелей разумно использовать стоповые фразы "отель" и "хостел".  

### <a name="topics--poll-for-job-results"></a>Темы — опрос результатов задания
**URL-адрес**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Пример запроса**

Передайте JobId, возвращенный на шаге "Отправить задание", для получения результатов. Мы рекомендуем вызывать эту конечную точку каждую минуту, пока состояние в ответе не изменится на "Завершено". Для завершения задания потребуется около 10 минут, для заданий с несколькими тысячами записей потребуется больше времени.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Во время его обработки ответ будет иметь следующий вид:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


API возвращает выходные данные в JSON в следующем формате:

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


Ниже приведены свойства для каждой части ответа:

**Свойства TopicInfo**

| Ключ | Описание |
|:--- |:--- |
| TopicId |Уникальный идентификатор каждой темы. |
| Оценка |Количество записей, назначенных теме. |
| KeyPhrase |Обобщающее слово или фраза для темы. Может состоять из одного или нескольких слов. |

**Свойства TopicAssignment**

| Ключ | Описание |
|:--- |:--- |
| Идентификатор |Идентификатор записи. Соответствует идентификатору, включенному во входные данные. |
| TopicId |Идентификатор темы, которому была назначена запись. |
| Distance |Уверенность в том, что запись принадлежит к разделу. Более близкое к нулю значение означает более высокую степень уверенности. |

