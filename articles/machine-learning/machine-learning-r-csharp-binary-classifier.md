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
# <a name="deprecated-binary-classifier"></a>Двоичный классификатор (устаревшая версия)

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Предположим, что есть набор данных и хотите toopredict двоичных зависимой переменной на основе hello независимых переменных. Для создания таких прогнозов часто используется статистическая технология логистической регрессии. Вот hello зависимой переменной binary или дихотомических и p — hello вероятность наличия характеристика hello интерес. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Может быть простой сценарий, где научный сотрудник пытается toopredict, является ли студент потенциального скорее всего tooaccept tooa университета допуском предложение, на основе сведений (GPA в средней школе, семейства доход, резидентных состояние пола). Hello прогнозируемый результат — hello вероятность потенциального студента hello принятия предложения допуском hello. Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/log_regression) подходить hello данных toohello модели логистической регрессии и выходы hello значение вероятности (y) для каждого наблюдений hello в данных hello.  

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.  
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Этот web service дает hello прогнозируемые значения из hello зависимой переменной на основе hello независимых переменных для всех наблюдений hello. Hello веб-служба ожидает hello конечного пользователя tooinput данные как строку, где строки разделяются запятой (,), а столбцы разделяются точкой с запятой (;). Hello веб-служба ожидает 1 строки за раз и ожидает hello первый столбец toobe hello зависимой переменной. Ниже приведен пример набора данных.

![Пример данных][1]

В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA. Hello входных данных для hello выше набор данных будет быть hello следующая строка: «1, 5 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, н/д; 3, 4». Hello вывода hello прогнозируемое значение для каждой из строк hello основан на hello независимых переменных. 

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Начало кода C# для использования веб-службы:
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


## <a name="creation-of-web-service"></a>Создание веб-службы
> Эта веб-служба была создана с помощью системы машинного обучения Azure. Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml). Ниже приведен снимок экрана приветствия эксперимента, созданные для каждого из модулей hello в эксперименте hello hello веб-службы и пример кода.
> 
> 

Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули извлечено в область hello. Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R. Существует 2 частей toothis поэкспериментировать: определение схемы и обучения модели + оценки. Первый модуль Hello определяет структуру hello ожидается hello входного набора данных, где hello первой переменной — hello зависимой переменной, а остальные переменные hello независимы. второй модуль Hello подгоняет модель универсального логистической регрессии для hello входных данных.    

![Ход эксперимента][2]

#### <a name="module-1"></a>Модуль 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Модуль 2:
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


## <a name="limitations"></a>Ограничения
Это очень простой пример веб-службы двоичной классификации. Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и службы hello предполагает, что все двоичные/непрерывной переменной (не категориальных признаков допускается), как hello службы только входные данные числовые значения во время hello hello создания данного объекта веб-служба. Кроме того служба hello в настоящее время обрабатывает данные ограниченный размер, из-за характера запроса и ответа toohello hello веб-служба вызова и hello факт, что hello модели, выполняется подходит каждый раз при вызове hello веб-службы. 

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

