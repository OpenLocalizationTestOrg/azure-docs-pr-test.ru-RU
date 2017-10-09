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
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="6a784-103">Интеграция машинного обучения в Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="6a784-104">Stream Analytics поддерживает определяемые пользователем функции, которые указывают конечные точки tooAzure машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="6a784-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="6a784-105">Эта возможность поддерживается REST API, описанные в hello [Stream Analytics REST API библиотеки](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a784-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="6a784-106">В этой статье приведены дополнительные сведения, необходимые для успешной реализации этой возможности в Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a784-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="6a784-107">Также было размещено руководство, которое доступно [здесь](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6a784-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="6a784-108">Обзор терминологии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="6a784-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="6a784-109">Машинного обучения Microsoft Azure предоставляет можно использовать средство совместной работы, и перетащите toobuild, тестировать и развертывать прогнозирующие аналитические решения на данные.</span><span class="sxs-lookup"><span data-stu-id="6a784-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="6a784-110">Это средство называется hello *студии машинного обучения Azure*.</span><span class="sxs-lookup"><span data-stu-id="6a784-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="6a784-111">Hello studio — используется toointeract с hello ресурсы машинного обучения и легко создавать, тестирования и прохода на разработку.</span><span class="sxs-lookup"><span data-stu-id="6a784-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="6a784-112">Эти ресурсы и их определения приведены ниже.</span><span class="sxs-lookup"><span data-stu-id="6a784-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="6a784-113">**Рабочая область**: hello *рабочей* — контейнер, который содержит другие ресурсы машинного обучения вместе в контейнере для управления и контроля.</span><span class="sxs-lookup"><span data-stu-id="6a784-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="6a784-114">**Эксперимент**: *экспериментов* созданные наборы tooutilize специалистами по анализу данных и обучить модель машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="6a784-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="6a784-115">**Конечная точка**: *конечные точки* : hello машинного обучения Azure функции tootake объект, используемый в качестве входных данных, применить модель указанного машинного обучения и возвращают Оцененный выходные данные.</span><span class="sxs-lookup"><span data-stu-id="6a784-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="6a784-116">**Оценивающая веб-служба**. *Оценивающая веб-служба* — это коллекция конечных точек, упомянутых выше.</span><span class="sxs-lookup"><span data-stu-id="6a784-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="6a784-117">Каждая конечная точка имеет API для пакетного и синхронного выполнения.</span><span class="sxs-lookup"><span data-stu-id="6a784-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="6a784-118">В Stream Analytics используется синхронное выполнение.</span><span class="sxs-lookup"><span data-stu-id="6a784-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="6a784-119">Hello конкретной службы называется [запросов и ответов службы](../machine-learning/machine-learning-consume-web-services.md) в AzureML studio.</span><span class="sxs-lookup"><span data-stu-id="6a784-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="6a784-120">Ресурсы машинного обучения, необходимые для заданий Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="6a784-121">В целях hello Stream Analytics задания обработки конечную точку запрос-ответ, [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), и определение swagger, необходимы для успешного выполнения.</span><span class="sxs-lookup"><span data-stu-id="6a784-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="6a784-122">Stream Analytics имеет дополнительные конечную точку, которая создает hello URL-адрес для конечной точки swagger, выполняет поиск интерфейса hello и возвращает пользователя toohello определение определяемой пользователем функции по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6a784-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="6a784-123">Настройка Stream Analytics и определяемой пользователем функции машинного обучения с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="6a784-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="6a784-124">С помощью API REST можно настроить функций Azure машинного языка toocall задания.</span><span class="sxs-lookup"><span data-stu-id="6a784-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="6a784-125">Ниже приведены шаги Hello.</span><span class="sxs-lookup"><span data-stu-id="6a784-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="6a784-126">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="6a784-127">Определение входных данных.</span><span class="sxs-lookup"><span data-stu-id="6a784-127">Define an input</span></span>
3. <span data-ttu-id="6a784-128">Определение выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6a784-128">Define an output</span></span>
4. <span data-ttu-id="6a784-129">Создание определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="6a784-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="6a784-130">Записи преобразования Stream Analytics, вызовы hello определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="6a784-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="6a784-131">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="6a784-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="6a784-132">Создание определяемой пользователем функции с базовыми свойствами</span><span class="sxs-lookup"><span data-stu-id="6a784-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="6a784-133">Например, следующий образец кода hello создает скалярной определяемой пользователем функции с именем *newudf* , который связывает конечной точки tooan машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="6a784-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="6a784-134">Обратите внимание, что hello *конечной точки* (служба URI) можно найти на странице приветствия API справки для выбранной службы и hello hello *apiKey* можно найти на главной странице служб hello.</span><span class="sxs-lookup"><span data-stu-id="6a784-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="6a784-135">Пример тела запроса:</span><span class="sxs-lookup"><span data-stu-id="6a784-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="6a784-136">Вызов конечной точки RetrieveDefaultDefinition для определяемой пользователем функции по умолчанию </span><span class="sxs-lookup"><span data-stu-id="6a784-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="6a784-137">Один раз hello основу, определяемая пользователем Функция создается hello полное определение hello необходима определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="6a784-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="6a784-138">Конечная точка RetreiveDefaultDefinition Hello помогает получить определение по умолчанию hello скалярной функцией, которая является конечной точкой привязанного tooan машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="6a784-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="6a784-139">полезные данные Hello ниже требуется определение определяемой пользователем функции по умолчанию hello tooget для скалярной функцией, которая является конечной точкой привязанного tooan машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="6a784-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="6a784-140">Как уже было предоставлено во время запроса PUT, он не определяет hello реальная конечная точка.</span><span class="sxs-lookup"><span data-stu-id="6a784-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="6a784-141">Stream Analytics вызывает hello конечных точек, предоставляемых в запросе hello, если оно предоставлено явным образом.</span><span class="sxs-lookup"><span data-stu-id="6a784-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="6a784-142">В противном случае он использует hello изначально ссылкой на одну.</span><span class="sxs-lookup"><span data-stu-id="6a784-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="6a784-143">Здесь hello определяемая пользователем Функция принимает один строка параметра (предложение) и возвращает один выходной строкового типа, который указывает метку «мнения» hello для этого предложения.</span><span class="sxs-lookup"><span data-stu-id="6a784-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="6a784-144">Пример тела запроса:</span><span class="sxs-lookup"><span data-stu-id="6a784-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="6a784-145">Вывод будет выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6a784-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="6a784-146">Исправление для определяемой пользователем функции с ответом hello</span><span class="sxs-lookup"><span data-stu-id="6a784-146">Patch UDF with hello response</span></span>
<span data-ttu-id="6a784-147">Теперь hello определяемой пользователем функции необходимо исправить с hello предыдущего ответа, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6a784-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="6a784-148">Текст запроса (вывод из RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="6a784-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="6a784-149">Реализовать Stream Analytics преобразования toocall hello определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="6a784-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="6a784-150">Теперь запрос hello определяемой пользователем функции (здесь с именем scoreTweet) для каждого входного события и записи ответа для выходного файла tooan событий.</span><span class="sxs-lookup"><span data-stu-id="6a784-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="6a784-151">Получение справки</span><span class="sxs-lookup"><span data-stu-id="6a784-151">Get help</span></span>
<span data-ttu-id="6a784-152">Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6a784-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a784-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a784-153">Next steps</span></span>
* [<span data-ttu-id="6a784-154">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6a784-155">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6a784-156">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6a784-157">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6a784-158">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6a784-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
