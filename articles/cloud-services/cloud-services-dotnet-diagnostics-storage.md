---
title: "aaaStore и просмотра диагностических данных в хранилище Azure | Документы Microsoft"
description: "Получение и просмотр диагностических данных Azure в хранилище Azure"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="ab702-103">Хранение и просмотр диагностических данных в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="ab702-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="ab702-104">Если передача toohello эмулятор хранилища Microsoft Azure или tooAzure хранилища диагностических данных не хранится без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="ab702-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="ab702-105">Поместив данные в хранилище, вы можете просматривать их с помощью одного из нескольких доступных средств.</span><span class="sxs-lookup"><span data-stu-id="ab702-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="ab702-106">Определение учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="ab702-106">Specify a storage account</span></span>
<span data-ttu-id="ab702-107">Можно указать hello хранилища учетной записи, которую toouse в файле ServiceConfiguration.cscfg hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="ab702-108">сведения об учетной записи Hello определяется как строка подключения в параметре конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ab702-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="ab702-109">Hello ниже приведен пример создания нового проекта облачной службы в Visual Studio строка подключения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="ab702-110">Можно изменить данные этой строки соединения tooprovide учетной записи для учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ab702-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="ab702-111">В зависимости от типа диагностических данных, собираемых hello Диагностика Azure использует hello BLOB-объектов или службе таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="ab702-112">Hello следующей таблице показаны сохраняемые источники данных hello и их формат.</span><span class="sxs-lookup"><span data-stu-id="ab702-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="ab702-113">Источник данных</span><span class="sxs-lookup"><span data-stu-id="ab702-113">Data source</span></span> | <span data-ttu-id="ab702-114">Формат хранения</span><span class="sxs-lookup"><span data-stu-id="ab702-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="ab702-115">Журналы Azure</span><span class="sxs-lookup"><span data-stu-id="ab702-115">Azure logs</span></span> |<span data-ttu-id="ab702-116">Таблица</span><span class="sxs-lookup"><span data-stu-id="ab702-116">Table</span></span> |
| <span data-ttu-id="ab702-117">Журналы IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="ab702-117">IIS 7.0 logs</span></span> |<span data-ttu-id="ab702-118">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ab702-118">Blob</span></span> |
| <span data-ttu-id="ab702-119">Журналы инфраструктуры системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="ab702-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="ab702-120">Таблица</span><span class="sxs-lookup"><span data-stu-id="ab702-120">Table</span></span> |
| <span data-ttu-id="ab702-121">Журналы трассировки невыполненных запросов</span><span class="sxs-lookup"><span data-stu-id="ab702-121">Failed Request Trace logs</span></span> |<span data-ttu-id="ab702-122">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ab702-122">Blob</span></span> |
| <span data-ttu-id="ab702-123">Журналы событий Windows</span><span class="sxs-lookup"><span data-stu-id="ab702-123">Windows Event logs</span></span> |<span data-ttu-id="ab702-124">Таблица</span><span class="sxs-lookup"><span data-stu-id="ab702-124">Table</span></span> |
| <span data-ttu-id="ab702-125">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="ab702-125">Performance counters</span></span> |<span data-ttu-id="ab702-126">Таблица</span><span class="sxs-lookup"><span data-stu-id="ab702-126">Table</span></span> |
| <span data-ttu-id="ab702-127">Аварийные дампы</span><span class="sxs-lookup"><span data-stu-id="ab702-127">Crash dumps</span></span> |<span data-ttu-id="ab702-128">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ab702-128">Blob</span></span> |
| <span data-ttu-id="ab702-129">Пользовательские журналы ошибок</span><span class="sxs-lookup"><span data-stu-id="ab702-129">Custom error logs</span></span> |<span data-ttu-id="ab702-130">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ab702-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="ab702-131">Передача диагностических данных</span><span class="sxs-lookup"><span data-stu-id="ab702-131">Transfer diagnostic data</span></span>
<span data-ttu-id="ab702-132">Для пакета SDK 2.5 и более поздних версиях hello запроса tootransfer диагностических данных может произойти через файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="ab702-133">Данные диагностики можно переносить через запланированные промежутки времени, как указано в конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="ab702-134">Для пакета SDK 2.4 и предыдущим можно запросить tootransfer hello диагностических данных через hello файл конфигурации, а также программным способом.</span><span class="sxs-lookup"><span data-stu-id="ab702-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="ab702-135">Hello программный подход также позволяет toodo передачи по запросу.</span><span class="sxs-lookup"><span data-stu-id="ab702-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab702-136">При передаче диагностических данных tooan учетной записи хранилища Azure, вас взимается плата за ресурсы хранилища hello, используемые вашими диагностическими данными.</span><span class="sxs-lookup"><span data-stu-id="ab702-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="ab702-137">Хранение диагностических данных</span><span class="sxs-lookup"><span data-stu-id="ab702-137">Store diagnostic data</span></span>
<span data-ttu-id="ab702-138">Данные журнала хранятся в хранилище BLOB-объекта или таблицы с hello следующие имена:</span><span class="sxs-lookup"><span data-stu-id="ab702-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="ab702-139">**Таблицы**</span><span class="sxs-lookup"><span data-stu-id="ab702-139">**Tables**</span></span>

* <span data-ttu-id="ab702-140">**WadLogsTable** - журналы, записываемые в коде с помощью прослушивателя трассировки hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="ab702-141">**WADDiagnosticInfrastructureLogsTable** : сведения об изменениях конфигурации и монитора диагностики.</span><span class="sxs-lookup"><span data-stu-id="ab702-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="ab702-142">**WADDirectoriesTable** — каталоги наблюдает монитор диагностики, hello.</span><span class="sxs-lookup"><span data-stu-id="ab702-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="ab702-143">Сюда входят журналы IIS, журналы неудачно завершенных запросов IIS и пользовательские папки.</span><span class="sxs-lookup"><span data-stu-id="ab702-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="ab702-144">в поле RelativePath hello Hello расположение файла журнала большого двоичного объекта hello указано в поле hello контейнера и имя hello hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ab702-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="ab702-145">поле AbsolutePath Hello указывает hello расположение и имя файла hello, находившимся hello виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="ab702-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="ab702-146">**WADPerformanceCountersTable** : данные счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="ab702-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="ab702-147">**WADWindowsEventLogsTable** : журналы событий Windows.</span><span class="sxs-lookup"><span data-stu-id="ab702-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="ab702-148">**BLOB-объекты**</span><span class="sxs-lookup"><span data-stu-id="ab702-148">**Blobs**</span></span>

* <span data-ttu-id="ab702-149">**wad-control-container** — (только для SDK 2.4 и предыдущих) содержит файлы конфигурации XML hello, управляющие hello диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="ab702-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="ab702-150">**wad-iis-failedreqlogfiles** : содержит сведения журналов неудачно завершенных запросов IIS.</span><span class="sxs-lookup"><span data-stu-id="ab702-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="ab702-151">**wad-iis-logfiles** : содержит сведения о журналах IIS.</span><span class="sxs-lookup"><span data-stu-id="ab702-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="ab702-152">**«custom»** — пользовательский контейнер, основанный на каталогах, которые отслеживаются монитором диагностики hello настройки.</span><span class="sxs-lookup"><span data-stu-id="ab702-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="ab702-153">Hello имя этого контейнера больших двоичных объектов указываются в элементе WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="ab702-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="ab702-154">Средства tooview диагностических данных</span><span class="sxs-lookup"><span data-stu-id="ab702-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="ab702-155">Несколько инструментов, доступных tooview hello данных после toostorage переносятся.</span><span class="sxs-lookup"><span data-stu-id="ab702-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="ab702-156">Например:</span><span class="sxs-lookup"><span data-stu-id="ab702-156">For example:</span></span>

* <span data-ttu-id="ab702-157">Обозреватель серверов в Visual Studio — Если вы установили hello Azure Tools для Microsoft Visual Studio, можно использовать узел хранилища Azure hello в обозревателе серверов tooview только для чтения больших двоичных объектов и таблиц данных из учетных записей хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ab702-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="ab702-158">Вы можете отображать данные из своей локальной учетной записи эмулятора хранения, а также из учетных записей хранения, созданных для Azure.</span><span class="sxs-lookup"><span data-stu-id="ab702-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="ab702-159">Дополнительные сведения см. в статье [Обзор ресурсов хранилища с помощью обозревателя сервера и управление ими](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="ab702-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="ab702-160">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) имеет отдельное приложение, позволяющее tooeasily работы с данными хранилища Azure для Windows, OSX и Linux.</span><span class="sxs-lookup"><span data-stu-id="ab702-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="ab702-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) включает в себя Azure Diagnostics Manager служащее tooview, загрузки и управления ими hello диагностические данные, собранные hello приложений, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="ab702-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab702-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab702-162">Next Steps</span></span>
[<span data-ttu-id="ab702-163">Поток hello трассировки в приложении облачные службы с помощью системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="ab702-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

