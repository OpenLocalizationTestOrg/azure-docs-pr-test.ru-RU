---
title: "AAA(deprecated) модели кластера - Azure | Документы Microsoft"
description: "Кластерная модель (устаревшая версия)"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="9c709-103">Кластерная модель (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="9c709-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="9c709-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="9c709-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="9c709-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9c709-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9c709-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="9c709-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9c709-107">Как можно прогнозировать групп поведений cardholders кредит в порядке tooreduce hello списания риска кредитной карты издателей?</span><span class="sxs-lookup"><span data-stu-id="9c709-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="9c709-108">Как мы группы можно определить из характеристик индивидуальность сотрудников tooimprove порядок их производительность на работе?</span><span class="sxs-lookup"><span data-stu-id="9c709-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="9c709-109">Как врачи можно классифицировать пациентов по группам на основе характеристик hello их болезней?</span><span class="sxs-lookup"><span data-stu-id="9c709-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="9c709-110">В принципе, на все эти вопросы помогает ответить кластерный анализ.</span><span class="sxs-lookup"><span data-stu-id="9c709-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9c709-111">Кластерный анализ позволяет разделить массив наблюдений на две или несколько взаимоисключающих неопределенных групп на основе сочетания переменных.</span><span class="sxs-lookup"><span data-stu-id="9c709-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="9c709-112">Hello анализа кластера служит toodiscover системы организации наблюдений, обычно людей или их характеристики по группам, где члены групп hello общими для свойства.</span><span class="sxs-lookup"><span data-stu-id="9c709-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="9c709-113">Это [службы](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) использует hello методологии K-средние, наиболее часто используемого метода кластеризации, toocluster произвольных данных в группы.</span><span class="sxs-lookup"><span data-stu-id="9c709-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="9c709-114">Эта веб-служба принимает данные hello и hello число k кластеров в качестве входных данных и создает прогнозы, из которых hello k группы toowhich принадлежит каждого наблюдения.</span><span class="sxs-lookup"><span data-stu-id="9c709-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="9c709-115">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9c709-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="9c709-116">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="9c709-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="9c709-117">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c709-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="9c709-118">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c709-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="9c709-119">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="9c709-119">Consumption of web service</span></span>
<span data-ttu-id="9c709-120">Эта веб-служба группирует данные hello набора k групп и выходы hello Назначение группы для каждой строки.</span><span class="sxs-lookup"><span data-stu-id="9c709-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="9c709-121">Hello веб-служба ожидает hello конечного пользователя tooinput данные как строку, где строки разделяются запятыми (,), а столбцы разделяются точками с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="9c709-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="9c709-122">Hello веб-служба ожидает 1 строки за раз.</span><span class="sxs-lookup"><span data-stu-id="9c709-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="9c709-123">Ниже приведен пример набора данных.</span><span class="sxs-lookup"><span data-stu-id="9c709-123">An example dataset could look like this:</span></span>

![Пример данных][1]

<span data-ttu-id="9c709-125">Предположим, что tooseparate пользователя было hello эти данные по 3 группам взаимно исключают друг друга.</span><span class="sxs-lookup"><span data-stu-id="9c709-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="9c709-126">Здравствуйте ввода для hello выше набор данных будет hello следующие данные: значение = «10, 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3, 4»; k = «3».</span><span class="sxs-lookup"><span data-stu-id="9c709-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="9c709-127">для каждой из строк hello Hello выходные данные hello членство в группе прогнозируемые.</span><span class="sxs-lookup"><span data-stu-id="9c709-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="9c709-128">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="9c709-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="9c709-129">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="9c709-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="9c709-130">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="9c709-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="9c709-131">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="9c709-131">Creation of web service</span></span>
> <span data-ttu-id="9c709-132">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c709-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="9c709-133">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="9c709-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="9c709-134">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="9c709-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="9c709-135">Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули извлечено в область hello.</span><span class="sxs-lookup"><span data-stu-id="9c709-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="9c709-136">Схема данных Hello была создана с помощью простого [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="9c709-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="9c709-137">Затем схемы данных hello был связанного toohello кластера раздел модели, вновь создается с [выполнение скрипта R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="9c709-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="9c709-138">В hello [выполнение скрипта R] [ execute-r-script] , используемое hello кластерной модели, hello веб-служба затем использует функции hello «k средние», которое является готовых в hello [выполнение скрипта R] [ execute-r-script] Azure машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="9c709-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Ход эксперимента][3]

#### <a name="module-1"></a><span data-ttu-id="9c709-140">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="9c709-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="9c709-141">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="9c709-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="9c709-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="9c709-142">Limitations</span></span>
<span data-ttu-id="9c709-143">Это очень простой пример веб-службы кластеризации.</span><span class="sxs-lookup"><span data-stu-id="9c709-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="9c709-144">Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и служба hello предполагает, что все непрерывной переменной (не категориальных признаков допускается), как hello службы только входные данные числовые значения во время hello hello создания этого веб-сайта Служба.</span><span class="sxs-lookup"><span data-stu-id="9c709-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="9c709-145">Кроме того служба hello в настоящее время обрабатывает данные ограниченный размер, из-за характера запроса и ответа toohello hello веб-служба вызова и hello факт, что hello модели, выполняется подходит каждый раз при вызове hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c709-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="9c709-146">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="9c709-146">FAQ</span></span>
<span data-ttu-id="9c709-147">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9c709-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

