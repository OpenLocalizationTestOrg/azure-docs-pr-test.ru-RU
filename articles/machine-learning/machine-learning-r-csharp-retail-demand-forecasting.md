---
title: "AAA(deprecated) Forecasting - ETS + STL - Azure | Документы Microsoft"
description: "Прогнозирование на основе ETS и STL (устаревшая версия)"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 550d423898d46564936fdcfbf05b7c88d2e292c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---ets--stl"></a>Прогнозирование на основе ETS и STL (устаревшая версия)

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и этот API устарел. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Это [веб-службы](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) реализует развернутого сезонных тенденций (STL) и экспоненциального сглаживания (ETS) прогнозов tooproduce моделей на основе hello исторических данных, hello пользователем. Будет hello запросу увеличивать определенного продукта в этом году? Можно ли прогнозирования продаж продукта для hello сезона Рождество, чтобы эффективно задавать my инвентаризации? Модели прогнозирования являются apt tooaddress такие вопросы. Учитывая hello данных, в прошлом эти модели проверки скрытые тенденции и будущие тенденции toopredict сезонности. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Эту веб-службу можно использовать через мобильное приложение, веб-сайт или на локальном компьютере. Но hello hello веб-службы служит также tooserve в качестве примера как машинного обучения Azure можно использовать toocreate веб-служб на основе кода R. Чтобы создать эксперимент с использованием кода R и опубликовать его как веб-службу, достаточно написать несколько строк кода R и нажать несколько кнопок в студии машинного обучения Azure. Hello веб-службы может быть опубликованным toohello Azure Marketplace и используемые пользователями и устройствами через Здравствуй, мир без настройки инфраструктуры автором hello hello веб-службы.  
> 
> 

## <a name="consumption-of-web-service"></a>Использование веб-службы
Эта служба принимает аргументы, 4 и вычисляет прогнозы hello.
Hello входными аргументами являются:

* Частота — указывает частоту hello hello необработанных данных (ежедневно или еженедельно или ежемесячно или ежеквартально/ежегодного резервного копирования).
* Горизонт: временные рамки прогноза на будущее.
* Дата — Добавление в hello нового временного ряда данных времени.
* Значение — Добавление в hello новые значения рядов времени данных.

выходные данные Hello hello службы — hello вычисляемые значения прогноза.

Пример вводимых данных: 

* Частота: 12
* Горизонт: 12
* Дата: 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014
* Значение: 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509

> Эта служба, размещенного на hello Azure Marketplace, — это служба OData; Это может быть вызвана через методы POST или GET. 
> 
> 

Существует несколько способов использования службы hello в автоматическом режиме (пример приложения — [здесь](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Начало кода C# для использования веб-службы:
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
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

В службах машинного обучения Azure создан пустой эксперимент. Загружен образец входных данных с заранее заданной схемой данных. Схема данных связанного toohello [выполнение скрипта R] [ execute-r-script] модуль, создающий STL и ETS моделей прогнозирования с помощью «stl», «ets» и «прогноза» функции R. 

### <a name="experiment-flow"></a>Ход эксперимента:
![Ход эксперимента][2]

#### <a name="module-1"></a>Модуль 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Пример данных][3]    

#### <a name="module-2"></a>Модуль 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a>Ограничения
Это очень простой пример прогнозирования ETS+STL. Как видно в приведенном выше примере кода hello, перехват ошибок не реализован, и службы hello предполагается, что все переменные hello, непрерывные или положительные значения и hello частоты должно быть целое число больше 1. Hello длина hello значения даты и векторов должна быть же hello и длина hello hello временных рядов должна быть больше, чем 2 * частоты. переменная приветствия даты должны соблюдаться toohello формат «мм/дд/гггг».

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Azure Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

