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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="ed65a-103">API-интерфейсы машинного обучения: текстовая аналитика для мнений, извлечение ключевой фразы, определение языка и определение темы</span><span class="sxs-lookup"><span data-stu-id="ed65a-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="ed65a-104">Это руководство предназначено для версии 1 hello API.</span><span class="sxs-lookup"><span data-stu-id="ed65a-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="ed65a-105">Для версии 2 [ **см. документ toothis**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="ed65a-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="ed65a-106">Версия 2 — теперь hello предпочтительную версию этого API.</span><span class="sxs-lookup"><span data-stu-id="ed65a-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="ed65a-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="ed65a-107">Overview</span></span>
<span data-ttu-id="ed65a-108">Hello API текст аналитики — это набор анализа текста [веб-службы](https://datamarket.azure.com/dataset/amla/text-analytics) с использованием машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="ed65a-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="ed65a-109">Hello API можно использовать tooanalyze неструктурированных текстовых для задач, таких как анализ мнений, извлечения ключевой фразы, обнаруженный язык и разделе обнаружения.</span><span class="sxs-lookup"><span data-stu-id="ed65a-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="ed65a-110">Нет обучающие данные необходимости toouse этот интерфейс API: просто Оживите свои данные текста.</span><span class="sxs-lookup"><span data-stu-id="ed65a-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="ed65a-111">Этот API использует расширенный естественный язык, наилучшим образом обработки toodeliver методы в классе прогнозов.</span><span class="sxs-lookup"><span data-stu-id="ed65a-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="ed65a-112">Аналитика текста в действии можно увидеть на наш [сайта](https://text-analytics-demo.azurewebsites.net/), где вы также найдете [образцы](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) о том, как анализа текста tooimplement в C# и Python.</span><span class="sxs-lookup"><span data-stu-id="ed65a-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="ed65a-113">Анализ мнений</span><span class="sxs-lookup"><span data-stu-id="ed65a-113">Sentiment analysis</span></span>
<span data-ttu-id="ed65a-114">Hello API возвращает численный показатель между 0 и 1.</span><span class="sxs-lookup"><span data-stu-id="ed65a-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="ed65a-115">Закрыть too1 оценки указывать положительных отзывов, тогда закрыть too0 оценки отрицательное мнений.</span><span class="sxs-lookup"><span data-stu-id="ed65a-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="ed65a-116">Оценка тональности создается с помощью методов классификации.</span><span class="sxs-lookup"><span data-stu-id="ed65a-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="ed65a-117">Классификатор toohello входных признаков Hello включают n грамм, функции, сформированный на основе тегов частей речи и внедряемые объекты word.</span><span class="sxs-lookup"><span data-stu-id="ed65a-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="ed65a-118">В настоящее время английский — hello поддерживается только язык.</span><span class="sxs-lookup"><span data-stu-id="ed65a-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="ed65a-119">Извлечение ключевой фразы</span><span class="sxs-lookup"><span data-stu-id="ed65a-119">Key phrase extraction</span></span>
<span data-ttu-id="ed65a-120">Hello API возвращает список строк, обозначающих ключа разговора hello с введенным текстом hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="ed65a-121">Мы используем методы из высокотехнологичного набора средств для обработки естественных языков Microsoft Office.</span><span class="sxs-lookup"><span data-stu-id="ed65a-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="ed65a-122">В настоящее время английский — hello поддерживается только язык.</span><span class="sxs-lookup"><span data-stu-id="ed65a-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="ed65a-123">Определение языка</span><span class="sxs-lookup"><span data-stu-id="ed65a-123">Language detection</span></span>
<span data-ttu-id="ed65a-124">Hello API возвращает hello обнаружил язык и численный показатель между 0 и 1.</span><span class="sxs-lookup"><span data-stu-id="ed65a-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="ed65a-125">Закрыть too1 оценки указывают точностью 100%, чтобы идентифицировать hello языка задано значение true.</span><span class="sxs-lookup"><span data-stu-id="ed65a-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="ed65a-126">Поддерживается всего 120 языков.</span><span class="sxs-lookup"><span data-stu-id="ed65a-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="ed65a-127">Определение темы</span><span class="sxs-lookup"><span data-stu-id="ed65a-127">Topic detection</span></span>
<span data-ttu-id="ed65a-128">Это выпущенном API, который возвращает hello разделы верхнего обнаруженных список записи текста.</span><span class="sxs-lookup"><span data-stu-id="ed65a-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="ed65a-129">Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов.</span><span class="sxs-lookup"><span data-stu-id="ed65a-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="ed65a-130">Данный API требует не менее 100 текста записывает toobe отправлен, но является спроектированный toodetect разделы сотен toothousands записей.</span><span class="sxs-lookup"><span data-stu-id="ed65a-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="ed65a-131">Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи.</span><span class="sxs-lookup"><span data-stu-id="ed65a-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="ed65a-132">Hello API — спроектированный toowork подходит для short, отдела, записать текст, например рецензии и отзывов пользователей.</span><span class="sxs-lookup"><span data-stu-id="ed65a-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="ed65a-133">Определение интерфейса API</span><span class="sxs-lookup"><span data-stu-id="ed65a-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="ed65a-134">Заголовки</span><span class="sxs-lookup"><span data-stu-id="ed65a-134">Headers</span></span>
<span data-ttu-id="ed65a-135">Убедитесь, что включены hello правильные заголовки в запросе, который должен иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="ed65a-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="ed65a-136">Ключ учетной записи из вашей учетной записи можно найти в hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="ed65a-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="ed65a-137">Обратите внимание, что в настоящее время в качества формата входных и выходных данных принимается только JSON.</span><span class="sxs-lookup"><span data-stu-id="ed65a-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="ed65a-138">XML не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ed65a-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="ed65a-139">API-интерфейсы отдельного ответа</span><span class="sxs-lookup"><span data-stu-id="ed65a-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="ed65a-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="ed65a-140">GetSentiment</span></span>
<span data-ttu-id="ed65a-141">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="ed65a-142">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-142">**Example request**</span></span>

<span data-ttu-id="ed65a-143">В вызове hello ниже запрашивающих анализ мнений hello фразу «Hello World»:</span><span class="sxs-lookup"><span data-stu-id="ed65a-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="ed65a-144">Возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="ed65a-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="ed65a-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="ed65a-145">GetKeyPhrases</span></span>
<span data-ttu-id="ed65a-146">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="ed65a-147">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-147">**Example request**</span></span>

<span data-ttu-id="ed65a-148">В вызове hello ниже мы запрашиваете hello ключевых фраз, найденных в тексте hello «Был замечательных toostay гостиницы в, с декоративных уникальное и понятное персонал»:</span><span class="sxs-lookup"><span data-stu-id="ed65a-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="ed65a-149">Возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="ed65a-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="ed65a-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="ed65a-150">GetLanguage</span></span>
<span data-ttu-id="ed65a-151">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="ed65a-152">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-152">**Example request**</span></span>

<span data-ttu-id="ed65a-153">В вызове GET hello ниже, мы запрашивается для hello мнения по hello ключевых фраз в тексте hello *Здравствуй, мир!*</span><span class="sxs-lookup"><span data-stu-id="ed65a-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="ed65a-154">Возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="ed65a-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="ed65a-155">**Необязательные параметры**</span><span class="sxs-lookup"><span data-stu-id="ed65a-155">**Optional parameters**</span></span>

<span data-ttu-id="ed65a-156">`NumberOfLanguagesToDetect` является необязательным параметром.</span><span class="sxs-lookup"><span data-stu-id="ed65a-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="ed65a-157">по умолчанию Hello — 1.</span><span class="sxs-lookup"><span data-stu-id="ed65a-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="ed65a-158">API-интерфейсы пакетной службы</span><span class="sxs-lookup"><span data-stu-id="ed65a-158">Batch APIs</span></span>
<span data-ttu-id="ed65a-159">службы анализа текста Hello позволяет toodo мнений и извлечения ключа фразы в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="ed65a-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="ed65a-160">Обратите внимание, что в каждой из записей hello счетчики оценивается как одна транзакция.</span><span class="sxs-lookup"><span data-stu-id="ed65a-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="ed65a-161">Таким образом, при получении тональности для 1000 записей в одном запросе будет вычтено 1000 транзакций.</span><span class="sxs-lookup"><span data-stu-id="ed65a-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="ed65a-162">Обратите внимание, что идентификаторы hello введенные в системе hello используются идентификаторы hello, возвращаемого системной hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="ed65a-163">Hello веб-службы не проверяет, что эти идентификаторы уникальны.</span><span class="sxs-lookup"><span data-stu-id="ed65a-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="ed65a-164">Это hello ответственность за уникальность tooverify hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="ed65a-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="ed65a-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="ed65a-165">GetSentimentBatch</span></span>
<span data-ttu-id="ed65a-166">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="ed65a-167">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-167">**Example request**</span></span>

<span data-ttu-id="ed65a-168">В hello POST вызовите ниже, мы запрашивается для hello sentiments фраз hello, «Hello World», «"Hello World Foo» и «Hello Мои World» в тексте hello hello запроса:</span><span class="sxs-lookup"><span data-stu-id="ed65a-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="ed65a-169">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="ed65a-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="ed65a-170">В ответе hello ниже вы получаете список hello показатели, связанные с текстом идентификаторы:</span><span class="sxs-lookup"><span data-stu-id="ed65a-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="ed65a-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="ed65a-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="ed65a-172">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="ed65a-173">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-173">**Example request**</span></span>

<span data-ttu-id="ed65a-174">В этом примере мы запрашиваете hello перечень sentiments для hello ключевых фраз в hello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="ed65a-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="ed65a-175">«Была замечательных toostay гостиницы на, декоративных уникальное и понятное персонала»</span><span class="sxs-lookup"><span data-stu-id="ed65a-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="ed65a-176">"It was an amazing build conference, with very interesting talks";</span><span class="sxs-lookup"><span data-stu-id="ed65a-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="ed65a-177">«hello трафика существовала, я потратил три часа будет toohello аэропорт»</span><span class="sxs-lookup"><span data-stu-id="ed65a-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="ed65a-178">Этот запрос выполняется как конечную точку toohello вызов POST:</span><span class="sxs-lookup"><span data-stu-id="ed65a-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="ed65a-179">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="ed65a-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="ed65a-180">В ответе hello ниже вы получаете hello список ключевых фраз, связанных с текстом идентификаторов:</span><span class="sxs-lookup"><span data-stu-id="ed65a-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="ed65a-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="ed65a-181">GetLanguageBatch</span></span>

<span data-ttu-id="ed65a-182">В вызове процедуры POST hello ниже запрашивающих определения языка для двух входных значений текста:</span><span class="sxs-lookup"><span data-stu-id="ed65a-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="ed65a-183">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="ed65a-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="ed65a-184">Возвращает следующий ответ, когда обнаруживается английского языка в первых входных данных hello и французский языки в вторую входную строку hello hello:</span><span class="sxs-lookup"><span data-stu-id="ed65a-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="ed65a-185">Интерфейсы API определения темы</span><span class="sxs-lookup"><span data-stu-id="ed65a-185">Topic Detection APIs</span></span>
<span data-ttu-id="ed65a-186">Это выпущенном API, который возвращает hello разделы верхнего обнаруженных список записи текста.</span><span class="sxs-lookup"><span data-stu-id="ed65a-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="ed65a-187">Тема определяется по ключевой фразе, которая может содержать одно или несколько связанных слов.</span><span class="sxs-lookup"><span data-stu-id="ed65a-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="ed65a-188">Обратите внимание, что для этого API-интерфейса тарифицируется каждая транзакция для текстовой записи.</span><span class="sxs-lookup"><span data-stu-id="ed65a-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="ed65a-189">Данный API требует не менее 100 текста записывает toobe отправлен, но является спроектированный toodetect разделы сотен toothousands записей.</span><span class="sxs-lookup"><span data-stu-id="ed65a-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="ed65a-190">Темы — отправить задание</span><span class="sxs-lookup"><span data-stu-id="ed65a-190">Topics – Submit job</span></span>
<span data-ttu-id="ed65a-191">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="ed65a-192">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-192">**Example request**</span></span>

<span data-ttu-id="ed65a-193">В вызове процедуры POST hello ниже запрашивающих разделы для набора 100 статей, где hello и фамилии ввода показываются статьи и два StopPhrases включены.</span><span class="sxs-lookup"><span data-stu-id="ed65a-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="ed65a-194">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="ed65a-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="ed65a-195">В ответе hello ниже вы получаете hello JobId hello отправленного задания:</span><span class="sxs-lookup"><span data-stu-id="ed65a-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="ed65a-196">Список из слов или фраз, которые не нужно возвращать в качестве темы.</span><span class="sxs-lookup"><span data-stu-id="ed65a-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="ed65a-197">Может быть используется toofilter out очень универсальным разделах.</span><span class="sxs-lookup"><span data-stu-id="ed65a-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="ed65a-198">Например, в наборе данных об обзорах отелей разумно использовать стоповые фразы "отель" и "хостел".</span><span class="sxs-lookup"><span data-stu-id="ed65a-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="ed65a-199">Темы — опрос результатов задания</span><span class="sxs-lookup"><span data-stu-id="ed65a-199">Topics – Poll for job results</span></span>
<span data-ttu-id="ed65a-200">**URL-адрес**</span><span class="sxs-lookup"><span data-stu-id="ed65a-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="ed65a-201">**Пример запроса**</span><span class="sxs-lookup"><span data-stu-id="ed65a-201">**Example request**</span></span>

<span data-ttu-id="ed65a-202">Передайте приветствия JobId возвращенные hello «отправить» шаг toofetch hello результаты задания.</span><span class="sxs-lookup"><span data-stu-id="ed65a-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="ed65a-203">Рекомендуется вызывать эту конечную точку каждую минуту, пока состояние = «Завершено» в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="ed65a-204">Он займет около 10 минут toocomplete задания или более заданий с нескольких тысяч записей.</span><span class="sxs-lookup"><span data-stu-id="ed65a-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="ed65a-205">Во время обработки, hello ответа будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ed65a-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="ed65a-206">Hello API возвращает выходные данные в формате JSON в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="ed65a-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="ed65a-207">Hello свойства для каждой части ответа hello выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ed65a-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="ed65a-208">**Свойства TopicInfo**</span><span class="sxs-lookup"><span data-stu-id="ed65a-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="ed65a-209">Ключ</span><span class="sxs-lookup"><span data-stu-id="ed65a-209">Key</span></span> | <span data-ttu-id="ed65a-210">Описание</span><span class="sxs-lookup"><span data-stu-id="ed65a-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ed65a-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="ed65a-211">TopicId</span></span> |<span data-ttu-id="ed65a-212">Уникальный идентификатор каждой темы.</span><span class="sxs-lookup"><span data-stu-id="ed65a-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="ed65a-213">Оценка</span><span class="sxs-lookup"><span data-stu-id="ed65a-213">Score</span></span> |<span data-ttu-id="ed65a-214">Количество записей назначить tootopic.</span><span class="sxs-lookup"><span data-stu-id="ed65a-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="ed65a-215">KeyPhrase</span><span class="sxs-lookup"><span data-stu-id="ed65a-215">KeyPhrase</span></span> |<span data-ttu-id="ed65a-216">Суммирование слово или фразу для раздела hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="ed65a-217">Может состоять из одного или нескольких слов.</span><span class="sxs-lookup"><span data-stu-id="ed65a-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="ed65a-218">**Свойства TopicAssignment**</span><span class="sxs-lookup"><span data-stu-id="ed65a-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="ed65a-219">Ключ</span><span class="sxs-lookup"><span data-stu-id="ed65a-219">Key</span></span> | <span data-ttu-id="ed65a-220">Описание</span><span class="sxs-lookup"><span data-stu-id="ed65a-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ed65a-221">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="ed65a-221">Id</span></span> |<span data-ttu-id="ed65a-222">Идентификатор записи hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-222">Identifier for hello record.</span></span> <span data-ttu-id="ed65a-223">Указывает идентификатор toohello, включенные во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="ed65a-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="ed65a-224">TopicId</span></span> |<span data-ttu-id="ed65a-225">Идентификатор раздела Hello назначены какие записи hello.</span><span class="sxs-lookup"><span data-stu-id="ed65a-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="ed65a-226">Distance</span><span class="sxs-lookup"><span data-stu-id="ed65a-226">Distance</span></span> |<span data-ttu-id="ed65a-227">Уверенность, что hello запись принадлежит toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="ed65a-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="ed65a-228">Расстояние ближе toozero указывает достоверности выше.</span><span class="sxs-lookup"><span data-stu-id="ed65a-228">Distance closer toozero indicates higher confidence.</span></span> |

