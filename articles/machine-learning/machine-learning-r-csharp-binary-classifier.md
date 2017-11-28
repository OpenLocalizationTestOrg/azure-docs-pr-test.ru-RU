---
title: "Двоичный классификатор в Azure (устаревшая версия) | Документация Майкрософт"
description: "Сведения о двоичном классификаторе (устаревшая версия)."
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
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="131d3-103">Двоичный классификатор (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="131d3-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="131d3-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="131d3-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="131d3-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="131d3-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="131d3-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="131d3-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="131d3-107">Предположим, у вас есть набор данных и вы хотите спрогнозировать значение двоичной зависимой переменной на основе независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="131d3-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="131d3-108">Для создания таких прогнозов часто используется статистическая технология логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="131d3-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="131d3-109">В этом случае зависимая переменная является двоичной или дихотомической, а p — это вероятность появления интересующей нас характеристики.</span><span class="sxs-lookup"><span data-stu-id="131d3-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="131d3-110">Простейшая ситуация применения этой модели — попытка определить, примет ли потенциальный студент приглашение в университет на основе информации о нем (средний балл в аттестате, семейный доход, место проживания, пол).</span><span class="sxs-lookup"><span data-stu-id="131d3-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="131d3-111">Прогнозируемый результат — это вероятность принятия таким потенциальным учащимся приглашения на учебу.</span><span class="sxs-lookup"><span data-stu-id="131d3-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="131d3-112">Эта [веб-службы](https://datamarket.azure.com/dataset/aml_labs/log_regression) соответствует модели логистической регрессии для данных и выводит значение вероятности (y) для каждого наблюдения в данных.</span><span class="sxs-lookup"><span data-stu-id="131d3-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="131d3-113">Пользователи могут работать с этой веб-службой через мобильное приложение, веб-сайт или даже локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="131d3-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="131d3-114">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="131d3-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="131d3-115">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="131d3-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="131d3-116">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="131d3-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="131d3-117">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="131d3-117">Consumption of web service</span></span>
<span data-ttu-id="131d3-118">Эта веб-служба выдает прогнозируемые значения зависимой переменной на основе независимых переменных для всех наблюдений.</span><span class="sxs-lookup"><span data-stu-id="131d3-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="131d3-119">Она принимает входные данные в виде блока, где строки разделены запятыми (,), а столбцы — точками с запятой ($).</span><span class="sxs-lookup"><span data-stu-id="131d3-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="131d3-120">Веб-служба принимает по одной строке, причем первый столбец должен содержать зависимую переменную.</span><span class="sxs-lookup"><span data-stu-id="131d3-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="131d3-121">Ниже приведен пример набора данных.</span><span class="sxs-lookup"><span data-stu-id="131d3-121">An example dataset could look like this:</span></span>

![Пример данных][1]

<span data-ttu-id="131d3-123">В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA.</span><span class="sxs-lookup"><span data-stu-id="131d3-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="131d3-124">Вот пример входной строки для такого набора данных: "1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4".</span><span class="sxs-lookup"><span data-stu-id="131d3-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="131d3-125">На выходе служба выдает прогнозируемое значение для каждой строки на основе независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="131d3-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="131d3-126">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="131d3-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="131d3-127">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="131d3-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="131d3-128">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="131d3-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="131d3-129">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="131d3-129">Creation of web service</span></span>
> <span data-ttu-id="131d3-130">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="131d3-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="131d3-131">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="131d3-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="131d3-132">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="131d3-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="131d3-133">В системе машинного обучения Azure был создан новый пустой эксперимент, и в рабочую область было помещено два модуля [Выполнение сценария R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="131d3-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="131d3-134">Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R.</span><span class="sxs-lookup"><span data-stu-id="131d3-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="131d3-135">Эксперимент состоит из двух частей: определение схемы и обучение модели + оценка.</span><span class="sxs-lookup"><span data-stu-id="131d3-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="131d3-136">Первый модуль определяет структуру ожидаемого входного набора данных, в котором первая переменная является зависимой, а остальные — независимыми.</span><span class="sxs-lookup"><span data-stu-id="131d3-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="131d3-137">Второй модуль применяет к входным данным стандартную модель логистической регрессии.</span><span class="sxs-lookup"><span data-stu-id="131d3-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Ход эксперимента][2]

#### <a name="module-1"></a><span data-ttu-id="131d3-139">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="131d3-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="131d3-140">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="131d3-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="131d3-141">Ограничения</span><span class="sxs-lookup"><span data-stu-id="131d3-141">Limitations</span></span>
<span data-ttu-id="131d3-142">Это очень простой пример веб-службы двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="131d3-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="131d3-143">Как видно из приведенного выше образца кода, в нем не отслеживаются ошибки, а служба предполагает, что все входные данные являются двоичными/непрерывными переменными (без категоризации), так как принимает только числовые значения.</span><span class="sxs-lookup"><span data-stu-id="131d3-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="131d3-144">Кроме того, веб-служба способна обработать лишь ограниченный объем данных, так как это служба запроса/ответа, а модель применяется каждый раз при ее вызове.</span><span class="sxs-lookup"><span data-stu-id="131d3-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="131d3-145">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="131d3-145">FAQ</span></span>
<span data-ttu-id="131d3-146">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="131d3-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

