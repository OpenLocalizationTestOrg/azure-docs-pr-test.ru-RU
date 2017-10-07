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
# <a name="deprecated-cluster-model"></a>Кластерная модель (устаревшая версия)

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Как можно прогнозировать групп поведений cardholders кредит в порядке tooreduce hello списания риска кредитной карты издателей? Как мы группы можно определить из характеристик индивидуальность сотрудников tooimprove порядок их производительность на работе? Как врачи можно классифицировать пациентов по группам на основе характеристик hello их болезней? В принципе, на все эти вопросы помогает ответить кластерный анализ.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Кластерный анализ позволяет разделить массив наблюдений на две или несколько взаимоисключающих неопределенных групп на основе сочетания переменных. Hello анализа кластера служит toodiscover системы организации наблюдений, обычно людей или их характеристики по группам, где члены групп hello общими для свойства. Это [службы](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) использует hello методологии K-средние, наиболее часто используемого метода кластеризации, toocluster произвольных данных в группы. Эта веб-служба принимает данные hello и hello число k кластеров в качестве входных данных и создает прогнозы, из которых hello k группы toowhich принадлежит каждого наблюдения. 

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.  
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Эта веб-служба группирует данные hello набора k групп и выходы hello Назначение группы для каждой строки. Hello веб-служба ожидает hello конечного пользователя tooinput данные как строку, где строки разделяются запятыми (,), а столбцы разделяются точками с запятой (;). Hello веб-служба ожидает 1 строки за раз. Ниже приведен пример набора данных.

![Пример данных][1]

Предположим, что tooseparate пользователя было hello эти данные по 3 группам взаимно исключают друг друга. Здравствуйте ввода для hello выше набор данных будет hello следующие данные: значение = «10, 5 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3, 4»; k = «3». для каждой из строк hello Hello выходные данные hello членство в группе прогнозируемые.

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Начало кода C# для использования веб-службы:
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




## <a name="creation-of-web-service"></a>Создание веб-службы
> Эта веб-служба была создана с помощью системы машинного обучения Azure. Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml). Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.
> 
> 

Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули извлечено в область hello. Схема данных Hello была создана с помощью простого [выполнение скрипта R][execute-r-script]. Затем схемы данных hello был связанного toohello кластера раздел модели, вновь создается с [выполнение скрипта R][execute-r-script]. В hello [выполнение скрипта R] [ execute-r-script] , используемое hello кластерной модели, hello веб-служба затем использует функции hello «k средние», которое является готовых в hello [выполнение скрипта R] [ execute-r-script] Azure машинного обучения.    

![Ход эксперимента][3]

#### <a name="module-1"></a>Модуль 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Модуль 2:
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


## <a name="limitations"></a>Ограничения
Это очень простой пример веб-службы кластеризации. Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и служба hello предполагает, что все непрерывной переменной (не категориальных признаков допускается), как hello службы только входные данные числовые значения во время hello hello создания этого веб-сайта Служба. Кроме того служба hello в настоящее время обрабатывает данные ограниченный размер, из-за характера запроса и ответа toohello hello веб-служба вызова и hello факт, что hello модели, выполняется подходит каждый раз при вызове hello веб-службы. 

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

