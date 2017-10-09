---
title: "Анализ Выживаемости с машинного обучения Azure AAA(deprecated) | Документы Microsoft"
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
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="c8422-103">Анализ выживаемости (устаревшая версия)</span><span class="sxs-lookup"><span data-stu-id="c8422-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="c8422-104">Hello Microsoft DataMarket прекращено, и этот API устарел.</span><span class="sxs-lookup"><span data-stu-id="c8422-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="c8422-105">Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="c8422-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="c8422-106">Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="c8422-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="c8422-107">Для многих сценариев hello основной результат в разделе оценки — интересующего события tooan время hello.</span><span class="sxs-lookup"><span data-stu-id="c8422-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="c8422-108">Другими словами hello вопрос «когда эти события возникают?»</span><span class="sxs-lookup"><span data-stu-id="c8422-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="c8422-109">В качестве примеров можно привести ситуации, в которых данные описывают время (дни, годы, расстояние и т.</span><span class="sxs-lookup"><span data-stu-id="c8422-109">is asked.</span></span> <span data-ttu-id="c8422-110">В качестве примеров, рассмотрите возможность ситуациях, где данные hello описывает hello затраченное время (дни, годы, расстояние, т. д.) до hello происходит событие (relapse заболеваний, кандидат наук степень получено, pad тормоза сбоя).</span><span class="sxs-lookup"><span data-stu-id="c8422-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="c8422-111">Каждый экземпляр в данных hello представляет определенный объект (пациента студент, автомобиль, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c8422-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="c8422-112">Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) отвечает на вопрос hello, «какова вероятность hello, hello интересующего события будет выполняться на n времени для объекта x?»</span><span class="sxs-lookup"><span data-stu-id="c8422-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="c8422-113">Предоставляя модель анализа практические советы, эта веб-служба позволяет пользователям toosupply tootrain hello модели и его проверка.</span><span class="sxs-lookup"><span data-stu-id="c8422-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="c8422-114">Основные темы Hello эксперимента hello — длина hello toomodel hello затраченное время, до наступления события hello интерес.</span><span class="sxs-lookup"><span data-stu-id="c8422-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="c8422-115">Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c8422-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="c8422-116">Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R.</span><span class="sxs-lookup"><span data-stu-id="c8422-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="c8422-117">Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c8422-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="c8422-118">Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c8422-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="c8422-119">Использование веб-службы</span><span class="sxs-lookup"><span data-stu-id="c8422-119">Consumption of web service</span></span>
<span data-ttu-id="c8422-120">в следующей таблице hello показана схема входных данных Hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c8422-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="c8422-121">Шесть части сведений требуются в качестве входных данных hello: обучающих данных, проверочных данных, процент времени, hello индекс измерения «время», индекс hello измерения «событие» и типы переменных hello (непрерывной или коэффициент).</span><span class="sxs-lookup"><span data-stu-id="c8422-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="c8422-122">Hello обучающих данных представляется со строкой hello строки разделяются запятой, куда hello столбцы разделяются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c8422-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="c8422-123">Hello несколько функций hello данных является гибкой.</span><span class="sxs-lookup"><span data-stu-id="c8422-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="c8422-124">Все элементы hello hello входной строке должен быть числовым.</span><span class="sxs-lookup"><span data-stu-id="c8422-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="c8422-125">В hello обучающих данных измерение времени «hello» указывает, что hello количество единиц времени (дни, годы, расстояние, т. д.), истекшее с момента hello начальную точку hello изучения (пациента получение лекарство работа программы, кандидат наук исследование начальный студента, начиная toobe автомобиля управляемые, и т. д.) пока не будет выполнена hello событие (hello patient возвращение toodrug использование hello студента получения hello кандидат наук степень, автомобиль hello наличие сбоя тормоза pad, т. д.).</span><span class="sxs-lookup"><span data-stu-id="c8422-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="c8422-126">Измерение «событие» Hello указывает, наступает ли hello событие в конце hello пример hello.</span><span class="sxs-lookup"><span data-stu-id="c8422-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="c8422-127">Значение «событий = 1» означает, что hello интересующее событие происходит во время hello, обозначенном hello измерения «время»; «Событие = 0» означает, что hello интересующее событие не произошло, время hello, определенное в измерении «время» hello.</span><span class="sxs-lookup"><span data-stu-id="c8422-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="c8422-128">trainingdata — строка символов.</span><span class="sxs-lookup"><span data-stu-id="c8422-128">trainingdata - A character string.</span></span> <span data-ttu-id="c8422-129">Строки разделяются запятой, а столбцы точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c8422-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="c8422-130">Каждая строка включает параметр "time", параметр "event" и прогностические переменные.</span><span class="sxs-lookup"><span data-stu-id="c8422-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="c8422-131">testingdata — одна строка данных, содержащая прогностические переменные для определенного объекта.</span><span class="sxs-lookup"><span data-stu-id="c8422-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="c8422-132">time_of_interest — время, затраченное hello n процентов.</span><span class="sxs-lookup"><span data-stu-id="c8422-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="c8422-133">index_time - hello индекс столбца (начиная с 1) измерения «время» hello.</span><span class="sxs-lookup"><span data-stu-id="c8422-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="c8422-134">index_event - hello индекс столбца (начиная с 1) измерения «событие» hello.</span><span class="sxs-lookup"><span data-stu-id="c8422-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="c8422-135">variable_types — строка символов, где разделителем является точка с запятой.</span><span class="sxs-lookup"><span data-stu-id="c8422-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="c8422-136">0 представляет непрерывные переменные, а 1 — факторные переменные.</span><span class="sxs-lookup"><span data-stu-id="c8422-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="c8422-137">выходные данные Hello — вероятность hello событие, которое происходит в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="c8422-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="c8422-138">Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET.</span><span class="sxs-lookup"><span data-stu-id="c8422-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="c8422-139">Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="c8422-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="c8422-140">Начало кода C# для использования веб-службы:</span><span class="sxs-lookup"><span data-stu-id="c8422-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="c8422-141">Интерпретация Hello этот тест будет следующим.</span><span class="sxs-lookup"><span data-stu-id="c8422-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="c8422-142">При условии, что цель hello hello данных — время, затраченное hello toomodel до hello возвращают toodrug использования для hello пациентов, которые — одно из двух hello работа программы.</span><span class="sxs-lookup"><span data-stu-id="c8422-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="c8422-143">Здравствуйте, выходные данные операций чтения службы web hello: пациентов, Возраст 35 лет, с предыдущей лекарства обработку 2 раза занимает hello долго частный работа программы, и сведениями об использовании heroin и cocaine hello вероятность возврата toohello лекарство использования % 95.64 по день 500.</span><span class="sxs-lookup"><span data-stu-id="c8422-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="c8422-144">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="c8422-144">Creation of web service</span></span>
> <span data-ttu-id="c8422-145">Эта веб-служба была создана с помощью системы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c8422-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="c8422-146">Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="c8422-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="c8422-147">Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.</span><span class="sxs-lookup"><span data-stu-id="c8422-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="c8422-148">Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули были «втянуты» в область hello.</span><span class="sxs-lookup"><span data-stu-id="c8422-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="c8422-149">Hello схемы данных был создан с помощью простого [выполнение скрипта R][execute-r-script], который определяет схему hello входные данные для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c8422-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="c8422-150">Этот модуль будет связан toohello второй [выполнение скрипта R] [ execute-r-script] модуль, в котором основной рабочий.</span><span class="sxs-lookup"><span data-stu-id="c8422-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="c8422-151">Этот модуль осуществляет предварительную обработку данных, построение модели и прогнозирование.</span><span class="sxs-lookup"><span data-stu-id="c8422-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="c8422-152">На этапе предварительной обработки данных hello представленный длинную строку входных данных hello преобразования и преобразуется в кадре данных.</span><span class="sxs-lookup"><span data-stu-id="c8422-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="c8422-153">На этапе построения модели hello внешних пакет R «survival_2.37 7.zip» сначала устанавливается при проведении анализа практические советы.</span><span class="sxs-lookup"><span data-stu-id="c8422-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="c8422-154">Затем функция «coxph» hello выполняется после ряда задач обработки данных.</span><span class="sxs-lookup"><span data-stu-id="c8422-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="c8422-155">Hello подробные сведения о функции «coxph» hello, для анализа практические советы могут считываться из документации hello R.</span><span class="sxs-lookup"><span data-stu-id="c8422-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="c8422-156">На этапе прогноза hello тестирования экземпляр предоставляется hello обученной модели с помощью функции «surfit» hello, а hello кривой практические советы для данного экземпляра тестирования создается как переменная «curve».</span><span class="sxs-lookup"><span data-stu-id="c8422-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="c8422-157">Наконец получается вероятность hello времени hello интерес.</span><span class="sxs-lookup"><span data-stu-id="c8422-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="c8422-158">Ход эксперимента:</span><span class="sxs-lookup"><span data-stu-id="c8422-158">Experiment flow:</span></span>
![Ход эксперимента][1]

#### <a name="module-1"></a><span data-ttu-id="c8422-160">Модуль 1:</span><span class="sxs-lookup"><span data-stu-id="c8422-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="c8422-161">Модуль 2:</span><span class="sxs-lookup"><span data-stu-id="c8422-161">Module 2:</span></span>
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

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
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

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
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

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="c8422-162">Ограничения</span><span class="sxs-lookup"><span data-stu-id="c8422-162">Limitations</span></span>
<span data-ttu-id="c8422-163">Эта веб-служба принимает только числовые значения для переменных функций (столбцов).</span><span class="sxs-lookup"><span data-stu-id="c8422-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="c8422-164">столбец «события» Hello может принимать только значение 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="c8422-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="c8422-165">столбец «время» Hello должен toobe положительным целым числом.</span><span class="sxs-lookup"><span data-stu-id="c8422-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="c8422-166">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c8422-166">FAQ</span></span>
<span data-ttu-id="c8422-167">Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="c8422-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

