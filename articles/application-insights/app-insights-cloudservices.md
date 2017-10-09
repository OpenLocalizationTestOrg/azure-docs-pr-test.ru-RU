---
title: "aaaApplication аналитики для облачных служб Azure | Документы Microsoft"
description: "Эффективное отслеживание веб-ролей и рабочих ролей с помощью Application Insights"
services: application-insights
documentationcenter: 
keywords: "WAD2AI, система диагностики Azure"
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Application Insights для облачных служб Azure
С помощью [Application Insights][start] можно отслеживать [приложения облачной службы Microsoft Azure](https://azure.microsoft.com/services/cloud-services/) на предмет доступности, производительности, сбоев и использования, объединяя данные из пакета SDK Application Insights с данными [диагностики Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) из облачных служб. Отзыв hello, получаемых о hello производительность и эффективность работы приложения в hello подстановки можно сделать правильный выбор hello направления проектирования hello в каждом жизненного цикла разработки.

![Пример](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Перед началом работы
Что вам понадобится:

* Потребуется подписка [Microsoft Azure](http://azure.com). Войдите, используя учетную запись Майкрософт, которая уже может быть у вас для Windows, XBox Live или других облачных служб Майкрософт. 
* Инструменты Microsoft Azure 2.9 или более поздней версии.
* Developer Analytics Tools 7.10 или более поздней версии.

## <a name="quick-start"></a>Быстрый запуск
Здравствуйте, toomonitor быстрее и проще всего облачной службы с помощью Application Insights — toochoose, при публикации tooAzure вашей службы.

![Пример](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Этот параметр, инструменты счетчики приложения во время выполнения, что дает вам все данные телеметрии hello toomonitor запросы, исключения и зависимости в веб-роли, а также производительность из ваших рабочих ролей. Все диагностические трассировки, сгенерированный вашим приложением tooApplication аналитики также передаются.

Если это все, что вам нужно, то все готово. Следующие шаги — [просмотр метрик приложения](app-insights-metrics-explorer.md), [запрос данных с помощью Аналитики](app-insights-analytics.md), и, возможно, настройка [мониторинга](app-insights-dashboards.md). Копирование может потребоваться tooset [тестов доступности](app-insights-monitor-web-app-availability.md) и [добавлять код tooyour веб-страницы](app-insights-javascript.md) toomonitor производительности в браузере hello.

Но можно также получить дополнительные возможности:

* Отправить данные из различных компонентов и конфигураций сборки tooseparate ресурсов.
* добавить пользовательские данные телеметрии из своего приложения.

Если эти параметры имеют tooyou интерес, читайте дальше.

## <a name="sample-application-instrumented-with-application-insights"></a>Пример приложения, инструментированного с помощью Application Insights
Рассмотрим это [образец приложения](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) в котором Application Insights добавляется tooa облачной службы с двумя рабочими ролями, размещенных в Azure. 

Далее рассказывается, как tooadapt облачной службы проект hello таким же образом.

## <a name="plan-resources-and-resource-groups"></a>Планирование ресурсов и групп ресурсов
Hello телеметрии из приложения сохраняется, анализируются и отображается в ресурс Azure типа Application Insights. 

Группа ресурсов tooa принадлежит каждый ресурс. Группы ресурсов используются для управления затратами, для предоставления доступа членов tooteam и toodeploy обновления в одной транзакции скоординированного. Например, можно было бы [записи toodeploy сценария](../azure-resource-manager/resource-group-template-deploy.md) облачной службы Azure и его Application Insights, отслеживание ресурсов в одной операции.

### <a name="resources-for-components"></a>Ресурсы для компонентов
Hello рекомендуемые схема является toocreate отдельный ресурс для каждого компонента приложения — то есть каждый веб-роли и рабочей роли. Можно анализировать каждый компонент отдельно, но можно создать [мониторинга](app-insights-dashboards.md) , объединяет в себе hello основные диаграммы из всех компонентов hello, можно сравнить и отслеживать их друг с другом. 

Альтернативные схемы является toosend hello телеметрии из более чем одной роли toohello одного ресурса, но [добавьте элемент измерения tooeach свойств телеметрии](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) , определяющий его роль источника. В этой схеме метрики диаграммы, такие как исключения обычно показывают агрегат hello счетчики hello разные роли, но можно отделить hello диаграммы с идентификатором hello роли, при необходимости. Поиск также можно фильтровать по hello одно измерение. Этот вариант делает его более удобным tooview все в hello же времени, но может также привести toosome путаницы между ролями hello.

Браузер телеметрии обычно включаются в hello того же ресурса в качестве его серверные веб-роли.

Поместите ресурсы Application Insights hello для различных компонентов hello в одну группу ресурсов. Это позволяет легко toomanage их вместе. 

### <a name="separating-development-test-and-production"></a>Разделение данных для разработки, тестирования и эксплуатации
При разработке пользовательских событий для следующего компонента при динамической hello предыдущей версии, необходимо toosend hello разработки телеметрии tooa отдельный ресурс Application Insights. В противном случае он будет жестких toofind телеметрии тестирования среди всех hello трафик от hello действующем сайте.

tooavoid этой ситуации создать отдельные ресурсы для каждой конфигурации сборки или «метка» (разработки, тестирования, производства,...) системы. Поместите hello ресурсы для каждой конфигурации сборки в отдельной группе ресурсов. 

toosend hello телеметрии toohello соответствующие ресурсы, можно выполнить настройку hello пакет SDK Application Insights, чтобы он собирает ключ инструментирования разные в зависимости от конфигурации построения hello. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Создание ресурса Application Insights для каждой роли
Если вы решили toocreate отдельный ресурс для каждой роли - и возможно отдельный набор для каждой конфигурации сборки -, то он является простым toocreate их на портале Application Insights hello. (Если гораздо создания ресурсов можно [автоматизации процесса hello](app-insights-powershell.md).

1. В hello [портал Azure][portal], создать новый ресурс Application Insights. Для параметра типа приложения выберите приложение ASP.NET. 

    ![Нажмите "Создать" и "Application Insights"](./media/app-insights-cloudservices/01-new.png)
2. Обратите внимание, что каждый ресурс идентифицируется с помощью ключа инструментирования. Возможно потребуется позже при необходимости toomanually настройте или проверьте конфигурацию hello hello SDK.

    ![Щелкните свойства, выберите раздел hello и нажмите клавиши ctrl + C](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Настройка системы диагностики Azure для каждой роли
Задайте этот параметр toomonitor приложения с помощью Application Insights. Для веб-ролей это обеспечивает мониторинг производительности, создание оповещений и диагностику, а также анализ сведений об использовании. Для других ролей можно найти и отслеживать диагностики Azure, такие как перезапуск, счетчики производительности и tooSystem.Diagnostics.Trace вызовы. 

1. В обозревателе решений Visual Studio в разделе &lt;YourCloudService&gt;, роли, откройте свойства каждой роли hello.
2. В **конфигурации**, задайте **отправка данных диагностики tooApplication аналитики** и выберите hello соответствующего ресурса Application Insights, созданного ранее.

Если вы решили toouse отдельный ресурс Application Insights для каждой конфигурации сборки, сначала выберите конфигурацию hello.

![В окне приветствия свойства каждой роли Azure Настройка Application Insights](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Действует hello вставки ключи инструментирования Application Insights в hello файлы с именем `ServiceConfiguration.*.cscfg`. ([Пример кода](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Следует toovary уровень hello диагностические сведения, передаваемые tooApplication аналитики это можно сделать [путем редактирования hello `.cscfg` непосредственно файлы](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Установка пакета SDK для hello в каждом проекте
Этот параметр добавляет hello возможность tooadd пользовательские бизнес-телеметрии tooany роли, для более тщательного анализа того, как используется приложение и выполняет.

В Visual Studio настройте hello пакет SDK Application Insights для каждого проекта облачных приложений.

1. **Веб-ролей**: щелкните правой кнопкой мыши проект hello и выберите **настроить Application Insights** или **Добавить > телеметрии Application Insights**.

2. **Рабочие роли**: 
 * Щелкните правой кнопкой мыши проект hello и выберите **управление пакетами Nuget**.
 * Добавьте [Application Insights для Windows Servers](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/).

    ![Поиск Application Insights](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Настройка данных toosend toohello ресурс Application Insights для hello SDK.

    В функцию запуска подходящий задайте ключ инструментирования hello в параметр конфигурации hello в cscfg-файле hello:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Сделайте это для каждой роли в вашем приложении. См. Примеры hello.
   
   * [Веб-роль](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Рабочая роль](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [При работе с веб-страницами](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Toobe файл ApplicationInsights.config hello набор всегда копируются toohello выходной каталог. 
   
    (В файле .config hello, вы увидите попросить вас tooplace hello ключ инструментирования существует сообщения. Однако для облачных приложений это лучше tooset его из hello cscfg-файле. Это гарантирует, что эта роль hello правильно задан в портал hello.)

#### <a name="run-and-publish-hello-app"></a>Запустить и опубликовать приложение hello
Запустите приложение и войдите в Azure. Создать ресурсы Application Insights Привет открыть, и вы увидите отдельных точек данных в [поиска](app-insights-diagnostic-search.md), и статистические данные в [Explorer метрика](app-insights-metrics-explorer.md). 

Добавьте дополнительные телеметрии - разделах hello ниже - и опубликуйте приложение tooget динамической диагностике и использовании отзыв. 

#### <a name="no-data"></a>Данные отсутствуют?
* Откройте hello [поиска] [ diagnostic] плитки toosee отдельные события.
* С помощью приложения hello, открыв разные страницы, чтобы он создает некоторые телеметрии.
* Подождите несколько секунд и нажмите "Обновить".
* Ознакомьтесь с разделом [Устранение неполадок][qna].

## <a name="view-azure-diagnostic-events"></a>Просмотр событий диагностики Azure
Где toofind hello [диагностики Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) данные в Application Insights:

* Счетчики производительности отображаются в виде настраиваемых метрик. 
* Журналы событий Windows отображаются в виде трассировок и настраиваемых событий.
* Журналы приложений, журналы трассировки событий Windows и все журналы инфраструктуры диагностики отображаются в виде трассировок.

toosee счетчики производительности и счетчики событий, откройте [обозревателя метрик](app-insights-metrics-explorer.md) и добавить новую диаграмму:

![Диагностические данные Azure](./media/app-insights-cloudservices/23-wad.png)

Используйте [поиска](app-insights-diagnostic-search.md) или [аналитический запрос](app-insights-analytics-tour.md) toosearch через hello, различными трассировки журналов, отправляемых системой диагностики Azure. Например предположим, что у вас есть необрабатываемое исключение, вызвавшее toocrash роли и повторный запуск. Эти сведения будут отображаться в hello приложения канал журнала событий Windows. Можно использовать toolook поиска на ошибки в журнале событий Windows hello и получить hello полную трассировку стека для исключения hello. Помогут вам найти hello причину проблемы hello.

![Поиск диагностических данных Azure](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Дополнительные данные телеметрии
Здравствуйте, разделы ниже показано как tooget дополнительные данные телеметрии из различных аспектов приложения.

## <a name="track-requests-from-worker-roles"></a>Отслеживание запросов из рабочих ролей
В веб-роли модуля hello запросов автоматически собирает данные о HTTP-запросов. В разделе hello [пример MVCWebRole](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) примеры как можно переопределить поведение коллекции по умолчанию hello. 

Можно записать производительности hello вызовов tooworker ролей путем их отслеживания в hello так же, как HTTP-запросов. В Application Insights тип телеметрии запроса hello измеряет единицы именованный серверные работы, которая была ограничена по времени и могут независимо друг от друга завершаются успехом или сбоем. Во время HTTP-запросы автоматически фиксируются по hello SDK, вы можете вставить свои собственные роли tooworker запросов tootrack кода.

В разделе hello два образца рабочих ролей инструментированного tooreport запросов: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) и [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Исключения
Способы сбора необработанных исключений, выдаваемых веб-приложениями разных типов, см. в статье [Настройка Application Insights: диагностика исключений](app-insights-asp-net-exceptions.md).

веб-роль Образец Hello имеет MVC5 и веб-API 2 устройства. Hello необработанные исключения из двух hello регистрируются с hello следующие обработчики.

* объектом [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs), заданным [здесь](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) для контроллеров MVC5;
* объектом [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs), заданным [здесь](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) для контроллеров веб-API 2.

Для рабочих ролей существует два способа tootrack исключения:

* TrackException(ex);
* При добавлении пакета NuGet прослушивателя трассировки Application Insights hello, можно использовать **System.Diagnostics.Trace** toolog исключения. [Пример кода](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Счетчики производительности
по умолчанию собираются Hello следующие счетчики:

    * \Process(??APP_WIN32_PROC??)\% Загруженность процессора
    * \Память\доступные байты
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# Исключений в секунду
    * \Process(??APP_WIN32_PROC??)\Байт исключительного пользования
    * \Process(??APP_WIN32_PROC??)\I/O — обмен данными, байт в секунду
    * \Processor(_Total)\% Загруженность процессора

Эти счетчики также собираются для веб-ролей.

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Запросов в секунду
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Время выполнения запросов
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Запросы в очереди приложений

Можно указать дополнительные пользовательские или другие счетчики производительности Windows, изменив файл ApplicationInsights.config, [как показано в этом примере](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Счетчики производительности](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Коррелированная телеметрия для рабочих ролей
Это богатые возможности диагностики, можно увидеть, какие индикаторы tooa сбой или высокой задержкой запроса. С веб-ролей приветствия SDK автоматически настраивает корреляции между сопутствующей телеметрии. Для рабочих ролей tooset инициализатора пользовательского телеметрии общий атрибут контекста Operation.Id можно использовать для всех tooachieve телеметрии hello это. Это позволяет вам toosee проблему задержки и сбоев hello, вызываемые из-за зависимостей tooa или код, с первого взгляда! 

Этот процесс описывается далее.

* Задайте идентификатор корреляции hello в CallContext, как показано [здесь](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). В этом случае мы используем hello ИД запроса как идентификатор корреляции hello
* Добавление пользовательской реализации TelemetryInitializer, tooset hello Operation.Id toohello correlationId больше. Пример: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13).
* Добавьте инициализатор пользовательского телеметрии hello. Это можно сделать в файле ApplicationInsights.config hello, или в коде следующим [здесь](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

Вот и все! взаимодействие с порталом Hello уже подключено toohelp позволяет просматривать все связанные данные телеметрии с одного взгляда:

![Коррелированные данные телеметрии](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Данные телеметрии клиента
[Добавить hello JavaScript SDK tooyour веб-страницы] [ client] tooget на основе браузера телеметрии, например число просмотров страниц, время загрузки страницы, исключений в скриптах и toolet записи настраиваемой телеметрии в скриптах страницы.

## <a name="availability-tests"></a>Тесты доступности
[Настройка веб-тестов] [ availability] toomake убедиться, что приложение остается динамической и отвечать на запросы.

## <a name="display-everything-together"></a>Отображение всей информации вместе
tooget общее представление о системе, можно использовать ключ hello диаграммы мониторинга вместе на одном [мониторинга](app-insights-dashboards.md). Например можно закрепить запрос hello и неудачных установок для каждой роли. 

Если в системе используются другие службы Azure, такие как Stream Analytics, добавьте и их диаграммы мониторинга. 

Если у вас есть мобильные клиентские приложения, некоторые коды toosend пользовательских событий ключа пользовательские операции вставки и создать [HockeyApp моста](app-insights-hockeyapp-bridge-app.md). Создание запросов в [Analytics](app-insights-analytics.md) toodisplay hello счетчиков событий и закреплять их toohello панели мониторинга.

## <a name="example"></a>Пример
[пример Hello](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) отслеживает службу с веб-роли и два рабочих ролей.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Исключение "метод не найден" при выполнении в облачных службах Azure
Выполняется сборка для .NET 4.6? Версия 4.6 не поддерживается автоматически в ролях облачных служб Azure. [установите версию 4.6 в каждой роли](../cloud-services/cloud-services-dotnet-install-dotnet.md) .

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Дальнейшие действия
* [Настройка отправки аналитики tooApplication диагностики Azure](app-insights-azure-diagnostics.md)
* [Автоматизация создания ресурсов Application Insights](app-insights-powershell.md)
* [Автоматизация системы диагностики Azure](app-insights-powershell-azure-diagnostics.md)
* [Функции Azure](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
