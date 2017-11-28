---
title: "Включение метрик хранилища на портале Azure | Документация Майкрософт"
description: "Как включить метрики хранилища для служб больших двоичных объектов, очередей, таблиц и файлов."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4d6065597a41372ea6d320ab318b0c71d6a48b2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="c5ed8-103">Включение метрик хранилища и просмотр данных метрик</span><span class="sxs-lookup"><span data-stu-id="c5ed8-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="c5ed8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c5ed8-104">Overview</span></span>
<span data-ttu-id="c5ed8-105">Метрики хранилища включаются по умолчанию при создании учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="c5ed8-106">Вы можете нас троить мониторинг с помощью [классического портала Azure](https://manage.windowsazure.com), Windows PowerShell или программно с помощью API службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-106">You can configure monitoring using either the [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="c5ed8-107">При включении метрик хранилища необходимо выбрать период хранения данных. Он определяет длительность хранения метрик службой хранилища и размер оплаты пространства, необходимого для их хранения.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-107">When you enable Storage Metrics, you must choose a retention period for the data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="c5ed8-108">Как правило, следует использовать менее длительный период хранения для минутных метрик, нежели для часовых метрик, так как минутные метрики требуют значительно большего пространства.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="c5ed8-109">Следует выбрать такой период хранения, чтобы было достаточно времени на анализ данных и скачивание метрик, которые требуется сохранить локально для анализа или составления отчета.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="c5ed8-110">Помните, что за скачивание данных метрик из учетной записи хранения также взимается плата.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a><span data-ttu-id="c5ed8-111">Как включить метрики хранилища с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="c5ed8-111">How to enable Storage metrics using the Azure Classic Portal</span></span>
<span data-ttu-id="c5ed8-112">На [классическом портале Azure](https://manage.windowsazure.com)управление метриками хранилища осуществляется на странице "Настройка" для определенной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-112">In the [Azure Classic Portal](https://manage.windowsazure.com), you use the Configure page for a storage account to control Storage Metrics.</span></span> <span data-ttu-id="c5ed8-113">Для выполнения мониторинга можно задать уровень и период хранения (в днях) для каждого большого двоичного объекта, таблицы и очереди.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="c5ed8-114">В каждом из случаев используется один из следующих уровней:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-114">In each case, the level is one of the following:</span></span>

* <span data-ttu-id="c5ed8-115">"Выключено" — сбор метрик не осуществляется.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="c5ed8-116">Минимальный — метрики хранилища собирают базовый набор таких метрик, как исходящие и входящие данные, доступность, задержка и процент успешных операций, который агрегируется для служб BLOB-объектов, таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for the Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="c5ed8-117">"Подробный" — осуществляется сбор полного набора метрик, включая метрики для каждой операции API хранилища, а также метрик уровня службы.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-117">Verbose — Storage Metrics collects a full set of metrics that includes the same metrics for each storage API operation, in addition to the service-level metrics.</span></span> <span data-ttu-id="c5ed8-118">Подробные метрики позволяют осуществлять более тщательный анализ проблем, возникающих во время работы приложений.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="c5ed8-119">Обратите внимание, что в настоящее время классический портал Azure не позволяет настраивать минутные метрики в учетной записи хранения. Их необходимо включить с помощью PowerShell или программно.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-119">Note that the Azure Classic Portal does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-storage-metrics-using-powershell"></a><span data-ttu-id="c5ed8-120">Как включить метрики хранилища с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5ed8-120">How to enable Storage metrics using PowerShell</span></span>
<span data-ttu-id="c5ed8-121">Чтобы настроить метрики хранилища для учетной записи хранения, можно использовать PowerShell на локальном компьютере, выполнив командлет Azure PowerShell Get-AzureStorageServiceMetricsProperty для получения текущих настроек и командлет Set-AzureStorageServiceMetricsProperty для их изменения.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="c5ed8-122">Командлеты, позволяющие управлять метриками хранилища, имеют следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="c5ed8-123">Возможными значениями MetricsType являются Hour и Minute.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="c5ed8-124">Возможными значениями ServiceType являются Blob, Queue и Table.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="c5ed8-125">Возможными значениями MetricsLevel являются None (эквивалентно значению "Выключено" на классическом портале Azure), Service (эквивалентно значению "Минимальный" на классическом портале Azure) и ServiceAndApi (эквивалентно значению "Подробный" на классическом портале Azure).</span><span class="sxs-lookup"><span data-stu-id="c5ed8-125">MetricsLevel possible values are None (equivalent to Off in the Azure Classic Portal), Service (equivalent to Minimal in the Azure Classic Portal), and ServiceAndApi (equivalent to Verbose in the Azure Classic Portal).</span></span>

<span data-ttu-id="c5ed8-126">Например, следующая команда выключает минутные метрики для службы BLOB-объектов в учетной записи хранения по умолчанию с установкой пятидневного периода хранения:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-126">For example, the following command switches on minute metrics for the blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="c5ed8-127">Следующая команда получает текущий уровень часовых метрик и длительность периода хранения в днях для службы BLOB-объектов в учетной записи хранения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="c5ed8-128">Дополнительные сведения о настройке командлетов Azure PowerShell для работы с подпиской Azure и о выборе учетной записи хранения по умолчанию см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5ed8-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="c5ed8-129">Как программно включить метрики хранилища</span><span class="sxs-lookup"><span data-stu-id="c5ed8-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="c5ed8-130">В следующем фрагменте кода C# показано, как включить метрики и ведение журнала для службы BLOB-объектов с помощью клиентской библиотеки хранилища для .NET.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="c5ed8-131">Просмотр метрик хранилища</span><span class="sxs-lookup"><span data-stu-id="c5ed8-131">Viewing Storage metrics</span></span>
<span data-ttu-id="c5ed8-132">После настройки метрик хранилища для мониторинга учетной записи хранения метрики записываются в набор известных таблиц в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-132">When you have configured Storage Metrics to monitor your storage account, it records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="c5ed8-133">Просматривать часовые метрики по мере их появления на диаграмме можно на странице "Монитор" учетной записи хранения на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-133">You can use the Monitor page for your storage account in the Azure Classic Portal to view the hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="c5ed8-134">На этой странице классического портала Azure можно:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-134">On this page in the Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="c5ed8-135">Выбирать метрики для отображения на диаграмме (набор доступных метрик зависит от того, какой тип мониторинга службы выбран на странице "Настройка": подробный или минимальный).</span><span class="sxs-lookup"><span data-stu-id="c5ed8-135">Select which metrics to plot on the chart (the choice of available metrics will depend on whether you chose verbose or minimal monitoring for the service on the Configure page).</span></span>
* <span data-ttu-id="c5ed8-136">Выбирать интервал времени для метрик, отображаемых на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-136">Select the time range for the metrics displayed on the chart.</span></span>
* <span data-ttu-id="c5ed8-137">Выбирать абсолютную или относительную шкалу для построения метрик.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-137">Choose to use an absolute or relative scale to plot the metrics.</span></span>
* <span data-ttu-id="c5ed8-138">Настраивать оповещения по электронной почте, чтобы получать уведомления при достижении определенного значения конкретной метрики.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-138">Configure email alerts to notify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="c5ed8-139">Чтобы скачивать метрики для длительного хранения или анализа в локальной среде, необходимо использовать соответствующий инструмент или написать код для чтения таблиц.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to use a tool or write some code to read the tables.</span></span> <span data-ttu-id="c5ed8-140">Необходимо скачать минутные метрики для анализа.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-140">You must download the minute metrics for analysis.</span></span> <span data-ttu-id="c5ed8-141">Таблицы не отображаются, если в учетной записи хранения выведены все таблицы. Однако к ним можно обращаться напрямую по имени.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-141">The tables do not appear if you list all the tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="c5ed8-142">Многие сторонние инструменты обзора хранилищ поддерживают эти таблицы и позволяют просматривать их непосредственно (см. список доступных инструментов в записи блога [Обозреватели службы хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)).</span><span class="sxs-lookup"><span data-stu-id="c5ed8-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly (see the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="c5ed8-143">Часовые метрики</span><span class="sxs-lookup"><span data-stu-id="c5ed8-143">Hourly metrics</span></span>
* <span data-ttu-id="c5ed8-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="c5ed8-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="c5ed8-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="c5ed8-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="c5ed8-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="c5ed8-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="c5ed8-147">Минутные метрики</span><span class="sxs-lookup"><span data-stu-id="c5ed8-147">Minute metrics</span></span>
* <span data-ttu-id="c5ed8-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="c5ed8-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="c5ed8-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="c5ed8-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="c5ed8-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="c5ed8-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="c5ed8-151">Емкость</span><span class="sxs-lookup"><span data-stu-id="c5ed8-151">Capacity</span></span>
* <span data-ttu-id="c5ed8-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="c5ed8-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="c5ed8-153">Подробные сведения о схемах для этих таблиц см. в разделе [Схема таблицы метрик аналитики хранилища](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5ed8-153">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="c5ed8-154">В примере строк ниже отражена только часть доступных столбцов, однако он иллюстрирует некоторые важные возможности сохранения метрик с помощью метрик хранилища:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-154">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="c5ed8-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="c5ed8-155">PartitionKey</span></span> | <span data-ttu-id="c5ed8-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="c5ed8-156">RowKey</span></span> | <span data-ttu-id="c5ed8-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c5ed8-157">Timestamp</span></span> | <span data-ttu-id="c5ed8-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="c5ed8-158">TotalRequests</span></span> | <span data-ttu-id="c5ed8-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="c5ed8-159">TotalBillableRequests</span></span> | <span data-ttu-id="c5ed8-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="c5ed8-160">TotalIngress</span></span> | <span data-ttu-id="c5ed8-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="c5ed8-161">TotalEgress</span></span> | <span data-ttu-id="c5ed8-162">Доступность</span><span class="sxs-lookup"><span data-stu-id="c5ed8-162">Availability</span></span> | <span data-ttu-id="c5ed8-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="c5ed8-163">AverageE2ELatency</span></span> | <span data-ttu-id="c5ed8-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="c5ed8-164">AverageServerLatency</span></span> | <span data-ttu-id="c5ed8-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="c5ed8-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c5ed8-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-166">20140522T1100</span></span> |<span data-ttu-id="c5ed8-167">user;All</span><span class="sxs-lookup"><span data-stu-id="c5ed8-167">user;All</span></span> |<span data-ttu-id="c5ed8-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c5ed8-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c5ed8-169">7</span><span class="sxs-lookup"><span data-stu-id="c5ed8-169">7</span></span> |<span data-ttu-id="c5ed8-170">7</span><span class="sxs-lookup"><span data-stu-id="c5ed8-170">7</span></span> |<span data-ttu-id="c5ed8-171">4003</span><span class="sxs-lookup"><span data-stu-id="c5ed8-171">4003</span></span> |<span data-ttu-id="c5ed8-172">46801</span><span class="sxs-lookup"><span data-stu-id="c5ed8-172">46801</span></span> |<span data-ttu-id="c5ed8-173">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-173">100</span></span> |<span data-ttu-id="c5ed8-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="c5ed8-174">104.4286</span></span> |<span data-ttu-id="c5ed8-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="c5ed8-175">6.857143</span></span> |<span data-ttu-id="c5ed8-176">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-176">100</span></span> |
| <span data-ttu-id="c5ed8-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-177">20140522T1100</span></span> |<span data-ttu-id="c5ed8-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="c5ed8-178">user;QueryEntities</span></span> |<span data-ttu-id="c5ed8-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="c5ed8-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="c5ed8-180">5</span><span class="sxs-lookup"><span data-stu-id="c5ed8-180">5</span></span> |<span data-ttu-id="c5ed8-181">5</span><span class="sxs-lookup"><span data-stu-id="c5ed8-181">5</span></span> |<span data-ttu-id="c5ed8-182">2694</span><span class="sxs-lookup"><span data-stu-id="c5ed8-182">2694</span></span> |<span data-ttu-id="c5ed8-183">45951</span><span class="sxs-lookup"><span data-stu-id="c5ed8-183">45951</span></span> |<span data-ttu-id="c5ed8-184">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-184">100</span></span> |<span data-ttu-id="c5ed8-185">143.8</span><span class="sxs-lookup"><span data-stu-id="c5ed8-185">143.8</span></span> |<span data-ttu-id="c5ed8-186">7.8</span><span class="sxs-lookup"><span data-stu-id="c5ed8-186">7.8</span></span> |<span data-ttu-id="c5ed8-187">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-187">100</span></span> |
| <span data-ttu-id="c5ed8-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-188">20140522T1100</span></span> |<span data-ttu-id="c5ed8-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="c5ed8-189">user;QueryEntity</span></span> |<span data-ttu-id="c5ed8-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c5ed8-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c5ed8-191">1</span><span class="sxs-lookup"><span data-stu-id="c5ed8-191">1</span></span> |<span data-ttu-id="c5ed8-192">1</span><span class="sxs-lookup"><span data-stu-id="c5ed8-192">1</span></span> |<span data-ttu-id="c5ed8-193">538</span><span class="sxs-lookup"><span data-stu-id="c5ed8-193">538</span></span> |<span data-ttu-id="c5ed8-194">633</span><span class="sxs-lookup"><span data-stu-id="c5ed8-194">633</span></span> |<span data-ttu-id="c5ed8-195">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-195">100</span></span> |<span data-ttu-id="c5ed8-196">3</span><span class="sxs-lookup"><span data-stu-id="c5ed8-196">3</span></span> |<span data-ttu-id="c5ed8-197">3</span><span class="sxs-lookup"><span data-stu-id="c5ed8-197">3</span></span> |<span data-ttu-id="c5ed8-198">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-198">100</span></span> |
| <span data-ttu-id="c5ed8-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-199">20140522T1100</span></span> |<span data-ttu-id="c5ed8-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="c5ed8-200">user;UpdateEntity</span></span> |<span data-ttu-id="c5ed8-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c5ed8-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c5ed8-202">1</span><span class="sxs-lookup"><span data-stu-id="c5ed8-202">1</span></span> |<span data-ttu-id="c5ed8-203">1</span><span class="sxs-lookup"><span data-stu-id="c5ed8-203">1</span></span> |<span data-ttu-id="c5ed8-204">771</span><span class="sxs-lookup"><span data-stu-id="c5ed8-204">771</span></span> |<span data-ttu-id="c5ed8-205">217</span><span class="sxs-lookup"><span data-stu-id="c5ed8-205">217</span></span> |<span data-ttu-id="c5ed8-206">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-206">100</span></span> |<span data-ttu-id="c5ed8-207">9</span><span class="sxs-lookup"><span data-stu-id="c5ed8-207">9</span></span> |<span data-ttu-id="c5ed8-208">6</span><span class="sxs-lookup"><span data-stu-id="c5ed8-208">6</span></span> |<span data-ttu-id="c5ed8-209">100</span><span class="sxs-lookup"><span data-stu-id="c5ed8-209">100</span></span> |

<span data-ttu-id="c5ed8-210">В этом примере данных минутной метрики для ключа раздела используется время с минутным разрешением.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-210">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="c5ed8-211">Ключ строки определяет тип данных, которые хранятся в строке, и состоит из двух фрагментов данных — типа доступа и типа запроса:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-211">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="c5ed8-212">Типом доступа является либо user, либо system, где user означает все запросы пользователей к службе хранилища, а system означает запросы, выполненные с помощью аналитики хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-212">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="c5ed8-213">Типом запроса является либо all, в случае чего это строка сводки, либо он определяет конкретный API, например QueryEntity или UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-213">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="c5ed8-214">В примере данных выше показаны все записи за одну минуту (начиная с 11:00). Таким образом, если сложить количество запросов QueryEntities, количество запросов QueryEntity и количество запросов UpdateEntity, в сумме получится семь, и эта сумма отображается в строке user:All.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-214">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="c5ed8-215">Аналогичным образом можно определить среднюю сквозную задержку 104.4286 в строке user:All, вычислив ((143,8 * 5) + 3 + 9)/7.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-215">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="c5ed8-216">Рекомендуется настроить оповещения на странице "Монитор" классического портала Azure, чтобы автоматически получать уведомления от метрик хранилища в случае внесения важных изменений в поведение служб хранилища. Если данные метрик скачиваются в формате с разделителями через обозреватель хранилища, их можно анализировать с помощью Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-216">You should consider setting up alerts in the Azure Classic Portal on the Monitor page so that Storage Metrics can automatically notify you of any important changes in the behavior of your storage services.If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="c5ed8-217">Список доступных инструментов обозревателя хранилища см. в записи блога [Обозреватели службы хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5ed8-217">See the blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="c5ed8-218">Программный доступ к данным метрик</span><span class="sxs-lookup"><span data-stu-id="c5ed8-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="c5ed8-219">В следующем списке показан пример кода на C#, в котором реализован доступ к минутным метрикам для диапазона минут с отображением результатов в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-219">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="c5ed8-220">В данном случае используется библиотека хранилища Azure версии 4, включающая класс CloudAnalyticsClient, упрощающий доступ к таблицам метрик в хранилище.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-220">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="c5ed8-221">Какова стоимость включения метрик хранилища?</span><span class="sxs-lookup"><span data-stu-id="c5ed8-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="c5ed8-222">За запросы записи на создание сущностей таблиц для метрик взимается плата в соответствии со стандартными тарифами, применимыми ко всем операциям службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-222">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="c5ed8-223">К запросам на чтение и удаление, формируемым клиентом в отношении данных метрик, также применяются стандартные тарифы.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-223">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="c5ed8-224">Если вы настроили политику хранения данных, за удаление старых данных метрик хранилищем Azure плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="c5ed8-225">Однако при удалении данных аналитики с учетной записи будет взиматься плата за операции удаления.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-225">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="c5ed8-226">За пространство, занимаемое таблицами метрик, также взимается плата. Оценить объем пространства, используемый для хранения данных метрик, можно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-226">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="c5ed8-227">Если за каждый час служба использует каждый API в каждой службе, то каждый час в таблицах транзакций метрик сохраняется примерно 148 КБ данных, если сводка охватывает уровень службы и уровень API.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="c5ed8-228">Если за каждый час служба использует каждый API в каждой службе, то каждый час в таблицах транзакций метрик сохраняется примерно 12 КБ данных, если сводка охватывает только уровень службы.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="c5ed8-229">В таблице емкости больших двоичных объектов ежедневно добавляются две строки (если пользователь выбрал использование журналов). При этом размер этой таблицы ежедневно увеличивается примерно на 300 байтов.</span><span class="sxs-lookup"><span data-stu-id="c5ed8-229">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5ed8-230">Дальнейшие действия:</span><span class="sxs-lookup"><span data-stu-id="c5ed8-230">Next steps:</span></span>
[<span data-ttu-id="c5ed8-231">Включение ведения журнала аналитики и доступа к данным журнала хранилища</span><span class="sxs-lookup"><span data-stu-id="c5ed8-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
