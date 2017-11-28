---
title: "aaaUse хранилища больших двоичных объектов для служб IIS и таблица хранения событий в службе анализа журналов Azure | Документы Microsoft"
description: "Аналитика журналов можно считывать hello журналы для служб Azure, которые записывают tootable хранилищ диагностики или журналы IIS записывались tooblob хранилища."
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
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="4e851-103">Использование хранилища BLOB-объектов Azure для IIS и хранилища таблиц Azure для событий в Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4e851-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="4e851-104">Служба аналитики журналов может читать журналы hello для следующих служб, которые записывают диагностики tootable хранилища или IIS, журналы хранения письменного tooblob hello:</span><span class="sxs-lookup"><span data-stu-id="4e851-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="4e851-105">кластеры Service Fabric (предварительная версия);</span><span class="sxs-lookup"><span data-stu-id="4e851-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="4e851-106">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="4e851-106">Virtual Machines</span></span>
* <span data-ttu-id="4e851-107">Веб-роль или рабочая роль.</span><span class="sxs-lookup"><span data-stu-id="4e851-107">Web/Worker Roles</span></span>

<span data-ttu-id="4e851-108">Чтобы служба Log Analytics могла собирать данные для этих ресурсов, необходимо включить систему диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="4e851-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="4e851-109">После включения диагностики можно использовать портал Azure hello или PowerShell Настройка журналов hello toocollect анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="4e851-110">Диагностика Azure — это расширение Azure, позволяющий toocollect диагностических данных из рабочей роли, веб-роли или виртуальной машины, работающей в Azure.</span><span class="sxs-lookup"><span data-stu-id="4e851-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="4e851-111">Hello данные хранятся в учетной записи хранилища Azure и затем может быть собранные службой аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="4e851-112">Для анализа журналов toocollect эти журналы диагностики Azure hello журналы должны находиться в hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="4e851-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="4e851-113">Тип журнала</span><span class="sxs-lookup"><span data-stu-id="4e851-113">Log Type</span></span> | <span data-ttu-id="4e851-114">Тип ресурса</span><span class="sxs-lookup"><span data-stu-id="4e851-114">Resource Type</span></span> | <span data-ttu-id="4e851-115">Расположение</span><span class="sxs-lookup"><span data-stu-id="4e851-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e851-116">Журналы IIS</span><span class="sxs-lookup"><span data-stu-id="4e851-116">IIS logs</span></span> |<span data-ttu-id="4e851-117">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="4e851-117">Virtual Machines</span></span> <br> <span data-ttu-id="4e851-118">Веб-роли</span><span class="sxs-lookup"><span data-stu-id="4e851-118">Web roles</span></span> <br> <span data-ttu-id="4e851-119">Рабочие роли</span><span class="sxs-lookup"><span data-stu-id="4e851-119">Worker roles</span></span> |<span data-ttu-id="4e851-120">wad-iis-logfiles (хранилище BLOB-объектов)</span><span class="sxs-lookup"><span data-stu-id="4e851-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="4e851-121">syslog</span><span class="sxs-lookup"><span data-stu-id="4e851-121">Syslog</span></span> |<span data-ttu-id="4e851-122">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="4e851-122">Virtual Machines</span></span> |<span data-ttu-id="4e851-123">LinuxsyslogVer2v0 (хранилище таблиц)</span><span class="sxs-lookup"><span data-stu-id="4e851-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="4e851-124">Операционные события Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="4e851-125">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-125">Service Fabric nodes</span></span> |<span data-ttu-id="4e851-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="4e851-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="4e851-127">События субъектов Service Fabric Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="4e851-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="4e851-128">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-128">Service Fabric nodes</span></span> |<span data-ttu-id="4e851-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="4e851-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="4e851-130">События надежных служб Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="4e851-131">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-131">Service Fabric nodes</span></span> |<span data-ttu-id="4e851-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="4e851-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="4e851-133">Журналы событий Windows</span><span class="sxs-lookup"><span data-stu-id="4e851-133">Windows Event logs</span></span> |<span data-ttu-id="4e851-134">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="4e851-135">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="4e851-135">Virtual Machines</span></span> <br> <span data-ttu-id="4e851-136">Веб-роли</span><span class="sxs-lookup"><span data-stu-id="4e851-136">Web roles</span></span> <br> <span data-ttu-id="4e851-137">Рабочие роли</span><span class="sxs-lookup"><span data-stu-id="4e851-137">Worker roles</span></span> |<span data-ttu-id="4e851-138">WADWindowsEventLogsTable (хранилище таблиц)</span><span class="sxs-lookup"><span data-stu-id="4e851-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="4e851-139">Журналы трассировки событий Windows</span><span class="sxs-lookup"><span data-stu-id="4e851-139">Windows ETW logs</span></span> |<span data-ttu-id="4e851-140">Узлы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4e851-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="4e851-141">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="4e851-141">Virtual Machines</span></span> <br> <span data-ttu-id="4e851-142">Веб-роли</span><span class="sxs-lookup"><span data-stu-id="4e851-142">Web roles</span></span> <br> <span data-ttu-id="4e851-143">Рабочие роли</span><span class="sxs-lookup"><span data-stu-id="4e851-143">Worker roles</span></span> |<span data-ttu-id="4e851-144">WADETWEventTable (хранилище таблиц)</span><span class="sxs-lookup"><span data-stu-id="4e851-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="4e851-145">Журналы IIS веб-сайтов Azure в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4e851-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="4e851-146">Для виртуальных машин, у вас есть возможность установить hello hello [анализа журналов агента](log-analytics-azure-vm-extension.md) в вашей виртуальной машины tooenable дополнительные функции анализа.</span><span class="sxs-lookup"><span data-stu-id="4e851-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="4e851-147">Кроме toobeing может tooanalyze IIS и журналов событий, можно выполнить дополнительный анализ, включая отслеживание изменений конфигурации, оценку SQL и оценку обновлений.</span><span class="sxs-lookup"><span data-stu-id="4e851-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="4e851-148">Включение диагностики Azure в виртуальной машине для сбора журналов событий и журналов IIS</span><span class="sxs-lookup"><span data-stu-id="4e851-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="4e851-149">Hello используйте следующие процедуры tooenable диагностики Azure в виртуальной машине для сбора, с помощью портала Microsoft Azure hello журналов событий и журналов IIS.</span><span class="sxs-lookup"><span data-stu-id="4e851-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="4e851-150">tooenable диагностики Azure в виртуальную машину с портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="4e851-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="4e851-151">При создании виртуальной машины, установите агент ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="4e851-152">Если hello виртуальная машина уже существует, убедитесь, что приветствия уже установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4e851-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="4e851-153">В hello портал Azure, перейдите toohello виртуальной машины, выберите **необязательная конфигурация**, затем **диагностики** и задайте **состояние** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="4e851-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="4e851-154">По завершении hello виртуальных Машин с расширением hello диагностики Azure установлены и запущены.</span><span class="sxs-lookup"><span data-stu-id="4e851-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="4e851-155">Это расширение отвечает за сбор диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="4e851-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="4e851-156">На существующей виртуальной машине включите мониторинг и настройте ведение журнала событий.</span><span class="sxs-lookup"><span data-stu-id="4e851-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="4e851-157">Можно включить диагностику на hello уровня виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4e851-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="4e851-158">Диагностика tooenable и затем настроить ведение журнала событий, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="4e851-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="4e851-159">Выберите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4e851-159">Select hello VM.</span></span>
   2. <span data-ttu-id="4e851-160">Щелкните **Мониторинг**.</span><span class="sxs-lookup"><span data-stu-id="4e851-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="4e851-161">Щелкните **Диагностика**.</span><span class="sxs-lookup"><span data-stu-id="4e851-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="4e851-162">Набор hello **состояние** слишком**ON**.</span><span class="sxs-lookup"><span data-stu-id="4e851-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="4e851-163">Выберите каждый журнал диагностики, которые должны toocollect.</span><span class="sxs-lookup"><span data-stu-id="4e851-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="4e851-164">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4e851-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="4e851-165">Включение диагностики в веб-роли для сбора журналов IIS и событий</span><span class="sxs-lookup"><span data-stu-id="4e851-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="4e851-166">См. слишком[как tooEnable диагностики в облачной службе](../cloud-services/cloud-services-dotnet-diagnostics.md) общие инструкции о включении диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="4e851-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="4e851-167">Приведенные ниже инструкции Hello эти сведения можно использовать и настройте его для использования с помощью аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="4e851-168">При включении диагностики Azure происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="4e851-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="4e851-169">По умолчанию данные передаются через интервал передачи scheduledTransferPeriod hello хранятся журналы IIS.</span><span class="sxs-lookup"><span data-stu-id="4e851-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="4e851-170">Журналы событий Windows по умолчанию не передаются.</span><span class="sxs-lookup"><span data-stu-id="4e851-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="4e851-171">Диагностика tooenable</span><span class="sxs-lookup"><span data-stu-id="4e851-171">tooenable diagnostics</span></span>
<span data-ttu-id="4e851-172">tooenable журналы событий Windows или toochange hello scheduledTransferPeriod, настройте диагностику Azure, с помощью hello XML-файл конфигурации (diagnostics.wadcfg), как показано в [шаг 4: Создание файла конфигурации диагностики и установка hello расширение](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="4e851-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="4e851-173">Hello следующий файл конфигурации собирает журналы IIS и все события из приложения hello и системные журналы:</span><span class="sxs-lookup"><span data-stu-id="4e851-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
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

<span data-ttu-id="4e851-174">Убедитесь, что в параметре ConfigurationSettings указана учетная запись хранения, как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="4e851-175">Hello **AccountName** и **AccountKey** значения находятся в hello портал Azure в мониторинга учетной записи хранения hello под управление ключами доступа.</span><span class="sxs-lookup"><span data-stu-id="4e851-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="4e851-176">Hello для hello строки подключения должен использоваться протокол **https**.</span><span class="sxs-lookup"><span data-stu-id="4e851-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="4e851-177">После применения обновленная конфигурация диагностики hello tooyour облачной службы и он производит запись диагностики tooAzure хранилища, то будут готовы tooconfigure анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="4e851-178">Использовать журналы Azure портала toocollect hello из хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="4e851-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="4e851-179">Hello Azure портала tooconfigure журнала toocollect hello журналы аналитики можно использовать для следующих служб Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4e851-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="4e851-180">Кластеры Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4e851-180">Service Fabric clusters</span></span>
* <span data-ttu-id="4e851-181">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="4e851-181">Virtual Machines</span></span>
* <span data-ttu-id="4e851-182">Веб-роль или рабочая роль.</span><span class="sxs-lookup"><span data-stu-id="4e851-182">Web/Worker Roles</span></span>

<span data-ttu-id="4e851-183">В hello портал Azure перейдите в рабочую область службы анализа журналов tooyour и выполните следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="4e851-184">Щелкните *Storage accounts logs* (Журналы учетных записей хранения).</span><span class="sxs-lookup"><span data-stu-id="4e851-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="4e851-185">Нажмите кнопку hello *добавить* задач</span><span class="sxs-lookup"><span data-stu-id="4e851-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="4e851-186">Выберите учетную запись хранения hello, содержащий журналы диагностики hello</span><span class="sxs-lookup"><span data-stu-id="4e851-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="4e851-187">Это может быть классическая учетная запись хранения или учетная запись хранения Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4e851-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="4e851-188">Выберите тип данных, который будет toocollect журналы для hello</span><span class="sxs-lookup"><span data-stu-id="4e851-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="4e851-189">Hello доступны журналы IIS; События; Syslog (Linux); Журналы трассировки событий Windows; События Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4e851-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="4e851-190">значение Hello источник заполняется автоматически основании hello данные типа и не может быть изменен</span><span class="sxs-lookup"><span data-stu-id="4e851-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="4e851-191">Нажмите кнопку ОК toosave hello конфигурации</span><span class="sxs-lookup"><span data-stu-id="4e851-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="4e851-192">Повторите шаги 2 – 6 для дополнительного хранилища учетных записей и типы данных, которые должны toocollect анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="4e851-193">Около 30 минут, может toosee данные из учетной записи хранилища hello в службе анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="4e851-194">Вы увидите только данные, записываемые toostorage после применения конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="4e851-195">Служба аналитики журналов не считывает hello существующих данных из учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="4e851-196">портал Hello не проверяет, hello источника существует в учетной записи хранения hello, или если новые данные записываются.</span><span class="sxs-lookup"><span data-stu-id="4e851-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="4e851-197">Включение диагностики Azure на виртуальной машине для сбора журналов событий и журналов IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e851-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="4e851-198">Используйте hello шагов в [tooindex Настройка аналитики журналов диагностики Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse tooread PowerShell из службы диагностики Azure, написанных tootable хранилища.</span><span class="sxs-lookup"><span data-stu-id="4e851-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="4e851-199">С помощью Azure PowerShell можно более точно указать hello, события должны записываться tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="4e851-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="4e851-200">Дополнительную информацию см. в статье [Включение диагностики на виртуальных машинах Azure](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="4e851-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="4e851-201">Можно включить и обновить hello следующий сценарий PowerShell с помощью диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="4e851-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="4e851-202">Его также можно использовать с пользовательской конфигурацией ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="4e851-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="4e851-203">Изменение учетной записи хранилища hello сценария tooset hello, имя службы и имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4e851-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="4e851-204">Hello скрипт использует командлеты для классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4e851-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="4e851-205">Просмотрите следующий образец скрипта hello, скопировать его, измените нужным образом, сохраните как файл скрипта PowerShell образец hello и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="4e851-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e851-206">Next steps</span></span>
* <span data-ttu-id="4e851-207">[Сбор журналов и метрик для поддерживаемых служб Azure](log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4e851-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="4e851-208">[Включить решения](log-analytics-add-solutions.md) tooprovide понимание данных hello.</span><span class="sxs-lookup"><span data-stu-id="4e851-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="4e851-209">[Использовать запросы поиска](log-analytics-log-searches.md) tooanalyze hello данных.</span><span class="sxs-lookup"><span data-stu-id="4e851-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
