---
title: "(Не рекомендуется.) Многофакторная линейная регрессия в Azure | Документация Майкрософт"
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
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="80b44-103">(Не рекомендуется.) Многофакторная линейная регрессия</span><span class="sxs-lookup"><span data-stu-id="80b44-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="80b44-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="80b44-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="80b44-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="80b44-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="80b44-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="80b44-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="80b44-107">Предположим, у вас есть набор данных и вы хотите быстро спрогнозировать значение зависимой переменной (y) для каждого отдельного значения (i) на основе независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="80b44-107">Suppose you have a dataset and would like to quickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="80b44-108">Для создания таких прогнозов часто используется статистическая технология линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="80b44-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="80b44-109">Здесь каждая зависимая переменная y считается принимающей непрерывные значения.</span><span class="sxs-lookup"><span data-stu-id="80b44-109">Here the dependent variable y is assumed to be a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="80b44-110">Простейший случай применения этого метода — попытка спрогнозировать вес человека (y) на основе его роста (x).</span><span class="sxs-lookup"><span data-stu-id="80b44-110">A simple scenario could be where the researcher is trying to predict the weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="80b44-111">В более сложном сценарии может быть доступна дополнительная информация об исследуемом человеке (например, его пол, раса и т. д.), на основе которой требуется определить его вес.</span><span class="sxs-lookup"><span data-stu-id="80b44-111">A more advanced scenario could be where the researcher has additional information for the individual (such as weight, gender, race) and attempts to predict the weight of the individual.</span></span> <span data-ttu-id="80b44-112">Эта [веб-служба](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) применяет модель линейной регрессии к данным и выдает прогнозируемое значение (y) для каждого из входящих в ряд данных наблюдения.</span><span class="sxs-lookup"><span data-stu-id="80b44-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits the linear regression model to the data and outputs the predicted value (y) for each of the observations in the data.</span></span>

> <span data-ttu-id="80b44-113">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="80b44-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="80b44-114">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="80b44-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="80b44-115">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="80b44-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="80b44-116">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="80b44-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="80b44-117">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="80b44-117">Consumption of web service</span></span>
<span data-ttu-id="80b44-118">Эта веб-служба выдает прогнозируемые значения зависимой переменной на основе независимых переменных для всех наблюдений.</span><span class="sxs-lookup"><span data-stu-id="80b44-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="80b44-119">Она принимает входные данные в виде блока, где строки разделены запятыми (,), а столбцы — точками с запятой (;).</span><span class="sxs-lookup"><span data-stu-id="80b44-119">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="80b44-120">Веб-служба принимает по одной строке, причем первый столбец должен содержать зависимую переменную.</span><span class="sxs-lookup"><span data-stu-id="80b44-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="80b44-121">Ниже приведен пример набора данных.</span><span class="sxs-lookup"><span data-stu-id="80b44-121">An example dataset could look like this:</span></span>

![Пример данных][1]

<span data-ttu-id="80b44-123">В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA.</span><span class="sxs-lookup"><span data-stu-id="80b44-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="80b44-124">Вот пример входной строки для такого набора данных: "10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4".</span><span class="sxs-lookup"><span data-stu-id="80b44-124">The data input for the above dataset would be the following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="80b44-125">На выходе служба выдает прогнозируемое значение для каждой строки на основе независимых переменных.</span><span class="sxs-lookup"><span data-stu-id="80b44-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="80b44-126">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="80b44-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="80b44-127">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="80b44-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="80b44-128">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="80b44-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="80b44-129">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="80b44-129">Creation of web service</span></span>
> <span data-ttu-id="80b44-130">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="80b44-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="80b44-131">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="80b44-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="80b44-132">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="80b44-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="80b44-133">В системе машинного обучения Azure был создан пустой эксперимент, и в рабочую область было помещено два модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="80b44-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="80b44-134">Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R.</span><span class="sxs-lookup"><span data-stu-id="80b44-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="80b44-135">Эксперимент состоит из двух частей: определение схемы и обучение модели + оценка.</span><span class="sxs-lookup"><span data-stu-id="80b44-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="80b44-136">Первый модуль определяет структуру ожидаемого входного набора данных, в котором первая переменная является зависимой, а остальные — независимыми.</span><span class="sxs-lookup"><span data-stu-id="80b44-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="80b44-137">Второй модуль применяет к входным данным стандартную модель линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="80b44-137">The second module fits a generic linear regression model for the input data.</span></span>  

![Ход эксперимента][3]

#### <a name="module-1"></a><span data-ttu-id="80b44-139">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="80b44-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="80b44-140">определение схемы</span><span class="sxs-lookup"><span data-stu-id="80b44-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="80b44-141">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="80b44-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="80b44-142">моделирование LM</span><span class="sxs-lookup"><span data-stu-id="80b44-142">LM modeling</span></span>
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

## <a name="limitations"></a><span data-ttu-id="80b44-143">Ограничения</span><span class="sxs-lookup"><span data-stu-id="80b44-143">Limitations</span></span>
<span data-ttu-id="80b44-144">Это очень простой пример веб-службы многофакторной линейной регрессии.</span><span class="sxs-lookup"><span data-stu-id="80b44-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="80b44-145">Как видно из приведенного выше образца кода, в нем не отслеживаются ошибки, а служба предполагает, что все входные данные являются непрерывными переменными (без категоризации), так как принимает только числовые значения.</span><span class="sxs-lookup"><span data-stu-id="80b44-145">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="80b44-146">Кроме того, веб-служба способна обработать лишь ограниченный объем данных, так как это служба запроса/ответа, а модель применяется каждый раз при ее вызове.</span><span class="sxs-lookup"><span data-stu-id="80b44-146">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="80b44-147">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="80b44-147">FAQ</span></span>
<span data-ttu-id="80b44-148">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="80b44-148">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

