---
title: "приложения aaaMonitor Docker в Azure Application Insights | Документы Microsoft"
description: "Docker счетчики производительности, событий и исключений могут отображаться на Application Insights вместе с hello телеметрии из hello контейнерных приложений."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Мониторинг приложений Docker в Application Insights
События жизненного цикла и счетчики производительности из контейнеров [Docker](https://www.docker.com/) можно выводить в виде диаграмм в Application Insights. Установка hello [Application Insights](app-insights-overview.md) образ контейнера в узле, который отображает счетчики производительности для узла hello, как хорошо как для hello других изображений.

С помощью Docker ваши приложения распространяются в упрощенных контейнерах со всеми зависимостями. Их можно запустить на любом хост-компьютере с модулем Docker.

При запуске hello [Application Insights изображение](https://hub.docker.com/r/microsoft/applicationinsights/) на узле Docker, вы получаете следующие преимущества:

* Жизненный цикл данных телеметрии о всех запущенных контейнеров hello на узле hello - запуск, остановку и т. д.
* Счетчики производительности для всех контейнеров hello. ЦП, память, использование сети и многое другое.
* Если вы [установлен пакет SDK Application Insights для Java](app-insights-java-live.md) в hello приложений, выполняющихся в контейнерах hello, все данные телеметрии hello этих приложений будут иметь дополнительные свойства, идентифицирующий контейнера hello и хост-компьютера. Например, если имеются экземпляры приложения, запущенные на нескольких узлах, вы легко сможете отфильтровать данные телеметрии приложения по узлу.

![пример](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Настройка ресурса Application Insights
1. Вход в [портал Microsoft Azure](https://azure.com) и открыть ресурс Application Insights hello для вашего приложения; или [создайте новую](app-insights-create-new-resource.md). 
   
    *Какой ресурс использовать?* Если были разработаны hello приложений, работающих на узле другим пользователем, то нужно слишком[создать новый ресурс Application Insights](app-insights-create-new-resource.md). Это, где Просмотр и анализ телеметрии hello. (Выберите «Общие» для типа приложения hello).
   
    Но если вы разработчик приложения hello hello, затем мы надеемся, что вы [добавить пакет SDK Application Insights](app-insights-java-live.md) tooeach из них. Если они все компоненты действительно одной бизнес-приложения, то можно настроить все из них toosend телеметрии tooone ресурсов, и будет использовать те же самые ресурсов toodisplay hello Docker жизненный цикл и производительности данные. 
   
    Третий сценарий, разработанных большинство приложений hello, что вы используете отдельные ресурсы toodisplay их телеметрии. В этом случае вы, вероятно, также требуется toocreate отдельный ресурс для hello данных Docker. 
2. Добавить плитку Docker hello: выберите **добавить плитку**, перетащите hello Docker плитки из галереи hello и нажмите кнопку **сделать**. 
   
    ![пример](./media/app-insights-docker/03.png)
3. Нажмите кнопку hello **Essentials** раскрывающийся список и скопируйте ключ инструментирования hello. Используйте этот tootell hello SDK где toosend его телеметрии.

    ![пример](./media/app-insights-docker/02-props.png)

Оставьте это окно браузера под рукой, как вы сможете вернуться tooit скоро toolook в телеметрии.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Запустить монитор hello Application Insights на узле
Теперь, когда у вас есть где-нибудь toodisplay hello телеметрии, можно настроить приложение hello контейнерах, который будет собирать и отправлять их.

1. Подключите узел Docker tooyour. 
2. Включите свой ключ инструментирования в следующую команду и выполните ее:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Для каждого узла Docker требуется только один образ Application Insights. Если приложение развертывается на нескольких узлах Docker, затем повторите команду hello на каждом узле.

## <a name="update-your-app"></a>Обновление приложения
Если приложение инструментируется hello [пакет SDK Application Insights для Java](app-insights-java-get-started.md), добавить следующие строки в файл ApplicationInsights.xml hello в вашем проекте, в списке hello hello `<TelemetryInitializers>` элемента:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Это добавляет сведения о Docker, например контейнером и узлом идентификатор tooevery телеметрии item отправляемых из приложения.

## <a name="view-your-telemetry"></a>Просмотр телеметрии
Вы можете вернуться tooyour ресурс Application Insights в hello портал Azure.

Пролистайте hello Docker плитки.

Скоро появится данных, поступающих из приложения hello Docker, особенно в том случае, если у вас есть другие контейнеры, работающих на ваш подсистемы Docker.

Ниже приведены некоторые hello представления, которые можно получить.

### <a name="perf-counters-by-host-activity-by-image"></a>Счетчики производительности узла, активность образа
![пример](./media/app-insights-docker/10.png)

![пример](./media/app-insights-docker/11.png)

Щелкните имя любого узла или образа, чтобы получить подробные данные.

представление toocustomize hello, щелкните любой диаграммы, заголовок сетки hello, или добавить диаграмму следует использовать. 

[Ознакомьтесь с дополнительными сведениями об обозревателе метрик](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>События контейнера Docker
![пример](./media/app-insights-docker/13.png)

tooinvestigate отдельные события, щелкните [поиска](app-insights-diagnostic-search.md). Поиск и фильтрация событий toofind hello. Выберите любое событие tooget более подробно.

### <a name="exceptions-by-container-name"></a>Исключения по имени контейнера
![пример](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Docker контекст добавлен tooapp телеметрии
Запрос телеметрии передается из приложения hello встроены AI SDK, также Docker контекста:

![пример](./media/app-insights-docker/16.png)

Счетчики производительности для загруженности процессора и доступной памяти, насыщенные, дополненные и сгруппированные по имени контейнера Docker:

![пример](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Вопросы и ответы
*Какие возможности Application Insights отсутствуют в Docker?*

* Подробные показатели счетчиков производительности по контейнерам и образам.
* Интегрированные данные контейнера и приложения на одной панели мониторинга.
* [Экспортировать данные телеметрии](app-insights-export-telemetry.md) для дальнейшего анализа tooa базы данных Power BI или другие панели мониторинга.

*Получение телеметрии из самого приложения hello*

* Установите пакет SDK Application Insights hello в приложение hello. Узнайте, как это сделать в [веб-приложениях Java](app-insights-java-get-started.md) и [Windows](app-insights-asp-net.md).

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Дальнейшие действия

* [Application Insights для Java](app-insights-java-get-started.md)
* [Application Insights для Node.js](app-insights-nodejs.md)
* [Application Insights для ASP.NET](app-insights-asp-net.md)
