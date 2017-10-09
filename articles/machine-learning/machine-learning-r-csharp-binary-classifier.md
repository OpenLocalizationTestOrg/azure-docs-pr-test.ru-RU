---
title: "AAA(deprecated) бинарного классификатора - Azure | Документы Microsoft"
description: "Двоичный классификатор (устаревшая версия)"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="7d81c-103">Двоичный классификатор (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="7d81c-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="7d81c-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="7d81c-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="7d81c-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="7d81c-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="7d81c-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="7d81c-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="7d81c-107">Предположим, что есть набор данных и хотите toopredict двоичных зависимой переменной на основе hello независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="7d81c-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="7d81c-108">Для создания таких прогнозов часто используется статистическая технология логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="7d81c-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="7d81c-109">Вот hello зависимой переменной binary или дихотомических и p — hello вероятность наличия характеристика hello интерес.</span><span class="sxs-lookup"><span data-stu-id="7d81c-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="7d81c-110">Может быть простой сценарий, где научный сотрудник пытается toopredict, является ли студент потенциального скорее всего tooaccept tooa университета допуском предложение, на основе сведений (GPA в средней школе, семейства доход, резидентных состояние пола).</span><span class="sxs-lookup"><span data-stu-id="7d81c-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="7d81c-111">Hello прогнозируемый результат — hello вероятность потенциального студента hello принятия предложения допуском hello.</span><span class="sxs-lookup"><span data-stu-id="7d81c-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="7d81c-112">Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/log_regression) подходить hello данных toohello модели логистической регрессии и выходы hello значение вероятности (y) для каждого наблюдений hello в данных hello.</span><span class="sxs-lookup"><span data-stu-id="7d81c-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="7d81c-113">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7d81c-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="7d81c-114">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="7d81c-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="7d81c-115">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="7d81c-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="7d81c-116">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7d81c-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="7d81c-117">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="7d81c-117">Consumption of web service</span></span>
<span data-ttu-id="7d81c-118">Этот web service дает hello прогнозируемые значения из hello зависимой переменной на основе hello независимых переменных для всех наблюдений hello.</span><span class="sxs-lookup"><span data-stu-id="7d81c-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="7d81c-119">Hello веб-служба ожидает hello конечного пользователя tooinput данные как строку, где строки разделяются запятой (,), а столбцы разделяются точкой с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="7d81c-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="7d81c-120">Hello веб-служба ожидает 1 строки за раз и ожидает hello первый столбец toobe hello зависимой переменной.</span><span class="sxs-lookup"><span data-stu-id="7d81c-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="7d81c-121">Ниже приведен пример набора данных.</span><span class="sxs-lookup"><span data-stu-id="7d81c-121">An example dataset could look like this:</span></span>

![Пример данных][1]

<span data-ttu-id="7d81c-123">В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA.</span><span class="sxs-lookup"><span data-stu-id="7d81c-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="7d81c-124">Hello входных данных для hello выше набор данных будет быть hello следующая строка: «1, 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, н/д; 3, 4».</span><span class="sxs-lookup"><span data-stu-id="7d81c-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="7d81c-125">Hello вывода hello прогнозируемое значение для каждой из строк hello основан на hello независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="7d81c-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="7d81c-126">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="7d81c-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="7d81c-127">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="7d81c-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="7d81c-128">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="7d81c-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="7d81c-129">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="7d81c-129">Creation of web service</span></span>
> <span data-ttu-id="7d81c-130">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="7d81c-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="7d81c-131">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="7d81c-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="7d81c-132">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="7d81c-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="7d81c-133">Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули извлечено в область hello.</span><span class="sxs-lookup"><span data-stu-id="7d81c-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="7d81c-134">Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R.</span><span class="sxs-lookup"><span data-stu-id="7d81c-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="7d81c-135">Существует 2 частей toothis поэкспериментировать: определение схемы и обучения модели + оценки.</span><span class="sxs-lookup"><span data-stu-id="7d81c-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="7d81c-136">Первый модуль Hello определяет структуру hello ожидается hello входного набора данных, где hello первой переменной — hello зависимой переменной, а остальные переменные hello независимы.</span><span class="sxs-lookup"><span data-stu-id="7d81c-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="7d81c-137">второй модуль Hello подгоняет модель универсального логистической регрессии для hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="7d81c-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="7d81c-139">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="7d81c-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="7d81c-140">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="7d81c-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="7d81c-141">Ограничения</span><span class="sxs-lookup"><span data-stu-id="7d81c-141">Limitations</span></span>
<span data-ttu-id="7d81c-142">Это очень простой пример веб-службы двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="7d81c-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="7d81c-143">Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и службы hello предполагает, что все двоичные/непрерывной переменной (не категориальных признаков допускается), как hello службы только входные данные числовые значения во время hello hello создания данного объекта веб-служба.</span><span class="sxs-lookup"><span data-stu-id="7d81c-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="7d81c-144">Кроме того служба hello в настоящее время обрабатывает данные ограниченный размер, из-за характера запроса и ответа toohello hello веб-служба вызова и hello факт, что hello модели, выполняется подходит каждый раз при вызове hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7d81c-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="7d81c-145">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="7d81c-145">FAQ</span></span>
<span data-ttu-id="7d81c-146">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="7d81c-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

