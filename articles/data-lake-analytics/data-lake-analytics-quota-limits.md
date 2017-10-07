---
title: "aaaAzure квоты аналитика Озера данных | Документы Microsoft"
description: "Узнайте, как tooadjust, увеличение квоты ограничений в учетные записи аналитики Озера данных Azure (ADLA)."
services: data-lake-analytics
keywords: "Аналитика озера данных Azure"
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="0bc64-104">Квота Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0bc64-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="0bc64-105">Узнайте, как tooadjust, увеличение квоты ограничений в учетные записи аналитики Озера данных Azure (ADLA).</span><span class="sxs-lookup"><span data-stu-id="0bc64-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="0bc64-106">Зная ее ограничения, вы сможете понять поведение задания U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0bc64-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="0bc64-107">Все квоты, мягкое, поэтому можно увеличить дисковое пространство, занимаемое hello по достижении toous.</span><span class="sxs-lookup"><span data-stu-id="0bc64-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="0bc64-108">Ограничения подписок Azure</span><span class="sxs-lookup"><span data-stu-id="0bc64-108">Azure subscriptions limits</span></span>

<span data-ttu-id="0bc64-109">**Максимальное количество учетных записей Azure Data Lake Analytics в одной подписке:** 5.</span><span class="sxs-lookup"><span data-stu-id="0bc64-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="0bc64-110">Это максимальное число hello ADLA учетные записи, которые можно создать для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="0bc64-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="0bc64-111">Если учетная запись ADLA toocreate шестом, будет формировать ошибку «В области под именем подписки достигнуто hello максимальное количество аналитики Озера данных учетных записей (5)».</span><span class="sxs-lookup"><span data-stu-id="0bc64-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="0bc64-112">В этом случае удалите все неиспользуемые учетные записи ADLA или связаться с toous [отправив запрос в службу поддержки](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="0bc64-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="0bc64-113">Ограничения учетной записи Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0bc64-113">ADLA account limits</span></span>

<span data-ttu-id="0bc64-114">**Максимальное количество единиц аналитики на учетную запись:** 250.</span><span class="sxs-lookup"><span data-stu-id="0bc64-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="0bc64-115">Это максимальное число hello Сиднейское, которые могут выполняться параллельно в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0bc64-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="0bc64-116">Если общее количество единиц аналитики по всем выполняемым заданиям превысит это ограничение, новые задания будут автоматически помещаться в очередь.</span><span class="sxs-lookup"><span data-stu-id="0bc64-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="0bc64-117">Например:</span><span class="sxs-lookup"><span data-stu-id="0bc64-117">For example:</span></span>

* <span data-ttu-id="0bc64-118">Если имеется только одно задание с 250 Сиднейское при отправке второе задание он будет ожидать в очереди заданий hello до завершения первого задания hello.</span><span class="sxs-lookup"><span data-stu-id="0bc64-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="0bc64-119">Если уже имеется пять заданий, выполняемых каждой используется 50 Сиднейское при отправке шестой задание, которое требуется 20 Сиднейское ожидает в очереди заданий hello до 20 Сиднейское доступны.</span><span class="sxs-lookup"><span data-stu-id="0bc64-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="0bc64-120">**Максимальное число одновременно выполняемых заданий U-SQL на учетную запись:** 20.</span><span class="sxs-lookup"><span data-stu-id="0bc64-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="0bc64-121">Это hello максимальное количество заданий, которые могут одновременно работать в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0bc64-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="0bc64-122">При достижении этого значения новые задания автоматически помещаются в очередь.</span><span class="sxs-lookup"><span data-stu-id="0bc64-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="0bc64-123">Корректировка квот Azure Data Lake Analytics для учетной записи</span><span class="sxs-lookup"><span data-stu-id="0bc64-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="0bc64-124">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bc64-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0bc64-125">Выберите существующую учетную запись ADLA.</span><span class="sxs-lookup"><span data-stu-id="0bc64-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="0bc64-126">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0bc64-126">Click **Properties**.</span></span>
4. <span data-ttu-id="0bc64-127">Настройка **параллелизма** и **одновременно выполняемых заданий** toosuit вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="0bc64-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="0bc64-129">Увеличение максимальной квоты</span><span class="sxs-lookup"><span data-stu-id="0bc64-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="0bc64-130">Откройте запрос на поддержку на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0bc64-130">Open a support request in Azure Portal.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="0bc64-133">Выберите тип проблемы hello **квоты**.</span><span class="sxs-lookup"><span data-stu-id="0bc64-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="0bc64-134">Выберите **подписку**, которая не является пробной.</span><span class="sxs-lookup"><span data-stu-id="0bc64-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="0bc64-135">Выберите тип квоты **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0bc64-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="0bc64-137">В колонке hello проблема объясняется лимита запрошенное увеличение с **сведения** почему нужно это дополнительная емкость.</span><span class="sxs-lookup"><span data-stu-id="0bc64-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="0bc64-139">Проверьте свои контактные данные и создать запрос на получение поддержки hello.</span><span class="sxs-lookup"><span data-stu-id="0bc64-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="0bc64-140">Корпорация Майкрософт не рассмотрит вашу заявку и пытается tooaccommodate бизнесу необходимо как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="0bc64-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bc64-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bc64-141">Next steps</span></span>

* [<span data-ttu-id="0bc64-142">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0bc64-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0bc64-143">Управление аналитикой озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bc64-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="0bc64-144">Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="0bc64-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
