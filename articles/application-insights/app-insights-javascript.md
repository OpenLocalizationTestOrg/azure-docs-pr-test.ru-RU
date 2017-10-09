---
title: "aaaAzure Application Insights для JavaScript веб-приложений | Документы Microsoft"
description: "Получайте данные о количестве просмотров страницы и количестве сеансов, данные веб-клиента и отслеживайте закономерности использования. Выявляйте исключения и проблемы с производительностью на веб-страницах JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Application Insights для веб-страниц
Сведения о производительности hello и использования веб-страницы или приложения. При добавлении [Application Insights](app-insights-overview.md) tooyour сценарий страницы, вы получаете времени загрузки страницы и AJAX вызовы, количеством и подробности исключения браузера и сбои AJAX, а также пользователей и число сеансов. Все эти данные можно разбить по страницам, версии клиентской ОС и браузера, географическому расположению и другим показателям. Можно также настроить оповещения для определенного количества сбоев или медленной загрузки страниц. И вставляя трассировки вызовов в коде JavaScript, можно отслеживать использования различных функций hello приложения веб-страницы.

Application Insights можно использовать с любыми веб-страницами — просто добавьте небольшой фрагмент кода JavaScript. Для веб-службы [Java](app-insights-java-get-started.md) или [ASP.NET](app-insights-asp-net.md) можно интегрировать данные телеметрии, полученные с сервера и клиентских компьютеров.

![На сайте portal.azure.com откройте ресурс приложения и щелкните "Браузер".](./media/app-insights-javascript/03.png)

Вам потребуется подписка слишком[Microsoft Azure](https://azure.com). Если у команды есть подписка организации, попросите владельца tooadd hello tooit вашей учетной записи Майкрософт. Разработка и использование в небольших масштабах не потребуют никаких денежных затрат.

## <a name="set-up-application-insights-for-your-web-page"></a>Настройка Application Insights для веб-страницы
Добавьте hello загрузчика кода фрагмент tooyour веб-страницы, следующим образом.

### <a name="open-or-create-application-insights-resource"></a>Открытие или создание ресурса Application Insights
Hello ресурс Application Insights — которых отображаются данные о производительности и использования на странице. 

Войдите на [портал Azure](https://portal.azure.com).

Если вы настроили мониторинг на стороне сервера приложения hello, уже имеют ресурса:

![Последовательно выберите пункты «Обзор», «Службы для разработчиков» и «Application Insights».](./media/app-insights-javascript/01-find.png)

Если ресурса у вас нет, создайте его.

![Последовательно выберите пункты «Создать», «Службы для разработчиков», «Application Insights»](./media/app-insights-javascript/01-create.png)

*Уже появились вопросы?* [Дополнительная информация о создании ресурса](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Добавить скрипт tooyour hello пакет SDK для приложения или веб-страницы
В быстром запуске получение hello скрипта для веб-страниц:

![В колонке обзор вашего приложения выберите Быстрый запуск, получить код toomonitor веб-страницы. Скопируйте сценарий hello.](./media/app-insights-javascript/02-monitor-web-page.png)

Вставить скрипт hello непосредственно перед hello `</head>` тег каждой страницы, которую должна tootrack. Если веб-сайт имеет главной страницы, можно поместить скрипт hello существует. Например:

* В проекте ASP.NET MVC разместите сценарий на странице `View\Shared\_Layout.cshtml`
* На сайте SharePoint, на панели управления hello, откройте [параметры сайта / Главная страница](app-insights-sharepoint.md).

сценарий Hello содержит ключ инструментирования hello, указывающий ресурс Application Insights tooyour данных hello. 

([Подробно hello скрипта. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Если вы используете известную платформу веб-страницы, найдите адаптеры Application Insights. Например, [модуль AngularJS](http://ngmodules.org/modules/angular-appinsights).)*

## <a name="detailed-configuration"></a>Подробные сведения
Вы можете задать несколько [параметров](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config), хотя в большинстве случаев это не требуется. Например можно отключить или ограничить количество hello вызовов Ajax, регистрируемых в представление страницы (tooreduce трафик). Или можно задать перемещения телеметрии toohave режим отладки быстро через конвейер hello не выполняется в пакетном режиме.

tooset эти параметры поиска для этой строки в фрагменте кода hello и добавьте после него больше элементов, разделенных запятыми:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Hello [доступных параметров](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) включают:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Запуск приложения
Запуск веб-приложения, используйте его при toogenerate телеметрии и подождите несколько секунд. Можно выполнить с помощью hello **F5** ключа на компьютере разработки или опубликовать его и позволяют пользователям работать с его.

Toocheck hello телеметрии, веб-приложение отправляет tooApplication аналитики, используйте средства отладки в браузере (**F12** во многих браузерах). Данные отправляются toodc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Просмотр данных о производительности браузера
Откройте hello tooshow колонке браузера собранные данные о производительности из браузеры пользователей.

![На сайте portal.azure.com откройте ресурс приложения и щелкните "Параметры", а затем "Браузер".](./media/app-insights-javascript/03.png)

*Еще нет данных? Нажмите кнопку **обновление** вверху hello страницы приветствия. По-прежнему нет данных? См. раздел [Устранение неполадок](app-insights-troubleshoot-faq.md).*

панель обозревателя Hello — это [колонке обозревателя метрик](app-insights-metrics-explorer.md) с существующие фильтры и выбранные диаграммы. Диапазон времени hello, фильтры и конфигурации диаграммы можно изменить и сохранить результат hello в список избранного. Нажмите кнопку **восстановить значения по умолчанию** tooget задней toohello исходной колонке конфигурации.

## <a name="page-load-performance"></a>Производительность загрузки страниц
Hello верхней является сегментированных диаграмму времени загрузки страницы. Общая высота Hello hello диаграммы представляет hello среднее время tooload и отображения страницы из приложения в браузерах пользователей. Hello время отсчитывается с, когда hello браузер отправляет первоначальный HTTP-запрос hello до всего синхронного нагрузки, будут обработаны события, включая макет и выполнение скриптов. Асинхронные задачи, такие как загрузка веб-частей из вызовов AJAX, не учитываются.

Диаграмма Hello делит время загрузки всего страницы приветствия на hello [стандартные затраты времени определено консорциумом W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Обратите внимание, что hello *сетевых подключений* времени часто — ниже, чем предполагалось, так как среднее над всеми запросами с сервера toohello hello браузера. Множество отдельных запросов иметь время подключения 0, так как уже имеется сервер toohello активное соединение.

### <a name="slow-loading"></a>Медленная загрузка
Медленная загрузка страниц — основная причина недовольства пользователей. Если диаграмма hello указывает низкая скорость загрузки, это легко toodo некоторое исследование диагностики.

Hello диаграмме показано среднее hello загружает все страницы в приложении. toosee, если проблема hello ограничены tooparticular страниц, внешний вид дальнейшей вниз колонку hello, где имеется сетки, разбитых на URL-адрес страницы:

![](./media/app-insights-javascript/09-page-perf.png)

Обратите внимание, количество представления страниц hello и стандартное отклонение. Количество страниц hello очень мала, затем hello проблема не влияет ли пользователи намного. Высокий уровень стандартное отклонение (сопоставимых toohello среднее значение самого) указывает на большой объем различия между отдельные измерения.

**Данные для отдельного URL-адреса и отдельного просмотра страницы.** Щелкните любой toosee имя страницы панель диаграмм отфильтрованные просто toothat URL-адрес браузера; а затем на экземпляр представления страницы.

![](./media/app-insights-javascript/35.png)

Нажмите кнопку `...` полный список свойств для данного события или проверить вызовы Ajax hello и связанные события. Привет, влияют на медленных вызовов Ajax общее время загрузки страницы, если они являются синхронными. Связанные события включают запросы серверов на hello же URL-адрес (Если вы настроили Application Insights на веб-сервере).

**Производительность страниц со временем.** В колонке браузеры hello измените hello время загрузки страницы сетки в toosee линии диаграммы при отсутствии пики в том:

![Щелкните заголовок hello hello сетки и выберите новый тип диаграммы](./media/app-insights-javascript/10-page-perf-area.png)

**Сегментация по другим показателям.** Может быть страницы находятся медленнее tooload на конкретном отношении браузера, операционной системы клиента или пользователя? Добавить новую диаграмму и поэкспериментировать с hello **Group by** измерения.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Производительность вызовов AJAX
Убедитесь, что все вызовы AJAX на веб-страницах работают нормально. Это часто используется toofill частей страницы асинхронно. Несмотря на то, что hello страницы целиком может загрузить незамедлительно, пользователям может быть надоело перед пустой веб-частей, Ожидание tooappear данных в них.

Вызовы AJAX на веб-странице отображаются в колонке браузеры hello как зависимости.

Существует сводных диаграмм в верхней части колонки hello hello.

![](./media/app-insights-javascript/31.png)

Подробные таблицы приводятся ниже:

![](./media/app-insights-javascript/33.png)

Щелкните любую строку для получения подробной информации.

> [!NOTE]
> При удалении фильтра браузеры hello в колонке hello зависимостей AJAX и сервера включены в эти диаграммы. Нажмите кнопку Восстановить значения по умолчанию фильтр tooreconfigure hello.
> 
> 

**toodrill в неудачные вызовы Ajax** прокрутите вниз по сетке сбоев toohello зависимостей и нажмите кнопку toosee конкретные экземпляры строк.

![](./media/app-insights-javascript/37.png)


Щелкните `...` для hello полный телеметрии для вызова Ajax.

### <a name="no-ajax-calls-reported"></a>Вызовы AJAX не регистрируются?
Вызовы AJAX включают все вызовы HTTP/HTTPS, выполненные из скрипта hello веб-страницы. Если вы не видите их сообщил, проверьте, что фрагмент кода hello не hello `disableAjaxTracking` или `maxAjaxCallsPerView` [параметры](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Исключения браузера
В колонке браузеры hello является исключения Сводные диаграммы и сетки типов исключений дальнейшей вниз колонку hello.

![](./media/app-insights-javascript/39.png)

Если вы не видите исключения браузера, проверьте, этот фрагмент кода hello не hello `disableExceptionTracking` [параметр](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Изучение отдельных событий просмотра страницы

Обычно телеметрия просмотра страниц анализируется службой Application Insights, и вы видите только сводные отчеты со средними значениями для всех пользователей. Однако в целях отладки можно также изучать отдельные события просмотра страниц.

В колонке диагностики поиска hello задайте фильтры tooPage представления.

![](./media/app-insights-javascript/12-search-pages.png)

Выберите любое событие toosee более подробно. Hello сведения на странице нажмите кнопку «...» toosee еще более подробные сведения.

> [!NOTE]
> При использовании [поиска](app-insights-diagnostic-search.md), обратите внимание, наличие слова целиком toomatch: «О» и «Подробнее» о «About» не совпадают.
> 
> 

Можно также использовать hello мощные [языка запросов анализа журналов](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch страницы представления.

### <a name="page-view-properties"></a>Свойства просмотра страниц
* **Длительность просмотра страницы** 
  
  * По умолчанию hello он принимает tooload hello страница времени, toofull клиентом запроса загрузки (включая вспомогательные файлы, но исключая асинхронных задач, таких как вызовы Ajax). 
  * Если задать `overridePageViewDuration` в hello [конфигурация страницы](#detailed-configuration), сначала hello интервал между tooexecution запрос клиента из hello `trackPageView`. Если trackPageView перемещены из своего обычного положения после инициализации hello hello сценария, его отразят другое значение.
  * Если `overridePageViewDuration` и длительность, аргумент передан в hello `trackPageView()` вызова, то вместо него используется значение аргумента hello. 

## <a name="custom-page-counts"></a>Настраиваемые счетчики страниц
По умолчанию количество страниц происходит каждый раз, когда загрузка новой страницы в браузер клиента hello.  Однако при необходимости toocount дополнительная страница представления. Например страница может отобразить его содержимое во вкладках и требуется toocount страницей, когда пользователь hello переключает вкладки. Или кода JavaScript на странице приветствия может загрузить новое содержимое без изменения URL-адрес браузера hello.

В hello соответствующую точку в коде клиента, вставьте вызов JavaScript следующим образом:

    appInsights.trackPageView(myPageName);

имя страницы приветствия может содержать hello же символы URL-адрес, а любые после «#» или «?» игнорируется.

## <a name="usage-tracking"></a>Отслеживание использования
Требуется toofind пользователей, выполнять с помощью приложения?

* [Дополнительные сведения об отслеживании использования](app-insights-web-track-usage.md)
* [Дополнительные сведения об API пользовательских событий и метрик](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Видео


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Дальнейшие действия
* [Отслеживание использования](app-insights-web-track-usage.md)
* [Пользовательские события и метрики](app-insights-api-custom-events-metrics.md)
* [Сборка, измерение и обучение](app-insights-web-track-usage.md)

