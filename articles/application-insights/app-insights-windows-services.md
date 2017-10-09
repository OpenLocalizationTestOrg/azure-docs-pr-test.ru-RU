---
title: "aaaAzure аналитики приложений для Windows server ролей и рабочих ролей | Документы Microsoft"
description: "Вручную добавьте использование tooanalyze приложения ASP.NET tooyour hello пакет SDK Application Insights, доступности и производительности."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>Настройка Application Insights вручную для приложений .NET

Можно настроить [Application Insights](app-insights-overview.md) toomonitor широкий спектр приложений или ролей приложения, компоненты или микрослужбами. Для веб-приложений и служб Visual Studio предлагает [одноэтапную настройку](app-insights-asp-net.md). Для других типов приложений .NET, таких как внутренние роли сервера или классические приложения, вы можете настроить Application Insights вручную.

![Пример диаграмм мониторинга производительности](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Перед началом работы

Вам необходимы:

* Подписка слишком[Microsoft Azure](http://azure.com). Если в команде или организации имеет подписку Azure, в владелец hello добавлять tooit, с помощью вашей [учетную запись Майкрософт](http://live.com).
* Visual Studio 2013 или более поздняя версия.

## <a name="add"></a>1. Выбор ресурса Application Insights

ресурс «Hello» — где собираются и отображаются в hello портал Azure. Toodecide требуется ли toocreate создать новую или существующую общую папку.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Часть большего приложения. Использование имеющегося ресурса

Если веб-приложение содержит несколько компонентов — например, интерфейсный веб-приложения и один или несколько служб, -, то необходимо отправлять данные телеметрии из всех toohello компонентов hello того же ресурса. Это включает их toobe, отображаемые на карте одного приложения и сделать его возможных tootrace запроса из одного компонента tooanother.

Таким образом, если другие компоненты этого приложения уже мониторинг, затем просто воспользуйтесь hello же ресурса.

Откройте ресурс hello в hello [портал Azure](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Автономное приложение. Создание ресурса

Если новое приложение hello связаны tooother приложений, он должен иметь свой собственный ресурс.

Войдите в toohello [портал Azure](https://portal.azure.com/)и создать новый ресурс Application Insights. Выберите в качестве типа приложения hello ASP.NET.

![Нажмите "Создать" и "Application Insights"](./media/app-insights-windows-services/01-new-asp.png)

Выбор типа приложения Hello задает содержимое по умолчанию hello колонки ресурсов hello.

## <a name="2-copy-hello-instrumentation-key"></a>2. Скопируйте ключ инструментирования hello
ключ Hello идентифицирует ресурс hello. Оно будет установлено только в hello SDK, в порядке toodirect данных toohello ресурсов.

![Щелкните свойства, выберите раздел hello и нажмите клавиши ctrl + C](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Установить пакет аналитики приложения hello в приложении
Установка и настройка hello Application Insights пакета зависит от платформы hello, над которым вы работаете. 

1. В Visual Studio щелкните проект правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.
   
    ![Щелкните правой кнопкой мыши проект hello и выберите Управление пакетами Nuget](./media/app-insights-windows-services/03-nuget.png)
2. Установить пакет hello Application Insights для приложений Windows server, «Microsoft.ApplicationInsights.WindowsServer.»
   
    ![Поиск Application Insights](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Какую версию выбрать?*

    Проверьте **включить предварительный выпуск** Если tootry нашей новейших функций. Hello соответствующих документов или блоги Обратите внимание, следует ли предварительной версии.
    
    *Можно ли использовать другие пакеты?*
   
    Да. Выберите «Microsoft.ApplicationInsights» только toouse hello API toosend собственные телеметрии. пакет Windows Server Hello включает hello API, а также ряд других пакетов, таких как сбор данных счетчика производительности и отслеживание зависимостей. 

### <a name="tooupgrade-toofuture-package-versions"></a>версии пакетов toofuture tooupgrade
Мы выпуска новой версии hello SDK из tootime времени.

tooupgrade tooa [новый выпуск пакета hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), снова откройте диспетчер пакетов NuGet и фильтрации установленных пакетов. Выберите **Microsoft.ApplicationInsights.WindowsServer**, а затем — **Обновить**.

При внесении любого tooApplicationInsights.config настроек, сохраните ее копию перед выполнением обновления, а впоследствии объединить изменения в новой версии hello.

## <a name="4-send-telemetry"></a>4. Отправка данных телеметрии
**Если установлен только пакет hello API:**

* Задать ключ инструментирования hello в коде, например в `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *ваш ключ* `";` 
* [Запись телеметрии с помощью hello API](app-insights-api-custom-events-metrics.md#ikey).

**Если вы установили другие пакеты Application Insights** Если вы предпочитаете, воспользуйтесь разделом hello .config файл tooset hello инструментирования:

* Измените файл ApplicationInsights.config (которая была добавлена, установить NuGet hello). Вставьте это непосредственно перед закрывающим тегом hello:
  
    `<InstrumentationKey>`*вы скопировали ключ инструментирования hello*`</InstrumentationKey>`
* Убедитесь, что свойства hello ApplicationInsights.config в обозревателе решений задано слишком**действие построения = содержимое tooOutput копирования каталога = копирование**.

Это полезно tooset ключ инструментирования hello в коде, если требуется слишком[ключ hello коммутатора для разных конфигураций построения](app-insights-separate-resources.md). Если значение ключа hello в коде, не нужно tooset в hello `.config` файла.

## <a name="run"></a>Запуск проекта
Используйте hello **F5** toorun приложения и попробуйте: открытые различные страницы toogenerate некоторые телеметрии.

В Visual Studio вы увидите количество hello событий, которые были отправлены.

![Количество событий в Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Просмотр своих данных телеметрии
Вернуть toohello [портал Azure](https://portal.azure.com/) и найдите ресурс Application Insights tooyour.

Поиск данных в диаграммах Обзор hello. Сначала вы увидите только одну или две точки. Например:

![Перемещаться по данным toomore](./media/app-insights-windows-services/12-first-perf.png)

Нажмите кнопку через любой toosee диаграммы более подробные показатели. [Дополнительные сведения о метриках.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Данные отсутствуют?
* С помощью приложения hello, открыв разные страницы, чтобы он создает некоторые телеметрии.
* Откройте hello [поиска](app-insights-diagnostic-search.md) плитки toosee отдельные события. Иногда принимает события немного больше времени, во время tooget через конвейер метрики hello.
* Подождите несколько секунд и нажмите **Обновить**. Сами периодически обновлять диаграммы, но можно обновить вручную, если вы ожидаете для некоторых данных tooshow.
* См. раздел [Устранение неполадок](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Публикация приложения
Теперь развертывания сервера tooyour приложения или накапливать данные hello tooAzure и контрольных значений.

![Используйте Visual Studio toopublish приложения](./media/app-insights-windows-services/15-publish.png)

При запуске в режиме отладки телеметрии ускорено через конвейер hello, чтобы вы увидите данные за несколько секунд. При развертывании приложения в конфигурации выпуска данные накапливаются медленнее.

### <a name="no-data-after-you-publish-tooyour-server"></a>Нет данных после публикации tooyour сервера?
Откройте порты для исходящего трафика в брандмауэре сервера. В разделе [эту страницу](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) hello перечень необходимых адресов 

### <a name="trouble-on-your-build-server"></a>Проблемы на сервере сборки?
Изучите [этот элемент устранения неполадок](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).

> [!NOTE]
> Если приложение создает большой объем данных телеметрии, модуль адаптивной выборки hello автоматически уменьшит hello тома, отправляемое toohello портала, отправляя репрезентативной часть событий. Тем не менее события, которые связанные toohello того же запроса будет иметь или отмену выбора как группой, чтобы могли перемещаться между связанными событиями. 
> [Дополнительная информация о выборке](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Дальнейшие действия
* [Добавьте дополнительные телеметрии](app-insights-asp-net-more.md) tooget hello полной 360 градусов представления приложения.

