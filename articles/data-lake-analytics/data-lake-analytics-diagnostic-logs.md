---
title: "журналы диагностики aaaViewing для аналитики Озера данных Azure | Документы Microsoft"
description: "Понять, как toosetup и диагностики доступа в журналах данных Azure аналитики Озера "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="3cace-103">Доступ к журналам диагностики для Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3cace-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="3cace-104">Сбор данных диагностики можно использовать журналы аудита доступа к данным toocollect.</span><span class="sxs-lookup"><span data-stu-id="3cace-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="3cace-105">Эти журналы содержат такие сведения:</span><span class="sxs-lookup"><span data-stu-id="3cace-105">These logs provide information such as:</span></span>

* <span data-ttu-id="3cace-106">Список пользователей, доступ к которым hello данных.</span><span class="sxs-lookup"><span data-stu-id="3cace-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="3cace-107">Как часто осуществляется hello данных.</span><span class="sxs-lookup"><span data-stu-id="3cace-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="3cace-108">Сколько данных хранится в учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="3cace-109">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="3cace-109">Enable logging</span></span>

1. <span data-ttu-id="3cace-110">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3cace-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3cace-111">Открыть учетную запись аналитики Озера данных и выберите **журналы диагностики** из hello __монитор__ раздела.</span><span class="sxs-lookup"><span data-stu-id="3cace-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="3cace-112">Затем выберите __Turn on diagnostics__ (Включить диагностику).</span><span class="sxs-lookup"><span data-stu-id="3cace-112">Next, select __Turn on diagnostics__.</span></span>

    ![Включение аудита toocollect диагностики и журналы запросов](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="3cace-114">Из __параметры диагностики__, задать статус too__On__ hello и выберите параметры ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="3cace-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="3cace-115">![Включение аудита toocollect диагностики и журналы запросов](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "включить журналы диагностики")</span><span class="sxs-lookup"><span data-stu-id="3cace-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="3cace-116">Задать **состояние** слишком**на** tooenable ведения журнала диагностики.</span><span class="sxs-lookup"><span data-stu-id="3cace-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="3cace-117">Данные hello toostore или процесс можно тремя способами.</span><span class="sxs-lookup"><span data-stu-id="3cace-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="3cace-118">Выберите __архивировать учетной записи хранилища tooa__ toostore входит в учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3cace-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="3cace-119">Используйте этот параметр, если вы хотите tooarchive hello данные.</span><span class="sxs-lookup"><span data-stu-id="3cace-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="3cace-120">Если выбран этот параметр, необходимо предоставить Azure журналы учетной записи хранения toosave hello для.</span><span class="sxs-lookup"><span data-stu-id="3cace-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="3cace-121">Выберите **поток tooan концентратора событий** tooan данных журнала toostream концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="3cace-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="3cace-122">Этот параметр следует использовать, если есть конвейер последующей обработки, анализирующий входящие журналы в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="3cace-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="3cace-123">Если этот флажок установлен, должен предоставить сведения hello для hello требуется toouse концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="3cace-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="3cace-124">Выберите __отправки tooLog Analytics__ toosend hello данных toohello службы анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="3cace-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="3cace-125">Используйте этот параметр, если вы toogather toouse анализа журналов и анализ журналов.</span><span class="sxs-lookup"><span data-stu-id="3cace-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="3cace-126">Укажите, хотите ли вы журналы аудита tooget журналы запросов и/или.</span><span class="sxs-lookup"><span data-stu-id="3cace-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="3cace-127">В журнал запросов записываются все запросы API,</span><span class="sxs-lookup"><span data-stu-id="3cace-127">A request log captures every API request.</span></span> <span data-ttu-id="3cace-128">а в журнал аудита — все операции, активируемые запросами API.</span><span class="sxs-lookup"><span data-stu-id="3cace-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="3cace-129">Для __архивировать учетной записи хранилища tooa__, укажите номер hello данных hello tooretain дней.</span><span class="sxs-lookup"><span data-stu-id="3cace-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="3cace-130">Щелкните __Сохранить__.</span><span class="sxs-lookup"><span data-stu-id="3cace-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="3cace-131">Необходимо выбрать __архивировать учетной записи хранилища tooa__, __поток tooan концентратора событий__ или __отправки tooLog Analytics__ перед нажатием кнопки hello __Сохранить__кнопки.</span><span class="sxs-lookup"><span data-stu-id="3cace-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="3cace-132">После включения параметров диагностики можно вернуть toohello __журналы диагностики__ журналы hello tooview колонку.</span><span class="sxs-lookup"><span data-stu-id="3cace-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="3cace-133">Просмотр журналов</span><span class="sxs-lookup"><span data-stu-id="3cace-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="3cace-134">Используйте представление hello аналитики Озера данных</span><span class="sxs-lookup"><span data-stu-id="3cace-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="3cace-135">Из аналитики Озера данных учетной записи колонке в разделе **мониторинг**выберите **журналы диагностики** и затем выберите toodisplay записи в журналах.</span><span class="sxs-lookup"><span data-stu-id="3cace-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="3cace-136">![Просмотр ведения журнала диагностики](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Просмотр журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="3cace-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="3cace-137">Hello журналы разбиты на категории по **журналы аудита** и **журналы запросов**.</span><span class="sxs-lookup"><span data-stu-id="3cace-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![записи журнала](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="3cace-139">Журналы запросов сохранить каждый запрос API на hello учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="3cace-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="3cace-140">Журналы аудита, аналогичные toorequest журналы, но обеспечивает гораздо более подробный разбор hello операций.</span><span class="sxs-lookup"><span data-stu-id="3cace-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="3cace-141">Например, вызов API для одной передачи в журнале запросов может породить несколько операций добавления в журналах аудита.</span><span class="sxs-lookup"><span data-stu-id="3cace-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="3cace-142">Нажмите кнопку hello **загрузки** ссылку для toodownload запись журнала, что журнала.</span><span class="sxs-lookup"><span data-stu-id="3cace-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="3cace-143">Использовать учетную запись хранилища Azure hello, который содержит данные журнала</span><span class="sxs-lookup"><span data-stu-id="3cace-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="3cace-144">Откройте колонку учетной записи хранилища Azure hello, связанный с аналитики Озера данных для ведения журнала и нажмите кнопку __большие двоичные объекты__.</span><span class="sxs-lookup"><span data-stu-id="3cace-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="3cace-145">Hello **службе BLOB-объектов** колонке перечислены два контейнера.</span><span class="sxs-lookup"><span data-stu-id="3cace-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="3cace-146">![Просмотр ведения журнала диагностики](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Просмотр журналов диагностики")</span><span class="sxs-lookup"><span data-stu-id="3cace-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="3cace-147">контейнер Hello **аналитики журналов аудита** содержит журналы аудита hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="3cace-148">контейнер Hello **аналитики журналов запросов** содержит журналы запросов hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="3cace-149">В этих контейнерах hello журналы хранятся в hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="3cace-149">Within these containers, hello logs are stored under hello following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="3cace-150">Hello `##` записи в путь hello содержат hello года, месяца, дня и часа, в которой hello создания журнала.</span><span class="sxs-lookup"><span data-stu-id="3cace-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="3cace-151">Служба Data Lake Analytics создает один файл каждый час, поэтому параметр `m=` всегда содержит значение `00`.</span><span class="sxs-lookup"><span data-stu-id="3cace-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="3cace-152">Например журнал аудита tooan hello полный путь может быть:</span><span class="sxs-lookup"><span data-stu-id="3cace-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="3cace-153">Аналогичным образом может быть журнал запросов tooa hello полный путь.</span><span class="sxs-lookup"><span data-stu-id="3cace-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="3cace-154">Структура журнала</span><span class="sxs-lookup"><span data-stu-id="3cace-154">Log structure</span></span>

<span data-ttu-id="3cace-155">Hello журналы аудита и запрос, структурированный формат JSON.</span><span class="sxs-lookup"><span data-stu-id="3cace-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="3cace-156">Журналы запросов</span><span class="sxs-lookup"><span data-stu-id="3cace-156">Request logs</span></span>

<span data-ttu-id="3cace-157">Ниже приведен пример записи в журнале hello запроса в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="3cace-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="3cace-158">Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.</span><span class="sxs-lookup"><span data-stu-id="3cace-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="3cace-159">Схема журнала запросов</span><span class="sxs-lookup"><span data-stu-id="3cace-159">Request log schema</span></span>

| <span data-ttu-id="3cace-160">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="3cace-160">Name</span></span> | <span data-ttu-id="3cace-161">Тип</span><span class="sxs-lookup"><span data-stu-id="3cace-161">Type</span></span> | <span data-ttu-id="3cace-162">Описание</span><span class="sxs-lookup"><span data-stu-id="3cace-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cace-163">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="3cace-163">time</span></span> |<span data-ttu-id="3cace-164">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-164">String</span></span> |<span data-ttu-id="3cace-165">Здравствуйте, отметка времени (в формате UTC) hello журнала</span><span class="sxs-lookup"><span data-stu-id="3cace-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="3cace-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="3cace-166">resourceId</span></span> |<span data-ttu-id="3cace-167">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-167">String</span></span> |<span data-ttu-id="3cace-168">Идентификатор ресурса hello, затраченное на операцию Hello разместить на</span><span class="sxs-lookup"><span data-stu-id="3cace-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="3cace-169">category</span><span class="sxs-lookup"><span data-stu-id="3cace-169">category</span></span> |<span data-ttu-id="3cace-170">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-170">String</span></span> |<span data-ttu-id="3cace-171">Категория журнала Hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-171">hello log category.</span></span> <span data-ttu-id="3cace-172">Например, **Requests**.</span><span class="sxs-lookup"><span data-stu-id="3cace-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="3cace-173">operationName</span><span class="sxs-lookup"><span data-stu-id="3cace-173">operationName</span></span> |<span data-ttu-id="3cace-174">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-174">String</span></span> |<span data-ttu-id="3cace-175">Имя операции hello, который выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="3cace-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="3cace-176">Например, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="3cace-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="3cace-177">resultType</span><span class="sxs-lookup"><span data-stu-id="3cace-177">resultType</span></span> |<span data-ttu-id="3cace-178">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-178">String</span></span> |<span data-ttu-id="3cace-179">состояние Hello hello операции, например, 200.</span><span class="sxs-lookup"><span data-stu-id="3cace-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="3cace-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="3cace-180">callerIpAddress</span></span> |<span data-ttu-id="3cace-181">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-181">String</span></span> |<span data-ttu-id="3cace-182">Hello IP-адрес клиента hello, выполняющего запрос hello</span><span class="sxs-lookup"><span data-stu-id="3cace-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="3cace-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="3cace-183">correlationId</span></span> |<span data-ttu-id="3cace-184">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-184">String</span></span> |<span data-ttu-id="3cace-185">Идентификатор журнала hello Hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-185">hello identifier of hello log.</span></span> <span data-ttu-id="3cace-186">Это значение может быть используется toogroup набор соответствующие записи журнала.</span><span class="sxs-lookup"><span data-stu-id="3cace-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="3cace-187">identity</span><span class="sxs-lookup"><span data-stu-id="3cace-187">identity</span></span> |<span data-ttu-id="3cace-188">Объект</span><span class="sxs-lookup"><span data-stu-id="3cace-188">Object</span></span> |<span data-ttu-id="3cace-189">удостоверение Hello, создается журнал hello</span><span class="sxs-lookup"><span data-stu-id="3cace-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="3cace-190">properties</span><span class="sxs-lookup"><span data-stu-id="3cace-190">properties</span></span> |<span data-ttu-id="3cace-191">JSON</span><span class="sxs-lookup"><span data-stu-id="3cace-191">JSON</span></span> |<span data-ttu-id="3cace-192">См. в hello далее разделе (схема свойства запроса журнала)</span><span class="sxs-lookup"><span data-stu-id="3cace-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="3cace-193">Схема свойств журнала запросов</span><span class="sxs-lookup"><span data-stu-id="3cace-193">Request log properties schema</span></span>

| <span data-ttu-id="3cace-194">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="3cace-194">Name</span></span> | <span data-ttu-id="3cace-195">Тип</span><span class="sxs-lookup"><span data-stu-id="3cace-195">Type</span></span> | <span data-ttu-id="3cace-196">Описание</span><span class="sxs-lookup"><span data-stu-id="3cace-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cace-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="3cace-197">HttpMethod</span></span> |<span data-ttu-id="3cace-198">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-198">String</span></span> |<span data-ttu-id="3cace-199">Hello используемый метод HTTP для операции hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="3cace-200">Например, GET.</span><span class="sxs-lookup"><span data-stu-id="3cace-200">For example, GET.</span></span> |
| <span data-ttu-id="3cace-201">Путь</span><span class="sxs-lookup"><span data-stu-id="3cace-201">Path</span></span> |<span data-ttu-id="3cace-202">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-202">String</span></span> |<span data-ttu-id="3cace-203">Hello путь hello операции на</span><span class="sxs-lookup"><span data-stu-id="3cace-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="3cace-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="3cace-204">RequestContentLength</span></span> |<span data-ttu-id="3cace-205">int</span><span class="sxs-lookup"><span data-stu-id="3cace-205">int</span></span> |<span data-ttu-id="3cace-206">Длина содержимого Hello hello HTTP-запроса</span><span class="sxs-lookup"><span data-stu-id="3cace-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="3cace-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="3cace-207">ClientRequestId</span></span> |<span data-ttu-id="3cace-208">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-208">String</span></span> |<span data-ttu-id="3cace-209">Здравствуйте, идентификатор, однозначно определяющее этот запрос</span><span class="sxs-lookup"><span data-stu-id="3cace-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="3cace-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="3cace-210">StartTime</span></span> |<span data-ttu-id="3cace-211">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-211">String</span></span> |<span data-ttu-id="3cace-212">Hello время какие hello полученных hello запроса сервера</span><span class="sxs-lookup"><span data-stu-id="3cace-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="3cace-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="3cace-213">EndTime</span></span> |<span data-ttu-id="3cace-214">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-214">String</span></span> |<span data-ttu-id="3cace-215">время Hello какие hello server отправки ответа</span><span class="sxs-lookup"><span data-stu-id="3cace-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="3cace-216">Журналы аудита</span><span class="sxs-lookup"><span data-stu-id="3cace-216">Audit logs</span></span>

<span data-ttu-id="3cace-217">Ниже приведен пример записи в журнал аудита в формате JSON hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="3cace-218">Каждый большой двоичный объект имеет один корневой объект под названием **records** , который содержит массив объектов журнала.</span><span class="sxs-lookup"><span data-stu-id="3cace-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="3cace-219">Схема журнала аудита</span><span class="sxs-lookup"><span data-stu-id="3cace-219">Audit log schema</span></span>

| <span data-ttu-id="3cace-220">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="3cace-220">Name</span></span> | <span data-ttu-id="3cace-221">Тип</span><span class="sxs-lookup"><span data-stu-id="3cace-221">Type</span></span> | <span data-ttu-id="3cace-222">Описание</span><span class="sxs-lookup"><span data-stu-id="3cace-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cace-223">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="3cace-223">time</span></span> |<span data-ttu-id="3cace-224">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-224">String</span></span> |<span data-ttu-id="3cace-225">Здравствуйте, отметка времени (в формате UTC) hello журнала</span><span class="sxs-lookup"><span data-stu-id="3cace-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="3cace-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="3cace-226">resourceId</span></span> |<span data-ttu-id="3cace-227">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-227">String</span></span> |<span data-ttu-id="3cace-228">Идентификатор ресурса hello, затраченное на операцию Hello разместить на</span><span class="sxs-lookup"><span data-stu-id="3cace-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="3cace-229">category</span><span class="sxs-lookup"><span data-stu-id="3cace-229">category</span></span> |<span data-ttu-id="3cace-230">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-230">String</span></span> |<span data-ttu-id="3cace-231">Категория журнала Hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-231">hello log category.</span></span> <span data-ttu-id="3cace-232">Например, **Audit**.</span><span class="sxs-lookup"><span data-stu-id="3cace-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="3cace-233">operationName</span><span class="sxs-lookup"><span data-stu-id="3cace-233">operationName</span></span> |<span data-ttu-id="3cace-234">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-234">String</span></span> |<span data-ttu-id="3cace-235">Имя операции hello, который выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="3cace-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="3cace-236">Например, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="3cace-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="3cace-237">resultType</span><span class="sxs-lookup"><span data-stu-id="3cace-237">resultType</span></span> |<span data-ttu-id="3cace-238">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-238">String</span></span> |<span data-ttu-id="3cace-239">Дополнительные сведения о состоянии задания hello (Имя_операции).</span><span class="sxs-lookup"><span data-stu-id="3cace-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="3cace-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="3cace-240">resultSignature</span></span> |<span data-ttu-id="3cace-241">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-241">String</span></span> |<span data-ttu-id="3cace-242">Дополнительные сведения о состоянии задания hello (Имя_операции).</span><span class="sxs-lookup"><span data-stu-id="3cace-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="3cace-243">identity</span><span class="sxs-lookup"><span data-stu-id="3cace-243">identity</span></span> |<span data-ttu-id="3cace-244">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-244">String</span></span> |<span data-ttu-id="3cace-245">Hello пользователь, который запросил операцию hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-245">hello user that requested hello operation.</span></span> <span data-ttu-id="3cace-246">Например, susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3cace-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="3cace-247">properties</span><span class="sxs-lookup"><span data-stu-id="3cace-247">properties</span></span> |<span data-ttu-id="3cace-248">JSON</span><span class="sxs-lookup"><span data-stu-id="3cace-248">JSON</span></span> |<span data-ttu-id="3cace-249">См. в hello далее разделе (схема свойства журнала аудита)</span><span class="sxs-lookup"><span data-stu-id="3cace-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="3cace-250">**Тип resultType** и **resultSignature** содержат информацию о hello результат операции и содержать только значение при завершении операции.</span><span class="sxs-lookup"><span data-stu-id="3cace-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="3cace-251">К примеру, у них есть значение, только если у свойства **operationName** есть значение **JobStarted** или **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="3cace-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="3cace-252">Схема свойств журнала аудита</span><span class="sxs-lookup"><span data-stu-id="3cace-252">Audit log properties schema</span></span>

| <span data-ttu-id="3cace-253">Name (Имя)</span><span class="sxs-lookup"><span data-stu-id="3cace-253">Name</span></span> | <span data-ttu-id="3cace-254">Тип</span><span class="sxs-lookup"><span data-stu-id="3cace-254">Type</span></span> | <span data-ttu-id="3cace-255">Описание</span><span class="sxs-lookup"><span data-stu-id="3cace-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3cace-256">JobId</span><span class="sxs-lookup"><span data-stu-id="3cace-256">JobId</span></span> |<span data-ttu-id="3cace-257">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-257">String</span></span> |<span data-ttu-id="3cace-258">Hello идентификатор toohello назначенные задания</span><span class="sxs-lookup"><span data-stu-id="3cace-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="3cace-259">JobName</span><span class="sxs-lookup"><span data-stu-id="3cace-259">JobName</span></span> |<span data-ttu-id="3cace-260">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-260">String</span></span> |<span data-ttu-id="3cace-261">Имя Hello, предоставленный для задания hello</span><span class="sxs-lookup"><span data-stu-id="3cace-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="3cace-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="3cace-262">JobRunTime</span></span> |<span data-ttu-id="3cace-263">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-263">String</span></span> |<span data-ttu-id="3cace-264">Среда выполнения Hello использовала tooprocess hello задания</span><span class="sxs-lookup"><span data-stu-id="3cace-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="3cace-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="3cace-265">SubmitTime</span></span> |<span data-ttu-id="3cace-266">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-266">String</span></span> |<span data-ttu-id="3cace-267">Hello время (в формате UTC), задания hello</span><span class="sxs-lookup"><span data-stu-id="3cace-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="3cace-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="3cace-268">StartTime</span></span> |<span data-ttu-id="3cace-269">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-269">String</span></span> |<span data-ttu-id="3cace-270">Hello время hello запуска задания после отправки (в формате UTC)</span><span class="sxs-lookup"><span data-stu-id="3cace-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="3cace-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="3cace-271">EndTime</span></span> |<span data-ttu-id="3cace-272">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-272">String</span></span> |<span data-ttu-id="3cace-273">Задание hello Hello времени окончания</span><span class="sxs-lookup"><span data-stu-id="3cace-273">hello time hello job ended</span></span> |
| <span data-ttu-id="3cace-274">Parallelism</span><span class="sxs-lookup"><span data-stu-id="3cace-274">Parallelism</span></span> |<span data-ttu-id="3cace-275">Строка</span><span class="sxs-lookup"><span data-stu-id="3cace-275">String</span></span> |<span data-ttu-id="3cace-276">Hello число единиц аналитики Озера данных, запрошенных для этого задания во время передачи</span><span class="sxs-lookup"><span data-stu-id="3cace-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="3cace-277">**SubmitTime**, **StartTime**, **EndTime** и **Parallelism** предоставляют сведения об операции.</span><span class="sxs-lookup"><span data-stu-id="3cace-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="3cace-278">У этих записей есть значение только в том случае, если операция уже началась или завершилась.</span><span class="sxs-lookup"><span data-stu-id="3cace-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="3cace-279">Например **SubmitTime** содержит только значение после **operationName** имеет значение hello **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="3cace-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="3cace-280">Данные журнала процесса hello</span><span class="sxs-lookup"><span data-stu-id="3cace-280">Process hello log data</span></span>

<span data-ttu-id="3cace-281">Azure аналитики Озера данных также пример о том, как tooprocess и анализировать данные журнала hello.</span><span class="sxs-lookup"><span data-stu-id="3cace-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="3cace-282">Можно найти пример hello в [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="3cace-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cace-283">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3cace-283">Next steps</span></span>
* [<span data-ttu-id="3cace-284">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3cace-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
