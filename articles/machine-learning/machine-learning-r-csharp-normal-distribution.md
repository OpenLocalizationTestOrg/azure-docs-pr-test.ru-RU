---
title: "Набор веб-служб нормального распределения Azure (устаревшая версия) | Документация Майкрософт"
description: "Сведения о наборе веб-служб нормального распределения (устаревшая версия)."
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
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
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="5b928-103">Набор нормального распределения (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="5b928-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="5b928-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="5b928-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="5b928-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5b928-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5b928-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="5b928-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="5b928-107">Набор веб-служб нормального распределения состоит из трех веб-служб ([Генератор](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Калькулятор квантилей](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Калькулятор вероятностей](https://datamarket.azure.com/dataset/aml_labs/ndp5)), предназначенных для создания нормальных распределений и работы с ними.</span><span class="sxs-lookup"><span data-stu-id="5b928-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="5b928-108">С их помощью можно создать нормальное распределение любой длины, рассчитать квантили для любой заданной вероятности, а также вероятность — для заданного квантиля.</span><span class="sxs-lookup"><span data-stu-id="5b928-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="5b928-109">Каждая служба выдает собственный набор выходных данных (см. описание ниже).</span><span class="sxs-lookup"><span data-stu-id="5b928-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="5b928-110">В основе набора веб-служб нормального распределения лежит использование функций qnorm, rnorm и pnorm, которые входят в пакет статистических функций на языке R.</span><span class="sxs-lookup"><span data-stu-id="5b928-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="5b928-111">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5b928-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="5b928-112">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="5b928-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="5b928-113">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="5b928-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="5b928-114">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="5b928-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="5b928-115">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="5b928-115">Consumption of web service</span></span>
<span data-ttu-id="5b928-116">В состав набора веб-служб нормального распределения входят перечисленные ниже три службы.</span><span class="sxs-lookup"><span data-stu-id="5b928-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="5b928-117">Калькулятор квантилей нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="5b928-118">Эта служба принимает четыре аргумента нормального распределения и рассчитывает соответствующий квантиль.</span><span class="sxs-lookup"><span data-stu-id="5b928-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="5b928-119">Входные аргументы:</span><span class="sxs-lookup"><span data-stu-id="5b928-119">The input arguments are:</span></span>

* <span data-ttu-id="5b928-120">p — одна вероятность события с нормальным распределением.</span><span class="sxs-lookup"><span data-stu-id="5b928-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="5b928-121">Mean — среднее значение нормального распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="5b928-122">SD — стандартное отклонение нормального распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="5b928-123">Side — L для нижней или U для верхней части распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="5b928-124">На выходе служба выдает рассчитанный квантиль, связанный с заданной вероятностью.</span><span class="sxs-lookup"><span data-stu-id="5b928-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="5b928-125">Калькулятор вероятности нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="5b928-126">Эта служба принимает четыре аргумента нормального распределения и рассчитывает соответствующую вероятность.</span><span class="sxs-lookup"><span data-stu-id="5b928-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="5b928-127">Входные аргументы:</span><span class="sxs-lookup"><span data-stu-id="5b928-127">The input arguments are:</span></span>

* <span data-ttu-id="5b928-128">q — один квантиль события с нормальным распределением.</span><span class="sxs-lookup"><span data-stu-id="5b928-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="5b928-129">Mean — среднее значение нормального распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="5b928-130">SD — стандартное отклонение нормального распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="5b928-131">Side — L для нижней или U для верхней части распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="5b928-132">На выходе служба выдает рассчитанную вероятность, связанную с заданным квантилем.</span><span class="sxs-lookup"><span data-stu-id="5b928-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="5b928-133">Генератор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-133">Normal Distribution Generator</span></span>
<span data-ttu-id="5b928-134">Эта служба принимает три аргумента нормального распределения и создает случайную последовательность нормально распределенных чисел.</span><span class="sxs-lookup"><span data-stu-id="5b928-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="5b928-135">Ниже описаны аргументы, передаваемые этой службе в запросе.</span><span class="sxs-lookup"><span data-stu-id="5b928-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="5b928-136">n — количество наблюдений.</span><span class="sxs-lookup"><span data-stu-id="5b928-136">n - The number of observations.</span></span> 
* <span data-ttu-id="5b928-137">Mean — среднее значение нормального распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="5b928-138">SD — стандартное отклонение нормального распределения.</span><span class="sxs-lookup"><span data-stu-id="5b928-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="5b928-139">На выходе служба выдает последовательность чисел длины n с нормальным распределением на основе аргументов mean и sd.</span><span class="sxs-lookup"><span data-stu-id="5b928-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="5b928-140">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="5b928-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="5b928-141">Автоматизировать использование этой службы можно несколькими способами (примеры приложений: [Генератор](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Калькулятор вероятности](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Калькулятор квантилей](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="5b928-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="5b928-142">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="5b928-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="5b928-143">Калькулятор квантилей нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="5b928-144">Калькулятор вероятности нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="5b928-145">Генератор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="5b928-146">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="5b928-146">Creation of web service</span></span>
> <span data-ttu-id="5b928-147">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="5b928-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="5b928-148">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="5b928-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="5b928-149">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="5b928-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="5b928-150">Калькулятор квантилей нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="5b928-151">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="5b928-151">Experiment flow:</span></span>

![Ход эксперимента][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="5b928-153">Калькулятор вероятности нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="5b928-154">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="5b928-154">Experiment flow:</span></span>

![Ход эксперимента][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="5b928-156">Генератор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="5b928-156">Normal Distribution Generator</span></span>
<span data-ttu-id="5b928-157">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="5b928-157">Experiment flow:</span></span>

![Ход эксперимента][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="5b928-159">Ограничения</span><span class="sxs-lookup"><span data-stu-id="5b928-159">Limitations</span></span>
<span data-ttu-id="5b928-160">Это очень простой пример, выполняющий операции с нормальными распределениями.</span><span class="sxs-lookup"><span data-stu-id="5b928-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="5b928-161">Как видно из приведенного выше образца кода, в нем практически не отслеживаются ошибки.</span><span class="sxs-lookup"><span data-stu-id="5b928-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="5b928-162">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="5b928-162">FAQ</span></span>
<span data-ttu-id="5b928-163">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="5b928-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

