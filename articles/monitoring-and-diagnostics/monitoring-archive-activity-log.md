---
title: "hello aaaArchive журнал действий Azure | Документы Microsoft"
description: "Узнайте, как tooarchive Azure действие журнала для долгосрочного хранения в учетную запись хранилища."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="fb20a-103">Архив hello журнал действий Azure</span><span class="sxs-lookup"><span data-stu-id="fb20a-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="fb20a-104">В этой статье демонстрируется использование hello портал Azure, командлеты PowerShell или CLI кросс-платформенных tooarchive вашей [ **журнал действий Azure** ](monitoring-overview-activity-logs.md) в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fb20a-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="fb20a-105">Этот параметр полезен, если вы хотите tooretain больше 90 дней (с полный контроль над политикой хранения hello) для журналов действий аудита статического анализа или резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="fb20a-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="fb20a-106">Требуется tooretain событий 90 дней или меньше вы не обязательно tooset архивных tooa учетной записи хранилища, так как журнал действий события сохраняются в hello платформы Azure 90 дней без включения архивации.</span><span class="sxs-lookup"><span data-stu-id="fb20a-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb20a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb20a-107">Prerequisites</span></span>
<span data-ttu-id="fb20a-108">Прежде чем начать, вам потребуется слишком[создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich можно архивировать в журнал действий.</span><span class="sxs-lookup"><span data-stu-id="fb20a-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="fb20a-109">Настоятельно рекомендуется не использовать существующую учетную запись хранения с других, отличных от наблюдения за данными, хранимыми в нем, чтобы лучше управлять toomonitoring доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="fb20a-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="fb20a-110">Тем не менее если архивация выполняется также журналы диагностики и учетной записи хранения метрики tooa, может быть toouse смысле этой учетной записи хранения для активности журнала также tookeep все данные наблюдения в центральном расположении.</span><span class="sxs-lookup"><span data-stu-id="fb20a-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="fb20a-111">Hello учетной записи хранилища, используемого должна быть учетной записью хранения общего назначения, не учетную запись хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fb20a-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="fb20a-112">Учетная запись хранения Hello не имеет toobe в hello той же подписке, hello подписки выпуска журналы при условии, что hello пользователь, настраивающий приветствия имеет соответствующий RBAC доступа tooboth подписок.</span><span class="sxs-lookup"><span data-stu-id="fb20a-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="fb20a-113">Профиль журнала</span><span class="sxs-lookup"><span data-stu-id="fb20a-113">Log Profile</span></span>
<span data-ttu-id="fb20a-114">hello tooarchive журнал действий с помощью приведенных ниже способов hello, задайте hello **профиля журнала** для подписки.</span><span class="sxs-lookup"><span data-stu-id="fb20a-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="fb20a-115">Hello журнала профиль определяет тип события, которые хранятся или передавать их потоком hello и hello выходных данных — хранилище учетной записи и (или) события концентратора.</span><span class="sxs-lookup"><span data-stu-id="fb20a-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="fb20a-116">Он также определяет политику хранения hello (количество дней tooretain) для событий, которые хранятся в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb20a-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="fb20a-117">Если политика хранения hello toozero, события хранятся бессрочно.</span><span class="sxs-lookup"><span data-stu-id="fb20a-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="fb20a-118">В противном случае это может иметь значение tooany значение в диапазоне от 1 до 2147483647.</span><span class="sxs-lookup"><span data-stu-id="fb20a-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="fb20a-119">Политики хранения, примененных в день, поэтому hello регистрирует конец дня (UTC), с датой hello, что теперь находится за пределами hello политики хранения будут удалены.</span><span class="sxs-lookup"><span data-stu-id="fb20a-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="fb20a-120">Например если у вас есть политика хранения продолжительностью в один день, в начале hello сегодня день hello hello журналы из позавчерашнего дня hello, будет удален.</span><span class="sxs-lookup"><span data-stu-id="fb20a-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="fb20a-121">Дополнительные сведения о профилях журнала см. [здесь](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="fb20a-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="fb20a-122">Журнал действий с помощью портала hello hello архива</span><span class="sxs-lookup"><span data-stu-id="fb20a-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="fb20a-123">На портале hello щелкните hello **журнал действий** ссылку на hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="fb20a-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="fb20a-124">Если вы не видите ссылку для hello журнал действий, щелкните hello **более служб** сначала связать.</span><span class="sxs-lookup"><span data-stu-id="fb20a-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Перейдите в колонку tooActivity журнала](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="fb20a-126">Hello верхней части колонки hello, нажмите кнопку **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="fb20a-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Нажмите кнопку Экспорт hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="fb20a-128">В колонке hello, которое отображается, установите флажок "hello" для **Экспорт учетной записи хранилища tooa** и выберите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="fb20a-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![Настройка учетной записи хранения](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="fb20a-130">С помощью ползунка hello или текстовое поле, определите количество дней, для которых должна храниться журналом событий в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb20a-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="fb20a-131">Если вы предпочитаете toohave данные сохраняются в учетной записи хранения hello бесконечно, задайте этот номер toozero.</span><span class="sxs-lookup"><span data-stu-id="fb20a-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="fb20a-132">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb20a-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="fb20a-133">Архив hello журнал действий с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb20a-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="fb20a-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="fb20a-134">Property</span></span> | <span data-ttu-id="fb20a-135">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fb20a-135">Required</span></span> | <span data-ttu-id="fb20a-136">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="fb20a-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb20a-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="fb20a-137">StorageAccountId</span></span> |<span data-ttu-id="fb20a-138">Нет</span><span class="sxs-lookup"><span data-stu-id="fb20a-138">No</span></span> |<span data-ttu-id="fb20a-139">Идентификатор ресурса для учетной записи хранилища hello toowhich журналы действий должен быть сохранен.</span><span class="sxs-lookup"><span data-stu-id="fb20a-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="fb20a-140">Расположения</span><span class="sxs-lookup"><span data-stu-id="fb20a-140">Locations</span></span> |<span data-ttu-id="fb20a-141">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-141">Yes</span></span> |<span data-ttu-id="fb20a-142">Разделенные запятыми список регионов, для которых вы хотите toocollect журналом событий.</span><span class="sxs-lookup"><span data-stu-id="fb20a-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="fb20a-143">Можно просмотреть список всех областей [при посещении этой страницы](https://azure.microsoft.com/en-us/regions) или с помощью [hello API REST управления Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb20a-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="fb20a-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="fb20a-144">RetentionInDays</span></span> |<span data-ttu-id="fb20a-145">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-145">Yes</span></span> |<span data-ttu-id="fb20a-146">Количество дней, в течение которых будут храниться события: от 1 до 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="fb20a-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="fb20a-147">Нулевое значение хранятся журналы hello бесконечно (навсегда).</span><span class="sxs-lookup"><span data-stu-id="fb20a-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="fb20a-148">Категории</span><span class="sxs-lookup"><span data-stu-id="fb20a-148">Categories</span></span> |<span data-ttu-id="fb20a-149">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-149">Yes</span></span> |<span data-ttu-id="fb20a-150">Разделенный запятыми список категорий событий, которые будут собираться.</span><span class="sxs-lookup"><span data-stu-id="fb20a-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="fb20a-151">Возможные значения: Write, Delete или Action.</span><span class="sxs-lookup"><span data-stu-id="fb20a-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="fb20a-152">Архив hello журнал действий через интерфейс командной строки</span><span class="sxs-lookup"><span data-stu-id="fb20a-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="fb20a-153">Свойство</span><span class="sxs-lookup"><span data-stu-id="fb20a-153">Property</span></span> | <span data-ttu-id="fb20a-154">Обязательно</span><span class="sxs-lookup"><span data-stu-id="fb20a-154">Required</span></span> | <span data-ttu-id="fb20a-155">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="fb20a-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fb20a-156">name</span><span class="sxs-lookup"><span data-stu-id="fb20a-156">name</span></span> |<span data-ttu-id="fb20a-157">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-157">Yes</span></span> |<span data-ttu-id="fb20a-158">Имя профиля журнала.</span><span class="sxs-lookup"><span data-stu-id="fb20a-158">Name of your log profile.</span></span> |
| <span data-ttu-id="fb20a-159">storageId</span><span class="sxs-lookup"><span data-stu-id="fb20a-159">storageId</span></span> |<span data-ttu-id="fb20a-160">Нет</span><span class="sxs-lookup"><span data-stu-id="fb20a-160">No</span></span> |<span data-ttu-id="fb20a-161">Идентификатор ресурса для учетной записи хранилища hello toowhich журналы действий должен быть сохранен.</span><span class="sxs-lookup"><span data-stu-id="fb20a-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="fb20a-162">locations</span><span class="sxs-lookup"><span data-stu-id="fb20a-162">locations</span></span> |<span data-ttu-id="fb20a-163">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-163">Yes</span></span> |<span data-ttu-id="fb20a-164">Разделенные запятыми список регионов, для которых вы хотите toocollect журналом событий.</span><span class="sxs-lookup"><span data-stu-id="fb20a-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="fb20a-165">Можно просмотреть список всех областей [при посещении этой страницы](https://azure.microsoft.com/en-us/regions) или с помощью [hello API REST управления Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb20a-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="fb20a-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="fb20a-166">retentionInDays</span></span> |<span data-ttu-id="fb20a-167">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-167">Yes</span></span> |<span data-ttu-id="fb20a-168">Количество дней, в течение которых будут храниться события: от 1 до 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="fb20a-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="fb20a-169">Нулевое значение будет хранить журналы hello бесконечно (навсегда).</span><span class="sxs-lookup"><span data-stu-id="fb20a-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="fb20a-170">Категории</span><span class="sxs-lookup"><span data-stu-id="fb20a-170">categories</span></span> |<span data-ttu-id="fb20a-171">Да</span><span class="sxs-lookup"><span data-stu-id="fb20a-171">Yes</span></span> |<span data-ttu-id="fb20a-172">Разделенный запятыми список категорий событий, которые будут собираться.</span><span class="sxs-lookup"><span data-stu-id="fb20a-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="fb20a-173">Возможные значения: Write, Delete или Action.</span><span class="sxs-lookup"><span data-stu-id="fb20a-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="fb20a-174">Схема хранилища hello журнал действий</span><span class="sxs-lookup"><span data-stu-id="fb20a-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="fb20a-175">После настройки архивации, контейнер хранилища будут созданы в учетной записи хранилища hello, как только произойдет событие журнал действий.</span><span class="sxs-lookup"><span data-stu-id="fb20a-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="fb20a-176">Hello большие двоичные объекты в контейнере hello выполните hello в том же формате, в журнал действий hello и журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="fb20a-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="fb20a-177">Эти большие двоичные объекты Hello структура выглядит:</span><span class="sxs-lookup"><span data-stu-id="fb20a-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="fb20a-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ИД подписки}/y={год в четырехзначном формате}/m={месяц в двухзначном формате}/d={день в двухзначном формате}/h={время в двухзначном 24-часовом формате}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="fb20a-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="fb20a-179">Например, большой двоичный объект может иметь такое имя:</span><span class="sxs-lookup"><span data-stu-id="fb20a-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="fb20a-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="fb20a-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="fb20a-181">Каждый BLOB-объект PT1H.json содержит большой двоичный объект JSON, событий, произошедших в течение часа hello, указанный в URL-адрес hello больших двоичных объектов (например h = 12).</span><span class="sxs-lookup"><span data-stu-id="fb20a-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="fb20a-182">Во время hello присутствует час события, добавленных toohello PT1H.json файл, как только они происходят.</span><span class="sxs-lookup"><span data-stu-id="fb20a-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="fb20a-183">Здравствуйте, значение минуты (m = 00) всегда равно 00, поскольку журналом событий разбиваются на отдельные большие двоичные объекты в час.</span><span class="sxs-lookup"><span data-stu-id="fb20a-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="fb20a-184">В файле PT1H.json hello каждое событие хранится в массиве записей «hello», в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="fb20a-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="fb20a-185">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="fb20a-185">Element name</span></span> | <span data-ttu-id="fb20a-186">Описание</span><span class="sxs-lookup"><span data-stu-id="fb20a-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb20a-187">Twitter в режиме реального</span><span class="sxs-lookup"><span data-stu-id="fb20a-187">time</span></span> |<span data-ttu-id="fb20a-188">Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="fb20a-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="fb20a-189">resourceId</span></span> |<span data-ttu-id="fb20a-190">Идентификатор ресурса hello влияния ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fb20a-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="fb20a-191">operationName</span><span class="sxs-lookup"><span data-stu-id="fb20a-191">operationName</span></span> |<span data-ttu-id="fb20a-192">Имя операции hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-192">Name of hello operation.</span></span> |
| <span data-ttu-id="fb20a-193">category</span><span class="sxs-lookup"><span data-stu-id="fb20a-193">category</span></span> |<span data-ttu-id="fb20a-194">Категория действия hello, например.</span><span class="sxs-lookup"><span data-stu-id="fb20a-194">Category of hello action, eg.</span></span> <span data-ttu-id="fb20a-195">"Запись", "Чтение", "Действие"</span><span class="sxs-lookup"><span data-stu-id="fb20a-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="fb20a-196">resultType</span><span class="sxs-lookup"><span data-stu-id="fb20a-196">resultType</span></span> |<span data-ttu-id="fb20a-197">Тип результата hello Здравствуйте, например.</span><span class="sxs-lookup"><span data-stu-id="fb20a-197">hello type of hello result, eg.</span></span> <span data-ttu-id="fb20a-198">"Успешно", "Ошибка", "Запуск"</span><span class="sxs-lookup"><span data-stu-id="fb20a-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="fb20a-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="fb20a-199">resultSignature</span></span> |<span data-ttu-id="fb20a-200">Зависит от типа ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="fb20a-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="fb20a-201">durationMs</span></span> |<span data-ttu-id="fb20a-202">Время выполнения операции hello в миллисекундах</span><span class="sxs-lookup"><span data-stu-id="fb20a-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="fb20a-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="fb20a-203">callerIpAddress</span></span> |<span data-ttu-id="fb20a-204">IP-адрес hello пользователя, который выполнил операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности.</span><span class="sxs-lookup"><span data-stu-id="fb20a-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="fb20a-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="fb20a-205">correlationId</span></span> |<span data-ttu-id="fb20a-206">Как правило, GUID в строковом формате hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="fb20a-207">События, которые совместно используют correlationId принадлежат toohello же действию.</span><span class="sxs-lookup"><span data-stu-id="fb20a-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="fb20a-208">identity</span><span class="sxs-lookup"><span data-stu-id="fb20a-208">identity</span></span> |<span data-ttu-id="fb20a-209">BLOB-объектов JSON, описывающий авторизации hello и утверждений.</span><span class="sxs-lookup"><span data-stu-id="fb20a-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="fb20a-210">authorization</span><span class="sxs-lookup"><span data-stu-id="fb20a-210">authorization</span></span> |<span data-ttu-id="fb20a-211">Большой двоичный объект свойства RBAC события hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="fb20a-212">Обычно включает hello свойства «действие», «роль» и «область».</span><span class="sxs-lookup"><span data-stu-id="fb20a-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="fb20a-213">level</span><span class="sxs-lookup"><span data-stu-id="fb20a-213">level</span></span> |<span data-ttu-id="fb20a-214">Уровень события hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-214">Level of hello event.</span></span> <span data-ttu-id="fb20a-215">Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»</span><span class="sxs-lookup"><span data-stu-id="fb20a-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="fb20a-216">location</span><span class="sxs-lookup"><span data-stu-id="fb20a-216">location</span></span> |<span data-ttu-id="fb20a-217">Регион, в какой папке hello произошла (или глобальные).</span><span class="sxs-lookup"><span data-stu-id="fb20a-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="fb20a-218">properties</span><span class="sxs-lookup"><span data-stu-id="fb20a-218">properties</span></span> |<span data-ttu-id="fb20a-219">Набор `<Key, Value>` пары (т. е. словарь), описывающий hello подробных сведениях события hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="fb20a-220">свойства Hello и использовании этих свойств зависит от ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="fb20a-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fb20a-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb20a-221">Next steps</span></span>
* [<span data-ttu-id="fb20a-222">Скачивание больших двоичных объектов для анализа</span><span class="sxs-lookup"><span data-stu-id="fb20a-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="fb20a-223">Поток tooEvent журнал действий hello концентраторы</span><span class="sxs-lookup"><span data-stu-id="fb20a-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="fb20a-224">Дополнительные сведения о hello журнал действий</span><span class="sxs-lookup"><span data-stu-id="fb20a-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

