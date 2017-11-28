---
title: "AAA(deprecated) набор биномиальное распределение - Azure | Документы Microsoft"
description: "Набор биномиального распределения (устаревшая версия)"
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
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="3d7fc-103">Набор биномиального распределения (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="3d7fc-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="3d7fc-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3d7fc-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3d7fc-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3d7fc-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3d7fc-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3d7fc-107">Hello Suite биномиальное распределение — это набор образец веб-службы ([биномиальное генератор](https://datamarket.azure.com/dataset/aml_labs/bdg5), [калькулятора вероятности](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Квантиля калькулятора](https://datamarket.azure.com/dataset/aml_labs/bdq5)), помогающие при формировании и Работа с биномиального распределения.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="3d7fc-108">Hello служб разрешить создание последовательности биномиальное распределение любой длины, вычисление квантилей из заданного из заданного квантиля вероятности и расчета вероятности.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="3d7fc-109">Каждой из служб hello выдает различные выходы, на основе выбранных hello службы (см. описание ниже).</span><span class="sxs-lookup"><span data-stu-id="3d7fc-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="3d7fc-110">Hello биномиальное распределение набор основан на qbinom функции hello R, rbinom и pbinom, включенных в пакет stats R hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="3d7fc-111">Эти веб-службы может использоваться пользователей — потенциально непосредственно на рынке hello, через мобильные приложения на веб-сайте или на локальном компьютере, например.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3d7fc-112">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="3d7fc-113">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3d7fc-114">Hello веб-службы может быть затем опубликованных toohello Azure Marketplace и используемые пользователями и устройствами через hello world — не настраивать инфраструктуру автором hello hello веб-службы не требуется.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3d7fc-115">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="3d7fc-115">Consumption of web service</span></span>
<span data-ttu-id="3d7fc-116">Hello биномиальное распределение Suite включает следующие 3 службы hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3d7fc-117">Калькулятор квантилей биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="3d7fc-118">Эта служба принимает аргументы 4 нормального распределения и вычисляет квантиля связанные hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="3d7fc-119">Hello входными аргументами являются:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-119">hello input arguments are:</span></span>

* <span data-ttu-id="3d7fc-120">p — единое обобщенное значение вероятности для набора испытаний.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="3d7fc-121">размер - hello число испытаний.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-121">size - hello number of trials.</span></span>
* <span data-ttu-id="3d7fc-122">то функция вероятность - hello вероятность успеха в пробной версии.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="3d7fc-123">Сторона - L для hello нижней стороны hello распределения, U для hello верхней части hello распространения.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="3d7fc-124">Hello hello службы является квантиля hello вычисления, связанный с заданным вероятность hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3d7fc-125">Калькулятор вероятности биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="3d7fc-126">Эта служба принимает 4 аргументы биномиальное распределение и вычисляет вероятность связанные hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="3d7fc-127">Hello входными аргументами являются:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-127">hello input arguments are:</span></span>

* <span data-ttu-id="3d7fc-128">q — один квантиль события с биномиальным распределением.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="3d7fc-129">размер - hello число испытаний.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-129">size - hello number of trials.</span></span>
* <span data-ttu-id="3d7fc-130">то функция вероятность - hello вероятность успеха в пробной версии.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="3d7fc-131">сторона - L для нижней стороны распространения hello, U для hello верхней части распространения hello или E, равно tooa один количество успешных hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="3d7fc-132">выходные данные Hello hello службы — hello вычисляется вероятность, связанную с заданным квантиля hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="3d7fc-133">Генератор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="3d7fc-134">Эта служба принимает три аргумента биномиального распределения и создает случайную последовательность биномиально распределенных чисел.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="3d7fc-135">Hello следующие аргументы должны предоставляться tooit внутри hello запроса:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="3d7fc-136">n — количество наблюдений.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-136">n - Number of observations.</span></span> 
* <span data-ttu-id="3d7fc-137">size — количество испытаний.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-137">size - Number of trials.</span></span>
* <span data-ttu-id="3d7fc-138">prob — вероятность успеха.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-138">prob - Probability of success.</span></span>

<span data-ttu-id="3d7fc-139">выходные данные Hello hello службы — это последовательность n длины с биномиального распределения, в зависимости от размера и то функция вероятность аргументов hello.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="3d7fc-140">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3d7fc-141">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — здесь: [генератор](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [калькулятора вероятности](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Квантиля калькулятора](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="3d7fc-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3d7fc-142">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3d7fc-143">Калькулятор квантилей биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3d7fc-144">Калькулятор вероятности биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="3d7fc-145">Генератор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="3d7fc-146">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="3d7fc-146">Creation of web service</span></span>
> <span data-ttu-id="3d7fc-147">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3d7fc-148">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="3d7fc-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3d7fc-149">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3d7fc-150">Калькулятор квантилей биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-150">Binomial Distribution Quantile Calculator</span></span>
![Создание рабочей области][4]

#### <a name="module-1"></a><span data-ttu-id="3d7fc-152">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="3d7fc-153">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-153">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3d7fc-154">Калькулятор вероятности биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-154">Binomial Distribution Probability Calculator</span></span>
![Создание рабочей области][5]

#### <a name="module-1"></a><span data-ttu-id="3d7fc-156">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="3d7fc-157">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-157">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="3d7fc-158">Генератор биномиального распределения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-158">Binomial Distribution Generator</span></span>
![Создание рабочей области][6]

#### <a name="module-1"></a><span data-ttu-id="3d7fc-160">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="3d7fc-161">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="3d7fc-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="3d7fc-162">Ограничения</span><span class="sxs-lookup"><span data-stu-id="3d7fc-162">Limitations</span></span>
<span data-ttu-id="3d7fc-163">Это очень простой примеры вокруг hello биномиальное распределение.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="3d7fc-164">Как видно в приведенном выше примере кода hello, реализуется немного перехват ошибок.</span><span class="sxs-lookup"><span data-stu-id="3d7fc-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="3d7fc-165">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3d7fc-165">FAQ</span></span>
<span data-ttu-id="3d7fc-166">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3d7fc-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

