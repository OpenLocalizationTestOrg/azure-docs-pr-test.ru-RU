---
title: "aaaCollect журналы с помощью диагностики Azure | Документы Microsoft"
description: "В этой статье описывается, как tooset копирование toocollect диагностики Azure журналов из кластера Service Fabric, запущенных в Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Сбор журналов с помощью системы диагностики Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

При запуске кластера с Azure Service Fabric это журналы hello смысл toocollect со всех узлов hello в центральном расположении. Наличие журналы hello в центральном расположении, помогает выполнить анализ и устранение проблем в кластере, или в hello приложений и служб, работающих в этом кластере.

Собирать журналы и tooupload один из способов — расширение диагностики Azure toouse hello, какие передачи журналов tooAzure хранилища Azure Application Insights и концентраторов событий Azure. журналы Hello не окажется полезным непосредственно в хранилище или концентраторов событий. Однако вы можете использовать внешний процесс tooread hello событий из хранилища и поместите их в продукте [анализа журналов](../log-analytics/log-analytics-service-fabric.md) или другим решением для синтаксического анализа журнала. В [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) предоставляется с возможностью полного поиска по журналам и встроенной службой аналитики.

## <a name="prerequisites"></a>Предварительные требования
Используйте эти средства tooperform некоторые операции hello в этом документе:

* [Диагностика Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (о tooAzure облачные службы, но имеет хорошее сведения и примеры)
* [Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Клиент Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Шаблон Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Вы можете toocollect источников журнала
* **Журналы Service Fabric**: создается для hello платформы toostandard трассировки событий для Windows (ETW) и EventSource каналов. Журналы могут принадлежать к одному из следующих типов.
  * События операционного канала: журналы для операций, которые выполняет платформы Service Fabric hello. Некоторые примеры: создание приложений и служб, изменение состояния узлов и сведения об обновлении.
  * [События модели программирования на основе Reliable Actors](service-fabric-reliable-actors-diagnostics.md).
  * [События модели программирования на основе Reliable Services](service-fabric-reliable-services-diagnostics.md).
* **События приложения**: события, переданные из кода приложения службы и записывается с помощью вспомогательного класса EventSource hello, в Visual Studio шаблоны hello. Дополнительные сведения о как toowrite журналы из приложения в разделе [монитора и диагностики служб в случае установки локального компьютера разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Развертывание расширения диагностики hello
Первым шагом Hello в сбор журналов является расширение диагностики toodeploy hello в каждой из виртуальных машин hello в кластер Service Fabric hello. Hello расширения диагностики собирает журналы на каждой виртуальной Машине и отправляет их toohello учетной записи хранения, указанной вами. шаги Hello немного отличаться в зависимости от hello портал Azure или диспетчера ресурсов Azure. Hello действия также различаются в зависимости от возможность развертывания hello является частью создания кластера или кластера, который уже существует. Давайте рассмотрим hello действия для каждого сценария.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Развертывание расширения диагностики hello в процессе создания кластера через портал hello
toodeploy hello диагностики расширения toohello виртуальных машин в кластере hello в процессе создания кластера, используйте панель параметров диагностики hello, показано в hello после изображения. tooenable сбора событий службы Reliable Actor или надежные службы, убедитесь, что диагностики слишком**на** (по умолчанию hello). После создания кластера hello, нельзя изменить эти параметры с помощью портала hello.

![Параметры диагностики Azure hello портала для создания кластера](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Здравствуйте, группа поддержки Azure *требует* поддержки журналы toohelp resolve запросы в службу поддержки, создаваемые. Эти журналы собираются в режиме реального времени и хранятся в одной из учетных записей хранилища hello, создан в группе ресурсов hello. параметры диагностики Hello настройте события уровня приложения. К этим событиям относятся [службы Reliable Actor](service-fabric-reliable-actors-diagnostics.md) события, [надежного обмена](service-fabric-reliable-services-diagnostics.md) события, а некоторые события toobe Service Fabric системного уровня, в хранилище Azure.

Продукты, такие как [Elasticsearch](https://www.elastic.co/guide/index.html) собственного процесса, можно получить из учетной записи хранения hello hello события. В данный момент нет способа toofilter или очистки hello событий, отправляемых toohello таблицы. Если не реализовать tooremove обработки событий, из таблицы hello, таблица hello останется toogrow.

При создании кластера с помощью портала hello, настоятельно рекомендуется загрузить шаблон hello **до нажатия кнопки ОК** toocreate hello кластера. Дополнительные сведения приведены слишком[настроить кластер Service Fabric с помощью шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Потребуется hello шаблон toomake изменений более поздней версии, так как не удается внести некоторые изменения с помощью портала hello.

Шаблоны можно экспортировать из hello портала с помощью hello следующие шаги. Тем не менее эти шаблоны может быть сложнее toouse, так как они могут иметь значения null, в которых отсутствуют необходимые сведения.

1. Откройте группу ресурсов.
2. Выберите **параметры** toodisplay hello параметры панели.
3. Выберите **развертываний** «журнал» toodisplay hello развертывания.
4. Выберите сведения о hello развертывания toodisplay hello развертывания.
5. Выберите **Экспорт шаблона** toodisplay hello шаблона панели.
6. Выберите **сохранить toofile** tooexport ZIP-файл, содержащий шаблон hello, параметры и файлы PowerShell.

После экспорта файлов hello необходимо toomake изменение. Измените файл parameters.json hello и удалите hello **adminPassword** элемента. Запрашивать пароль hello произойдет при запуске скрипта развертывания hello. При запуске скрипта развертывания hello, может потребоваться toofix значения null для параметров.

toouse hello загрузить tooupdate шаблона конфигурации:

1. Извлеките hello содержимое tooa папку на локальном компьютере.
2. Измените hello содержимое tooreflect hello новую конфигурацию.
3. Запустите PowerShell и изменить папку toohello, которую было извлечено содержимое hello.
4. Запустите **deploy.ps1** и введите идентификатор подписки hello, имя группы ресурсов hello (используйте hello же конфигурации hello tooupdate имени) и имя развертывания.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Развертывание расширения диагностики hello в процессе создания кластера с помощью диспетчера ресурсов Azure
toocreate кластера с помощью диспетчера ресурсов необходимо tooadd hello диагностики конфигурации JSON toohello полного кластера шаблона диспетчера ресурсов перед созданием кластера hello. Мы предоставляем образец шаблона диспетчера ресурсов кластера пяти ВМ с конфигурацией диагностики добавлены tooit как часть наши примеры шаблона диспетчера ресурсов. Его можно просматривать в этом месте в коллекции примеров Azure hello: [пяти узла кластера с образцом шаблона диспетчера ресурсов диагностики](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

параметры диагностики toosee hello в hello шаблона диспетчера ресурсов, откройте hello azuredeploy.json файл и выполните поиск **IaaSDiagnostics**. toocreate кластера с помощью этого шаблона, выберите hello **развертывание tooAzure** кнопка доступны по ссылке на предыдущую hello.

Можно также загрузить образец hello диспетчера ресурсов, внести изменения tooit и создайте кластер с hello измененный шаблон с помощью hello `New-AzureRmResourceGroupDeployment` команду в окне Azure PowerShell. См. следующий код для hello параметры, которые передаются в команде toohello hello. Подробные сведения о том, как группировать toodeploy ресурса с помощью PowerShell. в статье hello [развертывания группы ресурсов с помощью шаблона Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>События диагностики toocollect работоспособности и загрузка обновления

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Обновление toocollect диагностики и отправлять журналы из новых каналов EventSource
журналы toocollect tooupdate диагностики из новых каналов EventSource, представляющие новое приложение, которое скоро будет toodeploy, выполнять hello же шаги как hello [предыдущего раздела](#deploywadarm) для настройки диагностики для существующей кластер.

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

## <a name="next-steps"></a>Дальнейшие действия
какие события следует искать при диагностике проблем с toounderstand более подробно см. события диагностики hello для [службы Reliable Actor](service-fabric-reliable-actors-diagnostics.md) и [надежного обмена](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Связанные статьи
* [Узнайте, как счетчики производительности toocollect или журналы с помощью hello расширения диагностики](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Service Fabric Solution in Log Analytics](../log-analytics/log-analytics-service-fabric.md) (Решение Service Fabric в Log Analytics)

