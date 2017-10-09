---
title: "метрики хранилища aaaEnabling в hello портал Azure | Документы Microsoft"
description: "Как tooenable метрик хранилища для hello служб больших двоичных объектов, очередей, таблицы и файла"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: f157dbdf9a256da7ab186f80db746b91d1a9beb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="c5981-103">Включение метрик хранилища Azure и просмотр данных метрик</span><span class="sxs-lookup"><span data-stu-id="c5981-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="c5981-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c5981-104">Overview</span></span>
<span data-ttu-id="c5981-105">Метрики хранилища включаются по умолчанию при создании учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c5981-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="c5981-106">Вы можете настроить отслеживание посредством hello [портал Azure](https://portal.azure.com) или Windows PowerShell или программно через одну из клиентских библиотек хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="c5981-107">Можно настроить срок хранения данных метрик hello: этот период определяет срок хранения hello служба поддерживает метрики hello и расходов для hello пространство необходимые toostore их.</span><span class="sxs-lookup"><span data-stu-id="c5981-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="c5981-108">Как правило следует использовать короткий срок хранения для ежеминутных метрик, нежели для часовых метрик из-за hello Требую значительно большего пространства для минутных метрик.</span><span class="sxs-lookup"><span data-stu-id="c5981-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="c5981-109">Таким образом, чтобы иметь достаточно времени tooanalyze hello данных и загрузку метрик, нужно tookeep локально для анализа или составления следует выбрать период хранения.</span><span class="sxs-lookup"><span data-stu-id="c5981-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="c5981-110">Помните, что за скачивание данных метрик из учетной записи хранения также взимается плата.</span><span class="sxs-lookup"><span data-stu-id="c5981-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="c5981-111">Как с помощью метрики tooenable hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="c5981-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="c5981-112">Выполните эти шаги метрики tooenable hello [портал Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="c5981-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="c5981-113">Перейдите tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5981-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="c5981-114">Выберите **диагностики** на hello **меню** колонку</span><span class="sxs-lookup"><span data-stu-id="c5981-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="c5981-115">Убедитесь, что **состояние** задано слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="c5981-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="c5981-116">Выберите hello метрики для hello служб, который следует toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c5981-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="c5981-117">Укажите политику хранения tooindicate продолжительность tooretain метрики и журнала данных.</span><span class="sxs-lookup"><span data-stu-id="c5981-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="c5981-118">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c5981-118">Select **Save**.</span></span>

<span data-ttu-id="c5981-119">Обратите внимание, что hello [портал Azure](https://portal.azure.com) не включает в настоящее время вы tooconfigure минутные показатели вашей учетной записи хранилища; необходимо включить ежеминутные метрики с помощью PowerShell или программно.</span><span class="sxs-lookup"><span data-stu-id="c5981-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="c5981-120">Как tooenable метрик, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5981-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="c5981-121">Можно использовать PowerShell на ваш локальный компьютер tooconfigure метрик хранилища в вашей учетной записи хранилища с помощью hello Azure PowerShell командлет Get-AzureStorageServiceMetricsProperty tooretrieve hello текущие параметры и hello командлета SET-AzureStorageServiceMetricsProperty toochange hello текущие параметры.</span><span class="sxs-lookup"><span data-stu-id="c5981-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="c5981-122">Hello командлеты, позволяющие управлять метриками хранилища используйте hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c5981-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="c5981-123">Возможными значениями MetricsType являются Hour и Minute.</span><span class="sxs-lookup"><span data-stu-id="c5981-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="c5981-124">Возможными значениями ServiceType являются Blob, Queue и Table.</span><span class="sxs-lookup"><span data-stu-id="c5981-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="c5981-125">Возможными значениями MetricsLevel являются None, Service и ServiceAndApi.</span><span class="sxs-lookup"><span data-stu-id="c5981-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="c5981-126">Например, hello следующая команда включает минуту метрики для службы BLOB-объектов hello в вашей учетной записи хранения по умолчанию с периодом хранения hello значение toofive дней:</span><span class="sxs-lookup"><span data-stu-id="c5981-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="c5981-127">Hello следующая команда извлекает hello текущего почасовых метрик уровня и хранения дней для hello BLOB-объектов в учетной записи по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c5981-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="c5981-128">Сведения о toowork tooconfigure hello Azure PowerShell командлеты с подпиской Azure и как tooselect hello хранилища по умолчанию учетной записи toouse см: [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5981-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="c5981-129">Как tooenable метрик хранилища программным способом</span><span class="sxs-lookup"><span data-stu-id="c5981-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="c5981-130">Привет, следующий фрагмент кода C# показано, как tooenable метрик и ведения журнала для службы BLOB-объектов hello с помощью hello клиентской библиотеки хранилища для .NET.</span><span class="sxs-lookup"><span data-stu-id="c5981-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="c5981-131">Просмотр метрик хранилища</span><span class="sxs-lookup"><span data-stu-id="c5981-131">Viewing Storage metrics</span></span>
<span data-ttu-id="c5981-132">После настройки учетной записи хранения toomonitor метрики аналитики хранилища аналитики хранилища записывает hello метрики в набор известных таблиц в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5981-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="c5981-133">Часовые показатели tooview диаграммы можно настроить в hello [портал Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="c5981-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="c5981-134">Перейдите tooyour учетной записи хранилища в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c5981-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="c5981-135">Выберите **метрики** в hello **меню** колонке hello службы которого метрик требуется tooview.</span><span class="sxs-lookup"><span data-stu-id="c5981-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="c5981-136">Выберите **изменить** на диаграмме hello требуется tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c5981-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="c5981-137">В hello **изменить диаграмму** колонки, выберите hello **диапазон времени**, **тип диаграммы**и hello метрик, которые необходимо отобразить на диаграмме hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="c5981-138">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c5981-138">Select **OK**</span></span>

<span data-ttu-id="c5981-139">Если требуется, чтобы toodownload hello метрики для долгосрочного хранения или tooanalyze их локально, необходимо:</span><span class="sxs-lookup"><span data-stu-id="c5981-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="c5981-140">Используйте это средство, которое учитывает эти таблицы позволяют tooview и загрузить их.</span><span class="sxs-lookup"><span data-stu-id="c5981-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="c5981-141">Написать пользовательские приложения или сценария tooread и хранить hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="c5981-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="c5981-142">Многие средства обзора хранилища сторонних учитывать эти таблицы и позволяют tooview их напрямую.</span><span class="sxs-lookup"><span data-stu-id="c5981-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="c5981-143">Список доступных инструментов указан в разделе [Клиентские инструменты службы хранилища Azure](storage-explorers.md).</span><span class="sxs-lookup"><span data-stu-id="c5981-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="c5981-144">Начиная с версии 0.8.0 hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), можно просматривать и загружать таблицы метрик аналитики hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="c5981-145">В порядке tooaccess hello analytics таблиц программными средствами, обратите внимание, что hello analytics таблицы не отображаются, если список всех таблиц hello в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5981-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="c5981-146">Можно получить доступ к их напрямую по имени, или использовать hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) в hello библиотеки клиента .NET tooquery имена таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="c5981-147">Часовые метрики</span><span class="sxs-lookup"><span data-stu-id="c5981-147">Hourly metrics</span></span>
* <span data-ttu-id="c5981-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="c5981-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="c5981-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="c5981-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="c5981-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="c5981-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="c5981-151">Минутные метрики</span><span class="sxs-lookup"><span data-stu-id="c5981-151">Minute metrics</span></span>
* <span data-ttu-id="c5981-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="c5981-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="c5981-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="c5981-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="c5981-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="c5981-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="c5981-155">Емкость</span><span class="sxs-lookup"><span data-stu-id="c5981-155">Capacity</span></span>
* <span data-ttu-id="c5981-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="c5981-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="c5981-157">Для этих таблиц можно найти подробные сведения о схемах hello [схема таблицы метрик аналитики хранилища](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5981-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="c5981-158">Hello примере строк ниже показывают только подмножество доступных столбцов hello, но иллюстрируют некоторые важные функции hello способ метрик хранилища сохраняет эти показатели:</span><span class="sxs-lookup"><span data-stu-id="c5981-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="c5981-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="c5981-159">PartitionKey</span></span> | <span data-ttu-id="c5981-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="c5981-160">RowKey</span></span> | <span data-ttu-id="c5981-161">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c5981-161">Timestamp</span></span> | <span data-ttu-id="c5981-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="c5981-162">TotalRequests</span></span> | <span data-ttu-id="c5981-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="c5981-163">TotalBillableRequests</span></span> | <span data-ttu-id="c5981-164">TotalIngress</span><span class="sxs-lookup"><span data-stu-id="c5981-164">TotalIngress</span></span> | <span data-ttu-id="c5981-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="c5981-165">TotalEgress</span></span> | <span data-ttu-id="c5981-166">Доступность</span><span class="sxs-lookup"><span data-stu-id="c5981-166">Availability</span></span> | <span data-ttu-id="c5981-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="c5981-167">AverageE2ELatency</span></span> | <span data-ttu-id="c5981-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="c5981-168">AverageServerLatency</span></span> | <span data-ttu-id="c5981-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="c5981-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="c5981-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5981-170">20140522T1100</span></span> |<span data-ttu-id="c5981-171">user;All</span><span class="sxs-lookup"><span data-stu-id="c5981-171">user;All</span></span> |<span data-ttu-id="c5981-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c5981-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c5981-173">7</span><span class="sxs-lookup"><span data-stu-id="c5981-173">7</span></span> |<span data-ttu-id="c5981-174">7</span><span class="sxs-lookup"><span data-stu-id="c5981-174">7</span></span> |<span data-ttu-id="c5981-175">4003</span><span class="sxs-lookup"><span data-stu-id="c5981-175">4003</span></span> |<span data-ttu-id="c5981-176">46801</span><span class="sxs-lookup"><span data-stu-id="c5981-176">46801</span></span> |<span data-ttu-id="c5981-177">100</span><span class="sxs-lookup"><span data-stu-id="c5981-177">100</span></span> |<span data-ttu-id="c5981-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="c5981-178">104.4286</span></span> |<span data-ttu-id="c5981-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="c5981-179">6.857143</span></span> |<span data-ttu-id="c5981-180">100</span><span class="sxs-lookup"><span data-stu-id="c5981-180">100</span></span> |
| <span data-ttu-id="c5981-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5981-181">20140522T1100</span></span> |<span data-ttu-id="c5981-182">user;QueryEntities</span><span class="sxs-lookup"><span data-stu-id="c5981-182">user;QueryEntities</span></span> |<span data-ttu-id="c5981-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="c5981-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="c5981-184">5</span><span class="sxs-lookup"><span data-stu-id="c5981-184">5</span></span> |<span data-ttu-id="c5981-185">5</span><span class="sxs-lookup"><span data-stu-id="c5981-185">5</span></span> |<span data-ttu-id="c5981-186">2694</span><span class="sxs-lookup"><span data-stu-id="c5981-186">2694</span></span> |<span data-ttu-id="c5981-187">45951</span><span class="sxs-lookup"><span data-stu-id="c5981-187">45951</span></span> |<span data-ttu-id="c5981-188">100</span><span class="sxs-lookup"><span data-stu-id="c5981-188">100</span></span> |<span data-ttu-id="c5981-189">143.8</span><span class="sxs-lookup"><span data-stu-id="c5981-189">143.8</span></span> |<span data-ttu-id="c5981-190">7.8</span><span class="sxs-lookup"><span data-stu-id="c5981-190">7.8</span></span> |<span data-ttu-id="c5981-191">100</span><span class="sxs-lookup"><span data-stu-id="c5981-191">100</span></span> |
| <span data-ttu-id="c5981-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5981-192">20140522T1100</span></span> |<span data-ttu-id="c5981-193">user;QueryEntity</span><span class="sxs-lookup"><span data-stu-id="c5981-193">user;QueryEntity</span></span> |<span data-ttu-id="c5981-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c5981-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c5981-195">1</span><span class="sxs-lookup"><span data-stu-id="c5981-195">1</span></span> |<span data-ttu-id="c5981-196">1</span><span class="sxs-lookup"><span data-stu-id="c5981-196">1</span></span> |<span data-ttu-id="c5981-197">538</span><span class="sxs-lookup"><span data-stu-id="c5981-197">538</span></span> |<span data-ttu-id="c5981-198">633</span><span class="sxs-lookup"><span data-stu-id="c5981-198">633</span></span> |<span data-ttu-id="c5981-199">100</span><span class="sxs-lookup"><span data-stu-id="c5981-199">100</span></span> |<span data-ttu-id="c5981-200">3</span><span class="sxs-lookup"><span data-stu-id="c5981-200">3</span></span> |<span data-ttu-id="c5981-201">3</span><span class="sxs-lookup"><span data-stu-id="c5981-201">3</span></span> |<span data-ttu-id="c5981-202">100</span><span class="sxs-lookup"><span data-stu-id="c5981-202">100</span></span> |
| <span data-ttu-id="c5981-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="c5981-203">20140522T1100</span></span> |<span data-ttu-id="c5981-204">user;UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="c5981-204">user;UpdateEntity</span></span> |<span data-ttu-id="c5981-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="c5981-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="c5981-206">1</span><span class="sxs-lookup"><span data-stu-id="c5981-206">1</span></span> |<span data-ttu-id="c5981-207">1</span><span class="sxs-lookup"><span data-stu-id="c5981-207">1</span></span> |<span data-ttu-id="c5981-208">771</span><span class="sxs-lookup"><span data-stu-id="c5981-208">771</span></span> |<span data-ttu-id="c5981-209">217</span><span class="sxs-lookup"><span data-stu-id="c5981-209">217</span></span> |<span data-ttu-id="c5981-210">100</span><span class="sxs-lookup"><span data-stu-id="c5981-210">100</span></span> |<span data-ttu-id="c5981-211">9</span><span class="sxs-lookup"><span data-stu-id="c5981-211">9</span></span> |<span data-ttu-id="c5981-212">6</span><span class="sxs-lookup"><span data-stu-id="c5981-212">6</span></span> |<span data-ttu-id="c5981-213">100</span><span class="sxs-lookup"><span data-stu-id="c5981-213">100</span></span> |

<span data-ttu-id="c5981-214">В этом примере данных минутной метрики для ключа раздела hello используется hello время с минутным разрешением.</span><span class="sxs-lookup"><span data-stu-id="c5981-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="c5981-215">Hello ключ строки определяет тип информации, хранящейся в строке приветствия hello и состоит из двух фрагментов информации, типом доступа hello и тип запроса hello:</span><span class="sxs-lookup"><span data-stu-id="c5981-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="c5981-216">Тип доступа Hello — пользователя или системы, где пользователь относится tooall пользователь запросов toohello хранилища службы, а система — toorequests, выполненные средством аналитики хранилища.</span><span class="sxs-lookup"><span data-stu-id="c5981-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="c5981-217">Тип запроса Hello — в этом случае это строка сводки, либо он определяет hello определенный интерфейс API, например QueryEntity или UpdateEntity.</span><span class="sxs-lookup"><span data-stu-id="c5981-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="c5981-218">пример Hello данных передачи, которые все hello записывает за одну минуту (начиная с 11:00 по тихоокеанскому времени), поэтому hello число QueryEntities запросов, а также hello число QueryEntity запросов, а также hello число запросов UpdateEntity сложить tooseven, которой является hello Общее показан на Строка Hello user: All.</span><span class="sxs-lookup"><span data-stu-id="c5981-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="c5981-219">Аналогичным образом, можно создать производные hello среднее конца в конец задержку 104.4286 в строке приветствия user: All, вычисляя ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="c5981-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="c5981-220">Оповещения метрик</span><span class="sxs-lookup"><span data-stu-id="c5981-220">Metrics alerts</span></span>
<span data-ttu-id="c5981-221">Настройка оповещений в hello следует [портал Azure](https://portal.azure.com) , метрик хранилища могут автоматически получать уведомления о важных изменениях в поведении hello устройств хранения.</span><span class="sxs-lookup"><span data-stu-id="c5981-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="c5981-222">Если вы используете toodownload средства обозревателя хранилища данные метрик в формате с разделителями, можно использовать Microsoft Excel tooanalyze hello данных.</span><span class="sxs-lookup"><span data-stu-id="c5981-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="c5981-223">Список доступных инструментов Storage Explorer см. в разделе [Клиентские инструменты службы хранилища Azure](storage-explorers.md).</span><span class="sxs-lookup"><span data-stu-id="c5981-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="c5981-224">Можно настроить оповещения в hello **предупреждения правила** колонке доступен в рамках **мониторинг** в колонке меню учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5981-225">Возможна задержка между событием хранилища и при записи hello соответствующие данные метрик каждый час или раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="c5981-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="c5981-226">В случае hello минутных метрик данные за несколько минут на запись одновременно.</span><span class="sxs-lookup"><span data-stu-id="c5981-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="c5981-227">Это может привести tootransactions из более ранних минут статистически в транзакцию hello для hello текущую минуту.</span><span class="sxs-lookup"><span data-stu-id="c5981-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="c5981-228">В этом случае hello предупреждение, что служба не может иметь все данные метрик, доступных для hello настроить оповещения интервал, который может вызвать срабатывание неожиданно tooalerts.</span><span class="sxs-lookup"><span data-stu-id="c5981-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="c5981-229">Программный доступ к данным метрик</span><span class="sxs-lookup"><span data-stu-id="c5981-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="c5981-230">Hello ниже приведен пример кода C#, обращается к hello минутным метрикам для диапазона минут и отображает результаты hello в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="c5981-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="c5981-231">Она использует hello библиотека хранилища Azure версии 4, включающая hello CloudAnalyticsClient класс, который упрощает доступ к таблицам метрик hello в хранилище.</span><span class="sxs-lookup"><span data-stu-id="c5981-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="c5981-232">Какова стоимость включения метрик хранилища?</span><span class="sxs-lookup"><span data-stu-id="c5981-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="c5981-233">Напишите запросы сущностей таблицы toocreate для метрик взимается плата в операции хранилища Azure применимо tooall стандартные тарифы hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="c5981-234">Чтение и удаление запросов по toometrics данных клиента, также применяются стандартные тарифы.</span><span class="sxs-lookup"><span data-stu-id="c5981-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="c5981-235">Если вы настроили политику хранения данных, за удаление старых данных метрик хранилищем Azure плата не взимается.</span><span class="sxs-lookup"><span data-stu-id="c5981-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="c5981-236">Однако при удалении данных аналитики, учетной записи взимается для операций delete hello.</span><span class="sxs-lookup"><span data-stu-id="c5981-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="c5981-237">Hello мощность, используемая hello таблицах метрик, также тарифицируется: можно использовать следующие tooestimate hello объем пространства, используемый для хранения данных метрик hello:</span><span class="sxs-lookup"><span data-stu-id="c5981-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="c5981-238">Если каждый час служба использует каждый API в каждой службе, примерно 148 КБ данных сохраняется каждый час в таблицах транзакций метрик hello при включении службы и уровне API сводки.</span><span class="sxs-lookup"><span data-stu-id="c5981-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="c5981-239">Если каждый час служба использует каждый API в каждой службе, примерно 12 КБ данных сохраняется каждый час в таблицах транзакций метрик hello при наличии только уровень службы сводки.</span><span class="sxs-lookup"><span data-stu-id="c5981-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="c5981-240">Hello таблице емкости BLOB-объектов имеет две строки, добавленные в день (если пользователь выбрал использование журналов): это означает, что каждый день hello размер этой таблицы увеличивается на копирование tooapproximately 300 байт.</span><span class="sxs-lookup"><span data-stu-id="c5981-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5981-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5981-241">Next steps</span></span>
[<span data-ttu-id="c5981-242">Включение ведения журнала и доступа к данным журнала хранилища</span><span class="sxs-lookup"><span data-stu-id="c5981-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
