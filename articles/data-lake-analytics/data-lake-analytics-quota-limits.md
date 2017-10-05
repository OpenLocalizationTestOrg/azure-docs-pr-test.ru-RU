---
title: "Квоты Azure Data Lake Analytics | Документация Майкрософт"
description: "Узнайте, как настроить или увеличить квоту в учетных записях Azure Data Lake Analytics (ADLA)."
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
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="78125-104">Квота Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="78125-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="78125-105">Узнайте, как настроить или увеличить квоту в учетных записях Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="78125-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="78125-106">Зная ее ограничения, вы сможете понять поведение задания U-SQL.</span><span class="sxs-lookup"><span data-stu-id="78125-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="78125-107">Все квоты являются мягкими, то есть вы всегда можете увеличить максимальное ограничение, направив нам соответствующий запрос.</span><span class="sxs-lookup"><span data-stu-id="78125-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="78125-108">Ограничения подписок Azure</span><span class="sxs-lookup"><span data-stu-id="78125-108">Azure subscriptions limits</span></span>

<span data-ttu-id="78125-109">**Максимальное количество учетных записей Azure Data Lake Analytics в одной подписке:** 5.</span><span class="sxs-lookup"><span data-stu-id="78125-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="78125-110">Это максимальное число учетных записей Azure Data Lake Analytics, которые можно создать, на подписку.</span><span class="sxs-lookup"><span data-stu-id="78125-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="78125-111">Если вы попытаетесь создать шестую учетную запись Azure Data Lake Analytics, то увидите сообщение о том, что достигнуто максимальное количество учетных записей Data Lake Analytics (5) для текущего региона и подписки.</span><span class="sxs-lookup"><span data-stu-id="78125-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="78125-112">Вы можете удалить неиспользуемые учетные записи ADLA или [отправить запрос в службу поддержки](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="78125-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="78125-113">Ограничения учетной записи Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="78125-113">ADLA account limits</span></span>

<span data-ttu-id="78125-114">**Максимальное количество единиц аналитики на учетную запись:** 250.</span><span class="sxs-lookup"><span data-stu-id="78125-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="78125-115">Это максимальное число единиц аналитики, которые могут выполняться параллельно в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="78125-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="78125-116">Если общее количество единиц аналитики по всем выполняемым заданиям превысит это ограничение, новые задания будут автоматически помещаться в очередь.</span><span class="sxs-lookup"><span data-stu-id="78125-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="78125-117">Например:</span><span class="sxs-lookup"><span data-stu-id="78125-117">For example:</span></span>

* <span data-ttu-id="78125-118">Если выполняется только одно задание на 250 единиц аналитики, то при отправке второго задания оно будет помещено в очередь, пока не завершится первое задание.</span><span class="sxs-lookup"><span data-stu-id="78125-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="78125-119">Если выполняются пять заданий, каждое из которых использует по 50 единиц аналитики, то при отправке шестого задания, на которое нужно 20 единиц аналитики, оно будет ожидать в очереди заданий, пока не освободятся эти 20 единиц аналитики.</span><span class="sxs-lookup"><span data-stu-id="78125-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="78125-120">**Максимальное число одновременно выполняемых заданий U-SQL на учетную запись:** 20.</span><span class="sxs-lookup"><span data-stu-id="78125-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="78125-121">Это максимальное число заданий, которые могут выполняться параллельно в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="78125-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="78125-122">При достижении этого значения новые задания автоматически помещаются в очередь.</span><span class="sxs-lookup"><span data-stu-id="78125-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="78125-123">Корректировка квот Azure Data Lake Analytics для учетной записи</span><span class="sxs-lookup"><span data-stu-id="78125-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="78125-124">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78125-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78125-125">Выберите существующую учетную запись ADLA.</span><span class="sxs-lookup"><span data-stu-id="78125-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="78125-126">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="78125-126">Click **Properties**.</span></span>
4. <span data-ttu-id="78125-127">Настройте значения параметров **Параллелизм** и **Параллельные задания** с учетом своих потребностей.</span><span class="sxs-lookup"><span data-stu-id="78125-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="78125-129">Увеличение максимальной квоты</span><span class="sxs-lookup"><span data-stu-id="78125-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="78125-130">Откройте запрос на поддержку на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="78125-130">Open a support request in Azure Portal.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="78125-133">Для типа проблемы укажите **Квота**.</span><span class="sxs-lookup"><span data-stu-id="78125-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="78125-134">Выберите **подписку**, которая не является пробной.</span><span class="sxs-lookup"><span data-stu-id="78125-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="78125-135">Выберите тип квоты **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="78125-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="78125-137">В колонке "Проблема" опишите необходимые увеличения квоты, а в поле **Сведения** укажите причины для такого увеличения.</span><span class="sxs-lookup"><span data-stu-id="78125-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Аналитика озера данных Azure: колонка на портале](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="78125-139">Проверьте введенные контактные данные и создайте запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="78125-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="78125-140">Корпорация Майкрософт проверит запрос и удовлетворит потребности вашего бизнеса как можно скорее.</span><span class="sxs-lookup"><span data-stu-id="78125-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78125-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78125-141">Next steps</span></span>

* [<span data-ttu-id="78125-142">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="78125-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="78125-143">Управление аналитикой озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78125-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="78125-144">Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="78125-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
