---
title: "aaaMonitor динамической ASP.NET веб-приложения с помощью Azure Application Insights | Документы Microsoft"
description: "Мониторинг производительности веб-сайта без необходимости его повторного развертывания. Работает с веб-приложениями ASP.NET, размещенными локально, на виртуальных машинах или в Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Инструментирование веб-приложений во время выполнения с помощью Application Insights


Можно инструментировать динамической веб-приложения с помощью Azure Application Insights, без необходимости toomodify или повторного развертывания вашего кода. Если приложения размещаются на локальном сервере IIS, необходимо установить монитор состояний. Случае веб-приложениях Azure или запустить на виртуальной Машине Azure, вы можете включить мониторинг Application Insights с помощью панели управления Azure hello. (См. статьи об инструментировании [динамических веб-приложений J2EE](app-insights-java-live.md) и [облачных служб Azure](app-insights-cloudservices.md).) Вам потребуется подписка [Microsoft Azure](http://azure.com) .

![примеры диаграмм](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Имеется выбор из трех маршруты tooapply Application Insights tooyour веб-приложений .NET:

* **Время сборки:** [hello добавить пакет SDK Application Insights] [ greenbrown] tooyour кода веб-приложения.
* **Время выполнения:** инструментирования веб-приложения на сервере hello, как описано ниже, без повторное создание и развертывание кода hello.
* **Both:** сборка hello SDK в код веб-приложения и также применить hello расширения во время выполнения. Получение hello наиболее обоих вариантов.

Ниже представлено общее сравнение предлагаемых вариантов.

|  | Во время сборки | Во время выполнения |
| --- | --- | --- |
| Запросы и исключения |Да |Да |
| [Более подробные исключения](app-insights-asp-net-exceptions.md) | |Да |
| [Диагностика зависимостей](app-insights-asp-net-dependencies.md) |На платформе .NET 4.6 или более поздней, неполные сведения |Да, полные сведения: коды результатов, текст команд SQL, HTTP-команда|
| [Счетчики производительности системы](app-insights-performance-counters.md) |Да |Да |
| [API для пользовательской телеметрии][api] |Да |Нет |
| [Интеграция журнала трассировки](app-insights-asp-net-trace-logs.md) |Да |Нет |
| [Просмотр страницы и пользовательские данные](app-insights-javascript.md) |Да |Нет |
| Требуется код toorebuild |Да | Нет |


## <a name="monitor-a-live-azure-web-app"></a>Мониторинг активного веб-приложения Azure

Если приложение выполняется как Azure веб-службы, здесь как tooswitch о наблюдении за:

* Выберите Application Insights на панели управления приложение hello в Azure.

    ![Настройка Application Insights для веб-приложения Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Когда открывается страница сводки hello Application Insights, щелкните ссылку hello в hello нижней tooopen hello полный ресурс Application Insights.

    ![Пролистайте tooApplication аналитики](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Мониторинг облачных приложений и приложений виртуальной машины](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Включение мониторинга на стороне клиента в Azure

Если вы включили Application Insights в Azure, можно добавить функцию для получения сведений о просмотрах страниц и данных телеметрии пользователя.

1. Выберите элементы "Параметры > Параметры приложения".
2.  В разделе "Параметры приложения" добавьте новую пару "ключ — значение": 
   
    Ключ: `APPINSIGHTS_JAVASCRIPT_ENABLED`. 
    
    Значение: `true`
3. **Сохранить** hello параметры и **перезапустите** приложения.

Теперь пакет SDK для Application Insights JavaScript Hello вставляется в каждой веб-страницы.

## <a name="monitor-a-live-iis-web-app"></a>Мониторинг активного веб-приложения IIS

Если приложение размещено на сервере IIS, включите Application Insights с помощью монитора состояний.

1. Войдите на веб-сервер IIS с учетными данными администратора.
2. Если монитор состояния Application Insights не установлена, загрузите и запустите hello [установщика монитор состояния](http://go.microsoft.com/fwlink/?LinkId=506648) (или запустите [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) и найдите в нем аналитики состояние приложения Монитор).
3. В мониторе состояния выберите hello установлен веб-приложение или веб-сайта, которые должны toomonitor. Выполните вход с использованием учетных данных Azure.

    Настройка ресурсов hello место toosee hello результаты на портале Application Insights hello. (Обычно является наилучшим toocreate новый ресурс. Выберите имеющийся ресурс, если у вас уже есть [веб-тесты][availability] или [наблюдение за клиентами][client] для этого приложения.) 

    ![Выберите приложение и ресурс.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Перезапустите IIS.

    ![Выберите перезапуска вверху hello диалогового окна "hello".](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Работа вашей веб-службы будет ненадолго прервана.

## <a name="customize-monitoring-options"></a>Настройка параметров мониторинга

Application Insights задействуется библиотек DLL и ApplicationInsights.config tooyour веб-приложения. Вы можете [изменить файл .config hello](app-insights-configuration-with-applicationinsights-config.md) toochange некоторых параметров hello.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>При повторной публикации приложения необходимо повторно включить Application Insights

Прежде чем повторно опубликовать приложение, рассмотрите возможность [добавления Application Insights toohello кода в Visual Studio][greenbrown]. Вы сможете получить более подробные данные телеметрии hello возможность toowrite настроенной телеметрии и.

Если требуется, чтобы toore-публикации без добавления Application Insights toohello кода, имейте в виду, что процесс развертывания hello может привести к удалению библиотек DLL hello и ApplicationInsights.config из hello публикации веб-узла. Таким образом:

1. При редактировании файла ApplicationInsights.config сделайте его копию, прежде чем повторно опубликовать приложение.
2. Повторно опубликуйте приложение.
3. Повторно включите мониторинг Application Insights. (Используйте соответствующий метод hello: панель управления hello Azure web app или hello монитор состояния узла IIS.)
4. Возобновить, любые изменения, выполняемые на hello config-файла.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Устранение неполадок конфигурации среды выполнения Application Insights

### <a name="cant-connect-no-telemetry"></a>Проблемы с подключением? Отсутствие данных телеметрии

* Откройте [hello необходимые исходящие порты](app-insights-ip-addresses.md#outgoing-ports) в toowork монитор состояния tooallow брандмауэра сервера.

* Откройте монитор состояний и на левой панели выберите свое приложение. Проверка наличия любые диагностические сообщения для этого приложения в раздел «Уведомления конфигурации» hello:

  ![Откройте колонку toosee hello производительность запроса, время отклика, зависимости и другие данные](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* На сервере hello Если вы видите сообщение «Недостаточно прав», выполните hello следующих действий:
  * В диспетчере служб IIS выберите пул приложений, откройте **Дополнительные параметры**и в разделе **модель процесса** Обратите внимание, идентификация hello.
  * В панели управления компьютера добавьте эту группу пользователей монитора производительности toohello удостоверений.
* Если на вашем сервере установлен MMA/SCOM (Systems Center Operations Manager), некоторые версии могут конфликтовать. Удалите SCOM и состояние монитора и снова установите последние версии hello.
* Ознакомьтесь с разделом [Устранение неполадок][qna].

## <a name="system-requirements"></a>Требования к системе
Операционные системы, которые поддерживаются для монитора состояний Application Insights на сервере:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2.
* Windows Server 2016

На них должны быть установлены последний пакет обновления и платформа .NET Framework 4.5.

На стороне клиента hello: Windows 7, 8, 8.1 и 10, с .NET Framework 4.5

Поддерживаются такие версии IIS: 7, 7.5, 8, 8.5 (IIS – обязательный компонент).

## <a name="automation-with-powershell"></a>Автоматизация с помощью PowerShell
Мониторинг можно запускать и останавливать с помощью PowerShell на сервере IIS.

Сначала следует импортируйте модуль hello Application Insights:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Узнайте, какие приложения отслеживаются:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Имя веб-приложения hello (необязательно).
* Отображает состояние мониторинга Application Insights для каждого веб-приложения (или с именем приложения hello) hello в сервер IIS.
* Возвращает `ApplicationInsightsApplication` для каждого приложения.

  * `SdkState==EnabledAfterDeployment`: Приложение отслеживается и была инструментирована во время выполнения средством hello монитор состояния либо с помощью `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: приложение hello не инструментированы для Application Insights. Он никогда не были инструментированы, либо во время выполнения наблюдение отключено средство hello монитор состояния или с `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: приложение hello были инструментированы, добавив hello SDK toohello исходного кода. Этот пакет SDK нельзя обновить или остановить.
  * `SdkVersion`отображается версия hello используется для наблюдения за этим приложением.
  * `LatestAvailableSdkVersion`Показывает в настоящее время доступна версия hello hello NuGet gallery. версия toothis приложения hello tooupgrade, используйте `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`Имя Hello приложение hello в службах IIS
* `-InstrumentationKey`Здравствуйте, ikey из hello место отображения toobe результаты hello ресурс Application Insights.
* Этот командлет влияет только на приложения, которые еще не инструментированы, то есть SdkState==NotInstrumented.

    командлет Hello не влияет на приложение, которое уже инструментирован. Она не важно, содержит ли приложение hello была инструментирована во время сборки, добавив код toohello SDK hello, или во время выполнения при предыдущем использовании этого командлета.

    приложение hello tooinstrument версия пакета SDK для Hello — hello версию, которая последний раз загрузили toothis сервер.

    последнюю версию toodownload hello, используйте ApplicationInsightsVersion обновления.
* В случае успешного выполнения возвращает `ApplicationInsightsApplication` . Если не удается, он регистрирует toostderr трассировки.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`Hello имя приложения в IIS
* `-All` — останавливает мониторинг всех приложений на этом сервере IIS, для которых `SdkState==EnabledAfterDeployment`.
* Останавливает наблюдение для hello иные приложения и удаляет инструментирования. Работает только для приложений, которые были инструментированы, во время выполнения с помощью hello наблюдение за состоянием средства или ApplicationInsightsApplication запуска. (`SdkState==EnabledAfterDeployment`)
* Возвращает ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: hello имя веб-приложения в IIS.
* `-InstrumentationKey` (необязательный параметр). Используйте этот toochange hello ресурсов toowhich hello телеметрии приложения отправляется.
* Этот командлет:
  * Hello обновления с именем toohello версии приложения hello SDK недавно загрузить toothis машины. (работает, только если `SdkState==EnabledAfterDeployment`).
  * При указании ключа инструментирования с именем приложения hello — перенастроен toosend телеметрии toohello ресурс с этим ключом. (работает, если `SdkState != Disabled`).

`Update-ApplicationInsightsVersion`

* Загружает hello последнего пакета SDK Application Insights toohello сервера.

## <a name="questions"></a>Вопросы о мониторе состояния

### <a name="what-is-status-monitor"></a>Что такое монитор состояния?

Классическое приложение, установленное на веб-сервер IIS. Оно позволяет инструментировать и настраивать веб-приложения. 

### <a name="when-do-i-use-status-monitor"></a>В каких случаях нужно использовать монитор состояния?

* tooinstrument любого веб-приложения, запущенного на сервере IIS -, даже если она уже запущена.
* tooenable дополнительные данные телеметрии для веб-приложений, которые были [созданного с помощью пакета SDK Application Insights hello](app-insights-asp-net.md) во время компиляции. 

### <a name="can-i-close-it-after-it-runs"></a>Можно ли его закрыть после выполнения?

Да. После его инструментирования hello веб-сайтов, при выборе, ее можно закрыть.

Монитор состояния не собирает данные телеметрии самостоятельно. Просто настраивает веб-приложения hello и задает некоторые разрешения.

### <a name="what-does-status-monitor-do"></a>Как работает монитор состояния?

При выборе веб-приложения для tooinstrument монитор состояния:

* Загружает и помещает сборки hello Application Insights и config-файл в папку с двоичными файлами веб-приложения hello.
* Изменяет `web.config` tooadd hello приложения аналитики отслеживания модуль HTTP.
* Включает вызовы зависимостей toocollect профилирования среды CLR.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>Зачем мне toorun монитор состояния при каждом обновлении приложение hello?

Нет, если повторное развертывание выполняется поэтапно. 

При выборе параметра «Удалить существующие файлы» hello в hello процесса публикации, необходимо выполнить toore монитор состояния tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>Какие данные телеметрии собираются?

Для приложений, инструментированных во время выполнения с использованием монитора состояния:

* HTTP-запросы;
* Вызывает toodependencies
* Исключения
* Счетчики производительности

Для уже инструментированных приложений во время компиляции:

 * счетчики процессов;
 * вызовы зависимостей (.NET 4.5) и возвращаемые значения в вызовах зависимостей (.NET 4.6);
 * значения трассировки стека исключений.

[Подробнее](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Дальнейшие действия

Просмотр телеметрии:

* [Просмотр метрик](app-insights-metrics-explorer.md) toomonitor производительности и использовании
* [Поиск событий и журналов] [ diagnostic] toodiagnose проблемы
* [Аналитика](app-insights-analytics.md) для создания расширенных запросов.
* [Создайте панели мониторинга](app-insights-dashboards.md)

Добавление данных телеметрии:

* [Создание веб-тестов] [ availability] toomake убедиться, что веб-узла остается в реальном времени.
* [Добавить клиента телеметрии веб] [ usage] toosee исключения из кода веб-страниц и вставке toolet Трассировка вызовов.
* [Добавьте код, пакет SDK Application Insights tooyour] [ greenbrown] , чтобы можно было вставить трассировки и записывать вызовы

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
