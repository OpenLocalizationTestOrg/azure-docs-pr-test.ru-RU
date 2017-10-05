---
title: "Высокая доступность и надежность планировщика"
description: "Высокая доступность и надежность планировщика"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 7e7fe49de7814b6058468d630f8638720e5864f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="2afd8-103">Высокая доступность и надежность планировщика</span><span class="sxs-lookup"><span data-stu-id="2afd8-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="2afd8-104">Высокая доступность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="2afd8-105">Будучи основной службой платформы Azure, планировщик Azure отличается высокой доступностью и отличается как географически избыточным развертыванием служб, так и репликацией заданий по географическим регионам.</span><span class="sxs-lookup"><span data-stu-id="2afd8-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="2afd8-106">Географически избыточное развертывание служб</span><span class="sxs-lookup"><span data-stu-id="2afd8-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="2afd8-107">Пользоваться планировщиком Azure можно через пользовательский интерфейс практически в любом географическом регионе, который входит в систему Azure на сегодняшний день.</span><span class="sxs-lookup"><span data-stu-id="2afd8-107">Azure Scheduler is available via the UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="2afd8-108">Список регионов, в которых доступен планировщик Azure, см. [здесь](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="2afd8-108">The list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="2afd8-109">Если центр обработки данных в регионе размещения отображается как недоступный, услуги планировщика Azure может предоставить другой центр обработки данных.</span><span class="sxs-lookup"><span data-stu-id="2afd8-109">If a data center in a hosted region is rendered unavailable, the failover capabilities of Azure Scheduler are such that the service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="2afd8-110">Репликация заданий по географическим регионам</span><span class="sxs-lookup"><span data-stu-id="2afd8-110">Geo-regional job replication</span></span>
<span data-ttu-id="2afd8-111">Планировщик Azure не только обеспечивает доступность внешнего интерфейса для запросов на управление, но и поддерживает репликацию ваших заданий по географическим регионам.</span><span class="sxs-lookup"><span data-stu-id="2afd8-111">Not only is the Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="2afd8-112">В случае сбоя в одном регионе планировщик Azure отрабатывает отказ и обеспечивает выполнение задания из другого центра обработки данных в связанном географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="2afd8-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that the job is run from another data center in the paired geographic region.</span></span>

<span data-ttu-id="2afd8-113">Например, если задание создано в Южно-Центральной части США, планировщик Azure обеспечивает его автоматическую репликацию в Северо-Центральной части США.</span><span class="sxs-lookup"><span data-stu-id="2afd8-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="2afd8-114">В случае сбоя в Южно-Центральной части США планировщик Azure гарантирует выполнение задания из Северо-Центральной части США.</span><span class="sxs-lookup"><span data-stu-id="2afd8-114">When there’s a failure in South Central US, Azure Scheduler ensures that the job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="2afd8-115">Таким образом, в случае сбоя системы Azure планировщик Azure сохраняет данные в том же расширенном географическом регионе.</span><span class="sxs-lookup"><span data-stu-id="2afd8-115">As a result, Azure Scheduler ensures that your data stays within the same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="2afd8-116">Это значит, что вам не нужно дублировать задание, чтобы повысить его доступность: планировщик Azure обеспечивает высокий уровень доступности заданий автоматически.</span><span class="sxs-lookup"><span data-stu-id="2afd8-116">As a result, you need not duplicate your job just to add high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="2afd8-117">Надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="2afd8-118">Доступность самого планировщика Azure поддерживается на высоком уровне, а к созданным пользователями заданиям применяются различные методы.</span><span class="sxs-lookup"><span data-stu-id="2afd8-118">Azure Scheduler guarantees its own high-availability and takes a different approach to user-created jobs.</span></span> <span data-ttu-id="2afd8-119">Например, предположим, что конечная точка HTTP, вызываемая вашим заданием, недоступна.</span><span class="sxs-lookup"><span data-stu-id="2afd8-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="2afd8-120">Несмотря на это, планировщик Azure пытается выполнить задание, предлагая вам альтернативные варианты обхода этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="2afd8-120">Azure Scheduler nonetheless tries to execute your job successfully, by giving you alternative options to deal with failure.</span></span> <span data-ttu-id="2afd8-121">Ниже описаны два варианта, предлагаемых планировщиком Azure.</span><span class="sxs-lookup"><span data-stu-id="2afd8-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="2afd8-122">Настройка политики повтора с помощью параметра retryPolicy</span><span class="sxs-lookup"><span data-stu-id="2afd8-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="2afd8-123">Планировщик Azure позволяет настроить политику повтора.</span><span class="sxs-lookup"><span data-stu-id="2afd8-123">Azure Scheduler allows you to configure a retry policy.</span></span> <span data-ttu-id="2afd8-124">По умолчанию при сбое задания планировщик выполняет еще четыре попытки выполнить это задание с интервалом 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="2afd8-124">By default, if a job fails, Scheduler tries the job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="2afd8-125">Эту политику повтора можно изменить в сторону большей или меньшей настойчивости (например, 10 попыток с интервалом 30 секунд или две попытки с интервалом в сутки).</span><span class="sxs-lookup"><span data-stu-id="2afd8-125">You may re-configure this retry policy to be more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="2afd8-126">Рассмотрим преимущество этой возможности на примере: предположим, что созданное пользователем задание выполняется один раз в неделю и включает вызов конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="2afd8-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="2afd8-127">Если к моменту выполнения задания конечная точка HTTP не работает уже нескольких часов, то задание, скорее всего, не будет выполнено даже после применения политики повтора по умолчанию, а следующая попытка будет произведена только через неделю.</span><span class="sxs-lookup"><span data-stu-id="2afd8-127">If the HTTP endpoint is down for a few hours when your job runs, you may not want to wait one more week for the job to run again since even the default retry policy will fail.</span></span> <span data-ttu-id="2afd8-128">Для таких случаев можно изменить стандартную политику повтора, задав выполнение повторных попыток, например, через каждые три часа (вместо 30 секунд).</span><span class="sxs-lookup"><span data-stu-id="2afd8-128">In such cases, you may reconfigure the standard retry policy to retry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="2afd8-129">Инструкции по настройке политики повтора см. в разделе [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span><span class="sxs-lookup"><span data-stu-id="2afd8-129">To learn how to configure a retry policy, refer to [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="2afd8-130">Возможность настройки альтернативных конечных точек с помощью параметра errorAction</span><span class="sxs-lookup"><span data-stu-id="2afd8-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="2afd8-131">Если конечная точка назначения для задания планировщика Azure остается недостижимой, после применения политики повтора планировщик Azure возвращается к альтернативной конечной точке для обработки ошибок.</span><span class="sxs-lookup"><span data-stu-id="2afd8-131">If the target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back to the alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="2afd8-132">Если для обработки ошибок настроена альтернативная конечная точка, она вызывается из планировщика Azure.</span><span class="sxs-lookup"><span data-stu-id="2afd8-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="2afd8-133">Альтернативная конечная точка обеспечивает высокий уровень доступности пользовательских заданий в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="2afd8-133">With an alternate endpoint, your own jobs are highly available in the face of failure.</span></span>

<span data-ttu-id="2afd8-134">Например, на приведенной ниже схеме планировщик Azure, следуя своей политике повтора, вызывает веб-службу в Нью-Йорке.</span><span class="sxs-lookup"><span data-stu-id="2afd8-134">As an example, in the diagram below, Azure Scheduler follows its retry policy to hit a New York web service.</span></span> <span data-ttu-id="2afd8-135">Когда повторная попытка не приносит успеха, он проверяет наличие альтернативной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="2afd8-135">After the retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="2afd8-136">После этого планировщик начинает запрашивать альтернативную конечную точку, следуя той же политике возврата.</span><span class="sxs-lookup"><span data-stu-id="2afd8-136">It then goes ahead and starts making requests to the alternate with the same retry policy.</span></span>

![][2]

<span data-ttu-id="2afd8-137">Обратите внимание на то, что и исходное, и альтернативное действие выполняются в соответствии с одной и той же политикой повтора.</span><span class="sxs-lookup"><span data-stu-id="2afd8-137">Note that the same retry policy applies to both the original action and the alternate error action.</span></span> <span data-ttu-id="2afd8-138">Также можно сделать так, чтобы тип альтернативного действия отличался от типа основного действия.</span><span class="sxs-lookup"><span data-stu-id="2afd8-138">It’s also possible to have the alternate error action’s action type be different from the main action’s action type.</span></span> <span data-ttu-id="2afd8-139">Например, если основное действие заключается в вызове конечной точки HTTP, то альтернативным может стать действие очереди хранилища, очереди служебной шины или раздела служебной шины, связанное с регистрацией ошибки.</span><span class="sxs-lookup"><span data-stu-id="2afd8-139">For example, while the main action may be invoking an HTTP endpoint, the error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="2afd8-140">Инструкции по настройке альтернативной конечной точки см. в разделе [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span><span class="sxs-lookup"><span data-stu-id="2afd8-140">To learn how to configure an alternate endpoint, refer to [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="2afd8-141">См. также</span><span class="sxs-lookup"><span data-stu-id="2afd8-141">See Also</span></span>
 [<span data-ttu-id="2afd8-142">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="2afd8-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="2afd8-143">Основные понятия, терминология и иерархия сущностей планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="2afd8-144">Приступая к работе с планировщиком Azure на портале Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-144">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="2afd8-145">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="2afd8-146">Как создавать сложные расписания и расширенное повторение с помощью планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-146">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="2afd8-147">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="2afd8-148">Справочник по командлетам PowerShell планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="2afd8-149">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="2afd8-150">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="2afd8-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
