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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="5ef1c-103">API-интерфейсы машинного обучения: текстовая аналитика для мнений, извлечение ключевой фразы, определение языка и определение темы</span><span class="sxs-lookup"><span data-stu-id="5ef1c-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="5ef1c-104">Это руководство предназначено для API версии 1.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="5ef1c-105">Руководство для версии 2 см. [**здесь**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="5ef1c-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="5ef1c-106">Теперь версия 2 является предпочтительной версией этого API.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="5ef1c-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="5ef1c-107">Overview</span></span>
<span data-ttu-id="5ef1c-108">API анализа текста — это набор [веб-служб](https://datamarket.azure.com/dataset/amla/text-analytics) для анализа текста, созданный с помощью машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="5ef1c-109">API можно использовать для анализа неструктурированного текста в таких задачах, как анализ мнений, извлечение ключевой фразы, определение языка и определение темы.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="5ef1c-110">Для работы с этим API данные для обучения не нужны, поэтому можно просто использовать свои текстовые данные.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="5ef1c-111">Для обеспечения лучшего в своем классе прогнозирования этот API применяет собственные расширенные методы обработки естественного языка.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="5ef1c-112">Анализ текста в действии можно увидеть на нашем [демонстрационном сайте](https://text-analytics-demo.azurewebsites.net/), где также находятся [примеры](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) реализации анализа текста в C# и Python.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="5ef1c-113">Анализ мнений</span><span class="sxs-lookup"><span data-stu-id="5ef1c-113">Sentiment analysis</span></span>
<span data-ttu-id="5ef1c-114">API возвращает численную оценку между 0 и 1.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="5ef1c-115">Если оценка приближается к 1, то у текста позитивная тональность, а если к 0, то негативная.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="5ef1c-116">Оценка тональности создается с помощью методов классификации.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="5ef1c-117">Входные признаки, поступающие в классификатор, включают n-граммы, признаки, созданные на основе частеречной разметки, и векторное представление слов.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="5ef1c-118">В настоящее время поддерживается только английский язык.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="5ef1c-119">Извлечение ключевой фразы</span><span class="sxs-lookup"><span data-stu-id="5ef1c-119">Key phrase extraction</span></span>
<span data-ttu-id="5ef1c-120">API возвращает список строк с обозначением ключевых тем разговора во входном тексте.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="5ef1c-121">Мы используем методы из высокотехнологичного набора средств для обработки естественных языков Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="5ef1c-122">В настоящее время поддерживается только английский язык.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="5ef1c-123">Определение языка</span><span class="sxs-lookup"><span data-stu-id="5ef1c-123">Language detection</span></span>
<span data-ttu-id="5ef1c-124">API возвращает определенный язык и численную оценку между 0 и 1.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="5ef1c-125">Если оценка приближается к 1, существует стопроцентная уверенность, что язык определен правильно.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="5ef1c-126">Поддерживается всего 120 языков.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="5ef1c-127">Определение темы</span><span class="sxs-lookup"><span data-stu-id="5ef1c-127">Topic detection</span></span>
<span data-ttu-id="5ef1c-128">Это только что выпущенный API, который определяет основные темы для списка отправленных текстовых записей.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="5ef1c-129">Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="5ef1c-130">Этот интерфейс API позволяет определять темы для количества текстовых записей от нескольких сотен до тысяч. При этом минимальное количество текстовых записей равно 100.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="5ef1c-131">Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="5ef1c-132">Этот API-интерфейс хорошо работает с короткими, написанными человеком текстами, такими как обзоры и отзывы пользователей.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="5ef1c-133">Определение интерфейса API</span><span class="sxs-lookup"><span data-stu-id="5ef1c-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="5ef1c-134">Заголовки</span><span class="sxs-lookup"><span data-stu-id="5ef1c-134">Headers</span></span>
<span data-ttu-id="5ef1c-135">Убедитесь, что в запрос, который должен иметь следующий вид, включены правильные заголовки:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="5ef1c-136">Ключ учетной записи можно найти в вашей учетной записи в [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="5ef1c-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="5ef1c-137">Обратите внимание, что в настоящее время в качества формата входных и выходных данных принимается только JSON.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="5ef1c-138">XML не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="5ef1c-139">API-интерфейсы отдельного ответа</span><span class="sxs-lookup"><span data-stu-id="5ef1c-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="5ef1c-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="5ef1c-140">GetSentiment</span></span>
<span data-ttu-id="5ef1c-141">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="5ef1c-142">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-142">**Example request**</span></span>

<span data-ttu-id="5ef1c-143">В приведенном ниже вызове запрашивается тональность фразы "Hello World".</span><span class="sxs-lookup"><span data-stu-id="5ef1c-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="5ef1c-144">Возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="5ef1c-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="5ef1c-145">GetKeyPhrases</span></span>
<span data-ttu-id="5ef1c-146">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="5ef1c-147">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-147">**Example request**</span></span>

<span data-ttu-id="5ef1c-148">В приведенном ниже вызове запрашиваются ключевые фразы в тексте "It was a wonderful hotel to stay at, with unique decor and friendly staff".</span><span class="sxs-lookup"><span data-stu-id="5ef1c-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="5ef1c-149">Возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="5ef1c-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="5ef1c-150">GetLanguage</span></span>
<span data-ttu-id="5ef1c-151">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="5ef1c-152">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-152">**Example request**</span></span>

<span data-ttu-id="5ef1c-153">В приведенном ниже вызове GET запрашивается тональность ключевых фраз в тексте *Hello World*</span><span class="sxs-lookup"><span data-stu-id="5ef1c-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="5ef1c-154">Возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="5ef1c-155">**Необязательные параметры**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-155">**Optional parameters**</span></span>

<span data-ttu-id="5ef1c-156">`NumberOfLanguagesToDetect` является необязательным параметром.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="5ef1c-157">Значение по умолчанию — 1.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="5ef1c-158">API-интерфейсы пакетной службы</span><span class="sxs-lookup"><span data-stu-id="5ef1c-158">Batch APIs</span></span>
<span data-ttu-id="5ef1c-159">Служба текстовой аналитики позволяет выполнять поиск на основе тональности и ключевых фраз в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="5ef1c-160">Обратите внимание, что каждая из записей считается как одна транзакция.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="5ef1c-161">Таким образом, при получении тональности для 1000 записей в одном запросе будет вычтено 1000 транзакций.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="5ef1c-162">Обратите внимание, что введенные в систему идентификаторы — это идентификаторы, возвращенные системой.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="5ef1c-163">Веб-служба не проверяет уникальность идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="5ef1c-164">Ответственность за проверку уникальности несет вызывающий объект.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="5ef1c-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="5ef1c-165">GetSentimentBatch</span></span>
<span data-ttu-id="5ef1c-166">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="5ef1c-167">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-167">**Example request**</span></span>

<span data-ttu-id="5ef1c-168">В приведенном ниже вызове POST запрашивается тональность следующих ключевых фраз в тексте запроса: "Hello World", "Hello Foo World" и "Hello My World".</span><span class="sxs-lookup"><span data-stu-id="5ef1c-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="5ef1c-169">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="5ef1c-170">В приведенном ниже ответе отображается список показателей, связанных с идентификаторами текста:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="5ef1c-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="5ef1c-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="5ef1c-172">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="5ef1c-173">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-173">**Example request**</span></span>

<span data-ttu-id="5ef1c-174">В приведенном ниже вызове запрашивается список тональностей ключевых фраз в следующих текстах:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="5ef1c-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff";</span><span class="sxs-lookup"><span data-stu-id="5ef1c-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="5ef1c-176">"It was an amazing build conference, with very interesting talks";</span><span class="sxs-lookup"><span data-stu-id="5ef1c-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="5ef1c-177">"The traffic was terrible, I spent three hours going to the airport".</span><span class="sxs-lookup"><span data-stu-id="5ef1c-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="5ef1c-178">Этот запрос выполняется как вызов метода POST в конечную точку:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="5ef1c-179">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="5ef1c-180">В приведенном ниже ответе можно получить список ключевых фраз, связанных с идентификаторами текста:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="5ef1c-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="5ef1c-181">GetLanguageBatch</span></span>

<span data-ttu-id="5ef1c-182">В приведенном ниже вызове POST запрашивается определение языка для двух входных значений текста:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="5ef1c-183">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="5ef1c-184">Возвращается следующий ответ, где в первом наборе входных данных определен английский язык, а в втором — французский.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="5ef1c-185">Интерфейсы API определения темы</span><span class="sxs-lookup"><span data-stu-id="5ef1c-185">Topic Detection APIs</span></span>
<span data-ttu-id="5ef1c-186">Это только что выпущенный API, который определяет основные темы для списка отправленных текстовых записей.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="5ef1c-187">Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="5ef1c-188">Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="5ef1c-189">Этот интерфейс API позволяет определять темы для количества текстовых записей от нескольких сотен до тысяч. При этом минимальное количество текстовых записей равно 100.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="5ef1c-190">Темы — отправить задание</span><span class="sxs-lookup"><span data-stu-id="5ef1c-190">Topics – Submit job</span></span>
<span data-ttu-id="5ef1c-191">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="5ef1c-192">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-192">**Example request**</span></span>

<span data-ttu-id="5ef1c-193">В приведенном ниже вызове POST запрашиваются темы для набора 100 статей, отображаются первая и последняя статьи, и включены две стоповые фразы.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="5ef1c-194">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="5ef1c-195">В приведенном ниже ответе вы получаете JobId для отправленного задания:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="5ef1c-196">Список из слов или фраз, которые не нужно возвращать в качестве темы.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="5ef1c-197">Можно использовать для исключения слишком общих тем.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="5ef1c-198">Например, в наборе данных об обзорах отелей разумно использовать стоповые фразы "отель" и "хостел".</span><span class="sxs-lookup"><span data-stu-id="5ef1c-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="5ef1c-199">Темы — опрос результатов задания</span><span class="sxs-lookup"><span data-stu-id="5ef1c-199">Topics – Poll for job results</span></span>
<span data-ttu-id="5ef1c-200">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="5ef1c-201">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-201">**Example request**</span></span>

<span data-ttu-id="5ef1c-202">Передайте JobId, возвращенный на шаге "Отправить задание", для получения результатов.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="5ef1c-203">Мы рекомендуем вызывать эту конечную точку каждую минуту, пока состояние в ответе не изменится на "Завершено".</span><span class="sxs-lookup"><span data-stu-id="5ef1c-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="5ef1c-204">Для завершения задания потребуется около 10 минут, для заданий с несколькими тысячами записей потребуется больше времени.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="5ef1c-205">Во время его обработки ответ будет иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="5ef1c-206">API возвращает выходные данные в JSON в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-206">The API returns output in JSON format in the following format:</span></span>

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


<span data-ttu-id="5ef1c-207">Ниже приведены свойства для каждой части ответа:</span><span class="sxs-lookup"><span data-stu-id="5ef1c-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="5ef1c-208">**Свойства TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="5ef1c-209">Ключ</span><span class="sxs-lookup"><span data-stu-id="5ef1c-209">Key</span></span> | <span data-ttu-id="5ef1c-210">Описание</span><span class="sxs-lookup"><span data-stu-id="5ef1c-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5ef1c-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="5ef1c-211">TopicId</span></span> |<span data-ttu-id="5ef1c-212">Уникальный идентификатор каждой темы.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="5ef1c-213">Оценка</span><span class="sxs-lookup"><span data-stu-id="5ef1c-213">Score</span></span> |<span data-ttu-id="5ef1c-214">Количество записей, назначенных теме.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="5ef1c-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="5ef1c-215">KeyPhrase</span></span> |<span data-ttu-id="5ef1c-216">Обобщающее слово или фраза для темы.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="5ef1c-217">Может состоять из одного или нескольких слов.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="5ef1c-218">**Свойства TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="5ef1c-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="5ef1c-219">Ключ</span><span class="sxs-lookup"><span data-stu-id="5ef1c-219">Key</span></span> | <span data-ttu-id="5ef1c-220">Описание</span><span class="sxs-lookup"><span data-stu-id="5ef1c-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5ef1c-221">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="5ef1c-221">Id</span></span> |<span data-ttu-id="5ef1c-222">Идентификатор записи.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-222">Identifier for the record.</span></span> <span data-ttu-id="5ef1c-223">Соответствует идентификатору, включенному во входные данные.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="5ef1c-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="5ef1c-224">TopicId</span></span> |<span data-ttu-id="5ef1c-225">Идентификатор темы, которому была назначена запись.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="5ef1c-226">Distance</span><span class="sxs-lookup"><span data-stu-id="5ef1c-226">Distance</span></span> |<span data-ttu-id="5ef1c-227">Уверенность в том, что запись принадлежит к разделу.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="5ef1c-228">Более близкое к нулю значение означает более высокую степень уверенности.</span><span class="sxs-lookup"><span data-stu-id="5ef1c-228">Distance closer to zero indicates higher confidence.</span></span> |

