---
title: "AAA(deprecated) набор службы нормальное распределение веб - Azure | Документы Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="91bce-103">Набор нормального распределения (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="91bce-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="91bce-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="91bce-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="91bce-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="91bce-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="91bce-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="91bce-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="91bce-107">Hello Suite нормальное распределение — это набор образец веб-служб ([генератор](https://datamarket.azure.com/dataset/aml_labs/ndg7), [калькулятора Квантиля](https://datamarket.azure.com/dataset/aml_labs/ndq5), [калькулятора вероятности](https://datamarket.azure.com/dataset/aml_labs/ndp5)), помогающие в создании и обработке нормальные распределения.</span><span class="sxs-lookup"><span data-stu-id="91bce-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="91bce-108">службы Hello разрешить создание последовательности из любой длины, вычисление квантилей из данного вероятности и расчета вероятности из заданного квантиля нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="91bce-109">Каждой из служб hello выдает различные выходы, на основе выбранных hello службы (см. описание ниже).</span><span class="sxs-lookup"><span data-stu-id="91bce-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="91bce-110">Hello нормальное распределение набор основан на qnorm функции hello R, rnorm и pnorm, включенных в пакет R статистики.</span><span class="sxs-lookup"><span data-stu-id="91bce-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="91bce-111">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="91bce-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="91bce-112">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="91bce-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="91bce-113">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="91bce-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="91bce-114">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="91bce-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="91bce-115">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="91bce-115">Consumption of web service</span></span>
<span data-ttu-id="91bce-116">Hello Suite нормальное распределение включает следующие 3 службы hello.</span><span class="sxs-lookup"><span data-stu-id="91bce-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="91bce-117">Калькулятор квантилей нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="91bce-118">Эта служба принимает аргументы 4 нормального распределения и вычисляет квантиля связанные hello.</span><span class="sxs-lookup"><span data-stu-id="91bce-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="91bce-119">Hello входными аргументами являются:</span><span class="sxs-lookup"><span data-stu-id="91bce-119">hello input arguments are:</span></span>

* <span data-ttu-id="91bce-120">p — одна вероятность события с нормальным распределением.</span><span class="sxs-lookup"><span data-stu-id="91bce-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="91bce-121">Среднее - среднее hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="91bce-122">SD - стандартное отклонение hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="91bce-123">-L для hello нижней стороны распространения hello и стороны U для hello верхней части hello распространения.</span><span class="sxs-lookup"><span data-stu-id="91bce-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="91bce-124">Hello hello службы является квантиля hello вычисления, связанный с заданным вероятность hello.</span><span class="sxs-lookup"><span data-stu-id="91bce-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="91bce-125">Калькулятор вероятности нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="91bce-126">Эта служба принимает аргументы 4 нормального распределения и вычисляет вероятность связанные hello.</span><span class="sxs-lookup"><span data-stu-id="91bce-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="91bce-127">Hello входными аргументами являются:</span><span class="sxs-lookup"><span data-stu-id="91bce-127">hello input arguments are:</span></span>

* <span data-ttu-id="91bce-128">q — один квантиль события с нормальным распределением.</span><span class="sxs-lookup"><span data-stu-id="91bce-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="91bce-129">Среднее - среднее hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="91bce-130">SD - стандартное отклонение hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="91bce-131">-L для hello нижней стороны распространения hello и стороны U для hello верхней части hello распространения.</span><span class="sxs-lookup"><span data-stu-id="91bce-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="91bce-132">выходные данные Hello hello службы — hello вычисляется вероятность, связанную с заданным квантиля hello.</span><span class="sxs-lookup"><span data-stu-id="91bce-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="91bce-133">Генератор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-133">Normal Distribution Generator</span></span>
<span data-ttu-id="91bce-134">Эта служба принимает три аргумента нормального распределения и создает случайную последовательность нормально распределенных чисел.</span><span class="sxs-lookup"><span data-stu-id="91bce-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="91bce-135">Hello следующие аргументы должны предоставляться tooit внутри hello запроса:</span><span class="sxs-lookup"><span data-stu-id="91bce-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="91bce-136">n - число hello наблюдений.</span><span class="sxs-lookup"><span data-stu-id="91bce-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="91bce-137">Среднее - среднее hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="91bce-138">SD - стандартное отклонение hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="91bce-139">выходные данные Hello hello службы — это последовательность n длины с нормальным распределением на основе hello среднее и sd аргументов.</span><span class="sxs-lookup"><span data-stu-id="91bce-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="91bce-140">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="91bce-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="91bce-141">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — здесь: [генератор](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [калькулятора вероятности](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Квантиля калькулятора](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="91bce-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="91bce-142">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="91bce-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="91bce-143">Калькулятор квантилей нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="91bce-144">Калькулятор вероятности нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="91bce-145">Генератор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="91bce-146">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="91bce-146">Creation of web service</span></span>
> <span data-ttu-id="91bce-147">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="91bce-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="91bce-148">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="91bce-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="91bce-149">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="91bce-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="91bce-150">Калькулятор квантилей нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="91bce-151">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="91bce-151">Experiment flow:</span></span>

![Ход эксперимента][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="91bce-153">Калькулятор вероятности нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="91bce-154">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="91bce-154">Experiment flow:</span></span>

![Ход эксперимента][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="91bce-156">Генератор нормального распределения</span><span class="sxs-lookup"><span data-stu-id="91bce-156">Normal Distribution Generator</span></span>
<span data-ttu-id="91bce-157">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="91bce-157">Experiment flow:</span></span>

![Ход эксперимента][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="91bce-159">Ограничения</span><span class="sxs-lookup"><span data-stu-id="91bce-159">Limitations</span></span>
<span data-ttu-id="91bce-160">Это очень простой примеры вокруг hello нормальное распределение.</span><span class="sxs-lookup"><span data-stu-id="91bce-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="91bce-161">Как видно в приведенном выше примере кода hello, реализуется немного перехват ошибок.</span><span class="sxs-lookup"><span data-stu-id="91bce-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="91bce-162">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="91bce-162">FAQ</span></span>
<span data-ttu-id="91bce-163">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="91bce-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

