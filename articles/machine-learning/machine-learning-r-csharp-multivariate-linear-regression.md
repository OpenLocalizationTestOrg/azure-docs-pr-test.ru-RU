---
title: "AAA(deprecated) многомерного линейной регрессии — Azure | Документы Microsoft"
description: "(Не рекомендуется.) Многофакторная линейная регрессия"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="80bcc-103">(Не рекомендуется.) Многофакторная линейная регрессия</span><span class="sxs-lookup"><span data-stu-id="80bcc-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="80bcc-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="80bcc-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="80bcc-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="80bcc-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="80bcc-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="80bcc-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="80bcc-107">Предположим, что у вас есть набор данных и бы как tooquickly прогнозирования зависимой переменной (y) для каждого отдельного (i), в зависимости от независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="80bcc-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="80bcc-108">Для создания таких прогнозов часто используется статистическая технология линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="80bcc-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="80bcc-109">Здесь предполагается toobe непрерывного значения y hello зависимой переменной.</span><span class="sxs-lookup"><span data-stu-id="80bcc-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="80bcc-110">Может быть простой сценарий, где научный сотрудник hello пытается вес hello toopredict лица (y) на основе их высоты (x).</span><span class="sxs-lookup"><span data-stu-id="80bcc-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="80bcc-111">Более сложные сценарии может быть где научный сотрудник hello дополнительную информацию для отдельных (например, вес, пол, состояние гонки) hello и пытается вес hello toopredict отдельных hello.</span><span class="sxs-lookup"><span data-stu-id="80bcc-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="80bcc-112">Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) подходить hello данных toohello модели линейной регрессии и выходы hello предсказанных значений (y) для каждого наблюдений hello в данных hello.</span><span class="sxs-lookup"><span data-stu-id="80bcc-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="80bcc-113">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="80bcc-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="80bcc-114">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="80bcc-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="80bcc-115">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="80bcc-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="80bcc-116">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="80bcc-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="80bcc-117">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="80bcc-117">Consumption of web service</span></span>
<span data-ttu-id="80bcc-118">Этот web service дает hello прогнозируемые значения из hello зависимой переменной на основе hello независимых переменных для всех наблюдений hello.</span><span class="sxs-lookup"><span data-stu-id="80bcc-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="80bcc-119">Hello веб-служба ожидает hello конечного пользователя tooinput данные как строку, где строки разделяются запятыми (,), а столбцы разделяются точками с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="80bcc-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="80bcc-120">Hello веб-служба ожидает 1 строки за раз и ожидает hello первый столбец toobe hello зависимой переменной.</span><span class="sxs-lookup"><span data-stu-id="80bcc-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="80bcc-121">Ниже приведен пример набора данных.</span><span class="sxs-lookup"><span data-stu-id="80bcc-121">An example dataset could look like this:</span></span>

![Пример данных][1]

<span data-ttu-id="80bcc-123">В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA.</span><span class="sxs-lookup"><span data-stu-id="80bcc-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="80bcc-124">Hello входных данных для hello выше набор данных будет быть hello следующая строка: «10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, н/д: 3: 4».</span><span class="sxs-lookup"><span data-stu-id="80bcc-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="80bcc-125">Hello вывода hello прогнозируемое значение для каждой из строк hello основан на hello независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="80bcc-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="80bcc-126">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="80bcc-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="80bcc-127">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="80bcc-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="80bcc-128">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="80bcc-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="80bcc-129">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="80bcc-129">Creation of web service</span></span>
> <span data-ttu-id="80bcc-130">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="80bcc-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="80bcc-131">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="80bcc-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="80bcc-132">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="80bcc-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="80bcc-133">Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули были «втянуты» в область hello.</span><span class="sxs-lookup"><span data-stu-id="80bcc-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="80bcc-134">Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R.</span><span class="sxs-lookup"><span data-stu-id="80bcc-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="80bcc-135">Существует 2 частей toothis поэкспериментировать: определение схемы и обучения модели + оценки.</span><span class="sxs-lookup"><span data-stu-id="80bcc-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="80bcc-136">Первый модуль Hello определяет структуру hello ожидается hello входного набора данных, где hello первой переменной — hello зависимой переменной, а остальные переменные hello независимы.</span><span class="sxs-lookup"><span data-stu-id="80bcc-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="80bcc-137">второй модуль Hello подгоняет модель универсального линейной регрессии для hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="80bcc-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Ход эксперимента][3]

#### <a name="module-1"></a><span data-ttu-id="80bcc-139">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="80bcc-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="80bcc-140">определение схемы</span><span class="sxs-lookup"><span data-stu-id="80bcc-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="80bcc-141">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="80bcc-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="80bcc-142">моделирование LM</span><span class="sxs-lookup"><span data-stu-id="80bcc-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="80bcc-143">Ограничения</span><span class="sxs-lookup"><span data-stu-id="80bcc-143">Limitations</span></span>
<span data-ttu-id="80bcc-144">Это очень простой пример веб-службы многофакторной линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="80bcc-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="80bcc-145">Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и служба hello предполагает, что все непрерывной переменной (не категориальных признаков допускается), как hello службы только входные данные числовые значения во время hello hello создания этого веб-сайта Служба.</span><span class="sxs-lookup"><span data-stu-id="80bcc-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="80bcc-146">Кроме того служба hello в настоящее время обрабатывает данные ограниченный размер, из-за характера запроса и ответа toohello hello веб-служба вызова и hello факт, что hello модели, выполняется подходит каждый раз при вызове hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="80bcc-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="80bcc-147">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="80bcc-147">FAQ</span></span>
<span data-ttu-id="80bcc-148">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="80bcc-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

