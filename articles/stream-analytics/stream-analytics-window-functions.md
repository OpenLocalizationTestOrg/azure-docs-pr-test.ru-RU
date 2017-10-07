---
title: "функции аналитики окна tooStream aaaIntroduction | Документы Microsoft"
description: "Дополнительные сведения о трех Оконные функции hello в Stream Analytics («переворачивающееся», «прыгающее», перемещая)."
keywords: "\"переворачивающееся\" окно, \"скользящее\" окно, \"прыгающее\" окно"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a>Введение tooStream Analytics Оконные функции
Многие реального времени сценариев потоковой передачи при необходимости tooperform операции только с hello данные, содержащиеся в темпоральных windows. Собственная поддержка для функций управления окнами является ключевой компонент Azure Stream Analytics, перемещающего hello стрелки на производительность разработчика в разработке задания по обработке сложных потока. Stream Analytics дает разработчикам toouse [ **Переворачивающееся**](https://msdn.microsoft.com/library/dn835055.aspx), [ **«прыгающие» окна** ](https://msdn.microsoft.com/library/dn835041.aspx) и [ **скользящий** ](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform операции со временем потоковой передачи данных. Стоит отметить, что все [окна](https://msdn.microsoft.com/library/dn835019.aspx) операции выводить результаты в hello **окончания** окна hello. выходные данные Hello hello окна будут основании hello агрегатной функции, используемой одно событие. событие Hello будет иметь отметку времени hello hello окончания периода hello и все Оконные функции определены с фиксированной длиной. Наконец он является важным toonote, который следует использовать все функции окна в [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) предложения.

![Концепции функций окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a>"Переворачивающееся" окно
Функции «переворачивающегося» окна используется toosegment потока данных на фрагменты отдельных времени и выполняет функцию с ними, например hello приведенном ниже примере. Hello ключа признаком «переворачивающегося» окна, что они повторяется, не будут перекрываться и события не может принадлежать toomore, чем один «переворачивающееся» окно.

![Введение в функции "переворачивающегося" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a>"Прыгающее" окно
Функции "прыгающего" окна смещаются вперед на фиксированный отрезок времени. Он может быть легко toothink их как Переворачивающиеся окна, которые могут перекрываться, поэтому события могут принадлежать toomore более одного результирующего набора окна «прыгающие» окна. toomake окна «прыгающие» окна hello же, как «переворачивающегося» окна одно просто указать toobe размер прыжка hello Здравствуйте таким же, как размер окна hello. 

![Введение в функции "прыгающего" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a>"Скользящее" окно
Функции "скользящего" окна, в отличие от "переворачивающихся" или "прыгающих" окон, создают выходные данные **только** при наступлении определенного события. Каждое окно будет иметь по крайней мере одно событие и окно hello постоянно перемещается вперед по € (epsilon). Как «прыгающих» окнах событий могут принадлежать toomore от одного скользящего окна.

![Введение в функции "скользящего" окна в Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a>Справочные сведения по функциям окна
Дополнительную помощь и поддержку вы можете получить на нашем [форуме Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Дальнейшие действия
* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

