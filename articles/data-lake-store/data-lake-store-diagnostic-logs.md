---
title: "Просмотр журналов диагностики Azure Data Lake Store | Документация Майкрософт"
description: "Узнайте, как настроить журналы диагностики для Azure Data Lake Store и просматривать их. "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="a1360-103">Доступ к журналам диагностики Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a1360-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="a1360-104">Узнайте, как включить ведение журнала диагностики для учетной записи Data Lake Store и просматривать журналы, собранные для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a1360-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="a1360-105">Организации могут включить ведение журнала диагностики для учетной записи Azure Data Lake Store, чтобы собирать журналы аудита доступа к данным, содержащие такие сведения, как список пользователей, обращавшихся к данным, частота доступа к данным, объем данных в учетной записи и т. д.</span><span class="sxs-lookup"><span data-stu-id="a1360-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1360-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1360-106">Prerequisites</span></span>
* <span data-ttu-id="a1360-107">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="a1360-107">**An Azure subscription**.</span></span> <span data-ttu-id="a1360-108">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1360-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a1360-109">**Учетная запись хранилища озера данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="a1360-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="a1360-110">Следуйте инструкциям в разделе [Приступая к работе с хранилищем озера данных Azure на портале Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a1360-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="a1360-111">Включение ведения журнала диагностики для учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a1360-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="a1360-112">Перейдите на новый [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1360-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a1360-113">Откройте свою учетную запись Data Lake Store. В колонке учетной записи Data Lake Store выберите **Параметры**, а затем щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="a1360-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="a1360-114">В колонке **Журналы диагностики** щелкните **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="a1360-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="a1360-115">![Включение ведения журналов диагностики](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Включение журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="a1360-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="a1360-116">В колонке **Диагностика** внесите следующие изменения, чтобы настроить ведение журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="a1360-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="a1360-117">![Включение ведения журналов диагностики](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Включение журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="a1360-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="a1360-118">Чтобы включить ведение журналов диагностики, для параметра **Состояние** установите значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="a1360-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="a1360-119">Хранить и обрабатывать данные можно разными способами.</span><span class="sxs-lookup"><span data-stu-id="a1360-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="a1360-120">Выберите параметр **Archive to a storage account** (Архивация в учетную запись хранения), чтобы сохранять журналы в учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a1360-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="a1360-121">Используйте этот параметр, если вы хотите архивировать данные для последующей пакетной обработки.</span><span class="sxs-lookup"><span data-stu-id="a1360-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="a1360-122">Если выбран этот параметр, то необходимо указать учетную запись хранения Azure для сохранения журналов.</span><span class="sxs-lookup"><span data-stu-id="a1360-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="a1360-123">Выберите параметр **Stream to an event hub** (Потоковая передача в концентратор событий), чтобы передавать поток данных журнала в концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="a1360-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="a1360-124">Чаще всего этот параметр используется, если имеется конвейер последующей обработки для анализа входящих журналов в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="a1360-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="a1360-125">При выборе этого параметра необходимо указать сведения о концентраторе событий Azure, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="a1360-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="a1360-126">Выберите параметр **Send to Log Analytics** (Отправить в Log Analytics), чтобы проанализировать данные созданного журнала с помощью Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a1360-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="a1360-127">При выборе этого параметра необходимо указать сведения для рабочей области Operations Management Suite, которая будет использоваться для анализа журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="a1360-128">Укажите, хотите ли вы получить журналы аудита или журналы запросов, либо и те, и другие.</span><span class="sxs-lookup"><span data-stu-id="a1360-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="a1360-129">Укажите число дней, в течение которых должны храниться данные.</span><span class="sxs-lookup"><span data-stu-id="a1360-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="a1360-130">Период удержания применяется, только если учетная запись хранения Azure используется для архивации данных журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="a1360-131">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a1360-131">Click **Save**.</span></span>

<span data-ttu-id="a1360-132">Включив параметры диагностики, вы сможете просматривать журналы на вкладке **Журналы диагностики** .</span><span class="sxs-lookup"><span data-stu-id="a1360-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="a1360-133">Просмотр журналов диагностики для учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a1360-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="a1360-134">Существует два способа просмотра данных журнала для учетной записи Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="a1360-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="a1360-135">из представления параметров учетной записи Data Lake Store;</span><span class="sxs-lookup"><span data-stu-id="a1360-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="a1360-136">из учетной записи хранения Azure, в которой хранятся данные.</span><span class="sxs-lookup"><span data-stu-id="a1360-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="a1360-137">Использование представления параметров Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a1360-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="a1360-138">В колонке **Параметры** учетной записи Data Lake Store щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="a1360-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="a1360-139">![Просмотр ведения журнала диагностики](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Просмотр журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="a1360-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="a1360-140">В колонке **Журналы диагностики** должны отображаться журналы, упорядоченные по категориям **Журналы аудита** и **Журналы запросов**.</span><span class="sxs-lookup"><span data-stu-id="a1360-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="a1360-141">В журналы запросов записываются все запросы API к учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a1360-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="a1360-142">Журналы аудита похожи на журналы запросов, но содержат более подробную статистику операций с учетной записью Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a1360-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="a1360-143">Например, вызов API для одной передачи в журнале запросов может породить несколько операций добавления в журналах аудита.</span><span class="sxs-lookup"><span data-stu-id="a1360-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="a1360-144">Щелкните ссылку **Скачать** для каждой записи журнала, чтобы скачать журналы.</span><span class="sxs-lookup"><span data-stu-id="a1360-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="a1360-145">Использование учетной записи хранения Azure, в которой хранятся данные</span><span class="sxs-lookup"><span data-stu-id="a1360-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="a1360-146">Откройте колонку учетной записи хранения Azure, связанную с Data Lake Store для ведения журнала, и щелкните "BLOB-объекты".</span><span class="sxs-lookup"><span data-stu-id="a1360-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="a1360-147">В колонке **Служба BLOB-объектов** отображается два контейнера.</span><span class="sxs-lookup"><span data-stu-id="a1360-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="a1360-148">![Просмотр ведения журнала диагностики](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Просмотр журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="a1360-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="a1360-149">В контейнере **insights-logs-audit** содержатся журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="a1360-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="a1360-150">В контейнере **insights-logs-requests** содержатся журналы запросов.</span><span class="sxs-lookup"><span data-stu-id="a1360-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="a1360-151">Журналы в этих контейнерах хранятся с использованием следующей структуры:</span><span class="sxs-lookup"><span data-stu-id="a1360-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="a1360-152">![Просмотр ведения журнала диагностики](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Просмотр журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="a1360-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="a1360-153">Например, полный путь к журналу аудита может выглядеть таким образом: `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="a1360-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="a1360-154">Аналогично, полный путь к журналу запросов может выглядеть так: `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="a1360-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="a1360-155">Описание структуры данных журнала</span><span class="sxs-lookup"><span data-stu-id="a1360-155">Understand the structure of the log data</span></span>
<span data-ttu-id="a1360-156">В журналах аудита и запросов используется формат JSON.</span><span class="sxs-lookup"><span data-stu-id="a1360-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="a1360-157">В этом разделе мы рассмотрим структуру JSON для журналов запросов и аудита.</span><span class="sxs-lookup"><span data-stu-id="a1360-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="a1360-158">Журналы запросов</span><span class="sxs-lookup"><span data-stu-id="a1360-158">Request logs</span></span>
<span data-ttu-id="a1360-159">Ниже приведен пример записи журнала запросов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="a1360-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="a1360-160">Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="a1360-161">Схема журнала запросов</span><span class="sxs-lookup"><span data-stu-id="a1360-161">Request log schema</span></span>
| <span data-ttu-id="a1360-162">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="a1360-162">Name</span></span> | <span data-ttu-id="a1360-163">Тип</span><span class="sxs-lookup"><span data-stu-id="a1360-163">Type</span></span> | <span data-ttu-id="a1360-164">Описание</span><span class="sxs-lookup"><span data-stu-id="a1360-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1360-165">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="a1360-165">time</span></span> |<span data-ttu-id="a1360-166">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-166">String</span></span> |<span data-ttu-id="a1360-167">Метка времени журнала (в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="a1360-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="a1360-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="a1360-168">resourceId</span></span> |<span data-ttu-id="a1360-169">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-169">String</span></span> |<span data-ttu-id="a1360-170">Идентификатор ресурса, с которым была выполнена операция.</span><span class="sxs-lookup"><span data-stu-id="a1360-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="a1360-171">category</span><span class="sxs-lookup"><span data-stu-id="a1360-171">category</span></span> |<span data-ttu-id="a1360-172">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-172">String</span></span> |<span data-ttu-id="a1360-173">Категория журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-173">The log category.</span></span> <span data-ttu-id="a1360-174">Например, **Requests**.</span><span class="sxs-lookup"><span data-stu-id="a1360-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="a1360-175">operationName</span><span class="sxs-lookup"><span data-stu-id="a1360-175">operationName</span></span> |<span data-ttu-id="a1360-176">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-176">String</span></span> |<span data-ttu-id="a1360-177">Имя операции, добавленной в журнал.</span><span class="sxs-lookup"><span data-stu-id="a1360-177">Name of the operation that is logged.</span></span> <span data-ttu-id="a1360-178">Например, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="a1360-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="a1360-179">resultType</span><span class="sxs-lookup"><span data-stu-id="a1360-179">resultType</span></span> |<span data-ttu-id="a1360-180">Строка</span><span class="sxs-lookup"><span data-stu-id="a1360-180">String</span></span> |<span data-ttu-id="a1360-181">Состояние операции. Например, 200.</span><span class="sxs-lookup"><span data-stu-id="a1360-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="a1360-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="a1360-182">callerIpAddress</span></span> |<span data-ttu-id="a1360-183">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-183">String</span></span> |<span data-ttu-id="a1360-184">IP-адрес клиента, отправившего запрос.</span><span class="sxs-lookup"><span data-stu-id="a1360-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="a1360-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="a1360-185">correlationId</span></span> |<span data-ttu-id="a1360-186">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-186">String</span></span> |<span data-ttu-id="a1360-187">Идентификатор журнала, который можно использовать для формирования набора связанных записей журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="a1360-188">identity</span><span class="sxs-lookup"><span data-stu-id="a1360-188">identity</span></span> |<span data-ttu-id="a1360-189">Объект</span><span class="sxs-lookup"><span data-stu-id="a1360-189">Object</span></span> |<span data-ttu-id="a1360-190">Идентификатор, для которого был создан журнал.</span><span class="sxs-lookup"><span data-stu-id="a1360-190">The identity that generated the log</span></span> |
| <span data-ttu-id="a1360-191">properties</span><span class="sxs-lookup"><span data-stu-id="a1360-191">properties</span></span> |<span data-ttu-id="a1360-192">JSON</span><span class="sxs-lookup"><span data-stu-id="a1360-192">JSON</span></span> |<span data-ttu-id="a1360-193">Дополнительные сведения см. ниже.</span><span class="sxs-lookup"><span data-stu-id="a1360-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="a1360-194">Схема свойств журнала запросов</span><span class="sxs-lookup"><span data-stu-id="a1360-194">Request log properties schema</span></span>
| <span data-ttu-id="a1360-195">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="a1360-195">Name</span></span> | <span data-ttu-id="a1360-196">Тип</span><span class="sxs-lookup"><span data-stu-id="a1360-196">Type</span></span> | <span data-ttu-id="a1360-197">Описание</span><span class="sxs-lookup"><span data-stu-id="a1360-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1360-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="a1360-198">HttpMethod</span></span> |<span data-ttu-id="a1360-199">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-199">String</span></span> |<span data-ttu-id="a1360-200">Метод HTTP, использованный для операции.</span><span class="sxs-lookup"><span data-stu-id="a1360-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="a1360-201">Например, GET.</span><span class="sxs-lookup"><span data-stu-id="a1360-201">For example, GET.</span></span> |
| <span data-ttu-id="a1360-202">Путь</span><span class="sxs-lookup"><span data-stu-id="a1360-202">Path</span></span> |<span data-ttu-id="a1360-203">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-203">String</span></span> |<span data-ttu-id="a1360-204">Путь выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="a1360-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="a1360-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="a1360-205">RequestContentLength</span></span> |<span data-ttu-id="a1360-206">int</span><span class="sxs-lookup"><span data-stu-id="a1360-206">int</span></span> |<span data-ttu-id="a1360-207">Длина содержимого HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="a1360-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="a1360-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="a1360-208">ClientRequestId</span></span> |<span data-ttu-id="a1360-209">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-209">String</span></span> |<span data-ttu-id="a1360-210">Идентификатор, однозначно определяющий данный запрос.</span><span class="sxs-lookup"><span data-stu-id="a1360-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="a1360-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="a1360-211">StartTime</span></span> |<span data-ttu-id="a1360-212">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-212">String</span></span> |<span data-ttu-id="a1360-213">Время получения запроса сервером.</span><span class="sxs-lookup"><span data-stu-id="a1360-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="a1360-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="a1360-214">EndTime</span></span> |<span data-ttu-id="a1360-215">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-215">String</span></span> |<span data-ttu-id="a1360-216">Время отправки ответа сервером.</span><span class="sxs-lookup"><span data-stu-id="a1360-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="a1360-217">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="a1360-217">Audit logs</span></span>
<span data-ttu-id="a1360-218">Ниже приведен пример записи журнала аудита в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="a1360-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="a1360-219">Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="a1360-220">Схема журнала аудита</span><span class="sxs-lookup"><span data-stu-id="a1360-220">Audit log schema</span></span>
| <span data-ttu-id="a1360-221">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="a1360-221">Name</span></span> | <span data-ttu-id="a1360-222">Тип</span><span class="sxs-lookup"><span data-stu-id="a1360-222">Type</span></span> | <span data-ttu-id="a1360-223">Описание</span><span class="sxs-lookup"><span data-stu-id="a1360-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1360-224">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="a1360-224">time</span></span> |<span data-ttu-id="a1360-225">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-225">String</span></span> |<span data-ttu-id="a1360-226">Метка времени журнала (в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="a1360-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="a1360-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="a1360-227">resourceId</span></span> |<span data-ttu-id="a1360-228">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-228">String</span></span> |<span data-ttu-id="a1360-229">Идентификатор ресурса, с которым была выполнена операция.</span><span class="sxs-lookup"><span data-stu-id="a1360-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="a1360-230">category</span><span class="sxs-lookup"><span data-stu-id="a1360-230">category</span></span> |<span data-ttu-id="a1360-231">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-231">String</span></span> |<span data-ttu-id="a1360-232">Категория журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-232">The log category.</span></span> <span data-ttu-id="a1360-233">Например, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="a1360-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="a1360-234">operationName</span><span class="sxs-lookup"><span data-stu-id="a1360-234">operationName</span></span> |<span data-ttu-id="a1360-235">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-235">String</span></span> |<span data-ttu-id="a1360-236">Имя операции, добавленной в журнал.</span><span class="sxs-lookup"><span data-stu-id="a1360-236">Name of the operation that is logged.</span></span> <span data-ttu-id="a1360-237">Например, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="a1360-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="a1360-238">resultType</span><span class="sxs-lookup"><span data-stu-id="a1360-238">resultType</span></span> |<span data-ttu-id="a1360-239">Строка</span><span class="sxs-lookup"><span data-stu-id="a1360-239">String</span></span> |<span data-ttu-id="a1360-240">Состояние операции. Например, 200.</span><span class="sxs-lookup"><span data-stu-id="a1360-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="a1360-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="a1360-241">correlationId</span></span> |<span data-ttu-id="a1360-242">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-242">String</span></span> |<span data-ttu-id="a1360-243">Идентификатор журнала, который можно использовать для формирования набора связанных записей журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="a1360-244">identity</span><span class="sxs-lookup"><span data-stu-id="a1360-244">identity</span></span> |<span data-ttu-id="a1360-245">Объект</span><span class="sxs-lookup"><span data-stu-id="a1360-245">Object</span></span> |<span data-ttu-id="a1360-246">Идентификатор, для которого был создан журнал.</span><span class="sxs-lookup"><span data-stu-id="a1360-246">The identity that generated the log</span></span> |
| <span data-ttu-id="a1360-247">properties</span><span class="sxs-lookup"><span data-stu-id="a1360-247">properties</span></span> |<span data-ttu-id="a1360-248">JSON</span><span class="sxs-lookup"><span data-stu-id="a1360-248">JSON</span></span> |<span data-ttu-id="a1360-249">Дополнительные сведения см. ниже.</span><span class="sxs-lookup"><span data-stu-id="a1360-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="a1360-250">Схема свойств журнала аудита</span><span class="sxs-lookup"><span data-stu-id="a1360-250">Audit log properties schema</span></span>
| <span data-ttu-id="a1360-251">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="a1360-251">Name</span></span> | <span data-ttu-id="a1360-252">Тип</span><span class="sxs-lookup"><span data-stu-id="a1360-252">Type</span></span> | <span data-ttu-id="a1360-253">Описание</span><span class="sxs-lookup"><span data-stu-id="a1360-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1360-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="a1360-254">StreamName</span></span> |<span data-ttu-id="a1360-255">Строковый</span><span class="sxs-lookup"><span data-stu-id="a1360-255">String</span></span> |<span data-ttu-id="a1360-256">Путь выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="a1360-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="a1360-257">Примеры обработки данных журнала</span><span class="sxs-lookup"><span data-stu-id="a1360-257">Samples to process the log data</span></span>
<span data-ttu-id="a1360-258">В Azure Data Lake Store есть пример обработки и анализа данных журнала.</span><span class="sxs-lookup"><span data-stu-id="a1360-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="a1360-259">Этот пример можно найти по адресу [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="a1360-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="a1360-260">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a1360-260">See also</span></span>
* [<span data-ttu-id="a1360-261">Обзор хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="a1360-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="a1360-262">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="a1360-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

