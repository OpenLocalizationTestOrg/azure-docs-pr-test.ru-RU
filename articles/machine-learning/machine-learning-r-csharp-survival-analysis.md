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
# <a name="deprecated-survival-analysis"></a>Анализ выживаемости (устаревшая версия)

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Для многих сценариев hello основной результат в разделе оценки — интересующего события tooan время hello. Другими словами hello вопрос «когда эти события возникают?» В качестве примеров можно привести ситуации, в которых данные описывают время (дни, годы, расстояние и т. В качестве примеров, рассмотрите возможность ситуациях, где данные hello описывает hello затраченное время (дни, годы, расстояние, т. д.) до hello происходит событие (relapse заболеваний, кандидат наук степень получено, pad тормоза сбоя). Каждый экземпляр в данных hello представляет определенный объект (пациента студент, автомобиль, и т. д.).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) отвечает на вопрос hello, «какова вероятность hello, hello интересующего события будет выполняться на n времени для объекта x?» Предоставляя модель анализа практические советы, эта веб-служба позволяет пользователям toosupply tootrain hello модели и его проверка. Основные темы Hello эксперимента hello — длина hello toomodel hello затраченное время, до наступления события hello интерес. 

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.  
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
в следующей таблице hello показана схема входных данных Hello hello веб-службы. Шесть части сведений требуются в качестве входных данных hello: обучающих данных, проверочных данных, процент времени, hello индекс измерения «время», индекс hello измерения «событие» и типы переменных hello (непрерывной или коэффициент). Hello обучающих данных представляется со строкой hello строки разделяются запятой, куда hello столбцы разделяются точкой с запятой. Hello несколько функций hello данных является гибкой. Все элементы hello hello входной строке должен быть числовым. В hello обучающих данных измерение времени «hello» указывает, что hello количество единиц времени (дни, годы, расстояние, т. д.), истекшее с момента hello начальную точку hello изучения (пациента получение лекарство работа программы, кандидат наук исследование начальный студента, начиная toobe автомобиля управляемые, и т. д.) пока не будет выполнена hello событие (hello patient возвращение toodrug использование hello студента получения hello кандидат наук степень, автомобиль hello наличие сбоя тормоза pad, т. д.). Измерение «событие» Hello указывает, наступает ли hello событие в конце hello пример hello. Значение «событий = 1» означает, что hello интересующее событие происходит во время hello, обозначенном hello измерения «время»; «Событие = 0» означает, что hello интересующее событие не произошло, время hello, определенное в измерении «время» hello.

* trainingdata — строка символов. Строки разделяются запятой, а столбцы точкой с запятой. Каждая строка включает параметр "time", параметр "event" и прогностические переменные.
* testingdata — одна строка данных, содержащая прогностические переменные для определенного объекта.
* time_of_interest — время, затраченное hello n процентов.
* index_time - hello индекс столбца (начиная с 1) измерения «время» hello.
* index_event - hello индекс столбца (начиная с 1) измерения «событие» hello.
* variable_types — строка символов, где разделителем является точка с запятой. 0 представляет непрерывные переменные, а 1 — факторные переменные.

выходные данные Hello — вероятность hello событие, которое происходит в определенный момент времени. 

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Начало кода C# для использования веб-службы:
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




Интерпретация Hello этот тест будет следующим. При условии, что цель hello hello данных — время, затраченное hello toomodel до hello возвращают toodrug использования для hello пациентов, которые — одно из двух hello работа программы. Здравствуйте, выходные данные операций чтения службы web hello: пациентов, Возраст 35 лет, с предыдущей лекарства обработку 2 раза занимает hello долго частный работа программы, и сведениями об использовании heroin и cocaine hello вероятность возврата toohello лекарство использования % 95.64 по день 500.

## <a name="creation-of-web-service"></a>Создание веб-службы
> Эта веб-служба была создана с помощью системы машинного обучения Azure. Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml). Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.
> 
> 

Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули были «втянуты» в область hello. Hello схемы данных был создан с помощью простого [выполнение скрипта R][execute-r-script], который определяет схему hello входные данные для hello веб-службы. Этот модуль будет связан toohello второй [выполнение скрипта R] [ execute-r-script] модуль, в котором основной рабочий. Этот модуль осуществляет предварительную обработку данных, построение модели и прогнозирование. На этапе предварительной обработки данных hello представленный длинную строку входных данных hello преобразования и преобразуется в кадре данных. На этапе построения модели hello внешних пакет R «survival_2.37 7.zip» сначала устанавливается при проведении анализа практические советы. Затем функция «coxph» hello выполняется после ряда задач обработки данных. Hello подробные сведения о функции «coxph» hello, для анализа практические советы могут считываться из документации hello R. На этапе прогноза hello тестирования экземпляр предоставляется hello обученной модели с помощью функции «surfit» hello, а hello кривой практические советы для данного экземпляра тестирования создается как переменная «curve». Наконец получается вероятность hello времени hello интерес. 

### <a name="experiment-flow"></a>Ход эксперимента:
![Ход эксперимента][1]

#### <a name="module-1"></a>Модуль 1:
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

#### <a name="module-2"></a>Модуль 2:
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




## <a name="limitations"></a>Ограничения
Эта веб-служба принимает только числовые значения для переменных функций (столбцов). столбец «события» Hello может принимать только значение 0 или 1. столбец «время» Hello должен toobe положительным целым числом.

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

