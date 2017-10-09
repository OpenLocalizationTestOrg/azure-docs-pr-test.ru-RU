---
title: "Статистическая обработка событий структуры службы с помощью системы диагностики Windows Azure aaaAzure | Документы Microsoft"
description: "Ознакомьтесь со сведениями об агрегации и сборе событий с использованием WAD для мониторинга и диагностики кластеров Azure Service Fabric."
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
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Агрегирование и сбор событий с помощью системы диагностики Microsoft Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

При запуске кластера с Azure Service Fabric это журналы hello смысл toocollect со всех узлов hello в центральном расположении. Наличие журналы hello в центральном расположении, помогает выполнить анализ и устранение проблем в кластере, или в hello приложений и служб, работающих в этом кластере.

Собирать журналы и tooupload один из способов — расширение диагностики Windows Azure (WAD) toouse hello, передает журналы tooAzure хранилища, которое имеет hello параметр toosend журналы tooAzure Application Insights или концентраторов событий. Можно также использовать внешний процесс tooread hello событий из хранилища и поместите их в платформа продуктом анализа [аналитики журнала OMS](../log-analytics/log-analytics-service-fabric.md) или другим решением для синтаксического анализа журнала.

## <a name="prerequisites"></a>Предварительные требования
Эти средства, используемые tooperform некоторые операции hello в этом документе:

* [Диагностика Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (о tooAzure облачные службы, но имеет хорошее сведения и примеры)
* [Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Клиент Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Шаблон Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Источники журналов и событий

### <a name="service-fabric-platform-events"></a>События платформы Service Fabric
Как было сказано в [в этой статье](service-fabric-diagnostics-event-generation-infra.md), Service Fabric задает вы с несколько каналов ведения журнала out of box, из которой hello следующие каналы легко настраивать WAD toosend наблюдение и диагностику tooa хранения таблицы данных или Где-нибудь ещё:
  * События операционного канала: операции более высокого уровня, которые hello выполняет платформы Service Fabric. Некоторые примеры: создание приложений и служб, изменение состояния узлов и сведения об обновлении. Они передаются в рамках журнала трассировки событий для Windows (ETW).
  * [События модели программирования на основе Reliable Actors](service-fabric-reliable-actors-diagnostics.md).
  * [События модели программирования на основе Reliable Services](service-fabric-reliable-services-diagnostics.md).

### <a name="application-events"></a>События приложения
 События, переданные из кода вашего приложения и службы и записывается с помощью вспомогательного класса EventSource hello указан в hello шаблонов Visual Studio. Дополнительные сведения о как toowrite EventSource журналы из приложения в разделе [монитора и диагностики служб в случае установки локального компьютера разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Развертывание расширения диагностики hello
Первым шагом Hello в сбор журналов является расширение диагностики toodeploy hello в каждой из виртуальных машин hello в кластер Service Fabric hello. Hello расширения диагностики собирает журналы на каждой виртуальной Машине и отправляет их toohello учетной записи хранения, указанной вами. шаги Hello немного отличаться в зависимости от hello портал Azure или диспетчера ресурсов Azure. Hello действия также различаются в зависимости от возможность развертывания hello является частью создания кластера или кластера, который уже существует. Давайте рассмотрим hello действия для каждого сценария.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Развертывание расширения диагностики hello в процессе создания кластера через портал Azure
toodeploy hello диагностики расширения toohello виртуальных машин в кластере hello в процессе создания кластера, используйте панель параметров диагностики hello, показано в следующих hello изображение — убедитесь, что диагностики слишком**на** (hello по умолчанию) . После создания кластера hello, нельзя изменить эти параметры с помощью портала hello.

![Параметры диагностики Azure hello портала для создания кластера](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

При создании кластера с помощью портала hello, настоятельно рекомендуется загрузить шаблон hello **до нажатия кнопки ОК** toocreate hello кластера. Дополнительные сведения приведены слишком[настроить кластер Service Fabric с помощью шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Потребуется hello шаблон toomake изменений более поздней версии, так как не удается внести некоторые изменения с помощью портала hello.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Развертывание расширения диагностики hello в процессе создания кластера с помощью диспетчера ресурсов Azure
toocreate кластера с помощью диспетчера ресурсов необходимо tooadd hello диагностики конфигурации JSON toohello полного кластера шаблона диспетчера ресурсов перед созданием кластера hello. Мы предоставляем образец шаблона диспетчера ресурсов кластера пяти ВМ с конфигурацией диагностики добавлены tooit как часть наши примеры шаблона диспетчера ресурсов. Его можно просматривать в этом месте в коллекции примеров Azure hello: [пяти узла кластера с образцом шаблона диспетчера ресурсов диагностики](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

параметры диагностики toosee hello в hello шаблона диспетчера ресурсов, откройте hello azuredeploy.json файл и выполните поиск **IaaSDiagnostics**. toocreate кластера с помощью этого шаблона, выберите hello **развертывание tooAzure** кнопка доступны по ссылке на предыдущую hello.

Можно также загрузить образец hello диспетчера ресурсов, внести изменения tooit и создайте кластер с hello измененный шаблон с помощью hello `New-AzureRmResourceGroupDeployment` команду в окне Azure PowerShell. См. следующий код для hello параметры, которые передаются в команде toohello hello. Подробные сведения о том, как группировать toodeploy ресурса с помощью PowerShell. в статье hello [развертывания группы ресурсов с помощью шаблона Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Развертывание существующего кластера расширения диагностики tooan hello
При наличии существующего кластера, у которого нет диагностики развертывания или вы хотите toomodify существующей конфигурации, можно добавить или обновить ее. Изменение шаблона диспетчера ресурсов hello, используемые toocreate hello существующего кластера или загрузить шаблон hello из портала hello, как описано выше. Измените файл template.json hello, выполнив следующие задачи hello.

Добавьте новый шаблон toohello ресурсов хранения, добавив раздел ресурсов toohello.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Добавьте параметры toohello статьи сразу после определения учетной записи хранилища hello, между `supportLogStorageAccountName` и `vmNodeType0Name`. Замените текст заполнителя hello *здесь имя учетной записи хранения* с именем hello hello учетной записи хранения.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Обновите hello `VirtualMachineProfile` раздел файла template.json hello, добавив следующий код в пределах массива расширения hello hello. Быть убедиться, что tooadd запятая в начале hello или в конце hello, в зависимости от того, куда вставляется.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

После изменения файла template.json hello, как описано, повторная публикация шаблона диспетчера ресурсов hello. Если шаблон hello был экспортирован, выполняется файл deploy.ps1 hello опубликует hello шаблона. После развертывания убедитесь, что параметр **ProvisioningState** имеет значение **Succeeded**.

## <a name="collect-health-and-load-events"></a>Сбор событий работоспособности и нагрузки

Начиная с выпуска hello 5.4 Service Fabric, работоспособности и загрузка метрики события, доступные для коллекции. Эти события отражают события, создаваемые системой hello или код с помощью работоспособности hello или загрузить отчетов интерфейсы API, такие как [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) или [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Это обеспечивает статистическую обработку и просмотр состояния работоспособности системы с течением временем, а также оповещение на основе событий работоспособности или нагрузки. Эти события в окне просмотра событий диагностики в Visual Studio добавьте tooview «Microsoft-ServiceFabric:4:0x4000000000000008» toohello список поставщиков трассировки событий Windows.

события toocollect hello, изменить tooinclude шаблона диспетчера ресурсов hello

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Сбор событий обратного прокси-сервера

Начиная с выпуска hello 5.7 Service Fabric [обратный прокси-сервер](service-fabric-reverseproxy.md) события, доступные для коллекции.
Обратный прокси-сервер передает события в два канала, одна ошибка содержащего отражения события ошибок при обработке запроса и hello других одна из которых содержит подробные события, о всех hello запросов, обрабатываемых в hello обратного прокси-сервера. 

1. Собирать события ошибок: tooview, добавьте эти события в окне просмотра событий диагностики в Visual Studio «Microsoft-ServiceFabric:4:0x4000000000000010» toohello список поставщиков трассировки событий Windows.
события hello toocollect из Azure кластеров изменить tooinclude шаблона диспетчера ресурсов hello

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Собирает события обработки запроса: В Visual Studio диагностические средства просмотра событий, запись hello Microsoft ServiceFabric update в слишком hello список поставщиков трассировки событий Windows "Microsoft-ServiceFabric:4:0x4000000000000020».
Для кластеров Azure Service Fabric измените tooinclude шаблона диспетчера ресурсов hello

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> Рекомендуется toojudiciously включить сбор событий из этого канала, как это собирает весь трафик через hello обратного прокси-сервера и может привести к быстрому потреблению емкости хранилища.

Для кластеров Azure Service Fabric hello события из всех узлов hello собираются и статистически hello SystemEventTable.
Подробные сведения об устранении hello события обратного прокси-сервера, описаны hello [руководство по диагностике обратного прокси-сервера](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Сбор из новых каналов EventSource

журналы toocollect tooupdate диагностики из новых каналов EventSource, представляющие новое приложение, которое скоро будет toodeploy, выполнить hello же действия как описано выше для hello Настройка диагностики для существующего кластера.

Обновить hello `EtwEventSourceProviderConfiguration` раздела записи tooadd hello template.json файлов для обновления hello новых EventSource каналов перед применением hello конфигурации с помощью hello `New-AzureRmResourceGroupDeployment` команды PowerShell. Имя источника события hello Hello определяется как часть кода в файле hello ServiceEventSource.cs, созданный средой Visual Studio.

Например если источник события с именем My Eventsource, добавьте следующую hello tooplace коды событий из Мой Eventsource в таблицу с именем MyDestinationTableName hello.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

счетчики производительности toocollect или журналы событий изменения шаблона диспетчера ресурсов hello с помощью hello примеры, приведенные в [Создание виртуальной машины Windows с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Затем повторно опубликуйте hello шаблона диспетчера ресурсов.

## <a name="collect-performance-counters"></a>Сбор данных счетчиков производительности

метрики производительности toocollect из кластера, добавьте tooyour счетчики производительности hello «DiagnosticMonitorConfiguration WadCfg >» в hello шаблона диспетчера ресурсов для кластера. Дополнительные сведения о счетчиках производительности Service Fabric, которые мы рекомендуем собирать, см. в [этой статье](service-fabric-diagnostics-event-generation-perf.md).

Например, здесь мы устанавливаем один счетчик производительности, выборка каждые 15 секунд (это может быть изменено и следующим hello формат «PT\<время >\<единицы >», к примеру, PT3M бы образец каждые три минуты) и передать toohello Таблица соответствующих дисковых раз в минуту.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Если вы используете приемник Application Insights, как описано в разделе "hello" ниже и хотите эти показатели tooshow вверх в Application Insights, внесите убедиться, что имя приемника hello tooadd в разделе «приемники» hello, как показано выше. Кроме того, рассмотрите возможность создания toosend отдельную таблицу счетчиками производительности, поэтому они не заполнять out hello Здравствуйте, данные поступают из других каналов ведения журнала включен.


## <a name="send-logs-tooapplication-insights"></a>Отправить журналы аналитики tooApplication

Отправка данных мониторинга и диагностики, tooApplication аналитики (AI) может выполняться как часть конфигурации WAD hello. Если вы решите toouse AI для анализа событий и визуализации, чтение [анализ событий и визуализации с помощью Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset копирование приемник AI как часть «WadCfg».

## <a name="next-steps"></a>Дальнейшие действия

После правильной настройки диагностики Azure, вы увидите данные в таблицах хранилища из hello трассировки событий Windows и журналы EventSource. При выборе toouse OMS Kibana или любые другие данные аналитики и визуализации платформы, которая непосредственно не настроены на hello шаблона диспетчера ресурсов, внести в hello данные из этих таблиц хранилища, что tooset копирование hello платформа tooread ваш выбор. Сделать это для OMS несложно. Дополнительные сведения см. в статье [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md) (Анализ событий и журналов с помощью OMS). Application Insights бит в этом смысле особым случаем, поскольку его можно настроить как часть конфигурации расширения диагностики hello, таким образом обратитесь toohello [соответствующей статье](service-fabric-diagnostics-event-analysis-appinsights.md) при выборе toouse AI.

>[!NOTE]
>В данный момент нет способа toofilter или очистки hello событий, отправляемых toohello таблицы. Если не реализовать tooremove обработки событий, из таблицы hello, таблица hello останется toogrow. В настоящее время является примером службы очистки данных, работающей в hello [образца контрольного](https://github.com/Azure-Samples/service-fabric-watchdog-service), и рекомендуется записать его, если не дает веские причины для вас toostore журналы за период времени 30 или 90 дней.

* [Узнайте, как счетчики производительности toocollect или журналы с помощью hello расширения диагностики](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Анализ событий и визуализация с помощью Application Insights)
* [Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Анализ событий и журналов с помощью OMS)