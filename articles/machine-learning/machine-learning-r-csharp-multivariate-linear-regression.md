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
# <a name="deprecated-multivariate-linear-regression"></a>(Не рекомендуется.) Многофакторная линейная регрессия

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Предположим, что у вас есть набор данных и бы как tooquickly прогнозирования зависимой переменной (y) для каждого отдельного (i), в зависимости от независимых переменных. Для создания таких прогнозов часто используется статистическая технология линейной регрессии. Здесь предполагается toobe непрерывного значения y hello зависимой переменной.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Может быть простой сценарий, где научный сотрудник hello пытается вес hello toopredict лица (y) на основе их высоты (x). Более сложные сценарии может быть где научный сотрудник hello дополнительную информацию для отдельных (например, вес, пол, состояние гонки) hello и пытается вес hello toopredict отдельных hello. Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) подходить hello данных toohello модели линейной регрессии и выходы hello предсказанных значений (y) для каждого наблюдений hello в данных hello.

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.  
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Этот web service дает hello прогнозируемые значения из hello зависимой переменной на основе hello независимых переменных для всех наблюдений hello. Hello веб-служба ожидает hello конечного пользователя tooinput данные как строку, где строки разделяются запятыми (,), а столбцы разделяются точками с запятой (;). Hello веб-служба ожидает 1 строки за раз и ожидает hello первый столбец toobe hello зависимой переменной. Ниже приведен пример набора данных.

![Пример данных][1]

В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA. Hello входных данных для hello выше набор данных будет быть hello следующая строка: «10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, н/д: 3: 4». Hello вывода hello прогнозируемое значение для каждой из строк hello основан на hello независимых переменных. 

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

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

Из в машинном обучении Azure новый пустой эксперимент был создан и два [выполнение скрипта R] [ execute-r-script] модули были «втянуты» в область hello. Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R. Существует 2 частей toothis поэкспериментировать: определение схемы и обучения модели + оценки. Первый модуль Hello определяет структуру hello ожидается hello входного набора данных, где hello первой переменной — hello зависимой переменной, а остальные переменные hello независимы. второй модуль Hello подгоняет модель универсального линейной регрессии для hello входных данных.  

![Ход эксперимента][3]

#### <a name="module-1"></a>Модуль 1:
#### <a name="schema-definition"></a>определение схемы
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a>Модуль 2:
#### <a name="lm-modeling"></a>моделирование LM
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

## <a name="limitations"></a>Ограничения
Это очень простой пример веб-службы многофакторной линейной регрессии. Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и служба hello предполагает, что все непрерывной переменной (не категориальных признаков допускается), как hello службы только входные данные числовые значения во время hello hello создания этого веб-сайта Служба. Кроме того служба hello в настоящее время обрабатывает данные ограниченный размер, из-за характера запроса и ответа toohello hello веб-служба вызова и hello факт, что hello модели, выполняется подходит каждый раз при вызове hello веб-службы. 

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

