---
title: "aaaApplication аналитики телеметрии в Visual Studio CodeLens | Документы Microsoft"
description: "Быстро получайте доступ к телеметрии запросов и исключений Application Insights с помощью CodeLens в Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Телеметрия Application Insights в Visual Studio CodeLens
Методы в коде hello веб-приложения могут сопровождаться телеметрии об исключениях во время выполнения и запросить времени ответа. При установке [Azure Application Insights](app-insights-overview.md) в приложении, в Visual Studio появляется телеметрии hello [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello заметки hello верхней части каждой функции, в которых она используется полезные tooseeing сведения, например номер hello функции hello местах упоминается или hello последнего пользователя, его изменения.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights в CodeLens доступен в Visual Studio 2015 с обновлением 3 и более поздней версии или с hello последнюю версию [средства анализа для разработчиков расширение](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). Средство CodeLens доступно в выпусках Enterprise hello и профессиональные выпуски Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Где toofind данные Application Insights
Поиск телеметрии Application Insights в индикаторы CodeLens hello hello открытый запрос методов веб-приложения. Индикаторы CodeLens отображаются над объявлениями метода и другими объявлениями в коде C# и Visual Basic. При наличии данных Application Insights для метода вы увидите индикаторы запросов и исключений, например "Запросов: 100, не выполнено: 1 %" или "Исключений: 10". Для получения дополнительных сведений щелкните индикатор CodeLens. 

> [!TIP]
> Запрос Application Insights и индикаторы исключение может занять несколько секунд дополнительных tooload после появления другие индикаторы CodeLens.
> 
> 

## <a name="exceptions-in-codelens"></a>Исключения в CodeLens
![ПОДЛЕЖИТ УТОЧНЕНИЮ](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

индикатор CodeLens исключение Hello отображает hello число исключений, произошедших в hello за последние 24 часа из hello 15 большинства часто встречающееся исключений в приложении в этот период, во время обработки запроса hello обслуживаемых метод hello.

toosee более подробные сведения, щелкните индикатор CodeLens hello исключения:

* Процент Hello, изменения в число исключений из hello последние 24 часа относительный toohello предыдущие 24 часа
* Выберите **Go toocode** toonavigate toohello исходный код функции hello исключения hello
* Выберите **поиска** tooquery Здравствуйте, все экземпляры данного исключения, которые произошли в последние 24 часа.
* Выберите **тренда** tooview визуализации тренда вхождений данного исключения в hello за последние 24 часа
* Выберите **просмотреть все исключения в этом приложении** tooquery Здравствуйте, все исключения, которые произошли за последние 24 часа
* Выберите **исследовать тенденции исключение** tooview визуализации тренда для всех исключений, которые произошли в hello за последние 24 часа. 

> [!TIP]
> Вы видите «0 исключений» в CodeLens, но известно, что должно быть исключения, проверьте toomake отметку hello ресурса Application Insights в CodeLens. tooselect другой ресурс, щелкните правой кнопкой мыши проект в обозревателе решений hello и выберите **Application Insights > Выбор источника данных телеметрии**. CodeLens доступен только для hello 15 большинства часто встречающееся исключений в приложении в hello за последние 24 часа, таким образом, если исключение является hello шестнадцатый наиболее часто или даже меньше, вы увидите «0» исключения. Исключения из представления ASP.NET могут не отображаться в методах контроллера hello, созданные эти представления.
> 
> [!TIP]
> Если в CodeLens отображается индикатор "Исключений: ?", исключения» в CodeLens, необходимо tooassociate, истек срок действия учетной записи Azure вместе с Visual Studio или учетные данные учетной записи Azure. В любом случае щелкните индикатор "Исключений: ?" исключения» и выберите **добавить учетную запись...**  tooenter учетные данные.
> 
> 

## <a name="requests-in-codelens"></a>Запросы в CodeLens
![ПОДЛЕЖИТ УТОЧНЕНИЮ](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Hello запроса CodeLens отображается индикатор hello число HTTP-запросы, был обслужен методом в hello за 24 часа, а также процент hello эти запросы, которые не удалось.

toosee сведения, щелкните индикатор CodeLens запрашивает hello:

* Здравствуйте, абсолютное и процентное изменение номера запросов, неудачных запросов и среднее время ответа через hello за 24 часа по сравнению toohello предыдущие 24 часа
* надежность Hello метода hello, вычисляется как процент hello запросов, не нарушает в hello за последние 24 часа
* Выберите **поиска** для запросов или tooquery невыполненных запросов, все hello (сбой) запросы, произошедших в hello за последние 24 часа
* Выберите **тренда** tooview визуализации тренда для запросов, запросов с ошибками или среднего времени в hello за последние 24 часа.
* Выберите имя hello hello ресурс Application Insights в верхний левый угол hello hello CodeLens сведения о представлении toochange ресурса, который является источником данных элемента CodeLens hello.

## <a name="next"></a>Дальнейшие действия
|  |  |
| --- | --- |
| **[Работа с Application Insights в Visual Studio](app-insights-visual-studio.md)**<br/>Поиск телеметрии, просмотр данных в CodeLens и настройка Application Insights — все это в Visual Studio |![Щелкните правой кнопкой мыши проект hello и выберите идеи приложения поиска](./media/app-insights-visual-studio-codelens/34.png) |
| **[Добавление данных](app-insights-asp-net-more.md)**<br/>Мониторинг использования, доступности, зависимостей и исключений. Интеграция трассировок из платформ ведения журналов. Написание пользовательской телеметрии. |![Visual studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Работа с порталом Application Insights hello](app-insights-dashboards.md)**<br/>Панели мониторинга, эффективные средства диагностики и анализа, оповещения, карта динамических зависимостей приложения, а также экспорт данных телеметрии. |![Visual studio](./media/app-insights-visual-studio-codelens/62.png) |

