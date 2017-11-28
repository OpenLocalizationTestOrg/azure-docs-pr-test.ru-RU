---
title: "Прогнозирование на основе метода экспоненциального сглаживания в Azure (устаревшая версия) | Документация Майкрософт"
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
redirect_document_id: TRUE
ms.openlocfilehash: 736d5d4adb8ecfd1e3372d273b64917f4a2e76ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="b1fdd-103">Прогнозирование на основе метода экспоненциального сглаживания (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="b1fdd-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="b1fdd-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="b1fdd-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="b1fdd-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="b1fdd-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="b1fdd-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="b1fdd-107">Эта [веб-служба](https://datamarket.azure.com/dataset/aml_labs/ets) использует модель экспоненциального сглаживания (ETS) для формирования прогнозов на основе предоставленных пользователем исторических данных.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements the Exponential Smoothing model (ETS) to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="b1fdd-108">Увеличится ли в этом году спрос на определенный продукт?</span><span class="sxs-lookup"><span data-stu-id="b1fdd-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="b1fdd-109">Могу ли я предсказать объем продаж в сезон Рождества, чтобы эффективно спланировать товарные запасы?</span><span class="sxs-lookup"><span data-stu-id="b1fdd-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="b1fdd-110">Модели прогнозирования позволяют решать такие задачи.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="b1fdd-111">Используя прошлые данные в качестве базы, эти модели анализируют скрытые тенденции и сезонные колебания для прогнозирования будущих тенденций.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="b1fdd-112">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="b1fdd-113">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="b1fdd-114">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="b1fdd-115">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="b1fdd-116">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="b1fdd-116">Consumption of web service</span></span>
<span data-ttu-id="b1fdd-117">Эта служба принимает 4 аргумента и рассчитывает прогнозы ETS.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-117">This service accepts 4 arguments and calculates the ETS forecasts.</span></span>
<span data-ttu-id="b1fdd-118">Входные аргументы:</span><span class="sxs-lookup"><span data-stu-id="b1fdd-118">The input arguments are:</span></span>

* <span data-ttu-id="b1fdd-119">Частота: частота необработанных данных (ежедневно, еженедельно, ежемесячно, ежеквартально или ежегодно).</span><span class="sxs-lookup"><span data-stu-id="b1fdd-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="b1fdd-120">Горизонт: временные рамки прогноза на будущее.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="b1fdd-121">Дата: добавление новых данных временных рядов для времени.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="b1fdd-122">Значение: добавление новых значений данных временных рядов.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="b1fdd-123">Результатом выполнения службы являются рассчитанные значения прогноза.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="b1fdd-124">Пример вводимых данных:</span><span class="sxs-lookup"><span data-stu-id="b1fdd-124">Sample input could be:</span></span> 

* <span data-ttu-id="b1fdd-125">Частота: 12</span><span class="sxs-lookup"><span data-stu-id="b1fdd-125">Frequency - 12</span></span>
* <span data-ttu-id="b1fdd-126">Горизонт: 12</span><span class="sxs-lookup"><span data-stu-id="b1fdd-126">Horizon - 12</span></span>
* <span data-ttu-id="b1fdd-127">Дата: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="b1fdd-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="b1fdd-128">Значение: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="b1fdd-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="b1fdd-129">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="b1fdd-130">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="b1fdd-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="b1fdd-131">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="b1fdd-131">Starting C# code for web service consumption:</span></span>
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



## <a name="creation-of-web-service"></a><span data-ttu-id="b1fdd-132">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="b1fdd-132">Creation of web service</span></span>
> <span data-ttu-id="b1fdd-133">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="b1fdd-134">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="b1fdd-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="b1fdd-135">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="b1fdd-136">В службах машинного обучения Azure создан пустой эксперимент.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="b1fdd-137">Загружен образец входных данных с заранее заданной схемой данных.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="b1fdd-138">Со схемой данных связан модуль [Выполнить сценарий R][execute-r-script], который создает модель прогнозирования ETS с помощью функций ets и forecast языка R.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-138">Linked to the data schema is an [Execute R Script][execute-r-script] module that generates the ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="b1fdd-140">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="b1fdd-140">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Образец данных][3]    

#### <a name="module-2"></a><span data-ttu-id="b1fdd-142">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="b1fdd-142">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="b1fdd-143">Ограничения</span><span class="sxs-lookup"><span data-stu-id="b1fdd-143">Limitations</span></span>
<span data-ttu-id="b1fdd-144">Это очень простой пример использования модели прогнозирования ETS.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="b1fdd-145">Как видно из приведенного выше образца кода, в нем не отслеживаются ошибки, служба предполагает, что все переменные являются непрерывными или положительными значениями, а частота должна быть целым числом больше 1.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-145">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="b1fdd-146">Длина даты и векторов значений должна быть одинаковой.</span><span class="sxs-lookup"><span data-stu-id="b1fdd-146">The length of the date and value vectors should be the same.</span></span> <span data-ttu-id="b1fdd-147">Переменная даты должна быть в формате "мм/дд/гггг".</span><span class="sxs-lookup"><span data-stu-id="b1fdd-147">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="b1fdd-148">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="b1fdd-148">FAQ</span></span>
<span data-ttu-id="b1fdd-149">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="b1fdd-149">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

