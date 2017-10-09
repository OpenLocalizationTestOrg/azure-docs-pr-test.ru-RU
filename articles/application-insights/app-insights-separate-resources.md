---
title: "aaaSeparating телеметрии из среды разработки, тестирования и выпуска в Azure Application Insights | Документы Microsoft"
description: "Прямой телеметрии toodifferent ресурсы для разработки, тестирования и эксплуатации отметки."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Отделение телеметрии стадий разработки, тестирования и эксплуатации

При разработке hello следующей версии веб-приложение, вы не хотите toomix копирование hello [Application Insights](app-insights-overview.md) телеметрии из hello новой версии и версии hello уже освобожден. путаницы tooavoid отправки данных телеметрии hello разработки готовит tooseparate ресурсы Application Insights, ключи отдельные инструментария (ikeys). toomake его проще ключ инструментирования hello toochange как версия перемещает из tooanother один этап, это может быть полезно tooset ikey hello в коде, а не в файле конфигурации hello. 

(Если вы используете облачную службу Azure, есть [другой метод настройки отдельных ключей инструментирования ikey](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Ресурсы и ключи инструментирования

При настройке мониторинга Application Insights для веб-приложения вы создаете *ресурс* Application Insights в Microsoft Azure. Открыть этот ресурс в портал Azure в порядке toosee hello и анализ телеметрии hello, собранная из приложения. Hello ресурсов определяется *ключ инструментирования* (ikey). При установке hello Application Insights пакета toomonitor приложения, нужно настроить его с ключом инструментирования hello, чтобы он знал, где toosend hello телеметрии.

Обычно выбрать отдельные ресурсы toouse или одного общего ресурса в различных сценариях:

* Различные, независимые приложения: используйте отдельный ресурс и ключ инструментирования для каждого приложения.
* Использование нескольких компонентов или ролей приложения один бизнес - [один общий ресурс](app-insights-monitor-multi-role-apps.md) для всех hello компонента приложения. Можно выполнять фильтрацию и сегментируются свойством cloud_RoleName hello телеметрии.
* Разработка, тестирование и выпуски - использовать отдельный ресурс и ikey для версии системы hello, «метки» или этапа производства.
* Тестирование A или B. Используйте один ресурс. Создайте TelemetryInitializer tooadd телеметрии toohello свойство, идентифицирующее hello вариантов.


## <a name="dynamic-ikey"></a> Динамический ключ инструментирования

toomake упрощение ikey hello toochange как код hello перемещается между этапы производства, заданы в коде, а не в файле конфигурации hello.

Установите раздел hello в метод инициализации, например global.aspx.cs в службы ASP.NET.

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

В этом примере hello ikeys для разных ресурсов hello размещаются в различных версиях hello файл веб-конфигурации. Идет обмен файл веб-конфигурации hello - это можно сделать в скрипте выпуска hello - поменяет hello целевого ресурса.

### <a name="web-pages"></a>Веб-страницы
Hello iKey также используется в веб-страницы приложения в hello [скрипт, который получен из колонки быстрого запуска hello](app-insights-javascript.md). Вместо написания его буквально в сценарий hello, создайте его hello состояния сервера. Например, в приложении ASP.NET:

*JavaScript в Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Создание дополнительных ресурсов Application Insights
tooseparate телеметрии для разные компоненты приложения или для разных метках (разработки или тестирования и рабочего) hello одного компонента, то получите toocreate новый ресурс Application Insights.

В hello [portal.azure.com](https://portal.azure.com), добавьте ресурс Application Insights:

![Нажмите "Создать" и "Application Insights"](./media/app-insights-separate-resources/01-new.png)

* **Тип приложения** влияет на содержимое, отображаемое на колонки Обзор hello и hello свойств, доступных в [метрики обозревателя](app-insights-metrics-explorer.md). Если вы не видите того или иного типа приложения, выберите один из типов web hello для веб-страниц.
* **Группа ресурсов** — удобный способ для управления свойствами наподобие [контроля доступа](app-insights-resources-roles-access-control.md). Для разработки, тестирования и эксплуатации можно использовать отдельные группы ресурсов.
* **Подписка** представляет собой учетную запись для оплаты в Azure.
* **Расположение** – это место, в котором мы храним ваши данные. На данном этапе его нельзя изменить. 
* **Добавить toodashboard** помещает плитки быстрого доступа для ресурса на Azure домашней страницы. 

Создание ресурса hello занимает несколько секунд. Как только ресурс будет создан, появится предупреждение.

(Можно написать [сценарий PowerShell](app-insights-powershell-script-create-resource.md) toocreate ресурс автоматически.)

### <a name="getting-hello-instrumentation-key"></a>Получение ключа инструментирования hello
ключ инструментирования Hello идентифицирует созданный ресурс hello. 

![Установите Essentials, щелкните hello ключ инструментирования, CTRL + C](./media/app-insights-separate-resources/02-props.png)

Требуются ключи hello инструментирования из всех toowhich hello ресурсов приложения будет отправлять данные.

## <a name="filter-on-build-number"></a>Фильтрация по номеру сборки
При публикации новой версии приложения, будет необходимо toobe может tooseparate hello телеметрии из другой сборки.

Можно задать свойства версии приложения hello так, что позволяет фильтровать [поиска](app-insights-diagnostic-search.md) и [метрики explorer](app-insights-metrics-explorer.md) результаты.

![Фильтрация по свойству](./media/app-insights-separate-resources/050-filter.png)

Существует несколько разных способов задания свойства версии приложения hello.

* Напрямую:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Перенос эту строку в [инициализатора телеметрии](app-insights-api-custom-events-metrics.md#defaults) tooensure, все экземпляры TelemetryClient установлены постоянно.
* [ASP.NET] Версия набора hello в `BuildInfo.config`. веб-модуль Hello получат версии hello из узла BuildLabel hello. Включить этот файл в проект и запоминать tooset hello всегда Копировать свойства в обозревателе решений.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] Настройте автоматическое создание файла BuildInfo.config в MSBuild. toodo это, добавьте несколько строк tooyour `.csproj` файла:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Будет создан файл с именем *yourProjectName*. Hello BuildInfo.config. процесс публикации переименовывает его tooBuildInfo.config.

    Метка сборки Hello содержит заполнитель (AutoGen_), при построении с помощью Visual Studio. Однако при построении с помощью MSBuild, он заполняется hello правильный номер версии.

    как версии набора hello tooallow номера версий MSBuild toogenerate `1.0.*` в AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Отслеживание версии и выпуска
версия приложения hello tootrack, убедитесь, что `buildinfo.config` создается процессом Microsoft Build Engine. Добавьте в CSPROJ-файл:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Когда в нем сведения сборки hello, веб-модуля hello Application Insights автоматически добавляет **версия приложения** как элемент свойства tooevery телеметрии. Позволяющее вам toofilter версии при выполнении [диагностики выполняет](app-insights-diagnostic-search.md), или если вы [Просмотр метрик](app-insights-metrics-explorer.md).

Тем не менее Обратите внимание, что номер версии сборки hello формируется только hello Microsoft Build Engine, не разработчиком hello построения в Visual Studio.

### <a name="release-annotations"></a>Примечания к выпуску
Если вы используете Visual Studio Team Services, вы можете [получить маркер заметки](app-insights-annotations.md) добавляется tooyour диаграммы, при выпуске новой версии. Следующие изображения Hello показано, как выглядит этот маркер.

![Снимок экрана, где показана диаграмма с примером заметки о новом выпуске](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Дальнейшие действия

* [Monitor multi-component applications with Application Insights (preview)](app-insights-monitor-multi-role-apps.md) (Мониторинг приложений с несколькими компонентами с помощью Application Insights (предварительная версия))
* [Создание toodistinguish инициализатора телеметрии A | Варианты B](app-insights-api-filtering-sampling.md#add-properties)
