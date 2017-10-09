---
title: "aaaWhat — планировщика Azure? | Документация Майкрософт"
description: "Планировщик Azure позволяет вам toodeclaratively описывают toorun действия в облаке hello. Затем он планирует и выполняет эти действия автоматически."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="4ee7b-105">Что такое планировщик Azure?</span><span class="sxs-lookup"><span data-stu-id="4ee7b-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="4ee7b-106">Планировщик Azure позволяет вам toodeclaratively описывают toorun действия в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="4ee7b-107">Затем он планирует и выполняет эти действия автоматически.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="4ee7b-108">Планировщик делает это с помощью [hello портал Azure](scheduler-get-started-portal.md), код, [API-интерфейса REST](https://msdn.microsoft.com/library/mt629143.aspx), или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="4ee7b-109">Планировщик создает, обслуживает и вызывает запланированную работу.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="4ee7b-110">Планировщик не размещает какую-либо рабочую нагрузку и не выполняет код.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="4ee7b-111">Он только *вызывает* код, размещенный в другом месте — в Azure, на локальном компьютере или у другого поставщика.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="4ee7b-112">Он выполняет вызов с помощью HTTP, HTTPS, очереди хранилища, очереди сервисной шины или раздела сервисной шины.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="4ee7b-113">Планировщик расписания [заданий](scheduler-concepts-terms.md), ведет журнал результаты выполнения задания один можно просмотреть, что детерминированного и надежно запуска расписания toobe рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="4ee7b-114">Веб-задания Azure (часть компонента hello веб-приложений в службе приложений Azure) и других возможностей планирования Azure с помощью планировщика в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="4ee7b-115">Hello [REST API планировщика](https://msdn.microsoft.com/library/mt629143.aspx) помогает управлять hello связи для этих действий.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="4ee7b-116">Таким образом, планировщик поддерживает [сложные расписания и расширенное повторение](scheduler-advanced-complexity.md) .</span><span class="sxs-lookup"><span data-stu-id="4ee7b-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="4ee7b-117">Существует несколько вариантов использования планировщика toohello.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="4ee7b-118">Например:</span><span class="sxs-lookup"><span data-stu-id="4ee7b-118">For example:</span></span>

* <span data-ttu-id="4ee7b-119">*Повторение действий приложения.* Периодический сбор данных из Twitter и их передача в веб-канал.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="4ee7b-120">*Ежедневное обслуживание.* Ежедневное удаление журналов, создание резервных копий и другие задачи обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="4ee7b-121">Например администратор может выбрать tooback hello базы данных в 1:00.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="4ee7b-122">Каждый день в течение hello следующие девять месяцев.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-122">every day for hello next nine months.</span></span>

<span data-ttu-id="4ee7b-123">Планировщика позволяет toocreate, обновлять, удалять, просматривать и управлять заданий и [коллекции заданий](scheduler-concepts-terms.md) программно, с помощью скриптов и на портале hello.</span><span class="sxs-lookup"><span data-stu-id="4ee7b-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="4ee7b-124">См. также</span><span class="sxs-lookup"><span data-stu-id="4ee7b-124">See also</span></span>
 [<span data-ttu-id="4ee7b-125">Основные понятия, терминология и иерархия сущностей планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="4ee7b-126">Начало работы с планировщиком в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="4ee7b-127">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="4ee7b-128">Как планирует комплексного toobuild и дополнительно повторения с планировщиком Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="4ee7b-129">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="4ee7b-130">Справочник по командлетам PowerShell планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="4ee7b-131">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="4ee7b-132">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="4ee7b-133">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="4ee7b-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

