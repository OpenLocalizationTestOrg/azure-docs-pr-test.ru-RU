---
title: "AAA(deprecated) - Экспоненциальное сглаживание - Forecasting Azure | Документы Microsoft"
description: "Веб-служба: прогнозирование на основе метода экспоненциального сглаживания (устаревшая версия)."
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: ebc732d3a47943405b0cb26a373f529a50de9005
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="48896-103">Прогнозирование на основе метода экспоненциального сглаживания (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="48896-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="48896-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="48896-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="48896-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="48896-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="48896-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="48896-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="48896-107">Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/ets) реализует hello Экспоненциальное сглаживание прогнозы tooproduce модели (ETS) на основании исторических данных hello, предоставленный пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="48896-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements hello Exponential Smoothing model (ETS) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="48896-108">Будет hello запросу увеличивать определенного продукта в этом году?</span><span class="sxs-lookup"><span data-stu-id="48896-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="48896-109">Можно ли прогнозирования продаж продукта для hello сезона Рождество, чтобы эффективно задавать my инвентаризации?</span><span class="sxs-lookup"><span data-stu-id="48896-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="48896-110">Модели прогнозирования являются apt tooaddress такие вопросы.</span><span class="sxs-lookup"><span data-stu-id="48896-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="48896-111">Учитывая hello данных, в прошлом эти модели проверки скрытые тенденции и будущие тенденции toopredict сезонности.</span><span class="sxs-lookup"><span data-stu-id="48896-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="48896-112">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="48896-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="48896-113">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="48896-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="48896-114">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="48896-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="48896-115">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="48896-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="48896-116">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="48896-116">Consumption of web service</span></span>
<span data-ttu-id="48896-117">Эта служба принимает аргументы, 4 и вычисляет прогнозы ETS hello.</span><span class="sxs-lookup"><span data-stu-id="48896-117">This service accepts 4 arguments and calculates hello ETS forecasts.</span></span>
<span data-ttu-id="48896-118">Hello входными аргументами являются:</span><span class="sxs-lookup"><span data-stu-id="48896-118">hello input arguments are:</span></span>

* <span data-ttu-id="48896-119">Частота — указывает частоту hello hello необработанных данных (ежедневно или еженедельно или ежемесячно или ежеквартально/ежегодного резервного копирования).</span><span class="sxs-lookup"><span data-stu-id="48896-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="48896-120">Горизонт: временные рамки прогноза на будущее.</span><span class="sxs-lookup"><span data-stu-id="48896-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="48896-121">Дата — Добавление в hello нового временного ряда данных времени.</span><span class="sxs-lookup"><span data-stu-id="48896-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="48896-122">Значение — Добавление в hello новые значения рядов времени данных.</span><span class="sxs-lookup"><span data-stu-id="48896-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="48896-123">выходные данные Hello hello службы — hello вычисляемые значения прогноза.</span><span class="sxs-lookup"><span data-stu-id="48896-123">hello output of hello service is hello calculated forecast values.</span></span>

<span data-ttu-id="48896-124">Пример вводимых данных:</span><span class="sxs-lookup"><span data-stu-id="48896-124">Sample input could be:</span></span> 

* <span data-ttu-id="48896-125">Частота: 12</span><span class="sxs-lookup"><span data-stu-id="48896-125">Frequency - 12</span></span>
* <span data-ttu-id="48896-126">Горизонт: 12</span><span class="sxs-lookup"><span data-stu-id="48896-126">Horizon - 12</span></span>
* <span data-ttu-id="48896-127">Дата: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="48896-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="48896-128">Значение: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="48896-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="48896-129">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="48896-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="48896-130">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="48896-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="48896-131">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="48896-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a><span data-ttu-id="48896-132">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="48896-132">Creation of web service</span></span>
> <span data-ttu-id="48896-133">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="48896-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="48896-134">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="48896-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="48896-135">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="48896-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="48896-136">В службах машинного обучения Azure создан пустой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="48896-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="48896-137">Загружен образец входных данных с заранее заданной схемой данных.</span><span class="sxs-lookup"><span data-stu-id="48896-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="48896-138">Схема данных связанного toohello [выполнение скрипта R] [ execute-r-script] модуль, который приводит к возникновению ошибки hello ETS прогнозирование модели с помощью функции «ets» и «прогноз» из кода R.</span><span class="sxs-lookup"><span data-stu-id="48896-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module that generates hello ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="48896-140">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="48896-140">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Образец данных][3]    

#### <a name="module-2"></a><span data-ttu-id="48896-142">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="48896-142">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="48896-143">Ограничения</span><span class="sxs-lookup"><span data-stu-id="48896-143">Limitations</span></span>
<span data-ttu-id="48896-144">Это очень простой пример использования модели прогнозирования ETS.</span><span class="sxs-lookup"><span data-stu-id="48896-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="48896-145">Как видно в приведенном выше примере кода hello, перехват ошибок не реализован, и службы hello предполагается, что все переменные hello, непрерывные или положительные значения и hello частоты должно быть целое число больше 1.</span><span class="sxs-lookup"><span data-stu-id="48896-145">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="48896-146">Длина Hello hello векторов значения даты и следует hello же.</span><span class="sxs-lookup"><span data-stu-id="48896-146">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="48896-147">переменная приветствия даты должны соблюдаться toohello формат «мм/дд/гггг».</span><span class="sxs-lookup"><span data-stu-id="48896-147">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="48896-148">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="48896-148">FAQ</span></span>
<span data-ttu-id="48896-149">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="48896-149">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

