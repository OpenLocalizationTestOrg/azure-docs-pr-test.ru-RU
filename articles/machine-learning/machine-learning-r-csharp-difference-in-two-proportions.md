---
title: "Разница в тесте пропорции - Azure AAA(deprecated) | Документы Microsoft"
description: "Тест на разницу в пропорциях (устаревшая версия)"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a>Тест на разницу в пропорциях (устаревшая версия)

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Существует ли между двумя долями статистическая разница? Предположим, что пользователь хочет toocompare двух toodetermine фильмы, если один фильма имеет значительно большее количество «нравится» при сравнении toohello других. С большой образец может быть статистически значимой разницы между hello пропорции 0,50 и 0,51. С небольшой выборкой может отсутствовать toodetermine достаточно данных, если эти пропорции, фактически отличаются. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/prop_test) выполняет тест гипотезы hello разницы в двух пропорции, на основе ввода пользователя hello количество успешных и общее количество пробных версий для сравнения групп hello 2 hello. В один из возможных сценариев можно вызывать веб-службу из в приложении сравнения фильм, предписывая пользователя hello ли один фильмов hello «применено» чаще, чем другие, hello на основе фильма оценок.

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Эта служба принимает 4 аргумента и выполняет проверку гипотезы для долей.

Hello входными аргументами являются:

* Successes1 — количество успешных испытаний в выборке 1.
* Successes2 — количество успешных испытаний в выборке 2.
* Total1 — размер выборки 1.
* Total2 — размер выборки 2.

выходные данные Hello hello службы является результатом hello гипотезы hello тестов вместе с значение hello chi-square статистики, df, p и пропорция в пределах 1/2 и доверительный интервал образца.

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Начало кода C# для использования веб-службы:
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
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

В системе машинного обучения Azure был создан пустой эксперимент с двумя модулями [Выполнить сценарий R][execute-r-script]. В первый модуль hello hello схемы данных определен, второй модуль hello не используется команда prop.test hello в тест гипотезы hello tooperform R для 2 пропорций. 

### <a name="experiment-flow"></a>Ход эксперимента:
![Ход эксперимента][2]

#### <a name="module-1"></a>Модуль 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Модуль 2:
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a>Ограничения
Это очень простой пример проверки различия двух долей. Перехват ошибок не реализован как видно в приведенном выше примере кода hello, и служба hello предполагается, что все переменные hello непрерывной.

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

