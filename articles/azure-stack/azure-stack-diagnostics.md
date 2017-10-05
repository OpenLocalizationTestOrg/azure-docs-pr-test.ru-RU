---
title: "Диагностика в стек Azure | Документы Microsoft"
description: "Сведения о сборе файлов журнала диагностики в стек Azure"
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
ms.openlocfilehash: 70004cfd83360ac4c66fd4c90632d341709d2e6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="5fb8f-103">Средства диагностики Azure стека</span><span class="sxs-lookup"><span data-stu-id="5fb8f-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="5fb8f-104">Стек Azure имеет большое количество компонентов совместной работы и взаимодействия друг с другом.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="5fb8f-105">Все эти компоненты создают свои собственные уникальные журналы, это означает, что выявить проблемы, может быстро стать сложной задачи, особенно для ошибок, поступающих из нескольких взаимодействующих компонентов Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="5fb8f-106">Наши средства диагностики помогают убедитесь, что механизм сбора журналов проста и эффективна.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-106">Our diagnostics tools help make sure the log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="5fb8f-107">На следующей схеме показано влияние журнала средства сбора данных в работе стека Azure:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-107">The following diagram shows how log collection tools in Azure Stack work:</span></span>

![Средства сбора данных журнала](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="5fb8f-109">Сборщиком трассировки</span><span class="sxs-lookup"><span data-stu-id="5fb8f-109">Trace Collector</span></span>
 
<span data-ttu-id="5fb8f-110">По умолчанию включен сборщик трассировки.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-110">The Trace Collector is enabled by default.</span></span> <span data-ttu-id="5fb8f-111">Он непрерывно в фоновом режиме и собирает все журналы трассировки событий для Windows (ETW) из служб компонентов на стек Azure и сохраняет их на общие локальной общей папкой.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-111">It continuously runs in the background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="5fb8f-112">Ниже приведены важные сведения о сборщике данных трассировки.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-112">The following are important things to know about the Trace Collector:</span></span>
 
* <span data-ttu-id="5fb8f-113">Сборщиком трассировки выполняется постоянно с ограничениями размера по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-113">The Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="5fb8f-114">Значение по умолчанию, максимальный размер, допустимый для каждого файла (200 МБ) — **не** пороговый размер.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-114">The default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="5fb8f-115">Периодически происходит проверка размера (в настоящее время каждые 10 минут) и, если текущий файл > = 200 МБ, он сохраняется и создается новый файл.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-115">A size check occurs periodically (currently every 10 minutes) and if the current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="5fb8f-116">Также есть (8 ГБ настраиваемое) ограничение на размер всего файла, созданные для сеанса событий.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-116">There is also an 8 GB (configurable) limit on the total file size generated per event session.</span></span> <span data-ttu-id="5fb8f-117">По достижении этого предела самые старые файлы будут удалены при создании новых.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-117">Once this limit is reached, the oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="5fb8f-118">Ограничено возраст 5 дней в журналы.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-118">There is a 5-day age limit on the logs.</span></span> <span data-ttu-id="5fb8f-119">Это ограничение может быть настроен.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="5fb8f-120">Каждый компонент определяет свойства конфигурации трассировки с использованием файла JSON.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-120">Each component defines the trace configuration properties through a JSON file.</span></span> <span data-ttu-id="5fb8f-121">Файлы JSON хранятся в `C:\TraceCollector\Configuration`.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-121">The JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="5fb8f-122">При необходимости эти файлы можно изменять для изменения ограничения по размеру и возраст сбора журналов.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-122">If necessary, these files can be edited to change the age and size limits of the collected logs.</span></span> <span data-ttu-id="5fb8f-123">Изменения в эти файлы требуют перезапуска *сборщик трассировки стека Microsoft Azure* службу, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-123">Changes to these files require a restart of the *Microsoft Azure Stack Trace Collector* service for the changes to take effect.</span></span>
* <span data-ttu-id="5fb8f-124">Следующий пример является файл трассировки конфигурации JSON для операций FabricRingServices из XRP ВМ:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-124">The following example is a trace configuration JSON file for FabricRingServices Operations from the XRP VM:</span></span> 

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

* <span data-ttu-id="5fb8f-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="5fb8f-126">Этот параметр управляет возраста версий файлов.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-126">This parameter controls the age of files to keep.</span></span> <span data-ttu-id="5fb8f-127">Старые файлы журнала будут удалены.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-127">Older log files are deleted.</span></span>
* <span data-ttu-id="5fb8f-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="5fb8f-129">Этот параметр определяет пороговое значение размера для одного файла.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-129">This parameter controls the size threshold for a single file.</span></span> <span data-ttu-id="5fb8f-130">Если достигнуто, создается новый ETL-файла.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-130">If the size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="5fb8f-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="5fb8f-132">Этот параметр определяет общий объем .etl файлы, созданные из сеанса событий.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-132">This parameter controls the total size of the .etl files generated from an event session.</span></span> <span data-ttu-id="5fb8f-133">Если общий размер файлов превышает это значение параметра, старые файлы будут удалены.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-133">If the total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="5fb8f-134">Средство сбора журналов</span><span class="sxs-lookup"><span data-stu-id="5fb8f-134">Log collection tool</span></span>
 
<span data-ttu-id="5fb8f-135">Команда PowerShell `Get-AzureStackLog` может использоваться для сбора журналов из всех компонентов в среде Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-135">The PowerShell command `Get-AzureStackLog` can be used to collect logs from all the components  in an Azure Stack environment.</span></span> <span data-ttu-id="5fb8f-136">Она сохраняет их в ZIP-файлы в расположении определяемой пользователем.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="5fb8f-137">Наша группа технической поддержки должен журналов для помощи в устранении проблемы, может потребоваться для запуска этого средства.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-137">If our technical support team needs your logs to help troubleshoot an issue, they may ask you to run this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="5fb8f-138">Эти файлы журнала могут содержать личные сведения (PII).</span><span class="sxs-lookup"><span data-stu-id="5fb8f-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="5fb8f-139">Это учитывать перед отправкой любых файлов журнала открыто.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="5fb8f-140">В настоящее время мы собирать следующие типы журналов:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-140">We currently collect the following log types:</span></span>
*   <span data-ttu-id="5fb8f-141">**Журналы развертывания Azure стека**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="5fb8f-142">**Журналы событий Windows**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-142">**Windows event logs**</span></span>
*   <span data-ttu-id="5fb8f-143">**Журналы panther**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-143">**Panther logs**</span></span>

     <span data-ttu-id="5fb8f-144">Для устранения неполадок создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-144">To troubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="5fb8f-145">**Журнал кластера**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-145">**Cluster logs**</span></span>
*   <span data-ttu-id="5fb8f-146">**Журналы диагностики хранилища**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="5fb8f-147">**Журналы трассировки событий Windows**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-147">**ETW logs**</span></span>

    <span data-ttu-id="5fb8f-148">Эти сборщиком трассировки, которые хранятся в общей папке, откуда `Get-AzureStackLog` извлекает их.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-148">These are collected by the Trace Collector and stored in a share from where `Get-AzureStackLog` retrieves them.</span></span>
 
<span data-ttu-id="5fb8f-149">Определить все журналы, которые собираются из всех компонентов, можете `<Logs>` теги в файле конфигурации клиента, расположенный `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-149">To identify all the logs that get collected from all the components, refer to the `<Logs>` tags in the customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="to-run-get-azurestacklog"></a><span data-ttu-id="5fb8f-150">Для запуска Get AzureStackLog</span><span class="sxs-lookup"><span data-stu-id="5fb8f-150">To run Get-AzureStackLog</span></span>
1.  <span data-ttu-id="5fb8f-151">Войдите в систему как AzureStack\AzureStackAdmin на узле.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-151">Log in as AzureStack\AzureStackAdmin on the host.</span></span>
2.  <span data-ttu-id="5fb8f-152">Откройте окно PowerShell от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="5fb8f-153">Запустите `Get-AzureStackLog`.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-153">Run `Get-AzureStackLog`.</span></span>  

    <span data-ttu-id="5fb8f-154">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="5fb8f-154">**Examples**</span></span>

    - <span data-ttu-id="5fb8f-155">Собирать все журналы для всех ролей:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-155">Collect all logs for all roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="5fb8f-156">Соберите журналы из VirtualMachines и BareMetal роли:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-156">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="5fb8f-157">Соберите журналы из VirtualMachines и BareMetal роли, с датой фильтрации для файлов журнала последние 8 часов:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-157">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for the past 8 hours:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="5fb8f-158">Если `FromDate` и `ToDate` параметры не указаны, сбора журналов за последние 4 часа по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-158">If the `FromDate` and `ToDate` parameters are not specified, logs are collected for the past 4 hours by default.</span></span>

<span data-ttu-id="5fb8f-159">В настоящее время можно использовать `FilterByRole` параметр коллекцию фильтров журнала для следующих ролей:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-159">Currently, you can use the `FilterByRole` parameter to filter log collection by the following roles:</span></span>

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


<span data-ttu-id="5fb8f-160">Обратите внимание на несколько моментов:</span><span class="sxs-lookup"><span data-stu-id="5fb8f-160">A few things to note:</span></span>

* <span data-ttu-id="5fb8f-161">Это команда принимает некоторое время для сбора журналов, в зависимости от роли, которую журналы собираются.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-161">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="5fb8f-162">Ключевых факторов включают промежуток времени, указанный для сбора журналов, а также номера узлов в среде Azure стека.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-162">Contributing factors include the time duration specified for log collection, and the numbers of nodes in the Azure Stack environment.</span></span>
* <span data-ttu-id="5fb8f-163">После завершения сбора журналов, проверьте новой папки, созданные в `-OutputPath` параметр, указанный в команде.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-163">After log collection completes, check the new folder created in the `-OutputPath` parameter specified in the command.</span></span>
* <span data-ttu-id="5fb8f-164">Файл с именем `Get-AzureStackLog_Output.log` создается в папке, содержащей ZIP-файлы и содержит выходные данные команды, который может использоваться для устранения сбоев сбор данных журналов.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-164">A file called `Get-AzureStackLog_Output.log` is created in the folder containing the zip files and includes the command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="5fb8f-165">Каждая роль имеет журналов внутри отдельных ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-165">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="5fb8f-166">Чтобы изучить конкретный сбой, журналы могут быть необходимы из более чем одного компонента.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-166">To investigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="5fb8f-167">Журналы событий для всех виртуальных машин инфраструктуры и системы собираются в *VirtualMachines* роли.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-167">System and Event logs for all infrastructure VMs are collected in the *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="5fb8f-168">Системы и журналы событий для всех узлов сохраняются в *BareMetal* роли.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-168">System and Event logs for all hosts are collected in the *BareMetal* role.</span></span>
    -   <span data-ttu-id="5fb8f-169">Отказоустойчивый кластер и Hyper-V журналы событий сохраняются в *хранения* роли.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-169">Failover Cluster and Hyper-V event logs are collected in the *Storage* role.</span></span>
    -   <span data-ttu-id="5fb8f-170">ACS журналы собираются в *хранения* и *ACS* ролей.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-170">ACS logs are collected in the *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="5fb8f-171">Дополнительные сведения можно ссылаться в файл конфигурации клиента.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-171">For more details, you can refer to the customer configuration file.</span></span> <span data-ttu-id="5fb8f-172">Исследовать `<Logs>` теги для различных ролей.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-172">Investigate the `<Logs>` tags for the different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="5fb8f-173">Мы задать ограничения на размер и возраст в журналы, собранные как очень важно, чтобы обеспечить эффективное использование дискового пространства, чтобы убедиться в том, что не получают переполняющее с журналами.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-173">We are enforcing size and age limits to the logs collected as it is essential to ensure efficient utilization of your storage space to make sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="5fb8f-174">Вышесказанного, когда диагностики неполадок часто достаточно входит, больше не существует из-за этих ограничений применяется принудительно.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-174">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due to these limits being enforced.</span></span> <span data-ttu-id="5fb8f-175">Следовательно, это **настоятельно рекомендуется** , вы разгрузить журналов внешних дисковое пространство (учетной записи хранилища в Azure открытый, дополнительные локальное устройство хранения данных и т.д.) каждые 8 – 12 часов и сохранять их существует 1-3 месяцев в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="5fb8f-175">Hence, it is **highly recommended** that you offload your logs to an external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 to 12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5fb8f-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fb8f-176">Next steps</span></span>
[<span data-ttu-id="5fb8f-177">Microsoft Azure Stack troubleshooting (Устранение неполадок, связанных с Microsoft Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="5fb8f-177">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)
