---
title: "aaaAzure Application Insights поддерживает несколько компонентов, микрослужбами и контейнеры | Документы Microsoft"
description: "Мониторинг приложений, которые состоят из нескольких компонентов или ролей, для получения данных производительности и использования."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Мониторинг приложений с несколькими компонентами с помощью Application Insights (предварительная версия)

Вы можете отслеживать приложения, которые состоят из нескольких серверных компонентов, ролей или служб, с помощью [Azure Application Insights](app-insights-overview.md). Hello работоспособности компонентов hello и hello связи между ними, отображаются на карте одного приложения. Вы можете отслеживать отдельные операции для нескольких компонентов за счет автоматической корреляции HTTP. Диагностика контейнеров может быть интегрирована и сопоставлена с телеметрией приложения. Используйте один ресурс Application Insights для всех компонентов приложения hello. 

![Схема сопоставления многокомпонентных приложений](./media/app-insights-monitor-multi-role-apps/app-map.png)

Мы используем «компонент» здесь toomean любой работающую часть большого приложения. Например типичный бизнес-приложений может состоять из клиентского кода, выполняемого в веб-браузерами, идет речь tooone или дополнительные веб-приложения служб, которые в свою очередь, используют обратно завершения службы. Компоненты сервера может быть размещена локально на в облаке hello или может быть Azure рабочих и веб-ролей может работать в контейнерах, например Docker или Service Fabric. 

### <a name="sharing-a-single-application-insights-resource"></a>Совместное использование одного ресурса Application Insights 

Hello ключа методикой является toosend телеметрии из вашего приложения toohello каждый компонент одного ресурса Application Insights, но использование hello `cloud_RoleName` свойство toodistinguish компоненты при необходимости. пакет SDK для Application Insights Hello добавляет hello `cloud_RoleName` порождение свойство toohello телеметрии компонентов. Например, добавление hello SDK, имя веб-сайта или toohello имя службы роли `cloud_RoleName` свойство. Это значение можно переопределить с помощью telemetryinitializer. Сопоставления приложения Hello использует hello `cloud_RoleName` свойство tooidentify hello компоненты на карте hello.

Дополнительные сведения о том, как переопределить hello `cloud_RoleName` см. свойство [добавлять свойства: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

В некоторых случаях это может быть неприемлемо, и могут предпочесть toouse отдельные ресурсы для разных групп компонентов. Например может потребоваться toouse различные ресурсы для управления или составления счетов. Использование разных ресурсах означает, что вы не видите все компоненты hello, отображаемые на карте одного приложения; и что не удается запросить во всех компонентах в [Analytics](app-insights-analytics.md). Также имеется tooset hello отдельных ресурсов.

С этой оговорка мы предположим, в hello остальной части этого документа, вы должны toosend данные из нескольких компонентов tooone ресурс Application Insights.

## <a name="configure-multi-component-applications"></a>Настройка многокомпонентных приложений

сопоставление tooget многокомпонентные приложения, вы должны tooachieve этих целей:

* **Установить последнюю предварительную hello** пакета Application Insights в каждом компоненте приложения hello. 
* **Совместно использовать один ресурс Application Insights** для всех hello компоненты приложения.
* **Включить сопоставление нескольких ролей приложения** в колонке hello предварительного просмотра.

Настройте каждый компонент приложения с помощью hello соответствующий метод для его типа. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md)).

### <a name="1-install-hello-latest-pre-release-package"></a>1. Установите последнюю версию пакета предварительного выпуска hello

Обновление или установка пакетов аналитики приложений hello в проекте hello для каждого компонента сервера. Если вы используете Visual Studio:

1. Щелкните проект правой кнопкой мыши и выберите **Управление пакетами Nuget**. 
2. Выберите параметр **Включить предварительные выпуски**.
3. Если пакеты Application Insights отображаются в списке обновлений, выберите их. 

    В противном случае — найти и установить соответствующий пакет hello:
    
    * Microsoft.ApplicationInsights.WindowsServer;
    * Microsoft.ApplicationInsights.ServiceFabric — для компонентов, выполняющихся в качестве гостевых исполняемых файлов, и контейнеров Docker, работающих в приложениях Service Fabric;
    * Microsoft.ApplicationInsights.ServiceFabric.Native — для надежных служб в приложениях ServiceFabric;
    * Microsoft.ApplicationInsights.Kubernetes — для компонентов, выполняемых в Docker на Kubernetes.

### <a name="2-share-a-single-application-insights-resource"></a>2. Настройка совместного использования одного ресурса Application Insights

* В Visual Studio щелкните проект правой кнопкой мыши и выберите **Настроить Application Insights** или **Application Insights > Настроить**. Для первого проекта hello используйте мастер hello toocreate ресурс Application Insights. Для последующих проектов выберите hello того же ресурса.
* Если вы не видите меню Application Insights, выполните настройку вручную:

   1. В [портал Azure](https://portal,azure.com), открыть ресурс Application Insights hello уже создан для другого компонента.
   2. В колонке Обзор hello, вкладку Привет открыть Essentials раскрывающегося списка и копирования hello **ключ инструментирования.**
   3. В своем проекте откройте файл ApplicationInsights.config и вставьте: `<InstrumentationKey>your copied key</InstrumentationKey>`.

![Скопируйте файл .config toohello ключа инструментирования hello](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Включение схемы сопоставления приложений с несколькими ролями

Hello портал Azure откройте hello ресурса для приложения. В колонке hello предварительные версии, включите *карты несколькими ролями приложения*.

### <a name="4-enable-docker-metrics-optional"></a>4. Включение метрик Docker (необязательно) 

Если компонент работает в Docker, размещенной на виртуальной Машине Windows Azure, вы можете собирать дополнительные метрики из контейнера hello. Вставьте в файл конфигурации [системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md) следующий код:

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Использование компонентов tooseparate cloud_RoleName

Hello `cloud_RoleName` свойство имеет вложенные tooall телеметрии. Он идентифицирует компонент hello - hello роли или службы -, рассчитанная телеметрии hello. (Это не Здравствуйте таким же, как cloud_RoleInstance, который отделяет идентичные роли, которые выполняются параллельно на несколько серверных процессов или машины.)

На портале hello можно отфильтровать или сегментирования телеметрии с помощью этого свойства. В этом примере hello сбоев колонка находится отфильтрованные tooshow только сведения из hello интерфейсный веб-службы, отфильтровывая сбоев из внутренних CRM API hello:

![Диаграмма метрик, сегментированная по имени облачной роли](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Отслеживание операций между компонентами

Можно выполнить трассировку из одного компонента tooanother, hello вызовы, сделанные во время обработки отдельной операции.


![Отображение данных телеметрии для операции](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Пролистайте список коррелированные tooa телеметрии для этой операции через hello интерфейсного веб-сервера и внутреннего интерфейса API hello:

![Поиск по компонентам](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Дальнейшие действия

* [Отделение телеметрии стадий разработки, тестирования и эксплуатации](app-insights-separate-resources.md)
