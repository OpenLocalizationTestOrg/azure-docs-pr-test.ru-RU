---
title: "Примеры веб-служб машинного обучения на языке R в Azure (устаревшая версия) | Документация Майкрософт"
description: "Здесь вы найдете полезный набор примеров веб-служб, созданных с помощью кода R и системы машинного обучения и опубликованных в Azure Marketplace (устаревшая версия)."
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
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a>Примеры веб-служб, использующие код на языке R в системе машинного обучения Azure и опубликованные в Microsoft Azure Marketplace (устаревшая версия)

> [!NOTE]
> Работа Microsoft DataMarket прекращается, и эти API-интерфейсы больше не поддерживаются. 
> 
> Много полезных примеров экспериментов и API можно найти в [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com). Дополнительные сведения о коллекции см. в статье [Поиск ресурсов в коллекции Cortana Intelligence и обмен ими](machine-learning-gallery-how-to-use-contribute-publish.md).

В этой статье приводятся примеры веб-служб, созданные с помощью системы машинного обучения Azure и опубликованные в Azure Marketplace. К каждому примеру прилагается подробный документ, включающий образцы наборов данных для тестирования служб и объясняющий, как пользователь может самостоятельно создать аналогичную службу. 

С помощью Azure Machine Learning Studio пользователи могут написать код R и всего несколькими щелчками опубликовать его как веб-службу, чтобы другие приложения и устройства по всему миру могли ею пользоваться. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Благодаря простым вычислениям, предоставляющим статистические функции для создания средства прогнозирования мнений на основе интеллектуального анализа текстов, как новички, так и опытные пользователи кода R почувствуют, как легко пользователи системы машинного обучения Azure могут ввести его в действие. Хотя эти веб-службы могут применяться пользователями (потенциально через мобильное приложение или веб-сайт), они также служат примером того, как система машинного обучения Azure может вводить в действие скрипты R для аналитических целей и использоваться для создания веб-служб на основе кода R.

Каждый пример включает пример на языке C# для использования веб-службы.

![Схема кода R в системе машинного обучения Azure: решения на языке R для личного использования или публикации в Azure Marketplace.][1]

Рассмотрим следующие сценарии.

## <a name="scenario-1-generic-model"></a>Сценарий 1. Универсальная модель
Пользователь работает с универсальной моделью, которая может быть применена к новым пользовательским данным, например с базовым прогнозированием данных временных рядов или с пользовательским методом R с расширенной аналитикой. Этот пользователь публикует модель как веб-службу, чтобы другие пользователи могли использовать ее со своими данными.

* [Бинарный классификатор](machine-learning-r-csharp-binary-classifier.md)
* [Кластерная модель](machine-learning-r-csharp-cluster-model.md)
* [Многомерная линейная регрессия](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Прогнозирование на основе метода экспоненциального сглаживания](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [Прогнозирование ETS+STL](machine-learning-r-csharp-retail-demand-forecasting.md)
* [Прогнозирование: авторегрессионная интегрированная модель скользящего среднего (ARIMA)](machine-learning-r-csharp-arima.md)
* [Анализ выживаемости](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Сценарий 2. Обученная модель — определенные данные
У пользователя есть данные, которые предоставляют полезные прогнозы через код R, например большая выборка личностных анкет, кластеризованных с помощью алгоритма K-средних для прогнозирования типа личности пользователя, или данные исследования в области здравоохранения, которые могут использоваться для прогнозирования риска заболевания раком легких с помощью пакета R анализа выживаемости. Пользователь публикует данные через веб-службу, которая прогнозирует результат для нового пользователя.

## <a name="scenario-3-trained-model--generic-data"></a>Сценарий 3. Обученная модель — универсальные данные
У пользователя есть универсальные данные (например, текстовая база данных), позволяющие построить веб-службу и применять ее универсально для различных типов сценариев.

* [Анализ мнений на основе словаря](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Сценарий 4. Расширенный калькулятор
Пользователь предоставляет комплексные вычисления или моделирования, для которых не требуется обученная модель или подгонка модели под данные пользователя.

* [Тест на разницу в пропорциях](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Набор нормального распределения](machine-learning-r-csharp-normal-distribution.md)
* [Набор биномиального распределения](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>Часто задаваемые вопросы
Ознакомиться с часто задаваемыми вопросами по использованию веб-службы и публикации в Магазине можно [здесь](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



