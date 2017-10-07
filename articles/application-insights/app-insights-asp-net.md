---
title: "aaaSet копирование веб-аналитики приложений для ASP.NET с помощью Azure Application Insights | Документы Microsoft"
description: "Настройка средств аналитики производительности, доступности и использования для веб-сайта ASP.NET, размещенного локально или в Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>Настройка Application Insights для веб-сайта ASP.NET

Эта процедура позволяет настроить вашей ASP.NET web app toosend телеметрии toohello [Azure Application Insights](app-insights-overview.md) службы. Он работает для приложений ASP.NET, размещенных на сервере IIS или в облаке hello. Вы получите диаграммы и язык запросами, которые помогут понять hello производительности приложения и как люди используют ее, а также автоматического оповещения для сбоев или проблем с производительностью. Многим разработчикам кажутся эти функции отлично, как их можно, но можно расширить и настроить hello телеметрии, если необходимо.

Настройка выполняется несколькими щелчками в Visual Studio. У вас есть hello параметр tooavoid расходы, ограничивая объем hello телеметрии. Это позволяет вам tooexperiment и отладки или toomonitor сайт с не много пользователей. Если вы решите, нужно заранее toogo и мониторинга на рабочем сайте, это легко tooraise hello ограничить позже.

## <a name="before-you-start"></a>Перед началом
Вам необходимы:

* Visual Studio 2013 с обновлением 3 или более новая версия. Чем новее версия, тем лучше.
* Подписка слишком[Microsoft Azure](http://azure.com). Если в команде или организации имеет подписку Azure, владелец hello можно добавить вы tooit, с помощью вашей [учетную запись Майкрософт](http://live.com).

Если вы заинтересованы в существует toolook альтернативные разделы в:

* [инструментирование веб-приложения во время выполнения;](app-insights-monitor-performance-live-website-now.md)
* [облачных служб Azure](app-insights-cloudservices.md)

## <a name="ide"></a>Шаг 1: Добавление hello пакет SDK Application Insights

В обозревателе решений щелкните проект веб-приложения правой кнопкой мыши и выберите пункт **Добавить** > **Телеметрия Application Insights** или **Настроить Application Insights**.

![Снимок экрана с окном обозревателя решений, где выделен параметр "Добавить" и "Телеметрия Application Insights"](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(В Visual Studio 2015 также есть параметр tooadd Application Insights, в диалоговом окне нового проекта hello.)

Продолжить-страница конфигурации toohello Application Insights:

![Снимок экрана с окном страницы "Зарегистрировать приложение в Application Insights"](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**а.** Выберите учетную запись hello и подписки, которая используется tooaccess Azure.

**б.** Выберите ресурс hello в Azure, где вы хотите toosee hello данные из приложения. Обычно:

* Используйте [один ресурс для разных компонентов](app-insights-monitor-multi-role-apps.md) одного приложения. 
* Создавайте разные ресурсы для несвязанных приложений.
 
Tooset hello ресурсов группы или hello место хранения данных, нажмите кнопку **настройки**. Группы ресурсов — используется toocontrol toodata доступа. Например, если имеется несколько приложений, являющиеся частью hello же системе, может поместить данные Application Insights в hello одну группу ресурсов.

**в.** Задайте ограничение на ограничение тома данных free hello, tooavoid расходов. Application Insights Освободите tooa определенных объем телеметрии. После создания ресурса hello можно изменить выбранные параметры на портале hello, открыв **компоненты и цены** > **управление томами данных** > **ежедневно ограничение тома**.

**г.** Нажмите кнопку **зарегистрировать** toogo вперед и настраивать Application Insights для веб-приложения. Данные телеметрии будут отправляться toohello [портал Azure](https://portal.azure.com), во время отладки и после публикации приложения.

**д.** Если вы не хотите toosend телеметрии toohello портала во время отладки, просто добавьте tooyour приложение hello пакет SDK Application Insights, но не настраивайте ресурса в портале hello. Можно будет toosee телеметрии в Visual Studio в процессе отладки. Позже, можно вернуть страницу настройки toothis или удалось дождаться после развертывания приложения и [переключиться на телеметрии во время выполнения](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a> Шаг 2. Запуск приложения
Запустите приложение, нажав клавишу F5. Откройте некоторые телеметрии toogenerate разным страницам.

В Visual Studio отображается количество событий hello, которые были записаны.

![Снимок экрана, где отображается Visual Studio во время отладки отображается кнопке Hello Application Insights.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Шаг 3. Просмотр данных телеметрии
Вы увидите телеметрии в Visual Studio или на веб-портале Application Insights hello. Поиск телеметрии в Visual Studio toohelp отладке приложения. Мониторинг производительности и использовании hello веб-портале, когда система находится в режиме реального времени. 

### <a name="see-your-telemetry-in-visual-studio"></a>Просмотр данных телеметрии в Visual Studio

В Visual Studio откройте окно hello Application Insights. Либо щелкните hello **Application Insights** кнопку или щелкните правой кнопкой мыши проект в обозревателе решений выберите **Application Insights**и нажмите кнопку **поиск телеметрии Live**.

В окне поиска Visual Studio Application Insights hello просмотреть hello **данные из сеанса отладки** представление для телеметрии, созданные в hello серверная часть приложения. Поэкспериментируйте с фильтрами hello и щелкните любое событие toosee более подробно.

![Снимок экрана: hello, представления данных из сеанса отладки в окне приветствия Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Если данные не отображаются, убедитесь, что диапазон времени hello указано правильно и щелкните значок поиска hello.

[Дополнительные сведения о средствах Application Insights в Visual Studio](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Просмотр данных телеметрии на веб-портале

Также видно телеметрии на веб-портале Application Insights hello (если не выбран только hello tooinstall SDK). портал Hello имеет дополнительные диаграммы, аналитических средств и компонентов между представлениями, чем Visual Studio. портал Hello также предоставляет предупреждения.

Откройте ресурс Application Insights. Либо войти toohello [портал Azure](https://portal.azure.com/) и найти его, или щелкните правой кнопкой мыши hello проект в Visual Studio и позвольте ему перейти на него.

![Снимок экрана в Visual Studio, показывающий, как tooopen hello портале Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Если возникает ошибка доступа: имеется более одного набора учетных данных Майкрософт, и вы вошли hello не тот набор? На портале hello выйдите из системы и войти в систему.

Откроется портал Hello на представлении hello телеметрии из приложения.

![Снимок экрана, где отображается страница с обзором Application Insights](./media/app-insights-asp-net/66.png)

На портале hello щелкните любой плитки или диаграммы toosee более подробно.

[Дополнительные сведения об использовании Application Insights в hello портал Azure](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>Шах 4. Публикация приложения
Опубликуйте на сервере IIS tooyour приложения или tooAzure. Контрольное значение [обновляющегося потока метрики](app-insights-metrics-explorer.md#live-metrics-stream) toomake убедиться, что все работает плавно.

Накапливает телеметрии в Application Insights hello портал, где мониторинг метрик, поиск телеметрии и настроить [панелей мониторинга](app-insights-dashboards.md). Можно также использовать hello мощные [языка запросов анализа журналов](https://docs.loganalytics.io/) tooanalyze об использовании и производительности или toofind определенных событий.

Вы также можете продолжить tooanalyze телеметрии в [Visual Studio](app-insights-visual-studio.md), с помощью средства, такие как поиск диагностики и [тенденции](app-insights-visual-studio-trends.md).

> [!NOTE]
> Если приложение отправляет достаточно hello телеметрии tooapproach [ограничивает](app-insights-pricing.md#limits-summary)автоматической [выборки](app-insights-sampling.md) переключается. Выборка снижает количество hello телеметрии, отправляемых из приложения, во время сохранения связанных данных в целях диагностики.
>
>

## <a name="land"></a>Все готово

Поздравляем! Установленный пакет Application Insights hello в приложении и настроена служба Application Insights toohello toosend телеметрии на Azure.

![Диаграмма перемещения данных телеметрии](./media/app-insights-asp-net/01-scheme.png)

ресурс Azure, который получает телеметрии приложения Hello определяется *ключ инструментирования*. Этот ключ можно найти в файле ApplicationInsights.config hello.


## <a name="upgrade-toofuture-sdk-versions"></a>Обновление версии пакета SDK toofuture
tooupgrade tooa [новый выпуск пакета SDK для hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)откройте hello **диспетчера пакетов NuGet** еще раз и фильтр для установленных пакетов. Выберите элемент **Microsoft.ApplicationInsights.Web**, а затем — элемент **Обновить**.

При внесении любого tooApplicationInsights.config настроек, сохраните ее копию перед обновлением. Затем объединить изменения в новой версии hello.

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Дальнейшие действия

### <a name="more-telemetry"></a>Дополнительные данные телеметрии

* **[Данные загрузки браузера и страниц](app-insights-javascript.md)** — вставьте фрагмент кода в веб-страницы.
* **[Более подробные зависимости и данные отслеживание исключений](app-insights-monitor-performance-live-website-now.md)** — установите монитор состояния на сервере.
* **[Пользовательские события кода](app-insights-api-custom-events-metrics.md)**  toocount, время, или меры действия пользователя.
* **[Получение данных журнала](app-insights-asp-net-trace-logs.md)** — согласовывайте данные журналов с данными телеметрии.

### <a name="analysis"></a>Анализ

* **[Работа с Application Insights в Visual Studio](app-insights-visual-studio.md)**<br/>Содержит сведения об отладке с телеметрии, диагностики поиска и детализация toocode.
* **[Работа с порталом Application Insights hello](app-insights-dashboards.md)**<br/> Содержит сведения о панелях мониторинга, эффективных средствах диагностики и анализа, оповещениях, картах динамических зависимостей приложения, а также сведения об экспорте данных телеметрии.
* **[Аналитика](app-insights-analytics-tour.md)**  -hello запросами языка.

### <a name="alerts"></a>Оповещения

* [Проверяет доступность](app-insights-monitor-web-app-availability.md): Создание тестов toomake убедиться, что веб-сайт будет видимым в веб-hello.
* [Интеллектуальные диагностики](app-insights-proactive-diagnostics.md): эти тесты выполняются автоматически, поэтому не нужно toodo любые tooset их вверх. Благодаря ей вы узнаете о необычном количестве неудачных запросов.
* [Метрики оповещений](app-insights-alerts.md): задайте эти toowarn вы метрики пересекает пороговое значение. Их можно настроить для пользовательских метрик, добавляемых в код приложения.

### <a name="automation"></a>Служба автоматизации

* [Создание ресурсов Application Insights с помощью PowerShell](app-insights-powershell.md)
