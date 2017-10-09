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
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="67cb0-103">Агрегирование и сбор событий с помощью системы диагностики Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="67cb0-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67cb0-104">Windows</span><span class="sxs-lookup"><span data-stu-id="67cb0-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="67cb0-105">Linux</span><span class="sxs-lookup"><span data-stu-id="67cb0-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="67cb0-106">При запуске кластера с Azure Service Fabric это журналы hello смысл toocollect со всех узлов hello в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="67cb0-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="67cb0-107">Наличие журналы hello в центральном расположении, помогает выполнить анализ и устранение проблем в кластере, или в hello приложений и служб, работающих в этом кластере.</span><span class="sxs-lookup"><span data-stu-id="67cb0-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="67cb0-108">Собирать журналы и tooupload один из способов — расширение диагностики Windows Azure (WAD) toouse hello, передает журналы tooAzure хранилища, которое имеет hello параметр toosend журналы tooAzure Application Insights или концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="67cb0-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="67cb0-109">Можно также использовать внешний процесс tooread hello событий из хранилища и поместите их в платформа продуктом анализа [аналитики журнала OMS](../log-analytics/log-analytics-service-fabric.md) или другим решением для синтаксического анализа журнала.</span><span class="sxs-lookup"><span data-stu-id="67cb0-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67cb0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67cb0-110">Prerequisites</span></span>
<span data-ttu-id="67cb0-111">Эти средства, используемые tooperform некоторые операции hello в этом документе:</span><span class="sxs-lookup"><span data-stu-id="67cb0-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="67cb0-112">[Диагностика Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (о tooAzure облачные службы, но имеет хорошее сведения и примеры)</span><span class="sxs-lookup"><span data-stu-id="67cb0-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="67cb0-113">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="67cb0-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="67cb0-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="67cb0-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="67cb0-115">Клиент Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67cb0-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="67cb0-116">Шаблон Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67cb0-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="67cb0-117">Источники журналов и событий</span><span class="sxs-lookup"><span data-stu-id="67cb0-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="67cb0-118">События платформы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="67cb0-118">Service Fabric platform events</span></span>
<span data-ttu-id="67cb0-119">Как было сказано в [в этой статье](service-fabric-diagnostics-event-generation-infra.md), Service Fabric задает вы с несколько каналов ведения журнала out of box, из которой hello следующие каналы легко настраивать WAD toosend наблюдение и диагностику tooa хранения таблицы данных или Где-нибудь ещё:</span><span class="sxs-lookup"><span data-stu-id="67cb0-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="67cb0-120">События операционного канала: операции более высокого уровня, которые hello выполняет платформы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="67cb0-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="67cb0-121">Некоторые примеры: создание приложений и служб, изменение состояния узлов и сведения об обновлении.</span><span class="sxs-lookup"><span data-stu-id="67cb0-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="67cb0-122">Они передаются в рамках журнала трассировки событий для Windows (ETW).</span><span class="sxs-lookup"><span data-stu-id="67cb0-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * <span data-ttu-id="67cb0-123">[События модели программирования на основе Reliable Actors](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-123">[Reliable Actors programming model events](service-fabric-reliable-actors-diagnostics.md)</span></span>
  * <span data-ttu-id="67cb0-124">[События модели программирования на основе Reliable Services](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-124">[Reliable Services programming model events](service-fabric-reliable-services-diagnostics.md)</span></span>

### <a name="application-events"></a><span data-ttu-id="67cb0-125">События приложения</span><span class="sxs-lookup"><span data-stu-id="67cb0-125">Application events</span></span>
 <span data-ttu-id="67cb0-126">События, переданные из кода вашего приложения и службы и записывается с помощью вспомогательного класса EventSource hello указан в hello шаблонов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67cb0-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="67cb0-127">Дополнительные сведения о как toowrite EventSource журналы из приложения в разделе [монитора и диагностики служб в случае установки локального компьютера разработки](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="67cb0-128">Развертывание расширения диагностики hello</span><span class="sxs-lookup"><span data-stu-id="67cb0-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="67cb0-129">Первым шагом Hello в сбор журналов является расширение диагностики toodeploy hello в каждой из виртуальных машин hello в кластер Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="67cb0-130">Hello расширения диагностики собирает журналы на каждой виртуальной Машине и отправляет их toohello учетной записи хранения, указанной вами.</span><span class="sxs-lookup"><span data-stu-id="67cb0-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="67cb0-131">шаги Hello немного отличаться в зависимости от hello портал Azure или диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="67cb0-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="67cb0-132">Hello действия также различаются в зависимости от возможность развертывания hello является частью создания кластера или кластера, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="67cb0-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="67cb0-133">Давайте рассмотрим hello действия для каждого сценария.</span><span class="sxs-lookup"><span data-stu-id="67cb0-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="67cb0-134">Развертывание расширения диагностики hello в процессе создания кластера через портал Azure</span><span class="sxs-lookup"><span data-stu-id="67cb0-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="67cb0-135">toodeploy hello диагностики расширения toohello виртуальных машин в кластере hello в процессе создания кластера, используйте панель параметров диагностики hello, показано в следующих hello изображение — убедитесь, что диагностики слишком**на** (hello по умолчанию) .</span><span class="sxs-lookup"><span data-stu-id="67cb0-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="67cb0-136">После создания кластера hello, нельзя изменить эти параметры с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Параметры диагностики Azure hello портала для создания кластера](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="67cb0-138">При создании кластера с помощью портала hello, настоятельно рекомендуется загрузить шаблон hello **до нажатия кнопки ОК** toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="67cb0-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="67cb0-139">Дополнительные сведения приведены слишком[настроить кластер Service Fabric с помощью шаблона Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="67cb0-140">Потребуется hello шаблон toomake изменений более поздней версии, так как не удается внести некоторые изменения с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="67cb0-141">Развертывание расширения диагностики hello в процессе создания кластера с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="67cb0-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="67cb0-142">toocreate кластера с помощью диспетчера ресурсов необходимо tooadd hello диагностики конфигурации JSON toohello полного кластера шаблона диспетчера ресурсов перед созданием кластера hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="67cb0-143">Мы предоставляем образец шаблона диспетчера ресурсов кластера пяти ВМ с конфигурацией диагностики добавлены tooit как часть наши примеры шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67cb0-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="67cb0-144">Его можно просматривать в этом месте в коллекции примеров Azure hello: [пяти узла кластера с образцом шаблона диспетчера ресурсов диагностики](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="67cb0-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="67cb0-145">параметры диагностики toosee hello в hello шаблона диспетчера ресурсов, откройте hello azuredeploy.json файл и выполните поиск **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="67cb0-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="67cb0-146">toocreate кластера с помощью этого шаблона, выберите hello **развертывание tooAzure** кнопка доступны по ссылке на предыдущую hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="67cb0-147">Можно также загрузить образец hello диспетчера ресурсов, внести изменения tooit и создайте кластер с hello измененный шаблон с помощью hello `New-AzureRmResourceGroupDeployment` команду в окне Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67cb0-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="67cb0-148">См. следующий код для hello параметры, которые передаются в команде toohello hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="67cb0-149">Подробные сведения о том, как группировать toodeploy ресурса с помощью PowerShell. в статье hello [развертывания группы ресурсов с помощью шаблона Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="67cb0-150">Развертывание существующего кластера расширения диагностики tooan hello</span><span class="sxs-lookup"><span data-stu-id="67cb0-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="67cb0-151">При наличии существующего кластера, у которого нет диагностики развертывания или вы хотите toomodify существующей конфигурации, можно добавить или обновить ее.</span><span class="sxs-lookup"><span data-stu-id="67cb0-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="67cb0-152">Изменение шаблона диспетчера ресурсов hello, используемые toocreate hello существующего кластера или загрузить шаблон hello из портала hello, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="67cb0-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="67cb0-153">Измените файл template.json hello, выполнив следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="67cb0-154">Добавьте новый шаблон toohello ресурсов хранения, добавив раздел ресурсов toohello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="67cb0-155">Добавьте параметры toohello статьи сразу после определения учетной записи хранилища hello, между `supportLogStorageAccountName` и `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="67cb0-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="67cb0-156">Замените текст заполнителя hello *здесь имя учетной записи хранения* с именем hello hello учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="67cb0-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

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
<span data-ttu-id="67cb0-157">Обновите hello `VirtualMachineProfile` раздел файла template.json hello, добавив следующий код в пределах массива расширения hello hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="67cb0-158">Быть убедиться, что tooadd запятая в начале hello или в конце hello, в зависимости от того, куда вставляется.</span><span class="sxs-lookup"><span data-stu-id="67cb0-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="67cb0-159">После изменения файла template.json hello, как описано, повторная публикация шаблона диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="67cb0-160">Если шаблон hello был экспортирован, выполняется файл deploy.ps1 hello опубликует hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="67cb0-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="67cb0-161">После развертывания убедитесь, что параметр **ProvisioningState** имеет значение **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="67cb0-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="67cb0-162">Сбор событий работоспособности и нагрузки</span><span class="sxs-lookup"><span data-stu-id="67cb0-162">Collect health and load events</span></span>

<span data-ttu-id="67cb0-163">Начиная с выпуска hello 5.4 Service Fabric, работоспособности и загрузка метрики события, доступные для коллекции.</span><span class="sxs-lookup"><span data-stu-id="67cb0-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="67cb0-164">Эти события отражают события, создаваемые системой hello или код с помощью работоспособности hello или загрузить отчетов интерфейсы API, такие как [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) или [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="67cb0-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="67cb0-165">Это обеспечивает статистическую обработку и просмотр состояния работоспособности системы с течением временем, а также оповещение на основе событий работоспособности или нагрузки.</span><span class="sxs-lookup"><span data-stu-id="67cb0-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="67cb0-166">Эти события в окне просмотра событий диагностики в Visual Studio добавьте tooview «Microsoft-ServiceFabric:4:0x4000000000000008» toohello список поставщиков трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="67cb0-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="67cb0-167">события toocollect hello, изменить tooinclude шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="67cb0-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

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

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="67cb0-168">Сбор событий обратного прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="67cb0-168">Collect reverse proxy events</span></span>

<span data-ttu-id="67cb0-169">Начиная с выпуска hello 5.7 Service Fabric [обратный прокси-сервер](service-fabric-reverseproxy.md) события, доступные для коллекции.</span><span class="sxs-lookup"><span data-stu-id="67cb0-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="67cb0-170">Обратный прокси-сервер передает события в два канала, одна ошибка содержащего отражения события ошибок при обработке запроса и hello других одна из которых содержит подробные события, о всех hello запросов, обрабатываемых в hello обратного прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="67cb0-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="67cb0-171">Собирать события ошибок: tooview, добавьте эти события в окне просмотра событий диагностики в Visual Studio «Microsoft-ServiceFabric:4:0x4000000000000010» toohello список поставщиков трассировки событий Windows.</span><span class="sxs-lookup"><span data-stu-id="67cb0-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="67cb0-172">события hello toocollect из Azure кластеров изменить tooinclude шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="67cb0-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

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

2. <span data-ttu-id="67cb0-173">Собирает события обработки запроса: В Visual Studio диагностические средства просмотра событий, запись hello Microsoft ServiceFabric update в слишком hello список поставщиков трассировки событий Windows "Microsoft-ServiceFabric:4:0x4000000000000020».</span><span class="sxs-lookup"><span data-stu-id="67cb0-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="67cb0-174">Для кластеров Azure Service Fabric измените tooinclude шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="67cb0-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

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
> <span data-ttu-id="67cb0-175">Рекомендуется toojudiciously включить сбор событий из этого канала, как это собирает весь трафик через hello обратного прокси-сервера и может привести к быстрому потреблению емкости хранилища.</span><span class="sxs-lookup"><span data-stu-id="67cb0-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="67cb0-176">Для кластеров Azure Service Fabric hello события из всех узлов hello собираются и статистически hello SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="67cb0-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="67cb0-177">Подробные сведения об устранении hello события обратного прокси-сервера, описаны hello [руководство по диагностике обратного прокси-сервера](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="67cb0-178">Сбор из новых каналов EventSource</span><span class="sxs-lookup"><span data-stu-id="67cb0-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="67cb0-179">журналы toocollect tooupdate диагностики из новых каналов EventSource, представляющие новое приложение, которое скоро будет toodeploy, выполнить hello же действия как описано выше для hello Настройка диагностики для существующего кластера.</span><span class="sxs-lookup"><span data-stu-id="67cb0-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="67cb0-180">Обновить hello `EtwEventSourceProviderConfiguration` раздела записи tooadd hello template.json файлов для обновления hello новых EventSource каналов перед применением hello конфигурации с помощью hello `New-AzureRmResourceGroupDeployment` команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67cb0-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="67cb0-181">Имя источника события hello Hello определяется как часть кода в файле hello ServiceEventSource.cs, созданный средой Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67cb0-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="67cb0-182">Например если источник события с именем My Eventsource, добавьте следующую hello tooplace коды событий из Мой Eventsource в таблицу с именем MyDestinationTableName hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="67cb0-183">счетчики производительности toocollect или журналы событий изменения шаблона диспетчера ресурсов hello с помощью hello примеры, приведенные в [Создание виртуальной машины Windows с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67cb0-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="67cb0-184">Затем повторно опубликуйте hello шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67cb0-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="67cb0-185">Сбор данных счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="67cb0-185">Collect Performance Counters</span></span>

<span data-ttu-id="67cb0-186">метрики производительности toocollect из кластера, добавьте tooyour счетчики производительности hello «DiagnosticMonitorConfiguration WadCfg >» в hello шаблона диспетчера ресурсов для кластера.</span><span class="sxs-lookup"><span data-stu-id="67cb0-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="67cb0-187">Дополнительные сведения о счетчиках производительности Service Fabric, которые мы рекомендуем собирать, см. в [этой статье](service-fabric-diagnostics-event-generation-perf.md).</span><span class="sxs-lookup"><span data-stu-id="67cb0-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="67cb0-188">Например, здесь мы устанавливаем один счетчик производительности, выборка каждые 15 секунд (это может быть изменено и следующим hello формат «PT\<время >\<единицы >», к примеру, PT3M бы образец каждые три минуты) и передать toohello Таблица соответствующих дисковых раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="67cb0-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

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
  
<span data-ttu-id="67cb0-189">Если вы используете приемник Application Insights, как описано в разделе "hello" ниже и хотите эти показатели tooshow вверх в Application Insights, внесите убедиться, что имя приемника hello tooadd в разделе «приемники» hello, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="67cb0-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="67cb0-190">Кроме того, рассмотрите возможность создания toosend отдельную таблицу счетчиками производительности, поэтому они не заполнять out hello Здравствуйте, данные поступают из других каналов ведения журнала включен.</span><span class="sxs-lookup"><span data-stu-id="67cb0-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="67cb0-191">Отправить журналы аналитики tooApplication</span><span class="sxs-lookup"><span data-stu-id="67cb0-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="67cb0-192">Отправка данных мониторинга и диагностики, tooApplication аналитики (AI) может выполняться как часть конфигурации WAD hello.</span><span class="sxs-lookup"><span data-stu-id="67cb0-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="67cb0-193">Если вы решите toouse AI для анализа событий и визуализации, чтение [анализ событий и визуализации с помощью Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset копирование приемник AI как часть «WadCfg».</span><span class="sxs-lookup"><span data-stu-id="67cb0-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="67cb0-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67cb0-194">Next steps</span></span>

<span data-ttu-id="67cb0-195">После правильной настройки диагностики Azure, вы увидите данные в таблицах хранилища из hello трассировки событий Windows и журналы EventSource.</span><span class="sxs-lookup"><span data-stu-id="67cb0-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="67cb0-196">При выборе toouse OMS Kibana или любые другие данные аналитики и визуализации платформы, которая непосредственно не настроены на hello шаблона диспетчера ресурсов, внести в hello данные из этих таблиц хранилища, что tooset копирование hello платформа tooread ваш выбор.</span><span class="sxs-lookup"><span data-stu-id="67cb0-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="67cb0-197">Сделать это для OMS несложно. Дополнительные сведения см. в статье [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md) (Анализ событий и журналов с помощью OMS).</span><span class="sxs-lookup"><span data-stu-id="67cb0-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="67cb0-198">Application Insights бит в этом смысле особым случаем, поскольку его можно настроить как часть конфигурации расширения диагностики hello, таким образом обратитесь toohello [соответствующей статье](service-fabric-diagnostics-event-analysis-appinsights.md) при выборе toouse AI.</span><span class="sxs-lookup"><span data-stu-id="67cb0-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="67cb0-199">В данный момент нет способа toofilter или очистки hello событий, отправляемых toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="67cb0-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="67cb0-200">Если не реализовать tooremove обработки событий, из таблицы hello, таблица hello останется toogrow.</span><span class="sxs-lookup"><span data-stu-id="67cb0-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="67cb0-201">В настоящее время является примером службы очистки данных, работающей в hello [образца контрольного](https://github.com/Azure-Samples/service-fabric-watchdog-service), и рекомендуется записать его, если не дает веские причины для вас toostore журналы за период времени 30 или 90 дней.</span><span class="sxs-lookup"><span data-stu-id="67cb0-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="67cb0-202">Узнайте, как счетчики производительности toocollect или журналы с помощью hello расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="67cb0-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* <span data-ttu-id="67cb0-203">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Анализ событий и визуализация с помощью Application Insights)</span><span class="sxs-lookup"><span data-stu-id="67cb0-203">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)</span></span>
* <span data-ttu-id="67cb0-204">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Анализ событий и журналов с помощью OMS)</span><span class="sxs-lookup"><span data-stu-id="67cb0-204">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md)</span></span>