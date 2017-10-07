---
title: "aaaDebug приложений с Azure Application Insights в Visual Studio | Документы Microsoft"
description: "Анализ производительности веб-приложения и диагностика во время отладки и в рабочей среде."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Отладка приложений с помощью Azure Application Insights в Visual Studio
В Visual Studio 2015 и более поздних версиях можно анализировать производительность веб-приложения ASP.NET и диагностировать проблемы во время отладки и в рабочей среде с помощью телеметрии из [Azure Application Insights](app-insights-overview.md).

Если вы создали веб-приложения ASP.NET с помощью Visual Studio 2017 г. или более поздней версии, уже имеет hello пакет SDK Application Insights. В противном случае, если вы еще не сделали этого, [добавить Application Insights tooyour приложение](app-insights-asp-net.md).

toomonitor приложения, когда он находится в производственной, обычно просмотре телеметрии Application Insights hello в hello [портал Azure](https://portal.azure.com), где можно настроить оповещения и применить высокоэффективных средств мониторинга. Однако для отладки, можно также выполнить поиск и анализ телеметрии hello в Visual Studio. Можно использовать Visual Studio tooanalyze телеметрии из производственного сайта и отладка выполняется на компьютере разработки. В последнем случае hello даже если вы еще не настроили hello SDK toosend телеметрии toohello портал Azure можно анализировать отладки запусков. 

## <a name="run"></a> Отладка проекта
Нажмите клавишу F5, чтобы запустить веб-приложение в режиме локальной отладки. Откройте некоторые телеметрии toogenerate разным страницам.

В Visual Studio отображается количество hello событий, зарегистрированных модулем hello Application Insights в проект.

![В Visual Studio hello Application Insights кнопка показывает во время отладки.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Щелкните этот toosearch кнопку телеметрии. 

## <a name="application-insights-search"></a>Поиск Application Insights
в окне поиска Application Insights Hello отображаются события, которые были записаны. (Если вы вошли в tooAzure при настройке Application Insights, можно выполнить поиск hello того же события в hello портал Azure.)

![Щелкните правой кнопкой мыши проект hello и выберите идеи приложения поиска](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> После выбора или отмените выбор фильтров, нажмите кнопку поиска hello в конце hello hello текстовое поле поиска.
>

Hello свободного полнотекстовый поиск работает на все поля в событиях hello. Например поиск по части hello URL-адрес страницы; или hello значение свойства, такие как город клиентов; или ключевых слов в журнале трассировки.

Выберите любое событие toosee его подробные свойства.

Для запросов tooyour веб-приложения можно щелкнуть toohello кода.

![В области сведений о запросе нажмите кнопку toohello кода](./media/app-insights-visual-studio/31.png)

Можно также открыть связанные элементы toohelp диагностики запросов с ошибками или исключения.

![В области сведений о запросе прокрутите вниз элементы toorelated](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Просмотр исключений и неудачно завершенных запросов
Показать отчеты исключения в окне поиска hello. (В некоторых старых типов приложения ASP.NET, у вас есть слишком[настроить отслеживание исключений](app-insights-asp-net-exceptions.md) toosee исключений, которые обрабатываются средой hello.)

Щелкните исключение tooget трассировку стека. Если код hello приложение hello открыт в Visual Studio, можно щелкнуть через из hello трассировки стека toohello соответствующей строки кода hello.

![Трассировка стека исключений](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Просмотреть сводные данные о запросе и исключение в коде hello
В hello Code Lens строку выше каждого метода обработчика отображается число запросов hello и исключений, регистрируемых Application Insights в hello за последние 24 часа.

![Трассировка стека исключений](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Code Lens показывает только данные Application Insights, если у вас есть [настроены на портале Application Insights toosend телеметрии приложения toohello](app-insights-asp-net.md).
>

[Телеметрия Application Insights в Visual Studio CodeLens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Тренды
Тренды — это средство для визуализации того, как изменяется поведение приложения со временем. 

Выберите **исследовать тенденции телеметрии** из окна поиска Application Insights или кнопки панели инструментов hello Application Insights. Выберите один из пяти общие запросы tooget работы. Анализировать разные наборы данных можно на основе типов данных телеметрии, диапазонов времени и других свойств. 

toofind аномалий в данных, выберите один из вариантов аномалий hello в раскрывающемся списке «Тип представления» hello. параметры фильтрации Hello hello нижней части окна hello позволяют легко toohone в на определенные подмножества телеметрии.

![Тренды](./media/app-insights-visual-studio/51.png)

[Дополнительные сведения о тенденциях](app-insights-visual-studio-trends.md)

## <a name="local-monitoring"></a>Локальный мониторинг
(Из Visual Studio 2015 с обновлением 2) Если вы не еще настроили hello SDK toosend телеметрии toohello портале Application Insights (что в файле ApplicationInsights.config отсутствует ключ инструментирования) окно диагностики hello отображает телеметрии из сеанса последние отладки. 

Это предпочтительно, если вы уже опубликовали предыдущую версию своего приложения. Вы не хотите hello телеметрии из вашего отладки toobe сеансы смешивать hello телеметрии на hello портале Application Insights из опубликованного приложения hello.

Также полезно при наличии некоторые [пользовательского телеметрии](app-insights-api-custom-events-metrics.md) требуется toodebug перед отправкой телеметрии toohello портала.

* *Сначала я настроил полностью портале toohello телеметрии Application Insights toosend. Но сейчас я хочу телеметрии hello toosee только в Visual Studio.*
  
  * В параметрах окна поиска hello нет диагностики локальный параметр toosearch даже если приложение отправляет данные телеметрии toohello портала.
  * toostop телеметрии, отправляемых toohello портала, закомментируйте строку hello `<instrumentationkey>...` из ApplicationInsights.config. Когда вы будете готовы toosend телеметрии toohello портала раскомментируйте ее.


## <a name="next-steps"></a>Дальнейшие действия
|  |  |
| --- | --- |
| **[Добавление данных](app-insights-asp-net-more.md)**<br/>Мониторинг использования, доступности, зависимостей и исключений. Интеграция трассировок из платформ ведения журналов. Написание пользовательской телеметрии. |![Visual studio](./media/app-insights-visual-studio/64.png) |
| **[Работа с порталом Application Insights hello](app-insights-dashboards.md)**<br/>Просмотр панелей мониторинга, эффективных средств диагностики и анализа, оповещений, карты динамических зависимостей приложения, а также экспортированных данных телеметрии. |![Visual studio](./media/app-insights-visual-studio/62.png) |

