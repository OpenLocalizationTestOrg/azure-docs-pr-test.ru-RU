---
title: "Примеры веб-служб машинного обучения на языке R в Azure (устаревшая версия) | Документация Майкрософт"
description: "Здесь вы найдете полезный набор примеров веб-служб, созданных с помощью кода R и системы машинного обучения и опубликованных в Azure Marketplace (устаревшая версия)."
keywords: "csharp, код r, примеры веб-служб"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="5d52c-104">Примеры веб-служб, использующие код на языке R в системе машинного обучения Azure и опубликованные в Microsoft Azure Marketplace (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="5d52c-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="5d52c-105">Работа Microsoft DataMarket прекращается, и эти API-интерфейсы больше не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="5d52c-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="5d52c-106">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5d52c-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5d52c-107">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="5d52c-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="5d52c-108">В этой статье приводятся примеры веб-служб, созданные с помощью системы машинного обучения Azure и опубликованные в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5d52c-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="5d52c-109">К каждому примеру прилагается подробный документ, включающий образцы наборов данных для тестирования служб и объясняющий, как пользователь может самостоятельно создать аналогичную службу.</span><span class="sxs-lookup"><span data-stu-id="5d52c-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="5d52c-110">С помощью Azure Machine Learning Studio пользователи могут написать код R и всего несколькими щелчками опубликовать его как веб-службу, чтобы другие приложения и устройства по всему миру могли ею пользоваться.</span><span class="sxs-lookup"><span data-stu-id="5d52c-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="5d52c-111">Благодаря простым вычислениям, предоставляющим статистические функции для создания средства прогнозирования мнений на основе интеллектуального анализа текстов, как новички, так и опытные пользователи кода R почувствуют, как легко пользователи системы машинного обучения Azure могут ввести его в действие.</span><span class="sxs-lookup"><span data-stu-id="5d52c-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="5d52c-112">Хотя эти веб-службы могут применяться пользователями (потенциально через мобильное приложение или веб-сайт), они также служат примером того, как система машинного обучения Azure может вводить в действие скрипты R для аналитических целей и использоваться для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="5d52c-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="5d52c-113">Каждый пример включает пример на языке C# для использования веб-службы.</span><span class="sxs-lookup"><span data-stu-id="5d52c-113">Each example includes a C# example for web service consumption.</span></span>

![Схема кода R в системе машинного обучения Azure: решения на языке R для личного использования или публикации в Azure Marketplace.][1]

<span data-ttu-id="5d52c-115">Рассмотрим следующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="5d52c-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="5d52c-116">Сценарий 1. Универсальная модель</span><span class="sxs-lookup"><span data-stu-id="5d52c-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="5d52c-117">Пользователь работает с универсальной моделью, которая может быть применена к новым пользовательским данным, например с базовым прогнозированием данных временных рядов или с пользовательским методом R с расширенной аналитикой.</span><span class="sxs-lookup"><span data-stu-id="5d52c-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="5d52c-118">Этот пользователь публикует модель как веб-службу, чтобы другие пользователи могли использовать ее со своими данными.</span><span class="sxs-lookup"><span data-stu-id="5d52c-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="5d52c-119">Бинарный классификатор</span><span class="sxs-lookup"><span data-stu-id="5d52c-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="5d52c-120">Кластерная модель</span><span class="sxs-lookup"><span data-stu-id="5d52c-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="5d52c-121">Многомерная линейная регрессия</span><span class="sxs-lookup"><span data-stu-id="5d52c-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="5d52c-122">Прогнозирование на основе метода экспоненциального сглаживания</span><span class="sxs-lookup"><span data-stu-id="5d52c-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="5d52c-123">Прогнозирование ETS+STL</span><span class="sxs-lookup"><span data-stu-id="5d52c-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="5d52c-124">Прогнозирование: авторегрессионная интегрированная модель скользящего среднего (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="5d52c-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="5d52c-125">Анализ выживаемости</span><span class="sxs-lookup"><span data-stu-id="5d52c-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="5d52c-126">Сценарий 2. Обученная модель — определенные данные</span><span class="sxs-lookup"><span data-stu-id="5d52c-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="5d52c-127">У пользователя есть данные, которые предоставляют полезные прогнозы через код R, например большая выборка личностных анкет, кластеризованных с помощью алгоритма K-средних для прогнозирования типа личности пользователя, или данные исследования в области здравоохранения, которые могут использоваться для прогнозирования риска заболевания раком легких с помощью пакета R анализа выживаемости.</span><span class="sxs-lookup"><span data-stu-id="5d52c-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="5d52c-128">Пользователь публикует данные через веб-службу, которая прогнозирует результат для нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d52c-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="5d52c-129">Сценарий 3. Обученная модель — универсальные данные</span><span class="sxs-lookup"><span data-stu-id="5d52c-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="5d52c-130">У пользователя есть универсальные данные (например, текстовая база данных), позволяющие построить веб-службу и применять ее универсально для различных типов сценариев.</span><span class="sxs-lookup"><span data-stu-id="5d52c-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="5d52c-131">Анализ мнений на основе словаря</span><span class="sxs-lookup"><span data-stu-id="5d52c-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="5d52c-132">Сценарий 4. Расширенный калькулятор</span><span class="sxs-lookup"><span data-stu-id="5d52c-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="5d52c-133">Пользователь предоставляет комплексные вычисления или моделирования, для которых не требуется обученная модель или подгонка модели под данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="5d52c-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="5d52c-134">Тест на разницу в пропорциях</span><span class="sxs-lookup"><span data-stu-id="5d52c-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="5d52c-135">Набор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5d52c-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="5d52c-136">Набор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="5d52c-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="5d52c-137">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="5d52c-137">FAQ</span></span>
<span data-ttu-id="5d52c-138">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Магазине можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="5d52c-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



