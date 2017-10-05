---
title: "Анализ выживаемости в системе машинного обучения Azure (устаревшая версия) | Документация Майкрософт"
description: "Вероятность события анализа выживаемости (устаревшая версия)."
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="2ce41-103">Анализ выживаемости (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="2ce41-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="2ce41-104">Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2ce41-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2ce41-105">Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="2ce41-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2ce41-106">Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="2ce41-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2ce41-107">Во многих сценариях основной результат оценки — это время до наступления конкретного события.</span><span class="sxs-lookup"><span data-stu-id="2ce41-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="2ce41-108">Другими словами, задается вопрос "когда произойдет это событие?".</span><span class="sxs-lookup"><span data-stu-id="2ce41-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="2ce41-109">В качестве примеров можно привести ситуации, в которых данные описывают время (дни, годы, расстояние и т.</span><span class="sxs-lookup"><span data-stu-id="2ce41-109">is asked.</span></span> <span data-ttu-id="2ce41-110">В качестве примеров можно привести ситуации, в которых данные описывают время (дни, годы, расстояние и т. д.), прошедшее до наступления интересующего нас события (рецидив болезни, получение степени доктора наук, выход из строя тормозной колодки).</span><span class="sxs-lookup"><span data-stu-id="2ce41-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="2ce41-111">д.).</span><span class="sxs-lookup"><span data-stu-id="2ce41-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2ce41-112">Эта [веб-служба](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) отвечает на вопрос "Какова вероятность того, что определенное событие произойдет ко времени n для объекта x?".</span><span class="sxs-lookup"><span data-stu-id="2ce41-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="2ce41-113">Предоставляя модель анализа выживаемости, эта веб-служба позволяет пользователям загружать данные для обучения модели и тестировать их.</span><span class="sxs-lookup"><span data-stu-id="2ce41-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="2ce41-114">Основная тема эксперимента — моделирование периода времени до наступления определенного события.</span><span class="sxs-lookup"><span data-stu-id="2ce41-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="2ce41-115">С этой веб-службой могут работать пользователи — через мобильное приложение, веб-сайт или даже локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="2ce41-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2ce41-116">Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="2ce41-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="2ce41-117">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce41-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2ce41-118">Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="2ce41-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2ce41-119">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="2ce41-119">Consumption of web service</span></span>
<span data-ttu-id="2ce41-120">В следующей таблице показана схема входных данных веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2ce41-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="2ce41-121">Необходимо шесть фрагментов входных данных: обучающие данные, тестовые данные, время, индекс параметра time, индекс параметра event и типы переменных (непрерывные или факторные).</span><span class="sxs-lookup"><span data-stu-id="2ce41-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="2ce41-122">Обучающие данные представлены последовательностью символов, в которой строки разделяются запятой, а столбцы точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="2ce41-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="2ce41-123">Количество функций данных может меняться.</span><span class="sxs-lookup"><span data-stu-id="2ce41-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="2ce41-124">Все элементы во входной строке должны быть числовыми.</span><span class="sxs-lookup"><span data-stu-id="2ce41-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="2ce41-125">В обучающих данных параметр time указывает количество единиц времени (дни, годы, расстояние и т. д.), прошедших с момента начала исследования (пациент начал программу лечения от наркомании, кандидат начал писать диссертацию для получения степени доктора наук, автомобиль начал эксплуатироваться и т. д.) до наступления определенного события (возврат пациента к приему наркотиков, получение степени доктора наук, выход из строя тормозной колодки).</span><span class="sxs-lookup"><span data-stu-id="2ce41-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="2ce41-126">Параметр "event" указывает, происходит ли определенное событие в конце исследования.</span><span class="sxs-lookup"><span data-stu-id="2ce41-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="2ce41-127">Значение "event=1" означает, что определенное событие происходит ко времени, заданному параметром time, а "event=0" означает, что определенное событие еще не произошло ко времени, заданному параметром time.</span><span class="sxs-lookup"><span data-stu-id="2ce41-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="2ce41-128">trainingdata — строка символов.</span><span class="sxs-lookup"><span data-stu-id="2ce41-128">trainingdata - A character string.</span></span> <span data-ttu-id="2ce41-129">Строки разделяются запятой, а столбцы точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="2ce41-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="2ce41-130">Каждая строка включает параметр "time", параметр "event" и прогностические переменные.</span><span class="sxs-lookup"><span data-stu-id="2ce41-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="2ce41-131">testingdata — одна строка данных, содержащая прогностические переменные для определенного объекта.</span><span class="sxs-lookup"><span data-stu-id="2ce41-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="2ce41-132">time_of_interest — период времени, n.</span><span class="sxs-lookup"><span data-stu-id="2ce41-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="2ce41-133">index_time — индекс столбца параметра time (начиная с 1).</span><span class="sxs-lookup"><span data-stu-id="2ce41-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="2ce41-134">index_event — индекс столбца параметра event (начиная с 1).</span><span class="sxs-lookup"><span data-stu-id="2ce41-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="2ce41-135">variable_types — строка символов, где разделителем является точка с запятой.</span><span class="sxs-lookup"><span data-stu-id="2ce41-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="2ce41-136">0 представляет непрерывные переменные, а 1 — факторные переменные.</span><span class="sxs-lookup"><span data-stu-id="2ce41-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="2ce41-137">Выходные данные — это вероятность того, что событие произойдет к определенному времени.</span><span class="sxs-lookup"><span data-stu-id="2ce41-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="2ce41-138">Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET.</span><span class="sxs-lookup"><span data-stu-id="2ce41-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2ce41-139">Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2ce41-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2ce41-140">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="2ce41-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="2ce41-141">Интерпретация этого теста выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2ce41-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="2ce41-142">Предположим, что цель данных — смоделировать время до возврата к приему наркотиков пациентами, получавшими лечение по одной из двух программ.</span><span class="sxs-lookup"><span data-stu-id="2ce41-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="2ce41-143">Выходные данные веб-службы сообщают следующее: для пациентов в возрасте 35 лет, дважды проходивших лечение от наркомании, проходящих длительную стационарную реабилитацию и принимавших героин и кокаин, вероятность возврата к приему наркотиков составляет 95,64 % ко дню 500.</span><span class="sxs-lookup"><span data-stu-id="2ce41-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="2ce41-144">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="2ce41-144">Creation of web service</span></span>
> <span data-ttu-id="2ce41-145">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2ce41-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2ce41-146">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="2ce41-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2ce41-147">Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="2ce41-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="2ce41-148">В системе машинного обучения Azure был создан пустой эксперимент, и в рабочую область было помещено два модуля [Выполнить сценарий R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="2ce41-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="2ce41-149">Схема данных была создана с использованием простого модуля [Выполнить сценарий R][execute-r-script], который определяет схему входных данных для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2ce41-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="2ce41-150">Затем этот модуль был связан со вторым модулем [Выполнить сценарий R][execute-r-script], который отвечает за основные операции.</span><span class="sxs-lookup"><span data-stu-id="2ce41-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="2ce41-151">Этот модуль осуществляет предварительную обработку данных, построение модели и прогнозирование.</span><span class="sxs-lookup"><span data-stu-id="2ce41-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="2ce41-152">На этапе предварительной обработки данных входные данные, представленные длинной последовательностью символов, преобразуются в блок данных.</span><span class="sxs-lookup"><span data-stu-id="2ce41-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="2ce41-153">На этапе построения модели сначала устанавливается внешний пакет R "survival_2.37-7.zip" для проведения анализа выживаемости.</span><span class="sxs-lookup"><span data-stu-id="2ce41-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="2ce41-154">Затем после ряда задач по обработке данных выполняется функция "coxph".</span><span class="sxs-lookup"><span data-stu-id="2ce41-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="2ce41-155">Подробные сведения о функции coxph для анализа выживаемости можно найти в документации по языку R.</span><span class="sxs-lookup"><span data-stu-id="2ce41-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="2ce41-156">На шаге прогнозирования тестируемый экземпляр загружается в обученную модель с функцией "surfit", и для данного тестируемого экземпляра создается кривая выживаемости в виде переменной "curve".</span><span class="sxs-lookup"><span data-stu-id="2ce41-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="2ce41-157">Наконец, выдается ответ относительно вероятности того, что событие произойдет к указанному времени.</span><span class="sxs-lookup"><span data-stu-id="2ce41-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="2ce41-158">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="2ce41-158">Experiment flow:</span></span>
![Ход эксперимента][1]

#### <a name="module-1"></a><span data-ttu-id="2ce41-160">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="2ce41-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="2ce41-161">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="2ce41-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="2ce41-162">Ограничения</span><span class="sxs-lookup"><span data-stu-id="2ce41-162">Limitations</span></span>
<span data-ttu-id="2ce41-163">Эта веб-служба принимает только числовые значения для переменных функций (столбцов).</span><span class="sxs-lookup"><span data-stu-id="2ce41-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="2ce41-164">Столбец event принимает только значения 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="2ce41-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="2ce41-165">Столбец time должен быть положительным целым числом.</span><span class="sxs-lookup"><span data-stu-id="2ce41-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="2ce41-166">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="2ce41-166">FAQ</span></span>
<span data-ttu-id="2ce41-167">Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2ce41-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

