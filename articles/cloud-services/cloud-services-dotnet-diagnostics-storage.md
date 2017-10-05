---
title: "Хранение и просмотр диагностических данных в службе хранилища Azure | Документация Майкрософт"
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="2e944-103">Хранение и просмотр диагностических данных в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="2e944-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="2e944-104">Диагностические данные не хранятся долго. Для длительного хранения их необходимо переместить в эмулятор хранения Microsoft Azure или в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="2e944-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="2e944-105">Поместив данные в хранилище, вы можете просматривать их с помощью одного из нескольких доступных средств.</span><span class="sxs-lookup"><span data-stu-id="2e944-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="2e944-106">Определение учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="2e944-106">Specify a storage account</span></span>
<span data-ttu-id="2e944-107">Укажите учетную запись хранения, которая будет использоваться, в файле ServiceConfiguration.cscfg.</span><span class="sxs-lookup"><span data-stu-id="2e944-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="2e944-108">Сведения об учетной записи определяются в виде строки подключения в параметре конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2e944-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="2e944-109">В следующем примере приведена строка подключения по умолчанию, созданная для нового проекта облачной службы в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e944-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="2e944-110">Эту строку подключения можно изменить, чтобы указать сведения об учетной записи для учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2e944-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="2e944-111">В зависимости от типа собираемых диагностических данных система диагностики Azure использует службу BLOB-объектов или службу таблиц.</span><span class="sxs-lookup"><span data-stu-id="2e944-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="2e944-112">В следующей таблице приведены сохраняемые источники данных и их формат.</span><span class="sxs-lookup"><span data-stu-id="2e944-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="2e944-113">Источник данных</span><span class="sxs-lookup"><span data-stu-id="2e944-113">Data source</span></span> | <span data-ttu-id="2e944-114">Формат хранения</span><span class="sxs-lookup"><span data-stu-id="2e944-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="2e944-115">Журналы Azure</span><span class="sxs-lookup"><span data-stu-id="2e944-115">Azure logs</span></span> |<span data-ttu-id="2e944-116">Таблица</span><span class="sxs-lookup"><span data-stu-id="2e944-116">Table</span></span> |
| <span data-ttu-id="2e944-117">Журналы IIS 7.0</span><span class="sxs-lookup"><span data-stu-id="2e944-117">IIS 7.0 logs</span></span> |<span data-ttu-id="2e944-118">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="2e944-118">Blob</span></span> |
| <span data-ttu-id="2e944-119">Журналы инфраструктуры системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="2e944-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="2e944-120">Таблица</span><span class="sxs-lookup"><span data-stu-id="2e944-120">Table</span></span> |
| <span data-ttu-id="2e944-121">Журналы трассировки невыполненных запросов</span><span class="sxs-lookup"><span data-stu-id="2e944-121">Failed Request Trace logs</span></span> |<span data-ttu-id="2e944-122">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="2e944-122">Blob</span></span> |
| <span data-ttu-id="2e944-123">Журналы событий Windows</span><span class="sxs-lookup"><span data-stu-id="2e944-123">Windows Event logs</span></span> |<span data-ttu-id="2e944-124">Таблица</span><span class="sxs-lookup"><span data-stu-id="2e944-124">Table</span></span> |
| <span data-ttu-id="2e944-125">Счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="2e944-125">Performance counters</span></span> |<span data-ttu-id="2e944-126">Таблица</span><span class="sxs-lookup"><span data-stu-id="2e944-126">Table</span></span> |
| <span data-ttu-id="2e944-127">Аварийные дампы</span><span class="sxs-lookup"><span data-stu-id="2e944-127">Crash dumps</span></span> |<span data-ttu-id="2e944-128">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="2e944-128">Blob</span></span> |
| <span data-ttu-id="2e944-129">Пользовательские журналы ошибок</span><span class="sxs-lookup"><span data-stu-id="2e944-129">Custom error logs</span></span> |<span data-ttu-id="2e944-130">BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="2e944-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="2e944-131">Передача диагностических данных</span><span class="sxs-lookup"><span data-stu-id="2e944-131">Transfer diagnostic data</span></span>
<span data-ttu-id="2e944-132">При использовании пакета SDK 2.5 и более поздних версий запрос на передачу диагностических данных можно создавать с помощью файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2e944-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="2e944-133">Диагностические данные могут передаваться через запланированные промежутки времени, заданные в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2e944-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="2e944-134">При использовании пакета SDK 2.4 и предыдущих версий запрос на передачу диагностических данных можно выполнить с помощью файла конфигурации или программным образом.</span><span class="sxs-lookup"><span data-stu-id="2e944-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="2e944-135">Программный подход позволяет передавать данные по требованию.</span><span class="sxs-lookup"><span data-stu-id="2e944-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e944-136">При передаче диагностических данных в учетную запись хранения Azure с вас взимается плата за используемые этими данными ресурсы хранилища.</span><span class="sxs-lookup"><span data-stu-id="2e944-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="2e944-137">Хранение диагностических данных</span><span class="sxs-lookup"><span data-stu-id="2e944-137">Store diagnostic data</span></span>
<span data-ttu-id="2e944-138">Данные журнала хранятся в хранилище BLOB-объектов или в табличном хранилище со следующими именами.</span><span class="sxs-lookup"><span data-stu-id="2e944-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="2e944-139">**Таблицы**</span><span class="sxs-lookup"><span data-stu-id="2e944-139">**Tables**</span></span>

* <span data-ttu-id="2e944-140">**WadLogsTable** : включенные в код журналы с данными прослушивателя трассировки.</span><span class="sxs-lookup"><span data-stu-id="2e944-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="2e944-141">**WADDiagnosticInfrastructureLogsTable** : сведения об изменениях конфигурации и монитора диагностики.</span><span class="sxs-lookup"><span data-stu-id="2e944-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="2e944-142">**WADDirectoriesTable** : сведения о каталогах, которые отслеживает монитор диагностики.</span><span class="sxs-lookup"><span data-stu-id="2e944-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="2e944-143">Сюда входят журналы IIS, журналы неудачно завершенных запросов IIS и пользовательские папки.</span><span class="sxs-lookup"><span data-stu-id="2e944-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="2e944-144">Расположение файла журнала BLOB-объекта указано в поле Container, а имя большого двоичного объекта — в поле RelativePath.</span><span class="sxs-lookup"><span data-stu-id="2e944-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="2e944-145">В поле AbsolutePath указано расположение и имя файла на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="2e944-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="2e944-146">**WADPerformanceCountersTable** : данные счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="2e944-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="2e944-147">**WADWindowsEventLogsTable** : журналы событий Windows.</span><span class="sxs-lookup"><span data-stu-id="2e944-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="2e944-148">**BLOB-объекты**</span><span class="sxs-lookup"><span data-stu-id="2e944-148">**Blobs**</span></span>

* <span data-ttu-id="2e944-149">**wad-control-container** : содержит XML-файлы конфигурации, управляющие диагностикой Azure (только для пакета SDK 2.4 и предыдущих версий).</span><span class="sxs-lookup"><span data-stu-id="2e944-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="2e944-150">**wad-iis-failedreqlogfiles** : содержит сведения журналов неудачно завершенных запросов IIS.</span><span class="sxs-lookup"><span data-stu-id="2e944-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="2e944-151">**wad-iis-logfiles** : содержит сведения о журналах IIS.</span><span class="sxs-lookup"><span data-stu-id="2e944-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="2e944-152">**custom** : пользовательский контейнер на основе каталогов конфигурации, которые отслеживаются монитором диагностики.</span><span class="sxs-lookup"><span data-stu-id="2e944-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="2e944-153">Имя этого контейнера BLOB-объектов указывается в элементе WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="2e944-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="2e944-154">Средства для просмотра диагностических данных</span><span class="sxs-lookup"><span data-stu-id="2e944-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="2e944-155">Данные после их передачи в хранилище можно просмотреть с помощью нескольких средств.</span><span class="sxs-lookup"><span data-stu-id="2e944-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="2e944-156">Например:</span><span class="sxs-lookup"><span data-stu-id="2e944-156">For example:</span></span>

* <span data-ttu-id="2e944-157">Обозреватель сервера в Visual Studio. Если установлены инструменты Azure для Microsoft Visual Studio, можно использовать узел хранилища Azure в обозревателе сервера для просмотра больших двоичных объектов, доступных только для чтения, и табличных данных из учетных записей хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2e944-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="2e944-158">Вы можете отображать данные из своей локальной учетной записи эмулятора хранения, а также из учетных записей хранения, созданных для Azure.</span><span class="sxs-lookup"><span data-stu-id="2e944-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="2e944-159">Дополнительные сведения см. в статье [Обзор ресурсов хранилища с помощью обозревателя сервера и управление ими](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="2e944-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="2e944-160">[Обозреватель службы хранилища Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это автономное приложение, которое упрощает работу с данными из службы хранилища Azure на платформе Windows, OSX и Linux.</span><span class="sxs-lookup"><span data-stu-id="2e944-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="2e944-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) содержит диспетчер диагностики Azure, который позволяет просматривать и скачивать данные диагностики, которые собирают выполняемые в Azure приложения, а также управлять этими данными.</span><span class="sxs-lookup"><span data-stu-id="2e944-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e944-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e944-162">Next Steps</span></span>
[<span data-ttu-id="2e944-163">Трассировка потока в приложении облачных служб с помощью системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="2e944-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

