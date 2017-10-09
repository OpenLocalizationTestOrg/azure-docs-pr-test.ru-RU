---
title: "метрики хранилища aaaEnabling в hello портал Azure | Документы Microsoft"
description: "Как tooenable метрик хранилища для hello служб больших двоичных объектов, очередей, таблицы и файла"
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
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="e78af-103">Включение метрик хранилища и просмотр данных метрик</span><span class="sxs-lookup"><span data-stu-id="e78af-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="e78af-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e78af-104">Overview</span></span>
<span data-ttu-id="e78af-105">Метрики хранилища включаются по умолчанию при создании учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e78af-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="e78af-106">Вы можете настроить отслеживание с помощью либо hello [классический портал Azure](https://manage.windowsazure.com), Windows PowerShell или программно через API-Интерфейс хранилища.</span><span class="sxs-lookup"><span data-stu-id="e78af-106">You can configure monitoring using either hello [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="e78af-107">При включении метрик хранилища необходимо выбрать период хранения для данных hello: этот период определяет срок хранения hello служба поддерживает метрики hello и расходов для hello пространство необходимые toostore их.</span><span class="sxs-lookup"><span data-stu-id="e78af-107">When you enable Storage Metrics, you must choose a retention period for hello data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="e78af-108">Как правило следует использовать короткий срок хранения для ежеминутных метрик, нежели для часовых метрик из-за hello Требую значительно большего пространства для минутных метрик.</span><span class="sxs-lookup"><span data-stu-id="e78af-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="e78af-109">Таким образом, чтобы иметь достаточно времени tooanalyze hello данных и загрузку метрик, нужно tookeep локально для анализа или составления следует выбрать период хранения.</span><span class="sxs-lookup"><span data-stu-id="e78af-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="e78af-110">Помните, что за скачивание данных метрик из учетной записи хранения также взимается плата.</span><span class="sxs-lookup"><span data-stu-id="e78af-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a><span data-ttu-id="e78af-111">Как с помощью метрик хранилища tooenable hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="e78af-111">How tooenable Storage metrics using hello Azure Classic Portal</span></span>
<span data-ttu-id="e78af-112">В hello [классический портал Azure](https://manage.windowsazure.com), используйте страницу "Настройка" hello для toocontrol учетной записи хранения метрик хранилища.</span><span class="sxs-lookup"><span data-stu-id="e78af-112">In hello [Azure Classic Portal](https://manage.windowsazure.com), you use hello Configure page for a storage account toocontrol Storage Metrics.</span></span> <span data-ttu-id="e78af-113">Для выполнения мониторинга можно задать уровень и период хранения (в днях) для каждого большого двоичного объекта, таблицы и очереди.</span><span class="sxs-lookup"><span data-stu-id="e78af-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="e78af-114">В каждом случае hello уровень является одним из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="e78af-114">In each case, hello level is one of hello following:</span></span>

* <span data-ttu-id="e78af-115">"Выключено" — сбор метрик не осуществляется.</span><span class="sxs-lookup"><span data-stu-id="e78af-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="e78af-116">Минимум — Осуществляется сбор базового набора метрик, таких как исходящие и входящие данные, доступность, задержка и процент успешных операций, который агрегируется для служб больших двоичных объектов, таблиц и очередей hello.</span><span class="sxs-lookup"><span data-stu-id="e78af-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for hello Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="e78af-117">Подробный — Полный набор метрик, включая собирает метрики хранилища Здравствуйте одинаковых метрик для каждого хранилища API-операции, кроме toohello уровня обслуживания метрики.</span><span class="sxs-lookup"><span data-stu-id="e78af-117">Verbose — Storage Metrics collects a full set of metrics that includes hello same metrics for each storage API operation, in addition toohello service-level metrics.</span></span> <span data-ttu-id="e78af-118">Подробные метрики позволяют осуществлять более тщательный анализ проблем, возникающих во время работы приложений.</span><span class="sxs-lookup"><span data-stu-id="e78af-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="e78af-119">Обратите внимание, что hello классический портал Azure не поддерживает в настоящее время tooconfigure минутные показатели вашей учетной записи хранилища; необходимо включить ежеминутные метрики с помощью PowerShell или программно.</span><span class="sxs-lookup"><span data-stu-id="e78af-119">Note that hello Azure Classic Portal does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-storage-metrics-using-powershell"></a><span data-ttu-id="e78af-120">Как tooenable метрик хранилища, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e78af-120">How tooenable Storage metrics using PowerShell</span></span>
<span data-ttu-id="e78af-121">Можно использовать PowerShell на ваш локальный компьютер tooconfigure метрик хранилища в вашей учетной записи хранилища с помощью hello Azure PowerShell командлет Get-AzureStorageServiceMetricsProperty tooretrieve hello текущие параметры и hello командлета SET-AzureStorageServiceMetricsProperty toochange hello текущие параметры.</span><span class="sxs-lookup"><span data-stu-id="e78af-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="e78af-122">Hello командлеты, позволяющие управлять метриками хранилища используйте hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="e78af-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="e78af-123">Возможными значениями MetricsType являются Hour и Minute.</span><span class="sxs-lookup"><span data-stu-id="e78af-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="e78af-124">Возможными значениями ServiceType являются Blob, Queue и Table.</span><span class="sxs-lookup"><span data-stu-id="e78af-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="e78af-125">Возможными значениями MetricsLevel являются None (эквивалент tooOff в hello классический портал Azure), служба (эквивалент tooMinimal в hello классический портал Azure) и ServiceAndApi (эквивалент tooVerbose в hello классический портал Azure).</span><span class="sxs-lookup"><span data-stu-id="e78af-125">MetricsLevel possible values are None (equivalent tooOff in hello Azure Classic Portal), Service (equivalent tooMinimal in hello Azure Classic Portal), and ServiceAndApi (equivalent tooVerbose in hello Azure Classic Portal).</span></span>

<span data-ttu-id="e78af-126">Например, hello следующая команда включает минуту метрики для службы BLOB-объектов hello в вашей учетной записи хранения по умолчанию с периодом хранения hello значение toofive дней:</span><span class="sxs-lookup"><span data-stu-id="e78af-126">For example, hello following command switches on minute metrics for hello blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="e78af-127">Hello следующая команда извлекает hello текущего почасовых метрик уровня и хранения дней для hello BLOB-объектов в учетной записи по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="e78af-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="e78af-128">Сведения о toowork tooconfigure hello Azure PowerShell командлеты с подпиской Azure и как tooselect hello хранилища по умолчанию учетной записи toouse см: [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e78af-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="e78af-129">Как tooenable метрик хранилища программным способом</span><span class="sxs-lookup"><span data-stu-id="e78af-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="e78af-130">Привет, следующий фрагмент кода C# показано, как tooenable метрик и ведения журнала для службы BLOB-объектов hello с помощью hello клиентской библиотеки хранилища для .NET.</span><span class="sxs-lookup"><span data-stu-id="e78af-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="e78af-131">Просмотр метрик хранилища</span><span class="sxs-lookup"><span data-stu-id="e78af-131">Viewing Storage metrics</span></span>
<span data-ttu-id="e78af-132">После настройки метрик хранилища toomonitor вашей учетной записи хранилища, метрик hello записывается в набор известных таблиц в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="e78af-132">When you have configured Storage Metrics toomonitor your storage account, it records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="e78af-133">Страница приветствия монитора можно использовать для вашей учетной записи на классический портал Azure tooview hello часовых метрик hello как только они становятся доступными на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="e78af-133">You can use hello Monitor page for your storage account in hello Azure Classic Portal tooview hello hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="e78af-134">На этой странице в hello классический портал Azure вы можете:</span><span class="sxs-lookup"><span data-stu-id="e78af-134">On this page in hello Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="e78af-135">Выберите, какие tooplot метрик на диаграмме hello (hello набор доступных метрик зависит от выбранного того, какой наблюдение за службой hello на страницу "Настройка" hello).</span><span class="sxs-lookup"><span data-stu-id="e78af-135">Select which metrics tooplot on hello chart (hello choice of available metrics will depend on whether you chose verbose or minimal monitoring for hello service on hello Configure page).</span></span>
* <span data-ttu-id="e78af-136">Выберите диапазон времени hello для hello метрик, отображаемых на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="e78af-136">Select hello time range for hello metrics displayed on hello chart.</span></span>
* <span data-ttu-id="e78af-137">Выберите toouse абсолютный или относительный масштаб tooplot hello метрик.</span><span class="sxs-lookup"><span data-stu-id="e78af-137">Choose toouse an absolute or relative scale tooplot hello metrics.</span></span>
* <span data-ttu-id="e78af-138">Настройка toonotify оповещений по электронной почте при определенных метрика достигает определенного значения.</span><span class="sxs-lookup"><span data-stu-id="e78af-138">Configure email alerts toonotify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="e78af-139">Если необходимо toodownload hello метрики для долгосрочного хранения или tooanalyze их локально, будет необходимо toouse средство или написать код tooread hello таблиц.</span><span class="sxs-lookup"><span data-stu-id="e78af-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need toouse a tool or write some code tooread hello tables.</span></span> <span data-ttu-id="e78af-140">Необходимо загрузить минутные метрики hello для анализа.</span><span class="sxs-lookup"><span data-stu-id="e78af-140">You must download hello minute metrics for analysis.</span></span> <span data-ttu-id="e78af-141">Hello таблицы не отображаются, если список всех таблиц hello в вашей учетной записи хранилища, но они будут доступны непосредственно по имени.</span><span class="sxs-lookup"><span data-stu-id="e78af-141">hello tables do not appear if you list all hello tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="e78af-142">Многие средства обзора хранилища сторонних учитывать эти таблицы и позволяют tooview их напрямую (см. hello блога [обозреватели хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) список доступных средств).</span><span class="sxs-lookup"><span data-stu-id="e78af-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly (see hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="e78af-143">Часовые метрики</span><span class="sxs-lookup"><span data-stu-id="e78af-143">Hourly metrics</span></span>
* <span data-ttu-id="e78af-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="e78af-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="e78af-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="e78af-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="e78af-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="e78af-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="e78af-147">Минутные метрики</span><span class="sxs-lookup"><span data-stu-id="e78af-147">Minute metrics</span></span>
* <span data-ttu-id="e78af-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="e78af-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="e78af-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="e78af-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="e78af-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="e78af-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="e78af-151">Емкость</span><span class="sxs-lookup"><span data-stu-id="e78af-151">Capacity</span></span>
* <span data-ttu-id="e78af-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="e78af-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="e78af-153">Для этих таблиц можно найти подробные сведения о схемах hello [схема таблицы метрик аналитики хранилища](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="e78af-153">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="e78af-154">Hello примере строк ниже показывают только подмножество доступных столбцов hello, но иллюстрируют некоторые важные функции hello способ метрик хранилища сохраняет эти показатели:</span><span class="sxs-lookup"><span data-stu-id="e78af-154">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="e78af-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="e78af-155">PartitionKey</span></span> | <span data-ttu-id="e78af-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="e78af-156">RowKey</span></span> | <span data-ttu-id="e78af-157">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e78af-157">Timestamp</span></span> | <span data-ttu-id="e78af-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="e78af-158">TotalRequests</span></span> | <span data-ttu-id="e78af-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="e78af-159">TotalBillableRequests</span></span> | <span data-ttu-id="e78af-160">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="e78af-160">TotalIngress</span></span> | <span data-ttu-id="e78af-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="e78af-161">TotalEgress</span></span> | <span data-ttu-id="e78af-162">Доступность</span><span class="sxs-lookup"><span data-stu-id="e78af-162">Availability</span></span> | <span data-ttu-id="e78af-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="e78af-163">AverageE2ELatency</span></span> | <span data-ttu-id="e78af-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="e78af-164">AverageServerLatency</span></span> | <span data-ttu-id="e78af-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="e78af-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="e78af-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e78af-166">20140522T1100</span></span> |<span data-ttu-id="e78af-167">user;All</span><span class="sxs-lookup"><span data-stu-id="e78af-167">user;All</span></span> |<span data-ttu-id="e78af-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e78af-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e78af-169">7</span><span class="sxs-lookup"><span data-stu-id="e78af-169">7</span></span> |<span data-ttu-id="e78af-170">7</span><span class="sxs-lookup"><span data-stu-id="e78af-170">7</span></span> |<span data-ttu-id="e78af-171">4003</span><span class="sxs-lookup"><span data-stu-id="e78af-171">4003</span></span> |<span data-ttu-id="e78af-172">46801</span><span class="sxs-lookup"><span data-stu-id="e78af-172">46801</span></span> |<span data-ttu-id="e78af-173">100</span><span class="sxs-lookup"><span data-stu-id="e78af-173">100</span></span> |<span data-ttu-id="e78af-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="e78af-174">104.4286</span></span> |<span data-ttu-id="e78af-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="e78af-175">6.857143</span></span> |<span data-ttu-id="e78af-176">100</span><span class="sxs-lookup"><span data-stu-id="e78af-176">100</span></span> |
| <span data-ttu-id="e78af-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e78af-177">20140522T1100</span></span> |<span data-ttu-id="e78af-178">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="e78af-178">user;QueryEntities</span></span> |<span data-ttu-id="e78af-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="e78af-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="e78af-180">5</span><span class="sxs-lookup"><span data-stu-id="e78af-180">5</span></span> |<span data-ttu-id="e78af-181">5</span><span class="sxs-lookup"><span data-stu-id="e78af-181">5</span></span> |<span data-ttu-id="e78af-182">2694</span><span class="sxs-lookup"><span data-stu-id="e78af-182">2694</span></span> |<span data-ttu-id="e78af-183">45951</span><span class="sxs-lookup"><span data-stu-id="e78af-183">45951</span></span> |<span data-ttu-id="e78af-184">100</span><span class="sxs-lookup"><span data-stu-id="e78af-184">100</span></span> |<span data-ttu-id="e78af-185">143.8</span><span class="sxs-lookup"><span data-stu-id="e78af-185">143.8</span></span> |<span data-ttu-id="e78af-186">7.8</span><span class="sxs-lookup"><span data-stu-id="e78af-186">7.8</span></span> |<span data-ttu-id="e78af-187">100</span><span class="sxs-lookup"><span data-stu-id="e78af-187">100</span></span> |
| <span data-ttu-id="e78af-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e78af-188">20140522T1100</span></span> |<span data-ttu-id="e78af-189">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="e78af-189">user;QueryEntity</span></span> |<span data-ttu-id="e78af-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e78af-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e78af-191">1</span><span class="sxs-lookup"><span data-stu-id="e78af-191">1</span></span> |<span data-ttu-id="e78af-192">1</span><span class="sxs-lookup"><span data-stu-id="e78af-192">1</span></span> |<span data-ttu-id="e78af-193">538</span><span class="sxs-lookup"><span data-stu-id="e78af-193">538</span></span> |<span data-ttu-id="e78af-194">633</span><span class="sxs-lookup"><span data-stu-id="e78af-194">633</span></span> |<span data-ttu-id="e78af-195">100</span><span class="sxs-lookup"><span data-stu-id="e78af-195">100</span></span> |<span data-ttu-id="e78af-196">3</span><span class="sxs-lookup"><span data-stu-id="e78af-196">3</span></span> |<span data-ttu-id="e78af-197">3</span><span class="sxs-lookup"><span data-stu-id="e78af-197">3</span></span> |<span data-ttu-id="e78af-198">100</span><span class="sxs-lookup"><span data-stu-id="e78af-198">100</span></span> |
| <span data-ttu-id="e78af-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="e78af-199">20140522T1100</span></span> |<span data-ttu-id="e78af-200">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="e78af-200">user;UpdateEntity</span></span> |<span data-ttu-id="e78af-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="e78af-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="e78af-202">1</span><span class="sxs-lookup"><span data-stu-id="e78af-202">1</span></span> |<span data-ttu-id="e78af-203">1</span><span class="sxs-lookup"><span data-stu-id="e78af-203">1</span></span> |<span data-ttu-id="e78af-204">771</span><span class="sxs-lookup"><span data-stu-id="e78af-204">771</span></span> |<span data-ttu-id="e78af-205">217</span><span class="sxs-lookup"><span data-stu-id="e78af-205">217</span></span> |<span data-ttu-id="e78af-206">100</span><span class="sxs-lookup"><span data-stu-id="e78af-206">100</span></span> |<span data-ttu-id="e78af-207">9</span><span class="sxs-lookup"><span data-stu-id="e78af-207">9</span></span> |<span data-ttu-id="e78af-208">6</span><span class="sxs-lookup"><span data-stu-id="e78af-208">6</span></span> |<span data-ttu-id="e78af-209">100</span><span class="sxs-lookup"><span data-stu-id="e78af-209">100</span></span> |

<span data-ttu-id="e78af-210">В этом примере данных минутной метрики для ключа раздела hello используется hello время с минутным разрешением.</span><span class="sxs-lookup"><span data-stu-id="e78af-210">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="e78af-211">Hello ключ строки определяет тип информации, хранящейся в строке приветствия hello и состоит из двух фрагментов информации, типом доступа hello и тип запроса hello:</span><span class="sxs-lookup"><span data-stu-id="e78af-211">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="e78af-212">Тип доступа Hello — пользователя или системы, где пользователь относится tooall пользователь запросов toohello хранилища службы, а система — toorequests, выполненные средством аналитики хранилища.</span><span class="sxs-lookup"><span data-stu-id="e78af-212">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="e78af-213">Тип запроса Hello — в этом случае это строка сводки, либо он определяет hello определенный интерфейс API, например QueryEntity или UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="e78af-213">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="e78af-214">пример Hello данных передачи, которые все hello записывает за одну минуту (начиная с 11:00 по тихоокеанскому времени), поэтому hello число QueryEntities запросов, а также hello число QueryEntity запросов, а также hello число запросов UpdateEntity сложить tooseven, которой является hello Общее показан на Строка Hello user: All.</span><span class="sxs-lookup"><span data-stu-id="e78af-214">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="e78af-215">Аналогичным образом, можно создать производные hello среднее конца в конец задержку 104.4286 в строке приветствия user: All, вычисляя ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="e78af-215">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="e78af-216">Настройка оповещений в hello классический портал Azure на странице приветствия монитора рекомендуется, чтобы метрик хранилища может автоматически уведомлять все важные изменения в поведении hello устройств хранения. Если вы используете toodownload средства обозревателя хранилища данные метрик в формате с разделителями, можно использовать Microsoft Excel tooanalyze hello данных.</span><span class="sxs-lookup"><span data-stu-id="e78af-216">You should consider setting up alerts in hello Azure Classic Portal on hello Monitor page so that Storage Metrics can automatically notify you of any important changes in hello behavior of your storage services.If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="e78af-217">См. hello блога [обозреватели хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) список доступных средств обзора хранилища.</span><span class="sxs-lookup"><span data-stu-id="e78af-217">See hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="e78af-218">Программный доступ к данным метрик</span><span class="sxs-lookup"><span data-stu-id="e78af-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="e78af-219">Hello ниже приведен пример кода C#, обращается к hello минутным метрикам для диапазона минут и отображает результаты hello в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="e78af-219">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="e78af-220">Она использует hello библиотека хранилища Azure версии 4, включающая hello CloudAnalyticsClient класс, который упрощает доступ к таблицам метрик hello в хранилище.</span><span class="sxs-lookup"><span data-stu-id="e78af-220">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="e78af-221">Какова стоимость включения метрик хранилища?</span><span class="sxs-lookup"><span data-stu-id="e78af-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="e78af-222">Напишите запросы сущностей таблицы toocreate для метрик взимается плата в операции хранилища Azure применимо tooall стандартные тарифы hello.</span><span class="sxs-lookup"><span data-stu-id="e78af-222">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="e78af-223">Чтение и удаление запросов по toometrics данных клиента, также применяются стандартные тарифы.</span><span class="sxs-lookup"><span data-stu-id="e78af-223">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="e78af-224">Если вы настроили политику хранения данных, за удаление старых данных метрик хранилищем Azure плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="e78af-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="e78af-225">Однако при удалении данных аналитики, учетной записи взимается для операций delete hello.</span><span class="sxs-lookup"><span data-stu-id="e78af-225">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="e78af-226">Hello мощность, используемая hello таблицах метрик, также тарифицируется: можно использовать следующие tooestimate hello объем пространства, используемый для хранения данных метрик hello:</span><span class="sxs-lookup"><span data-stu-id="e78af-226">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="e78af-227">Если каждый час служба использует каждый API в каждой службе, примерно 148 КБ данных сохраняется каждый час в таблицах транзакций метрик hello при включении службы и уровне API сводки.</span><span class="sxs-lookup"><span data-stu-id="e78af-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="e78af-228">Если каждый час служба использует каждый API в каждой службе, примерно 12 КБ данных сохраняется каждый час в таблицах транзакций метрик hello при наличии только уровень службы сводки.</span><span class="sxs-lookup"><span data-stu-id="e78af-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="e78af-229">Hello таблице емкости BLOB-объектов имеет две строки, добавленные в день (если пользователь выбрал использование журналов): это означает, что каждый день hello размер этой таблицы увеличивается на копирование tooapproximately 300 байт.</span><span class="sxs-lookup"><span data-stu-id="e78af-229">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e78af-230">Дальнейшие действия:</span><span class="sxs-lookup"><span data-stu-id="e78af-230">Next steps:</span></span>
[<span data-ttu-id="e78af-231">Включение ведения журнала аналитики и доступа к данным журнала хранилища</span><span class="sxs-lookup"><span data-stu-id="e78af-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
