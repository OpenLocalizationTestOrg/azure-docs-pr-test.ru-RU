---
title: "Тест на разницу в пропорциях (устаревшая версия) | Документация Майкрософт"
description: "Сведения о тесте на разницу в пропорциях (устаревшая версия)."
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
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="3a070-103">Тест на разницу в пропорциях (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="3a070-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="3a070-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3a070-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3a070-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3a070-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3a070-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3a070-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3a070-107">Существует ли между двумя долями статистическая разница?</span><span class="sxs-lookup"><span data-stu-id="3a070-107">Are two proportions statistically different?</span></span> <span data-ttu-id="3a070-108">Предположим, что пользователь хочет сравнить два видеоролика и определить, действительно ли у одного из них доля положительных оценок значимо больше, чем у другого.</span><span class="sxs-lookup"><span data-stu-id="3a070-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="3a070-109">При большом размере выборки возможна статистически значительная разница между пропорциями 0,50 и 0,51.</span><span class="sxs-lookup"><span data-stu-id="3a070-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="3a070-110">При малом размере выборки может быть недостаточно данных, чтобы определить, отличаются ли эти пропорции на самом деле.</span><span class="sxs-lookup"><span data-stu-id="3a070-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="3a070-111">Эта [веб-служба](https://datamarket.azure.com/dataset/aml_labs/prop_test) проверяет гипотезу различия двух долей на основе введенных пользователем данных о количестве успешных испытаний и общем числе испытаний для двух сравниваемых групп.</span><span class="sxs-lookup"><span data-stu-id="3a070-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="3a070-112">Например, эту веб-службу может вызывать приложение, которое сравнивает видеоролики и на основе полученных ими оценок сообщает пользователю, действительно ли один из них был более положительно оценен зрителями, чем другой.</span><span class="sxs-lookup"><span data-stu-id="3a070-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="3a070-113">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3a070-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3a070-114">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="3a070-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="3a070-115">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="3a070-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3a070-116">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="3a070-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3a070-117">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="3a070-117">Consumption of web service</span></span>
<span data-ttu-id="3a070-118">Эта служба принимает 4 аргумента и выполняет проверку гипотезы для долей.</span><span class="sxs-lookup"><span data-stu-id="3a070-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="3a070-119">Входные аргументы:</span><span class="sxs-lookup"><span data-stu-id="3a070-119">The input arguments are:</span></span>

* <span data-ttu-id="3a070-120">Successes1 — количество успешных испытаний в выборке 1.</span><span class="sxs-lookup"><span data-stu-id="3a070-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="3a070-121">Successes2 — количество успешных испытаний в выборке 2.</span><span class="sxs-lookup"><span data-stu-id="3a070-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="3a070-122">Total1 — размер выборки 1.</span><span class="sxs-lookup"><span data-stu-id="3a070-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="3a070-123">Total2 — размер выборки 2.</span><span class="sxs-lookup"><span data-stu-id="3a070-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="3a070-124">На выходе служба выдает результат проверки гипотезы, а также статистику хи-квадрат, значение df, значение p, долю в выборках 1 и 2 и границы доверительного интервала.</span><span class="sxs-lookup"><span data-stu-id="3a070-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="3a070-125">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="3a070-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3a070-126">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="3a070-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3a070-127">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="3a070-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="3a070-128">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="3a070-128">Creation of web service</span></span>
> <span data-ttu-id="3a070-129">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="3a070-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3a070-130">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="3a070-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3a070-131">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="3a070-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="3a070-132">В системе машинного обучения Azure был создан пустой эксперимент с двумя модулями [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3a070-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="3a070-133">В первом из них определяется схема данных, а второй использует команду prop.test языка R для проверки гипотезы в отношении двух долей.</span><span class="sxs-lookup"><span data-stu-id="3a070-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="3a070-134">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="3a070-134">Experiment flow:</span></span>
![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="3a070-136">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="3a070-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="3a070-137">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="3a070-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="3a070-138">Ограничения</span><span class="sxs-lookup"><span data-stu-id="3a070-138">Limitations</span></span>
<span data-ttu-id="3a070-139">Это очень простой пример проверки различия двух долей.</span><span class="sxs-lookup"><span data-stu-id="3a070-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="3a070-140">Как видно из приведенного выше образца кода, в нем не отслеживаются ошибки, а служба предполагает, что все переменные являются непрерывными.</span><span class="sxs-lookup"><span data-stu-id="3a070-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="3a070-141">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3a070-141">FAQ</span></span>
<span data-ttu-id="3a070-142">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3a070-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

