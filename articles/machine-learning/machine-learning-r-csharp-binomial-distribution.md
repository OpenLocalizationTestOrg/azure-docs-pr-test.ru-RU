---
title: "Набор биномиального распределения Azure (устаревшая версия) | Документация Майкрософт"
description: "Сведения о наборе биномиального распределения (устаревшая версия)."
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="a8dff-103">Набор биномиального распределения (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="a8dff-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="a8dff-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a8dff-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="a8dff-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="a8dff-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a8dff-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a8dff-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="a8dff-107">Набор веб-служб биномиального распределения состоит из трех веб-служб ([Биномиальный генератор](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Калькулятор вероятностей](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Калькулятор квантилей](https://datamarket.azure.com/dataset/aml_labs/bdq5)), предназначенных для создания биномиальных распределений и работы с ними.</span><span class="sxs-lookup"><span data-stu-id="a8dff-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="a8dff-108">С их помощью можно создать биномиальное распределение любой длины, рассчитать квантили для любой заданной вероятности, а также вероятность — для заданного квантиля.</span><span class="sxs-lookup"><span data-stu-id="a8dff-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="a8dff-109">Каждая служба выдает собственный набор выходных данных (см. описание ниже).</span><span class="sxs-lookup"><span data-stu-id="a8dff-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="a8dff-110">В основе набора веб-служб биномиального распределения лежит использование функций qbinom, rbinom и pbinom, которые входят в пакет статистических функций языка R.</span><span class="sxs-lookup"><span data-stu-id="a8dff-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="a8dff-111">С этими веб-службами пользователи могут работать непосредственно из магазина, через мобильное приложение, веб-сайт или даже локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a8dff-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="a8dff-112">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="a8dff-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="a8dff-113">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dff-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="a8dff-114">Авторы таких служб могут размещать их в магазине Azure Marketplace и предлагать пользователям и устройствам со всего мира, не тратя время и усилия на создание соответствующей инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a8dff-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="a8dff-115">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="a8dff-115">Consumption of web service</span></span>
<span data-ttu-id="a8dff-116">В состав набора веб-служб биномиального распределения входят перечисленные ниже 3 службы.</span><span class="sxs-lookup"><span data-stu-id="a8dff-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="a8dff-117">Калькулятор квантилей биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="a8dff-118">Эта служба принимает четыре аргумента нормального распределения и рассчитывает соответствующий квантиль.</span><span class="sxs-lookup"><span data-stu-id="a8dff-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="a8dff-119">Входные аргументы:</span><span class="sxs-lookup"><span data-stu-id="a8dff-119">The input arguments are:</span></span>

* <span data-ttu-id="a8dff-120">p — единое обобщенное значение вероятности для набора испытаний.</span><span class="sxs-lookup"><span data-stu-id="a8dff-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="a8dff-121">size — количество испытаний</span><span class="sxs-lookup"><span data-stu-id="a8dff-121">size - The number of trials.</span></span>
* <span data-ttu-id="a8dff-122">prob — вероятность успешного испытания.</span><span class="sxs-lookup"><span data-stu-id="a8dff-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="a8dff-123">Side — L для нижней или U для верхней части распределения.</span><span class="sxs-lookup"><span data-stu-id="a8dff-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="a8dff-124">На выходе служба выдает рассчитанный квантиль, связанный с заданной вероятностью.</span><span class="sxs-lookup"><span data-stu-id="a8dff-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="a8dff-125">Калькулятор вероятности биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="a8dff-126">Эта служба принимает четыре аргумента биномиального распределения и рассчитывает соответствующую вероятность.</span><span class="sxs-lookup"><span data-stu-id="a8dff-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="a8dff-127">Входные аргументы:</span><span class="sxs-lookup"><span data-stu-id="a8dff-127">The input arguments are:</span></span>

* <span data-ttu-id="a8dff-128">q — один квантиль события с биномиальным распределением.</span><span class="sxs-lookup"><span data-stu-id="a8dff-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="a8dff-129">size — количество испытаний</span><span class="sxs-lookup"><span data-stu-id="a8dff-129">size - The number of trials.</span></span>
* <span data-ttu-id="a8dff-130">prob — вероятность успешного испытания.</span><span class="sxs-lookup"><span data-stu-id="a8dff-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="a8dff-131">side — L для нижней или U для верхней части распределения либо E (одно значение количества успешных испытаний).</span><span class="sxs-lookup"><span data-stu-id="a8dff-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="a8dff-132">На выходе служба выдает рассчитанную вероятность, связанную с заданным квантилем.</span><span class="sxs-lookup"><span data-stu-id="a8dff-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="a8dff-133">Генератор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="a8dff-134">Эта служба принимает три аргумента биномиального распределения и создает случайную последовательность биномиально распределенных чисел.</span><span class="sxs-lookup"><span data-stu-id="a8dff-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="a8dff-135">Ниже описаны аргументы, передаваемые этой службе в запросе.</span><span class="sxs-lookup"><span data-stu-id="a8dff-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="a8dff-136">n — количество наблюдений.</span><span class="sxs-lookup"><span data-stu-id="a8dff-136">n - Number of observations.</span></span> 
* <span data-ttu-id="a8dff-137">size — количество испытаний.</span><span class="sxs-lookup"><span data-stu-id="a8dff-137">size - Number of trials.</span></span>
* <span data-ttu-id="a8dff-138">prob — вероятность успеха.</span><span class="sxs-lookup"><span data-stu-id="a8dff-138">prob - Probability of success.</span></span>

<span data-ttu-id="a8dff-139">На выходе служба выдает последовательность чисел длины n с биномиальным распределением на основе аргументов size и prob.</span><span class="sxs-lookup"><span data-stu-id="a8dff-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="a8dff-140">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="a8dff-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="a8dff-141">Автоматизировать использование этой службы можно несколькими способами (примеры приложений: [Генератор](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Калькулятор вероятности](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Калькулятор квантилей](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="a8dff-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="a8dff-142">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="a8dff-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="a8dff-143">Калькулятор квантилей биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="a8dff-144">Калькулятор вероятности биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="a8dff-145">Генератор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="a8dff-146">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="a8dff-146">Creation of web service</span></span>
> <span data-ttu-id="a8dff-147">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a8dff-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="a8dff-148">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="a8dff-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="a8dff-149">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="a8dff-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="a8dff-150">Калькулятор квантилей биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-150">Binomial Distribution Quantile Calculator</span></span>
![Создание рабочей области][4]

#### <a name="module-1"></a><span data-ttu-id="a8dff-152">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="a8dff-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="a8dff-153">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="a8dff-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="a8dff-154">Калькулятор вероятности биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-154">Binomial Distribution Probability Calculator</span></span>
![Создание рабочей области][5]

#### <a name="module-1"></a><span data-ttu-id="a8dff-156">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="a8dff-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="a8dff-157">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="a8dff-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="a8dff-158">Генератор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="a8dff-158">Binomial Distribution Generator</span></span>
![Создание рабочей области][6]

#### <a name="module-1"></a><span data-ttu-id="a8dff-160">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="a8dff-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="a8dff-161">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="a8dff-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="a8dff-162">Ограничения</span><span class="sxs-lookup"><span data-stu-id="a8dff-162">Limitations</span></span>
<span data-ttu-id="a8dff-163">Это очень простой пример, выполняющий операции с биномиальными распределениями.</span><span class="sxs-lookup"><span data-stu-id="a8dff-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="a8dff-164">Как видно из приведенного выше образца кода, в нем практически не отслеживаются ошибки.</span><span class="sxs-lookup"><span data-stu-id="a8dff-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="a8dff-165">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="a8dff-165">FAQ</span></span>
<span data-ttu-id="a8dff-166">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a8dff-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

