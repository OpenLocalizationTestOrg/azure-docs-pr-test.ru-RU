---
title: "Кластерная модель Azure (устаревшая версия) | Документация Майкрософт"
description: "Сведения о кластерной модели (устаревшая версия)."
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
redirect_document_id: TRUE
ms.openlocfilehash: 7cbbbd6d4236dab638eb3051595a584557480841
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="4cb07-103">Кластерная модель (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="4cb07-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="4cb07-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4cb07-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4cb07-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4cb07-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4cb07-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4cb07-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4cb07-107">Как спрогнозировать поведение групп владельцев кредитных карт, чтобы снизить для их эмитентов риски, связанные с необходимостью списания безнадежных задолженностей?</span><span class="sxs-lookup"><span data-stu-id="4cb07-107">How can we predict groups of credit cardholders’ behaviors in order to reduce the charge-off risk of credit card issuers?</span></span> <span data-ttu-id="4cb07-108">Как определить группы личных качеств сотрудников, чтобы повысить производительность их труда?</span><span class="sxs-lookup"><span data-stu-id="4cb07-108">How can we define groups of personality traits of employees in order to improve their performance at work?</span></span> <span data-ttu-id="4cb07-109">Как врачам распределять пациентов по группам исходя из особенностей их заболеваний?</span><span class="sxs-lookup"><span data-stu-id="4cb07-109">How can doctors classify patients into groups based on the characteristics of their diseases?</span></span> <span data-ttu-id="4cb07-110">В принципе, на все эти вопросы помогает ответить кластерный анализ.</span><span class="sxs-lookup"><span data-stu-id="4cb07-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4cb07-111">Кластерный анализ позволяет разделить массив наблюдений на две или несколько взаимоисключающих неопределенных групп на основе сочетания переменных.</span><span class="sxs-lookup"><span data-stu-id="4cb07-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="4cb07-112">Цель этого метода заключается в создании схемы распределения наблюдений (как правило, людей или связанных с ними признаков) по группам, члены которых обладают некоторыми общими характеристиками.</span><span class="sxs-lookup"><span data-stu-id="4cb07-112">The purpose of cluster analysis is to discover a system of organizing observations, usually people or their characteristics, into groups, where members of the groups share properties in common.</span></span> <span data-ttu-id="4cb07-113">Эта [служба](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) использует для распределения произвольных значений по группам метод k-средних — один из распространенных способов кластеризации.</span><span class="sxs-lookup"><span data-stu-id="4cb07-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses the K-Means methodology, a commonly used clustering technique, to cluster arbitrary data into groups.</span></span> <span data-ttu-id="4cb07-114">Она принимает на всех данные и количество k-кластеров и выдает прогнозы относительно попадания каждого из наблюдений в ту или иную k-группу.</span><span class="sxs-lookup"><span data-stu-id="4cb07-114">This web service takes the data and the number of k clusters as input, and produces predictions of which of the k groups to which each observations belongs.</span></span> 

> <span data-ttu-id="4cb07-115">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4cb07-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4cb07-116">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="4cb07-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="4cb07-117">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb07-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4cb07-118">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="4cb07-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4cb07-119">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="4cb07-119">Consumption of web service</span></span>
<span data-ttu-id="4cb07-120">Эта веб-служба распределяет значения по k группам и выдает для каждой строки распределение по группам.</span><span class="sxs-lookup"><span data-stu-id="4cb07-120">This web service groups the data into a set of k groups and outputs the group assignment for each row.</span></span> <span data-ttu-id="4cb07-121">Она принимает входные данные в виде блока, где строки разделены запятыми (,), а столбцы — точками с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="4cb07-121">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="4cb07-122">Веб-служба принимает на вход по одной строке.</span><span class="sxs-lookup"><span data-stu-id="4cb07-122">The web service expects 1 row at a time.</span></span> <span data-ttu-id="4cb07-123">Ниже приведен пример набора данных.</span><span class="sxs-lookup"><span data-stu-id="4cb07-123">An example dataset could look like this:</span></span>

![Пример данных][1]

<span data-ttu-id="4cb07-125">Предположим, что пользователь хочет разделить эти значения на 3 взаимоисключающие группы.</span><span class="sxs-lookup"><span data-stu-id="4cb07-125">Suppose the user wanted to separate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="4cb07-126">Вот пример входной строки для такого набора данных: value = "10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4"; k="3".</span><span class="sxs-lookup"><span data-stu-id="4cb07-126">The data input for the above dataset would be the following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="4cb07-127">Результатом является прогноз распределения по группам значений в каждой из строк.</span><span class="sxs-lookup"><span data-stu-id="4cb07-127">The output is the predicted group membership for each of the rows.</span></span>

> <span data-ttu-id="4cb07-128">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="4cb07-128">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4cb07-129">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4cb07-129">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4cb07-130">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="4cb07-130">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="4cb07-131">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="4cb07-131">Creation of web service</span></span>
> <span data-ttu-id="4cb07-132">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb07-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4cb07-133">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4cb07-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4cb07-134">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="4cb07-134">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="4cb07-135">В системе машинного обучения Azure был создан новый пустой эксперимент, и в рабочую область было помещено два модуля [Выполнение сценария R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4cb07-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="4cb07-136">Схема данных была создана с помощью простого модуля [Выполнение сценария R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4cb07-136">The data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="4cb07-137">Затем она была связана с разделом кластерной модели, который также был создан на основе модуля [Выполнение сценария R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="4cb07-137">Then, the data schema was linked to the cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="4cb07-138">В модуле [Выполнение сценария R][execute-r-script], используемом для создания кластерной модели, веб-служба применяет стандартную функцию k-means, включенную в модуль [Execute R Script][execute-r-script] в среде машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb07-138">In the [Execute R Script][execute-r-script] used for the cluster model, the web service then utilizes the “k-means” function, which is prebuilt into the [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Ход эксперимента][3]

#### <a name="module-1"></a><span data-ttu-id="4cb07-140">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="4cb07-140">Module 1:</span></span>
    #Enter the input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="4cb07-141">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="4cb07-141">Module 2:</span></span>
    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="4cb07-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="4cb07-142">Limitations</span></span>
<span data-ttu-id="4cb07-143">Это очень простой пример веб-службы кластеризации.</span><span class="sxs-lookup"><span data-stu-id="4cb07-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="4cb07-144">Как видно из приведенного выше образца кода, в нем не отслеживаются ошибки, а служба предполагает, что все входные данные являются непрерывными переменными (без категоризации), так как принимает только числовые значения.</span><span class="sxs-lookup"><span data-stu-id="4cb07-144">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="4cb07-145">Кроме того, веб-служба способна обработать лишь ограниченный объем данных, так как это служба запроса/ответа, а модель применяется каждый раз при ее вызове.</span><span class="sxs-lookup"><span data-stu-id="4cb07-145">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="4cb07-146">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="4cb07-146">FAQ</span></span>
<span data-ttu-id="4cb07-147">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4cb07-147">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

