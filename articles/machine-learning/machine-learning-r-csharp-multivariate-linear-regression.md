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
# <a name="deprecated-multivariate-linear-regression"></a>(Не рекомендуется.) Многофакторная линейная регрессия

> [!NOTE]
> Работа Microsoft DataMarket прекращается, и этот API больше не поддерживается. 
> 
> Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).

Предположим, у вас есть набор данных и вы хотите быстро спрогнозировать значение зависимой переменной (y) для каждого отдельного значения (i) на основе независимых переменных. Для создания таких прогнозов часто используется статистическая технология линейной регрессии. Здесь каждая зависимая переменная y считается принимающей непрерывные значения.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Простейший случай применения этого метода — попытка спрогнозировать вес человека (y) на основе его роста (x). В более сложном сценарии может быть доступна дополнительная информация об исследуемом человеке (например, его пол, раса и т. д.), на основе которой требуется определить его вес. Эта [веб-служба](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) применяет модель линейной регрессии к данным и выдает прогнозируемое значение (y) для каждого из входящих в ряд данных наблюдения.

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Веб-служба также служит примером того, как машинное обучение Azure можно использовать для создания веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Затем веб-службу можно опубликовать в Azure Marketplace, и ее смогут применять пользователи и устройства по всему миру, при этом автору веб-службы не придется настраивать инфраструктуру.  
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Эта веб-служба выдает прогнозируемые значения зависимой переменной на основе независимых переменных для всех наблюдений. Она принимает входные данные в виде блока, где строки разделены запятыми (,), а столбцы — точками с запятой (;). Веб-служба принимает по одной строке, причем первый столбец должен содержать зависимую переменную. Ниже приведен пример набора данных.

![Пример данных][1]

В наблюдениях, в которых нет зависимой переменной, для значения y необходимо указать NA. Вот пример входной строки для такого набора данных: "10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4". На выходе служба выдает прогнозируемое значение для каждой строки на основе независимых переменных. 

> Эта служба, размещенная в Azure Marketplace, является службой на основе OData. Вызвать ее можно методами POST и GET. 
> 
> 

Есть несколько способов использования службы в автоматическом режиме (см. пример приложения [здесь](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

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
> Эта веб-служба была создана с помощью системы машинного обучения Azure. Чтобы получить бесплатную пробную версию и вводные видеоматериалы по созданию экспериментов и [публикации веб-служб](machine-learning-publish-a-machine-learning-web-service.md), посетите веб-страницу [azure.com/ml](http://azure.com/ml). Ниже приведен снимок экрана эксперимента, в результате которого была создана веб-служба, и пример кода для каждого модуля в эксперименте.
> 
> 

В системе машинного обучения Azure был создан пустой эксперимент, и в рабочую область было помещено два модуля [Выполнить сценарий R][execute-r-script]. Эта веб-служба выполняет эксперимент машинного обучения Azure на базе сценария R. Эксперимент состоит из двух частей: определение схемы и обучение модели + оценка. Первый модуль определяет структуру ожидаемого входного набора данных, в котором первая переменная является зависимой, а остальные — независимыми. Второй модуль применяет к входным данным стандартную модель линейной регрессии.  

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
Это очень простой пример веб-службы многофакторной линейной регрессии. Как видно из приведенного выше образца кода, в нем не отслеживаются ошибки, а служба предполагает, что все входные данные являются непрерывными переменными (без категоризации), так как принимает только числовые значения. Кроме того, веб-служба способна обработать лишь ограниченный объем данных, так как это служба запроса/ответа, а модель применяется каждый раз при ее вызове. 

## <a name="faq"></a>Часто задаваемые вопросы
Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Azure Marketplace можно [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

