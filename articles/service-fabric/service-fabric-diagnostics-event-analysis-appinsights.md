---
title: "Анализ событий структуры службы с помощью Application Insights aaaAzure | Документы Microsoft"
description: "Ознакомьтесь со сведениями о визуализации и анализе событий с использованием Application Insights для мониторинга и диагностики кластеров Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Анализ и визуализация событий с помощью Application Insights

Azure Application Insights — это расширяемая платформа для отслеживания и диагностики приложений. Она включает в себя эффективное средство аналитики и запросов, настраиваемую панель мониторинга, визуализации и дополнительные параметры, включая автоматическое оповещение. Это hello, рекомендуется использовать платформу для наблюдения и диагностики для приложения Service Fabric и службы.

## <a name="setting-up-application-insights"></a>Настройка Application Insights

### <a name="creating-an-ai-resource"></a>Создание ресурса Application Insights

ресурс toocreate AI, головной через toohello Azure Marketplace и выполните поиск «Application Insights». Оно должно отображаться hello первое решение (он находится в категории «Mobile Web +»). Нажмите кнопку **создать** при просмотре ресурса hello (Убедитесь, что путь к соответствует hello изображении ниже).

![Новый ресурс Application Insights](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Необходимо будет toofill некоторые сведения tooprovision hello ресурс правильно. В hello *тип приложения* поля, используйте «Веб-приложение ASP.NET» при использовании любого из Service Fabric модели программирования или публикации кластера toohello приложений .NET. Выберите значение "Общее", если вы будете развертывать гостевые исполняемые файлы и контейнеры. В общем случае tookeep «Веб-приложение ASP.NET» по умолчанию toousing варианты откройте в будущем hello. Имя Hello работает tooyour предпочтений и группы ресурсов hello и подписки, возможность изменения после развертывания hello ресурса. Мы рекомендуем ресурса AI возможности hello же группе ресурсов кластера. Если вам требуются дополнительные сведения, ознакомьтесь с разделом [Создание ресурса Application Insights](../application-insights/app-insights-create-new-resource.md).

Требуется ключ инструментирования AI hello tooconfigure AI со средством статистической обработки событий. После настройки ресурса AI (занимает несколько минут после проверки hello развертывания), перейдите tooit и найти hello **свойства** раздел на панели навигации слева hello. Откроется новая колонка с *ключом инструментирования*. Если требуется toochange hello подписка или группа ресурсов для ресурса hello, это можно сделать здесь также.

### <a name="configuring-ai-with-wad"></a>Настройка Application Insights с помощью WAD

Существует два основных способа toosend данные из WAD tooAzure AI, что можно сделать, добавив AI приемник toohello конфигурация WAD, как описано в [в этой статье](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Добавление ключа инструментирования Application Insights при создании кластера на портале Azure

![Добавление AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

При создании кластера, если Диагностика включен «», tooenter необязательное поле отображается ключ инструментирования аналитики приложений. При вставке здесь вашей IKey AI hello AI приемник будет автоматически настроена для hello шаблона диспетчера ресурсов, используемых toodeploy кластера.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Добавить шаблон диспетчера ресурсов toohello приемников AI hello

В hello «WadCfg «hello шаблона диспетчера ресурсов Добавьте «Приемник», включая hello, следующие два изменения:

1. Добавьте конфигурацию приемник hello:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Включите hello приемник в hello DiagnosticMonitorConfiguration, добавление hello, следующей строкой в «DiagnosticMonitorConfiguration» hello «WadCfg»:

    ```json
    "sinks": "applicationInsights"
    ```

В обоих фрагментах кода hello выше hello приемник hello используется toodescribe было имя «applicationInsights». Это не является обязательным, и при условии, что имя hello приемника hello включается в «приемники», можно задать строку tooany имени hello.

В настоящее время журналов из кластера hello отображаются как трассировки в средстве просмотра журналов в AI. Поскольку большинство hello трассировок, поступающих из платформы hello имеют уровень «Информационный», можно также рассмотреть изменение hello приемник конфигурации tooonly отправки журналов типа «Критическое» или «Ошибка». Это можно сделать путем добавления приемника tooyour «Каналы», как показано в [в этой статье](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>При использовании неверные IKey AI на портале или в шаблон диспетчера ресурсов, необходимо будет toomanually изменение ключа hello и обновление кластера hello / выполнить его повторное развертывание. 

### <a name="configuring-ai-with-eventflow"></a>Настройка Application Insights с помощью EventFlow

При использовании EventFlow tooaggregate события, убедитесь, что hello tooimport `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`пакет NuGet. Hello следующие имеет состава hello toobe *выводит* раздел hello *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Внесите изменения hello требуется убедиться, что toomake фильтрах, а также включать другие входные данные (вместе с соответствующими пакетами NuGet).

## <a name="aisdk"></a>AI.SDK

Обычно рекомендуется toouse EventFlow и WAD как решения статистической обработки, так как они позволяют более удобным toodiagnostics подход и наблюдения, т. е. Если требуется toochange вашей выходные данные EventFlow, требуется не фактические изменения tooyour инструментирование, просто файл конфигурации tooyour простое изменение. Если, тем не менее, решить tooinvest с помощью Application Insights и не являются скорее всего toochange tooa другой платформы, следует ознакомиться с помощью аналитики Активов в новый пакет SDK для статистической обработки событий и отправки их tooAI. Это означает, что больше не будет tooconfigure EventFlow toosend вашей tooAI данных, но вместо этого будет установить пакет Service Fabric NuGet hello ApplicationInsight. Можно найти сведения о пакете hello [здесь](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Поддержка Application Insights Микрослужбами и контейнеры](https://azure.microsoft.com/app-insights-microservices/) показаны некоторые новые функции hello, над которыми ведется работа на (по-прежнему присутствующие в бета-версия), которой позволяют toohave всестороннее out of box параметры мониторинга с помощью аналитики Активов. Эти условия включают отслеживание зависимостей (используется для построения служб и приложений в кластере и hello обмен данными между ними AppMap) и более корреляцию трассировок, поступающих от служб (помогает в более точное проблемы в hello рабочий процесс приложения или службы).

Если разработка в .NET и, вероятно, с помощью некоторых моделей программирования Service Fabric и являются пойти toouse AI качестве платформы для визуализации и анализа событий и журналов, рекомендуется перейти через hello AI SDK для маршрута наблюдение и рабочий процесс диагностики. Чтение [это](../application-insights/app-insights-asp-net-more.md) и [это](../application-insights/app-insights-asp-net-trace-logs.md) tooget работу с помощью функции AI toocollect и отображения журналов.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Перемещение ресурса AI hello на портале Azure

После настройки аналитики Активов в качестве выходных данных для событий и журналов сведения должно быть запущено tooshow в ресурса AI через несколько минут. Перейдите ресурса AI toohello, которая перенаправит вас toohello AI панели мониторинга ресурсов. Нажмите кнопку **поиска** в hello AI задач toosee hello последние трассировки, которые он получил и может toofilter toobe через них.

*Обозреватель метрик* — это полезное средство для создания пользовательских панелей мониторинга на основе метрик, которые могут предоставляться приложениями, службами и кластером. В разделе [изучение метрики в Application Insights](../application-insights/app-insights-metrics-explorer.md) tooset копирование несколько диаграмм для текущего пользователя на основе hello данных собираются.

Щелкнув **Analytics** вы перейдете toohello приложения аналитика Analytics портал, где вы можете запрашивать события и трассировки с большей областью и дополнительные возможности. Дополнительные сведения см. в статье [Аналитика в Application Insights](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Дальнейшие действия

* [Настройка оповещений в AI](../application-insights/app-insights-alerts.md) toobe уведомления об изменениях в производительности или использования
* [Смарт-обнаружение в Application Insights](../application-insights/app-insights-proactive-diagnostics.md) выполняет упреждающее анализ телеметрии hello, отправляемых tooAI toowarn о потенциальных проблем с производительностью
