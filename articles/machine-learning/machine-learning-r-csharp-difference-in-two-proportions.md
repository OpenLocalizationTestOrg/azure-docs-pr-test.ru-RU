---
title: "Разница в тесте пропорции - Azure AAA(deprecated) | Документы Microsoft"
description: "Тест на разницу в пропорциях (устаревшая версия)"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="76b6f-103">Тест на разницу в пропорциях (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="76b6f-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="76b6f-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="76b6f-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="76b6f-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="76b6f-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="76b6f-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="76b6f-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="76b6f-107">Существует ли между двумя долями статистическая разница?</span><span class="sxs-lookup"><span data-stu-id="76b6f-107">Are two proportions statistically different?</span></span> <span data-ttu-id="76b6f-108">Предположим, что пользователь хочет toocompare двух toodetermine фильмы, если один фильма имеет значительно большее количество «нравится» при сравнении toohello других.</span><span class="sxs-lookup"><span data-stu-id="76b6f-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="76b6f-109">С большой образец может быть статистически значимой разницы между hello пропорции 0,50 и 0,51.</span><span class="sxs-lookup"><span data-stu-id="76b6f-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="76b6f-110">С небольшой выборкой может отсутствовать toodetermine достаточно данных, если эти пропорции, фактически отличаются.</span><span class="sxs-lookup"><span data-stu-id="76b6f-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="76b6f-111">Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/prop_test) выполняет тест гипотезы hello разницы в двух пропорции, на основе ввода пользователя hello количество успешных и общее количество пробных версий для сравнения групп hello 2 hello.</span><span class="sxs-lookup"><span data-stu-id="76b6f-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="76b6f-112">В один из возможных сценариев можно вызывать веб-службу из в приложении сравнения фильм, предписывая пользователя hello ли один фильмов hello «применено» чаще, чем другие, hello на основе фильма оценок.</span><span class="sxs-lookup"><span data-stu-id="76b6f-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="76b6f-113">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="76b6f-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="76b6f-114">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="76b6f-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="76b6f-115">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="76b6f-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="76b6f-116">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="76b6f-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="76b6f-117">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="76b6f-117">Consumption of web service</span></span>
<span data-ttu-id="76b6f-118">Эта служба принимает 4 аргумента и выполняет проверку гипотезы для долей.</span><span class="sxs-lookup"><span data-stu-id="76b6f-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="76b6f-119">Hello входными аргументами являются:</span><span class="sxs-lookup"><span data-stu-id="76b6f-119">hello input arguments are:</span></span>

* <span data-ttu-id="76b6f-120">Successes1 — количество успешных испытаний в выборке 1.</span><span class="sxs-lookup"><span data-stu-id="76b6f-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="76b6f-121">Successes2 — количество успешных испытаний в выборке 2.</span><span class="sxs-lookup"><span data-stu-id="76b6f-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="76b6f-122">Total1 — размер выборки 1.</span><span class="sxs-lookup"><span data-stu-id="76b6f-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="76b6f-123">Total2 — размер выборки 2.</span><span class="sxs-lookup"><span data-stu-id="76b6f-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="76b6f-124">выходные данные Hello hello службы является результатом hello гипотезы hello тестов вместе с значение hello chi-square статистики, df, p и пропорция в пределах 1/2 и доверительный интервал образца.</span><span class="sxs-lookup"><span data-stu-id="76b6f-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="76b6f-125">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="76b6f-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="76b6f-126">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="76b6f-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="76b6f-127">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="76b6f-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="76b6f-128">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="76b6f-128">Creation of web service</span></span>
> <span data-ttu-id="76b6f-129">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="76b6f-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="76b6f-130">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="76b6f-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="76b6f-131">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="76b6f-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="76b6f-132">В системе машинного обучения Azure был создан пустой эксперимент с двумя модулями [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="76b6f-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="76b6f-133">В первый модуль hello hello схемы данных определен, второй модуль hello не используется команда prop.test hello в тест гипотезы hello tooperform R для 2 пропорций.</span><span class="sxs-lookup"><span data-stu-id="76b6f-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="76b6f-134">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="76b6f-134">Experiment flow:</span></span>
![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="76b6f-136">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="76b6f-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="76b6f-137">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="76b6f-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="76b6f-138">Ограничения</span><span class="sxs-lookup"><span data-stu-id="76b6f-138">Limitations</span></span>
<span data-ttu-id="76b6f-139">Это очень простой пример проверки различия двух долей.</span><span class="sxs-lookup"><span data-stu-id="76b6f-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="76b6f-140">Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и служба hello предполагается, что все переменные hello непрерывной.</span><span class="sxs-lookup"><span data-stu-id="76b6f-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="76b6f-141">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="76b6f-141">FAQ</span></span>
<span data-ttu-id="76b6f-142">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="76b6f-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

