---
title: "AAA(deprecated) машины обучения, веб-служб, примеры, созданного с помощью R - Azure | Документы Microsoft"
description: "(устарело) Найти полезные набор примеров web services создана с кодом R и машинное обучение и опубликована toohello Azure Marketplace."
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="57382-104">(устарело) Примеры использования кода R в машинном обучении Azure и опубликованных tooMicrosoft Azure Marketplace веб-службы</span><span class="sxs-lookup"><span data-stu-id="57382-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="57382-105">Hello Microsoft DataMarket прекращено, и эти API-интерфейсы являются устаревшими.</span><span class="sxs-lookup"><span data-stu-id="57382-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="57382-106">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="57382-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="57382-107">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="57382-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="57382-108">В этой статье, пример web services были созданы с помощью машинного обучения Azure и публикуются toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="57382-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="57382-109">Каждый пример веб-службы имеет полный документ, внедрение образцы наборов данных для тестирования службы hello и о том, как hello пользователь может создать аналогичную службу самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="57382-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="57382-110">В студии машинного обучения Azure пользователей можно написать код R и с помощью нескольких щелчков опубликовать его как веб-службы для приложения и устройства tooconsume вокруг Здравствуй, мир.</span><span class="sxs-lookup"><span data-stu-id="57382-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="57382-111">Вместо создания простого калькуляторы, предоставляющих статистические функции toocreating пользовательских прогнозирующих анализ мнений интеллектуального анализа текста, новых и опытных пользователей R могут использовать преимущества hello простота, с помощью которого пользователи машинного обучения Azure можно ввода в эксплуатацию R код.</span><span class="sxs-lookup"><span data-stu-id="57382-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="57382-112">Хотя эти веб-службы могут применяться пользователями, потенциально через мобильное приложение или веб-сайт hello цель этих веб-служб, tooshow, как можно эксплуатацию машинного обучения — примеры R скрипты для анализа и используется toocreate веб-службы на начало кода R.</span><span class="sxs-lookup"><span data-stu-id="57382-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="57382-113">Каждый пример включает пример на языке C# для использования веб-службы.</span><span class="sxs-lookup"><span data-stu-id="57382-113">Each example includes a C# example for web service consumption.</span></span>

![Схема кода R в машинном обучении Azure: решения R для использования собственных или опубликованные toohello Azure Marketplace.][1]

<span data-ttu-id="57382-115">Рассмотрим следующие сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="57382-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="57382-116">Сценарий 1. Универсальная модель</span><span class="sxs-lookup"><span data-stu-id="57382-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="57382-117">Пользователь работает с универсальной модели, который может быть применен tooa нового пользователя данных, например основные прогнозирования временного ряда данных или пользовательские метод R с расширенной аналитики.</span><span class="sxs-lookup"><span data-stu-id="57382-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="57382-118">Этот пользователь публикует hello модели веб-службы для других tooconsume с их данными.</span><span class="sxs-lookup"><span data-stu-id="57382-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="57382-119">Бинарный классификатор</span><span class="sxs-lookup"><span data-stu-id="57382-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="57382-120">Кластерная модель</span><span class="sxs-lookup"><span data-stu-id="57382-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="57382-121">Многомерная линейная регрессия</span><span class="sxs-lookup"><span data-stu-id="57382-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="57382-122">Прогнозирование на основе метода экспоненциального сглаживания</span><span class="sxs-lookup"><span data-stu-id="57382-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="57382-123">Прогнозирование ETS+STL</span><span class="sxs-lookup"><span data-stu-id="57382-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="57382-124">Прогнозирование: авторегрессионная интегрированная модель скользящего среднего (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="57382-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="57382-125">Анализ выживаемости</span><span class="sxs-lookup"><span data-stu-id="57382-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="57382-126">Сценарий 2. Обученная модель — определенные данные</span><span class="sxs-lookup"><span data-stu-id="57382-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="57382-127">У пользователя есть данные, которые предоставляют полезные прогнозы выполнение кода R, такие как большой образец опросов индивидуальность clustered через k средних алгоритм toopredict hello индивидуальность типа пользователя или работоспособности исследования данных, который можно использовать toopredict пользователя риск для вызывает рак с помощью пакета аналитики R практические советы.</span><span class="sxs-lookup"><span data-stu-id="57382-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="57382-128">Hello пользователь публикует hello данных через веб-службу, которая прогнозирует результат нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="57382-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="57382-129">Сценарий 3. Обученная модель — универсальные данные</span><span class="sxs-lookup"><span data-stu-id="57382-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="57382-130">У пользователя есть универсальный данные (например, в совокупности текста), позволяющий web service toobe построен и универсальная применения на разных типах варианты использования и сценарии.</span><span class="sxs-lookup"><span data-stu-id="57382-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="57382-131">Анализ мнений на основе словаря</span><span class="sxs-lookup"><span data-stu-id="57382-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="57382-132">Сценарий 4. Расширенный калькулятор</span><span class="sxs-lookup"><span data-stu-id="57382-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="57382-133">Пользователь предоставляет сложных расчетов или моделирования, не требующие любой обученной модели или подгонки пользователя toohello модели данных.</span><span class="sxs-lookup"><span data-stu-id="57382-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="57382-134">Тест на разницу в пропорциях</span><span class="sxs-lookup"><span data-stu-id="57382-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="57382-135">Набор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="57382-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="57382-136">Набор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="57382-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="57382-137">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="57382-137">FAQ</span></span>
<span data-ttu-id="57382-138">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="57382-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



