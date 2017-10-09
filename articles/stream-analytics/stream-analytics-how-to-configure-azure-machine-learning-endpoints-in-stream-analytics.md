---
title: "конечные точки машинного обучения Azure aaaUse в Stream Analytics | Документы Microsoft"
description: "Определяемые пользователем функции машинного обучения в Stream Analytics."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a>Интеграция машинного обучения в Stream Analytics
Stream Analytics поддерживает определяемые пользователем функции, которые указывают конечные точки tooAzure машинного обучения. Эта возможность поддерживается REST API, описанные в hello [Stream Analytics REST API библиотеки](https://msdn.microsoft.com/library/azure/dn835031.aspx). В этой статье приведены дополнительные сведения, необходимые для успешной реализации этой возможности в Stream Analytics. Также было размещено руководство, которое доступно [здесь](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Обзор терминологии машинного обучения Azure
Машинного обучения Microsoft Azure предоставляет можно использовать средство совместной работы, и перетащите toobuild, тестировать и развертывать прогнозирующие аналитические решения на данные. Это средство называется hello *студии машинного обучения Azure*. Hello studio — используется toointeract с hello ресурсы машинного обучения и легко создавать, тестирования и прохода на разработку. Эти ресурсы и их определения приведены ниже.

* **Рабочая область**: hello *рабочей* — контейнер, который содержит другие ресурсы машинного обучения вместе в контейнере для управления и контроля.
* **Эксперимент**: *экспериментов* созданные наборы tooutilize специалистами по анализу данных и обучить модель машинного обучения.
* **Конечная точка**: *конечные точки* : hello машинного обучения Azure функции tootake объект, используемый в качестве входных данных, применить модель указанного машинного обучения и возвращают Оцененный выходные данные.
* **Оценивающая веб-служба**. *Оценивающая веб-служба* — это коллекция конечных точек, упомянутых выше.

Каждая конечная точка имеет API для пакетного и синхронного выполнения. В Stream Analytics используется синхронное выполнение. Hello конкретной службы называется [запросов и ответов службы](../machine-learning/machine-learning-consume-web-services.md) в AzureML studio.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Ресурсы машинного обучения, необходимые для заданий Stream Analytics
В целях hello Stream Analytics задания обработки конечную точку запрос-ответ, [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), и определение swagger, необходимы для успешного выполнения. Stream Analytics имеет дополнительные конечную точку, которая создает hello URL-адрес для конечной точки swagger, выполняет поиск интерфейса hello и возвращает пользователя toohello определение определяемой пользователем функции по умолчанию.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Настройка Stream Analytics и определяемой пользователем функции машинного обучения с помощью REST API
С помощью API REST можно настроить функций Azure машинного языка toocall задания. Ниже приведены шаги Hello.

1. Создание задания Stream Analytics
2. Определение входных данных.
3. Определение выходных данных.
4. Создание определяемой пользователем функции
5. Записи преобразования Stream Analytics, вызовы hello определяемой пользователем функции.
6. Запустить задание hello

## <a name="creating-a-udf-with-basic-properties"></a>Создание определяемой пользователем функции с базовыми свойствами
Например, следующий образец кода hello создает скалярной определяемой пользователем функции с именем *newudf* , который связывает конечной точки tooan машинного обучения Azure. Обратите внимание, что hello *конечной точки* (служба URI) можно найти на странице приветствия API справки для выбранной службы и hello hello *apiKey* можно найти на главной странице служб hello.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Пример тела запроса:  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Вызов конечной точки RetrieveDefaultDefinition для определяемой пользователем функции по умолчанию 
Один раз hello основу, определяемая пользователем Функция создается hello полное определение hello необходима определяемой пользователем функции. Конечная точка RetreiveDefaultDefinition Hello помогает получить определение по умолчанию hello скалярной функцией, которая является конечной точкой привязанного tooan машинного обучения Azure. полезные данные Hello ниже требуется определение определяемой пользователем функции по умолчанию hello tooget для скалярной функцией, которая является конечной точкой привязанного tooan машинного обучения Azure. Как уже было предоставлено во время запроса PUT, он не определяет hello реальная конечная точка. Stream Analytics вызывает hello конечных точек, предоставляемых в запросе hello, если оно предоставлено явным образом. В противном случае он использует hello изначально ссылкой на одну. Здесь hello определяемая пользователем Функция принимает один строка параметра (предложение) и возвращает один выходной строкового типа, который указывает метку «мнения» hello для этого предложения.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Пример тела запроса:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Вывод будет выглядеть примерно так, как показано ниже.  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a>Исправление для определяемой пользователем функции с ответом hello
Теперь hello определяемой пользователем функции необходимо исправить с hello предыдущего ответа, как показано ниже.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Текст запроса (вывод из RetrieveDefaultDefinition):

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Реализовать Stream Analytics преобразования toocall hello определяемой пользователем функции.
Теперь запрос hello определяемой пользователем функции (здесь с именем scoreTweet) для каждого входного события и записи ответа для выходного файла tooan событий.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Получение справки
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
