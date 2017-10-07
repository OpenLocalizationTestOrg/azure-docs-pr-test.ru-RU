---
title: "AAA(deprecated) машины обучения, веб-служб, примеры, созданного с помощью R - Azure | Документы Microsoft"
description: "(устарело) Найти полезные набор примеров web services создана с кодом R и машинное обучение и опубликована toohello Azure Marketplace."
keywords: "csharp, код r, примеры веб-служб"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
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
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a>(устарело) Примеры использования кода R в машинном обучении Azure и опубликованных tooMicrosoft Azure Marketplace веб-службы

> [!NOTE]
> Hello Microsoft DataMarket прекращено, и эти API-интерфейсы являются устаревшими. 
> 
> Можно найти множество полезный пример экспериментов и API-интерфейсы в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции hello. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](machine-learning-gallery-how-to-use-contribute-publish.md).

В этой статье, пример web services были созданы с помощью машинного обучения Azure и публикуются toohello Azure Marketplace. Каждый пример веб-службы имеет полный документ, внедрение образцы наборов данных для тестирования службы hello и о том, как hello пользователь может создать аналогичную службу самостоятельно. 

В студии машинного обучения Azure пользователей можно написать код R и с помощью нескольких щелчков опубликовать его как веб-службы для приложения и устройства tooconsume вокруг Здравствуй, мир. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Вместо создания простого калькуляторы, предоставляющих статистические функции toocreating пользовательских прогнозирующих анализ мнений интеллектуального анализа текста, новых и опытных пользователей R могут использовать преимущества hello простота, с помощью которого пользователи машинного обучения Azure можно ввода в эксплуатацию R код. Хотя эти веб-службы могут применяться пользователями, потенциально через мобильное приложение или веб-сайт hello цель этих веб-служб, tooshow, как можно эксплуатацию машинного обучения — примеры R скрипты для анализа и используется toocreate веб-службы на начало кода R.

Каждый пример включает пример на языке C# для использования веб-службы.

![Схема кода R в машинном обучении Azure: решения R для использования собственных или опубликованные toohello Azure Marketplace.][1]

Рассмотрим следующие сценарии hello.

## <a name="scenario-1-generic-model"></a>Сценарий 1. Универсальная модель
Пользователь работает с универсальной модели, который может быть применен tooa нового пользователя данных, например основные прогнозирования временного ряда данных или пользовательские метод R с расширенной аналитики. Этот пользователь публикует hello модели веб-службы для других tooconsume с их данными.

* [Бинарный классификатор](machine-learning-r-csharp-binary-classifier.md)
* [Кластерная модель](machine-learning-r-csharp-cluster-model.md)
* [Многомерная линейная регрессия](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Прогнозирование на основе метода экспоненциального сглаживания](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [Прогнозирование ETS+STL](machine-learning-r-csharp-retail-demand-forecasting.md)
* [Прогнозирование: авторегрессионная интегрированная модель скользящего среднего (ARIMA)](machine-learning-r-csharp-arima.md)
* [Анализ выживаемости](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Сценарий 2. Обученная модель — определенные данные
У пользователя есть данные, которые предоставляют полезные прогнозы выполнение кода R, такие как большой образец опросов индивидуальность clustered через k средних алгоритм toopredict hello индивидуальность типа пользователя или работоспособности исследования данных, который можно использовать toopredict пользователя риск для вызывает рак с помощью пакета аналитики R практические советы. Hello пользователь публикует hello данных через веб-службу, которая прогнозирует результат нового пользователя.

## <a name="scenario-3-trained-model--generic-data"></a>Сценарий 3. Обученная модель — универсальные данные
У пользователя есть универсальный данные (например, в совокупности текста), позволяющий web service toobe построен и универсальная применения на разных типах варианты использования и сценарии.

* [Анализ мнений на основе словаря](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Сценарий 4. Расширенный калькулятор
Пользователь предоставляет сложных расчетов или моделирования, не требующие любой обученной модели или подгонки пользователя toohello модели данных.

* [Тест на разницу в пропорциях](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Набор нормального распределения](machine-learning-r-csharp-normal-distribution.md)
* [Набор биномиального распределения](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>Часто задаваемые вопросы
Часто задаваемые вопросы о потреблении hello веб-службы или публикации toohello Marketplace в разделе [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



