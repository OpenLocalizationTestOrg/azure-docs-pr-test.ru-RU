---
title: "aaaDiagnostics стека Azure | Документы Microsoft"
description: "Как файлы журнала toocollect для диагностики в стек Azure"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="d7415-103">Средства диагностики Azure стека</span><span class="sxs-lookup"><span data-stu-id="d7415-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="d7415-104">Стек Azure имеет большое количество компонентов совместной работы и взаимодействия друг с другом.</span><span class="sxs-lookup"><span data-stu-id="d7415-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="d7415-105">Все эти компоненты создают свои собственные уникальные журналы, это означает, что выявить проблемы, может быстро стать сложной задачи, особенно для ошибок, поступающих из нескольких взаимодействующих компонентов Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d7415-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="d7415-106">Наши средства диагностики помогают убедитесь, что механизм сбора журналов hello проста и эффективна.</span><span class="sxs-lookup"><span data-stu-id="d7415-106">Our diagnostics tools help make sure hello log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="d7415-107">Hello следующей схеме показано влияние журнала средства сбора данных в работе стека Azure:</span><span class="sxs-lookup"><span data-stu-id="d7415-107">hello following diagram shows how log collection tools in Azure Stack work:</span></span>

![Средства сбора данных журнала](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="d7415-109">Сборщиком трассировки</span><span class="sxs-lookup"><span data-stu-id="d7415-109">Trace Collector</span></span>
 
<span data-ttu-id="d7415-110">Hello сборщика трассировки включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d7415-110">hello Trace Collector is enabled by default.</span></span> <span data-ttu-id="d7415-111">Он постоянно выполняется в фоновом режиме hello и собирает все журналы трассировки событий для Windows (ETW) из служб компонентов на стек Azure и сохраняет их на общие локальной общей папкой.</span><span class="sxs-lookup"><span data-stu-id="d7415-111">It continuously runs in hello background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="d7415-112">Здесь представлены Hello tooknow важные вопросы о hello сборщика трассировки:</span><span class="sxs-lookup"><span data-stu-id="d7415-112">hello following are important things tooknow about hello Trace Collector:</span></span>
 
* <span data-ttu-id="d7415-113">Hello сбора данных выполняется постоянно с ограничениями размера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d7415-113">hello Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="d7415-114">по умолчанию максимальный размер, допустимый для каждого файла (200 МБ): Hello **не** пороговый размер.</span><span class="sxs-lookup"><span data-stu-id="d7415-114">hello default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="d7415-115">Периодически происходит проверка размера (в настоящее время каждые 10 минут) и если hello текущий файл > = 200 МБ, оно сохраняется и создается новый файл.</span><span class="sxs-lookup"><span data-stu-id="d7415-115">A size check occurs periodically (currently every 10 minutes) and if hello current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="d7415-116">Также есть (8 ГБ настраиваемое) ограничение на размер файла общее hello, созданные для сеанса событий.</span><span class="sxs-lookup"><span data-stu-id="d7415-116">There is also an 8 GB (configurable) limit on hello total file size generated per event session.</span></span> <span data-ttu-id="d7415-117">По достижении этого предела hello старые файлы будут удалены при создании новых.</span><span class="sxs-lookup"><span data-stu-id="d7415-117">Once this limit is reached, hello oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="d7415-118">О журналах hello ограничено возраст 5 дней.</span><span class="sxs-lookup"><span data-stu-id="d7415-118">There is a 5-day age limit on hello logs.</span></span> <span data-ttu-id="d7415-119">Это ограничение может быть настроен.</span><span class="sxs-lookup"><span data-stu-id="d7415-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="d7415-120">Каждый компонент определяет свойства конфигурации трассировки hello через JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="d7415-120">Each component defines hello trace configuration properties through a JSON file.</span></span> <span data-ttu-id="d7415-121">Hello файлы JSON хранятся в `C:\TraceCollector\Configuration`.</span><span class="sxs-lookup"><span data-stu-id="d7415-121">hello JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="d7415-122">При необходимости эти файлы можно редактировать toochange hello возраст и размер границы hello собираются журналы.</span><span class="sxs-lookup"><span data-stu-id="d7415-122">If necessary, these files can be edited toochange hello age and size limits of hello collected logs.</span></span> <span data-ttu-id="d7415-123">Файлы toothese изменения требуют перезапуска hello *сборщик трассировки стека Microsoft Azure* tootake эффект изменения службы для hello.</span><span class="sxs-lookup"><span data-stu-id="d7415-123">Changes toothese files require a restart of hello *Microsoft Azure Stack Trace Collector* service for hello changes tootake effect.</span></span>
* <span data-ttu-id="d7415-124">Hello ниже приведен файл трассировки конфигурации JSON для операций FabricRingServices от hello XRP виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="d7415-124">hello following example is a trace configuration JSON file for FabricRingServices Operations from hello XRP VM:</span></span> 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* <span data-ttu-id="d7415-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="d7415-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="d7415-126">Этот параметр управляет hello возраст tookeep файлов.</span><span class="sxs-lookup"><span data-stu-id="d7415-126">This parameter controls hello age of files tookeep.</span></span> <span data-ttu-id="d7415-127">Старые файлы журнала будут удалены.</span><span class="sxs-lookup"><span data-stu-id="d7415-127">Older log files are deleted.</span></span>
* <span data-ttu-id="d7415-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="d7415-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="d7415-129">Этот параметр управляет hello пороговое значение размера для одного файла.</span><span class="sxs-lookup"><span data-stu-id="d7415-129">This parameter controls hello size threshold for a single file.</span></span> <span data-ttu-id="d7415-130">При достижении размера hello создается новый ETL-файла.</span><span class="sxs-lookup"><span data-stu-id="d7415-130">If hello size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="d7415-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="d7415-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="d7415-132">Этот параметр управляет hello общий размер файлов .etl hello, созданного из сеанса событий.</span><span class="sxs-lookup"><span data-stu-id="d7415-132">This parameter controls hello total size of hello .etl files generated from an event session.</span></span> <span data-ttu-id="d7415-133">Если hello общий размер файлов превышает это значение параметра, старые файлы будут удалены.</span><span class="sxs-lookup"><span data-stu-id="d7415-133">If hello total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="d7415-134">Средство сбора журналов</span><span class="sxs-lookup"><span data-stu-id="d7415-134">Log collection tool</span></span>
 
<span data-ttu-id="d7415-135">Здравствуйте, команда PowerShell `Get-AzureStackLog` может быть используется toocollect журналы из всех компонентов hello в среде Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d7415-135">hello PowerShell command `Get-AzureStackLog` can be used toocollect logs from all hello components  in an Azure Stack environment.</span></span> <span data-ttu-id="d7415-136">Она сохраняет их в ZIP-файлы в расположении определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="d7415-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="d7415-137">Если наш Техническая поддержка потребностями группы вашей toohelp журналы Устранение проблемы, они могут попросить вас toorun этого средства.</span><span class="sxs-lookup"><span data-stu-id="d7415-137">If our technical support team needs your logs toohelp troubleshoot an issue, they may ask you toorun this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="d7415-138">Эти файлы журнала могут содержать личные сведения (PII).</span><span class="sxs-lookup"><span data-stu-id="d7415-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="d7415-139">Это учитывать перед отправкой любых файлов журнала открыто.</span><span class="sxs-lookup"><span data-stu-id="d7415-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="d7415-140">В настоящее время мы собираем hello следующие типы журналов:</span><span class="sxs-lookup"><span data-stu-id="d7415-140">We currently collect hello following log types:</span></span>
*   <span data-ttu-id="d7415-141">**Журналы развертывания Azure стека**</span><span class="sxs-lookup"><span data-stu-id="d7415-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="d7415-142">**Журналы событий Windows**</span><span class="sxs-lookup"><span data-stu-id="d7415-142">**Windows event logs**</span></span>
*   <span data-ttu-id="d7415-143">**Журналы panther**</span><span class="sxs-lookup"><span data-stu-id="d7415-143">**Panther logs**</span></span>

     <span data-ttu-id="d7415-144">проблемы создания tootroubleshoot виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d7415-144">tootroubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="d7415-145">**Журнал кластера**</span><span class="sxs-lookup"><span data-stu-id="d7415-145">**Cluster logs**</span></span>
*   <span data-ttu-id="d7415-146">**Журналы диагностики хранилища**</span><span class="sxs-lookup"><span data-stu-id="d7415-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="d7415-147">**Журналы трассировки событий Windows**</span><span class="sxs-lookup"><span data-stu-id="d7415-147">**ETW logs**</span></span>

    <span data-ttu-id="d7415-148">Они собираются по hello сборщика трассировки и сохраняются в общей папке, откуда `Get-AzureStackLog` извлекает их.</span><span class="sxs-lookup"><span data-stu-id="d7415-148">These are collected by hello Trace Collector and stored in a share from where `Get-AzureStackLog` retrieves them.</span></span>
 
<span data-ttu-id="d7415-149">Здравствуйте, все журналы, которые собираются из всех компонентов hello tooidentify ссылаться toohello `<Logs>` теги в файле конфигурации клиента hello, расположенный в `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span><span class="sxs-lookup"><span data-stu-id="d7415-149">tooidentify all hello logs that get collected from all hello components, refer toohello `<Logs>` tags in hello customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="toorun-get-azurestacklog"></a><span data-ttu-id="d7415-150">toorun Get AzureStackLog</span><span class="sxs-lookup"><span data-stu-id="d7415-150">toorun Get-AzureStackLog</span></span>
1.  <span data-ttu-id="d7415-151">Войдите в систему как AzureStack\AzureStackAdmin на узле hello.</span><span class="sxs-lookup"><span data-stu-id="d7415-151">Log in as AzureStack\AzureStackAdmin on hello host.</span></span>
2.  <span data-ttu-id="d7415-152">Откройте окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d7415-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="d7415-153">Запустите `Get-AzureStackLog`.</span><span class="sxs-lookup"><span data-stu-id="d7415-153">Run `Get-AzureStackLog`.</span></span>  

    <span data-ttu-id="d7415-154">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="d7415-154">**Examples**</span></span>

    - <span data-ttu-id="d7415-155">Собирать все журналы для всех ролей:</span><span class="sxs-lookup"><span data-stu-id="d7415-155">Collect all logs for all roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="d7415-156">Соберите журналы из VirtualMachines и BareMetal роли:</span><span class="sxs-lookup"><span data-stu-id="d7415-156">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="d7415-157">Соберите журналы из VirtualMachines и BareMetal роли, с датой фильтрации для файлов журналов для hello последние 8 часов:</span><span class="sxs-lookup"><span data-stu-id="d7415-157">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for hello past 8 hours:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="d7415-158">Если hello `FromDate` и `ToDate` параметры не указаны, сбора журналов за hello последние 4 часа по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d7415-158">If hello `FromDate` and `ToDate` parameters are not specified, logs are collected for hello past 4 hours by default.</span></span>

<span data-ttu-id="d7415-159">В настоящее время можно использовать hello `FilterByRole` параметр toofilter журнала коллекции с помощью hello следующих ролей:</span><span class="sxs-lookup"><span data-stu-id="d7415-159">Currently, you can use hello `FilterByRole` parameter toofilter log collection by hello following roles:</span></span>

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


<span data-ttu-id="d7415-160">Toonote несколько вещей:</span><span class="sxs-lookup"><span data-stu-id="d7415-160">A few things toonote:</span></span>

* <span data-ttu-id="d7415-161">Это команда принимает некоторое время для сбора журналов, в зависимости от роли, которую журналы собираются.</span><span class="sxs-lookup"><span data-stu-id="d7415-161">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="d7415-162">Такие факторы, составляющей hello продолжительность времени, указанных для сбора журналов и hello количеством узлов в среде Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="d7415-162">Contributing factors include hello time duration specified for log collection, and hello numbers of nodes in hello Azure Stack environment.</span></span>
* <span data-ttu-id="d7415-163">После завершения сбора журналов, проверьте hello новой папки, созданные в hello `-OutputPath` параметр, указанный в команде hello.</span><span class="sxs-lookup"><span data-stu-id="d7415-163">After log collection completes, check hello new folder created in hello `-OutputPath` parameter specified in hello command.</span></span>
* <span data-ttu-id="d7415-164">Файл с именем `Get-AzureStackLog_Output.log` создается в папке hello, содержащий hello ZIP-файлов и включает выходные данные команды hello, который может использоваться для устранения сбоев сбор данных журналов.</span><span class="sxs-lookup"><span data-stu-id="d7415-164">A file called `Get-AzureStackLog_Output.log` is created in hello folder containing hello zip files and includes hello command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="d7415-165">Каждая роль имеет журналов внутри отдельных ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="d7415-165">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="d7415-166">tooinvestigate конкретный сбой, журналы могут быть необходимы из более чем одного компонента.</span><span class="sxs-lookup"><span data-stu-id="d7415-166">tooinvestigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="d7415-167">Журналы событий для всех виртуальных машин инфраструктуры и системы собираются в hello *VirtualMachines* роли.</span><span class="sxs-lookup"><span data-stu-id="d7415-167">System and Event logs for all infrastructure VMs are collected in hello *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="d7415-168">Системы и журналы событий для всех узлов сохраняются в hello *BareMetal* роли.</span><span class="sxs-lookup"><span data-stu-id="d7415-168">System and Event logs for all hosts are collected in hello *BareMetal* role.</span></span>
    -   <span data-ttu-id="d7415-169">Отказоустойчивый кластер и Hyper-V журналы событий сохраняются в hello *хранения* роли.</span><span class="sxs-lookup"><span data-stu-id="d7415-169">Failover Cluster and Hyper-V event logs are collected in hello *Storage* role.</span></span>
    -   <span data-ttu-id="d7415-170">ACS журналы собираются в hello *хранения* и *ACS* ролей.</span><span class="sxs-lookup"><span data-stu-id="d7415-170">ACS logs are collected in hello *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="d7415-171">Дополнительные сведения можно ссылаться toohello файл конфигурации клиента.</span><span class="sxs-lookup"><span data-stu-id="d7415-171">For more details, you can refer toohello customer configuration file.</span></span> <span data-ttu-id="d7415-172">Исследовать hello `<Logs>` теги для различных ролей hello.</span><span class="sxs-lookup"><span data-stu-id="d7415-172">Investigate hello `<Logs>` tags for hello different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="d7415-173">Мы задать размер и возраст ограничивает toohello журналы, собранные как основные tooensure эффективное использование вашей toomake места хранения, убедиться, что он не получает переполняющее с журналами.</span><span class="sxs-lookup"><span data-stu-id="d7415-173">We are enforcing size and age limits toohello logs collected as it is essential tooensure efficient utilization of your storage space toomake sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="d7415-174">Вышесказанного, когда диагностики неполадок часто достаточно входит, больше не существует из-за ограничений toothese применяется принудительно.</span><span class="sxs-lookup"><span data-stu-id="d7415-174">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due toothese limits being enforced.</span></span> <span data-ttu-id="d7415-175">Следовательно, это **настоятельно рекомендуется** , вы разгрузить журналы tooan внешних дискового пространства (учетной записи хранилища в Azure открытый, дополнительные локальное устройство хранения данных и т.д.) каждые 8 часов too12 и сохранять их существует 1-3 месяцев в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="d7415-175">Hence, it is **highly recommended** that you offload your logs tooan external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 too12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7415-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7415-176">Next steps</span></span>
[<span data-ttu-id="d7415-177">Microsoft Azure Stack troubleshooting (Устранение неполадок, связанных с Microsoft Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="d7415-177">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)
