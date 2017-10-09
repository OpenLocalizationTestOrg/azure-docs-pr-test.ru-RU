---
title: "aaaMonitor производительности Azure веб-приложения | Документы Microsoft"
description: "Мониторинг производительности веб-приложений Azure. Диаграммы времени загрузки и ответа, информация о зависимостях и настройка оповещений о производительности."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Мониторинг производительности веб-приложения Azure
В hello [портала Azure](https://portal.azure.com) можно настроить наблюдение за производительностью приложений вашей [веб-приложениях Azure](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) инструментирует toosend данные телеметрии вашего приложения о toohello его действия служба Application Insights, где он хранится и проанализированы. Нет, можно использовать диаграммы метрик и средства поиска toohelp диагностики проблем, повышения производительности и оценить использование.

## <a name="run-time-or-build-time"></a>Инструментирование во время выполнения и во время сборки
Вы можете настроить отслеживание посредством инструментирования приложение hello одним из двух способов:

* **Во время выполнения.** Вы можете добавить расширение для мониторинга производительности уже во время работы вашего веб-приложения. Он не требуется toorebuild или переустановите приложение. Вы получаете стандартный набор пакетов для отслеживания времени отклика, частоты успешных выполнений, исключений, зависимостей и т. д. 
* **Во время сборки.** Вы можете добавить пакет в код своего приложения на этапе разработки. Этот способ является более гибким решением. В дополнение toohello же стандартных пакетов, можно написать код toocustomize hello телеметрии или toosend собственные телеметрии. Войти в определенных действий или запись событий в соответствии с семантикой toohello домена приложения. 

## <a name="run-time-instrumentation-with-application-insights"></a>Инструментирование во время выполнения с помощью Application Insights
Если вы уже используете веб-приложения в Azure, то наверняка получили определенные сведения мониторинга, касающиеся частоты запросов и ошибок. Добавьте дополнительные, например время отклика, мониторинга toodependencies вызовы, смарт-обнаружение и hello мощный язык запросов анализа журналов tooget Application Insights. 

1. **Выберите Application Insights** панели hello Azure управления для веб-приложения.
   
    ![В разделе "Мониторинг" выберите пункт Application Insights](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Выберите toocreate новый ресурс, если вы уже настроенных ресурс Application Insights для этого приложения другой маршрут.
2. **Выполните инструментирование веб-приложения** после установки Application Insights. 
   
    ![Инструментирование веб-приложения](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   **Включите мониторинг на стороне клиента** для получения сведений о просмотрах страниц и данных телеметрии пользователя.

   * Выберите элементы "Параметры > Параметры приложения".
   * В разделе "Параметры приложения" добавьте новую пару "ключ — значение": 
   
    Ключ: `APPINSIGHTS_JAVASCRIPT_ENABLED`. 
    
    Значение: `true`
   * **Сохранить** hello параметры и **перезапустите** приложения.
3. **Отслеживайте работу приложения**.  [Данные hello Expore](#explore-the-data).

Более поздней версии Если требуется, можно построить приложение hello с помощью Application Insights.

*Как удалить Application Insights, или переключиться toosending tooanother ресурсов?*

* В колонке управления Привет открыть web приложения Azure и средств разработки откройте **расширения**. Удалите расширение Application Insights hello. Затем в разделе наблюдения, выберите Application Insights и создайте или выберите ресурс hello.

## <a name="build-hello-app-with-application-insights"></a>Создать приложение hello с Application Insights
Установите пакет SDK в свое приложение, чтобы воспользоваться более подробными сведениями телеметрии Application Insights. В частности, можно собирать журналы трассировки, [написать код пользовательской телеметрии](app-insights-api-custom-events-metrics.md) и получать более подробные отчеты об исключениях.

1. **В Visual Studio** (2013 года с обновлением 2 или более поздней версии) настройте Application Insights для проекта.

    Щелкните правой кнопкой мыши hello веб-проекта и выберите **Добавить > Application Insights** или **настроить Application Insights**.
   
    ![Щелкните правой кнопкой мыши hello веб-проекта и нажмите кнопку Добавить или настроить Application Insights](./media/app-insights-azure-web-apps/03-add.png)
   
    В ответ на вопрос toosign в, используйте hello учетные данные для учетной записи Azure.
   
    Операция Hello оказывает влияние на два.
   
   1. Создает ресурс Application Insights, в котором выполняется отображение, хранение и анализ данных телеметрии.
   2. Добавляет hello NuGet аналитики приложений tooyour кода пакета (если она еще не существует) и настраивает его toohello телеметрии toosend ресурсов Azure.
2. **Тестирование телеметрии hello** , выполняемого приложения hello в компьютере разработки (F5).
3. **Публикация приложения hello** tooAzure в hello обычным способом. 

*Как переключаться toosending tooa другого ресурса Application Insights?*

* В Visual Studio, щелкните правой кнопкой мыши проект hello, выберите **настроить Application Insights** и выберите ресурс hello. Параметр toocreate hello получить новый ресурс. заново собрать или повторно развернуть ресурс.

## <a name="explore-hello-data"></a>Просмотр данных hello
1. В колонке hello Application Insights для вашего веб-приложения управления панели отображается Live метрик, которые показывает запросов и ошибок в секунду или две из них происходит. Эти отображаемые данные очень полезны в случае повторной публикации приложения, так как любые проблемы можно увидеть немедленно.
2. Пролистайте toohello полный ресурс Application Insights.

    ![Щелкните](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    Вы также можете перейти непосредственно по ссылке из ресурсов навигации Azure.

1. Пролистайте любой диаграммы tooget более подробно:
   
    ![В колонке Обзор hello Application Insights щелкните диаграмму](./media/app-insights-azure-web-apps/07-dependency.png)
   
    Вы можете [настроить колонки метрик](app-insights-metrics-explorer.md).
2. Переходите дальнейшей toosee отдельные события и их свойств.
   
    ![Нажмите кнопку tooopen тип события, поиска, отфильтрованные по этому типу](./media/app-insights-azure-web-apps/08-requests.png)
   
    Обратите внимание, «...» Здравствуйте, tooopen ссылку все свойства.
   
    Вы можете [настроить поисковые запросы](app-insights-diagnostic-search.md).

Для расширенного поиска по телеметрии использовать hello [языка запросов анализа журналов](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Дополнительные данные телеметрии

* [Данные о загрузке веб-страницы](app-insights-javascript.md)
* [Пользовательская телеметрия](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Дальнейшие действия
* [Запустите профилировщик hello в работающем приложении](app-insights-profiler.md).
* [Функции Azure.](https://github.com/christopheranderson/azure-functions-app-insights-sample) Отслеживайте функции Azure с помощью Application Insights.
* [Включение диагностики Azure](app-insights-azure-diagnostics.md) tooApplication toobe отправлено аналитики.
* [Отслеживать показатели работоспособности службы](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
* [Получайте уведомления](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) при возникновении операционных событий или превышении пороговых значений метрик.
* Используйте [Application Insights для приложений JavaScript и веб-страницы](app-insights-javascript.md) tooget телеметрии клиента с помощью браузеров hello, посетите веб-страницу.
* [Настройка доступности веб-тесты](app-insights-monitor-web-app-availability.md) toobe оповещение, если сайт не работает.

