---
title: "Использование хранилища BLOB-объектов для IIS и хранилища таблиц для событий в Azure Log Analytics | Документация Майкрософт"
description: "Log Analytics может считывать журналы служб Azure, которые записывают диагностические данные в хранилище таблиц, или журналы IIS, записанные в хранилище BLOB-объектов."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="fef5a-103">Использование хранилища BLOB-объектов Azure для IIS и хранилища таблиц Azure для событий в Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fef5a-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="fef5a-104">Log Analytics может считывать журналы следующих служб, которые записывают диагностические данные в хранилище таблиц, или журналы IIS, записанные в хранилище BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="fef5a-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="fef5a-105">кластеры Service Fabric (предварительная версия);</span><span class="sxs-lookup"><span data-stu-id="fef5a-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="fef5a-106">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fef5a-106">Virtual Machines</span></span>
* <span data-ttu-id="fef5a-107">Веб-роль или рабочая роль.</span><span class="sxs-lookup"><span data-stu-id="fef5a-107">Web/Worker Roles</span></span>

<span data-ttu-id="fef5a-108">Чтобы служба Log Analytics могла собирать данные для этих ресурсов, необходимо включить систему диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="fef5a-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="fef5a-109">После включения диагностики можно использовать портал Azure или PowerShell, чтобы настроить сбор журналов в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fef5a-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="fef5a-110">Система диагностики Azure — это расширение Azure, которое позволяет собирать диагностические данные из рабочей роли, веб-роли или виртуальной машины, выполняющейся в Azure.</span><span class="sxs-lookup"><span data-stu-id="fef5a-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="fef5a-111">Данные сохраняются в учетной записи хранения Azure и затем могут собираться Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fef5a-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="fef5a-112">Log Analytics может собирать эти журналы системы диагностики Azure, если они находятся в следующих расположениях:</span><span class="sxs-lookup"><span data-stu-id="fef5a-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="fef5a-113">Тип журнала</span><span class="sxs-lookup"><span data-stu-id="fef5a-113">Log Type</span></span> | <span data-ttu-id="fef5a-114">Тип ресурса</span><span class="sxs-lookup"><span data-stu-id="fef5a-114">Resource Type</span></span> | <span data-ttu-id="fef5a-115">Расположение</span><span class="sxs-lookup"><span data-stu-id="fef5a-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fef5a-116">Журналы IIS</span><span class="sxs-lookup"><span data-stu-id="fef5a-116">IIS logs</span></span> |<span data-ttu-id="fef5a-117">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fef5a-117">Virtual Machines</span></span> <br> <span data-ttu-id="fef5a-118">Веб-роли</span><span class="sxs-lookup"><span data-stu-id="fef5a-118">Web roles</span></span> <br> <span data-ttu-id="fef5a-119">Рабочие роли</span><span class="sxs-lookup"><span data-stu-id="fef5a-119">Worker roles</span></span> |<span data-ttu-id="fef5a-120">wad-iis-logfiles (хранилище BLOB-объектов)</span><span class="sxs-lookup"><span data-stu-id="fef5a-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="fef5a-121">syslog</span><span class="sxs-lookup"><span data-stu-id="fef5a-121">Syslog</span></span> |<span data-ttu-id="fef5a-122">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fef5a-122">Virtual Machines</span></span> |<span data-ttu-id="fef5a-123">LinuxsyslogVer2v0 (хранилище таблиц)</span><span class="sxs-lookup"><span data-stu-id="fef5a-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="fef5a-124">Операционные события Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="fef5a-125">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-125">Service Fabric nodes</span></span> |<span data-ttu-id="fef5a-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="fef5a-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="fef5a-127">События субъектов Service Fabric Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="fef5a-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="fef5a-128">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-128">Service Fabric nodes</span></span> |<span data-ttu-id="fef5a-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="fef5a-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="fef5a-130">События надежных служб Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="fef5a-131">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-131">Service Fabric nodes</span></span> |<span data-ttu-id="fef5a-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="fef5a-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="fef5a-133">Журналы событий Windows</span><span class="sxs-lookup"><span data-stu-id="fef5a-133">Windows Event logs</span></span> |<span data-ttu-id="fef5a-134">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="fef5a-135">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fef5a-135">Virtual Machines</span></span> <br> <span data-ttu-id="fef5a-136">Веб-роли</span><span class="sxs-lookup"><span data-stu-id="fef5a-136">Web roles</span></span> <br> <span data-ttu-id="fef5a-137">Рабочие роли</span><span class="sxs-lookup"><span data-stu-id="fef5a-137">Worker roles</span></span> |<span data-ttu-id="fef5a-138">WADWindowsEventLogsTable (хранилище таблиц)</span><span class="sxs-lookup"><span data-stu-id="fef5a-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="fef5a-139">Журналы трассировки событий Windows</span><span class="sxs-lookup"><span data-stu-id="fef5a-139">Windows ETW logs</span></span> |<span data-ttu-id="fef5a-140">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fef5a-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="fef5a-141">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fef5a-141">Virtual Machines</span></span> <br> <span data-ttu-id="fef5a-142">Веб-роли</span><span class="sxs-lookup"><span data-stu-id="fef5a-142">Web roles</span></span> <br> <span data-ttu-id="fef5a-143">Рабочие роли</span><span class="sxs-lookup"><span data-stu-id="fef5a-143">Worker roles</span></span> |<span data-ttu-id="fef5a-144">WADETWEventTable (хранилище таблиц)</span><span class="sxs-lookup"><span data-stu-id="fef5a-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="fef5a-145">Журналы IIS веб-сайтов Azure в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="fef5a-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="fef5a-146">При работе с виртуальными машинами вы можете установить [агент Log Analytics](log-analytics-azure-vm-extension.md) на виртуальную машину, чтобы включить дополнительные функции анализа.</span><span class="sxs-lookup"><span data-stu-id="fef5a-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="fef5a-147">Это позволит, помимо анализа журналов IIS и журналов событий, выполнять дополнительные виды анализа, включая отслеживание изменений конфигурации, оценку SQL и оценку обновлений.</span><span class="sxs-lookup"><span data-stu-id="fef5a-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="fef5a-148">Включение диагностики Azure в виртуальной машине для сбора журналов событий и журналов IIS</span><span class="sxs-lookup"><span data-stu-id="fef5a-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="fef5a-149">Следующая процедура используется для включения диагностики Azure на виртуальной машине для сбора журналов событий и журналов IIS с помощью портала Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fef5a-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="fef5a-150">Включение диагностики Azure на виртуальной машине с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="fef5a-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="fef5a-151">При создании виртуальной машины установите агент ВМ.</span><span class="sxs-lookup"><span data-stu-id="fef5a-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="fef5a-152">Если виртуальная машина уже существует, проверьте, установлен ли агент.</span><span class="sxs-lookup"><span data-stu-id="fef5a-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="fef5a-153">На портале Azure перейдите к виртуальной машине, выберите **Необязательная настройка**, а затем **Диагностика** и задайте для параметра **Состояние** значение **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="fef5a-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="fef5a-154">По завершении этой процедуры на виртуальной машине будет установлено и запущено расширение системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="fef5a-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="fef5a-155">Это расширение отвечает за сбор диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="fef5a-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="fef5a-156">На существующей виртуальной машине включите мониторинг и настройте ведение журнала событий.</span><span class="sxs-lookup"><span data-stu-id="fef5a-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="fef5a-157">Диагностику можно включить на уровне ВМ.</span><span class="sxs-lookup"><span data-stu-id="fef5a-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="fef5a-158">Чтобы включить диагностику, а затем настроить ведение журнала событий, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fef5a-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="fef5a-159">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="fef5a-159">Select the VM.</span></span>
   2. <span data-ttu-id="fef5a-160">Щелкните **Мониторинг**.</span><span class="sxs-lookup"><span data-stu-id="fef5a-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="fef5a-161">Щелкните **Диагностика**.</span><span class="sxs-lookup"><span data-stu-id="fef5a-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="fef5a-162">Установите для параметра **Состояние** значение **ВКЛ**.</span><span class="sxs-lookup"><span data-stu-id="fef5a-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="fef5a-163">Выберите все нужные журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="fef5a-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="fef5a-164">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fef5a-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="fef5a-165">Включение диагностики в веб-роли для сбора журналов IIS и событий</span><span class="sxs-lookup"><span data-stu-id="fef5a-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="fef5a-166">Порядок действий для включения системы диагностики Azure описан [здесь](../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fef5a-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="fef5a-167">Эта информация используется в приведенных ниже инструкциях по использованию системы диагностики в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fef5a-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="fef5a-168">При включении диагностики Azure происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="fef5a-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="fef5a-169">Журналы IIS по умолчанию сохраняются, а их данные передаются с интервалом, заданным с помощью параметра scheduledTransferPeriod/</span><span class="sxs-lookup"><span data-stu-id="fef5a-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="fef5a-170">Журналы событий Windows по умолчанию не передаются.</span><span class="sxs-lookup"><span data-stu-id="fef5a-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="fef5a-171">Включение диагностики</span><span class="sxs-lookup"><span data-stu-id="fef5a-171">To enable diagnostics</span></span>
<span data-ttu-id="fef5a-172">Чтобы включить журналы событий Windows или изменить значение scheduledTransferPeriod, настройте диагностику с помощью XML-файла конфигурации (diagnostics.wadcfg), как описывается в разделе [Шаг 4. Создание файла конфигурации системы диагностики и установка расширения](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="fef5a-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="fef5a-173">В следующем примере файл конфигурации собирает все журналы IIS и все события из журналов приложения и системы:</span><span class="sxs-lookup"><span data-stu-id="fef5a-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="fef5a-174">Убедитесь, что в параметре ConfigurationSettings указана учетная запись хранения, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="fef5a-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="fef5a-175">Значения **AccountName** и **AccountKey** можно найти на портале Azure. Для этого откройте раздел "Управление ключами доступа" на панели мониторинга учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fef5a-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="fef5a-176">Для строки подключения должен использоваться протокол **https**.</span><span class="sxs-lookup"><span data-stu-id="fef5a-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="fef5a-177">После того как обновленная конфигурация диагностики будет применена к облачной службе и диагностические данные начнут записываться в хранилище Azure, можно приступить к настройке Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fef5a-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="fef5a-178">Сбор журналов из хранилища Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="fef5a-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="fef5a-179">Чтобы настроить сбор журналов для следующих служб Azure в Log Analytics, можно использовать портал Azure:</span><span class="sxs-lookup"><span data-stu-id="fef5a-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="fef5a-180">Кластеры Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fef5a-180">Service Fabric clusters</span></span>
* <span data-ttu-id="fef5a-181">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="fef5a-181">Virtual Machines</span></span>
* <span data-ttu-id="fef5a-182">Веб-роль или рабочая роль.</span><span class="sxs-lookup"><span data-stu-id="fef5a-182">Web/Worker Roles</span></span>

<span data-ttu-id="fef5a-183">На портале Azure перейдите к рабочей области Log Analytics и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fef5a-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="fef5a-184">Щелкните *Storage accounts logs* (Журналы учетных записей хранения).</span><span class="sxs-lookup"><span data-stu-id="fef5a-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="fef5a-185">Щелкните задачу *Добавить*.</span><span class="sxs-lookup"><span data-stu-id="fef5a-185">Click the *Add* task</span></span>
3. <span data-ttu-id="fef5a-186">Выберите учетную запись, содержащую журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="fef5a-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="fef5a-187">Это может быть классическая учетная запись хранения или учетная запись хранения Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fef5a-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="fef5a-188">Выберите тип данных, по которому требуется собирать журналы.</span><span class="sxs-lookup"><span data-stu-id="fef5a-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="fef5a-189">Доступны следующие варианты: журналы IIS, журналы событий, системный журнал (Linux), журналы трассировки событий Windows, события Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fef5a-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="fef5a-190">Значение параметра "Источник" заполняется автоматически на основе типа данных, и его нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="fef5a-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="fef5a-191">Нажмите кнопку "ОК", чтобы сохранить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="fef5a-191">Click OK to save the configuration</span></span>

<span data-ttu-id="fef5a-192">Повторите шаги 2–6 для дополнительных учетных записей хранения и типов данных, которые нужно собирать в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="fef5a-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="fef5a-193">Приблизительно через полчаса в Log Analytics отобразятся данные из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fef5a-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="fef5a-194">Отобразятся только данные, записанные в хранилище после применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fef5a-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="fef5a-195">Log Analytics не считывает уже существующие данные из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fef5a-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="fef5a-196">Портал не проверяет существование источника, а также то, записываются ли новые данные.</span><span class="sxs-lookup"><span data-stu-id="fef5a-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="fef5a-197">Включение диагностики Azure на виртуальной машине для сбора журналов событий и журналов IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef5a-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="fef5a-198">В инструкциях раздела [Настройка Log Analytics для индексации системы диагностики Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) описано использование PowerShell для чтения данных системы диагностики Azure, записанных в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="fef5a-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="fef5a-199">С помощью Azure PowerShell можно более точно указать, какие события должны записываться в хранилище.</span><span class="sxs-lookup"><span data-stu-id="fef5a-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="fef5a-200">Дополнительную информацию см. в статье [Включение диагностики на виртуальных машинах Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fef5a-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="fef5a-201">Включить и обновить систему диагностики Azure можно с помощью приведенного ниже сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fef5a-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="fef5a-202">Его также можно использовать с пользовательской конфигурацией ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="fef5a-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="fef5a-203">Измените сценарий, указав учетную запись хранения, имя службы и имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fef5a-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="fef5a-204">Сценарий использует командлеты для классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fef5a-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="fef5a-205">Изучите приведенный ниже образец скрипта, скопируйте, измените нужным образом и сохраните как файл скрипта PowerShell, а затем выполните скрипт.</span><span class="sxs-lookup"><span data-stu-id="fef5a-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="fef5a-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fef5a-206">Next steps</span></span>
* <span data-ttu-id="fef5a-207">[Сбор журналов и метрик для поддерживаемых служб Azure](log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="fef5a-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="fef5a-208">[Включите решения](log-analytics-add-solutions.md) , чтобы обеспечить глубокое понимание данных.</span><span class="sxs-lookup"><span data-stu-id="fef5a-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="fef5a-209">[Воспользуйтесь запросами поиска](log-analytics-log-searches.md) для анализа данных.</span><span class="sxs-lookup"><span data-stu-id="fef5a-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
