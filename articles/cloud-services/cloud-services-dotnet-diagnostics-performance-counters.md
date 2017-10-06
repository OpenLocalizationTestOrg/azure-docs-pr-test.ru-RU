---
title: "Счетчики производительности в Azure Diagnostics aaaUse | Документы Microsoft"
description: "Использование счетчиков производительности в облачных служб Azure или узкие места toofind виртуальных машин и настройки производительности."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="db779-103">Создание и использование счетчиков производительности в приложении Azure</span><span class="sxs-lookup"><span data-stu-id="db779-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="db779-104">В этой статье описываются преимущества hello и как счетчики производительности tooput в приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="db779-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="db779-105">Можно использовать их данные toocollect, обнаруживать узкие места и настройки производительности системы и приложений.</span><span class="sxs-lookup"><span data-stu-id="db779-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="db779-106">Счетчики производительности, доступные для Windows Server, IIS и ASP.NET можно также собирать и использовать toodetermine работоспособности hello Azure веб-ролей, рабочих ролей и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="db779-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="db779-107">Вы также можете создавать и использовать настраиваемые счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="db779-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="db779-108">Вы можете проверить данные счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="db779-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="db779-109">Непосредственно на узле приложения hello с hello системный монитор получить доступ с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="db779-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="db779-110">Здравствуйте, пакет управления Azure с помощью System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="db779-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="db779-111">Другие средства мониторинга, которые обращаются к hello tooAzure хранилища переданных диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="db779-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="db779-112">Дополнительные сведения см. в статье [Хранение и просмотр диагностических данных в службе хранилища Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx).</span><span class="sxs-lookup"><span data-stu-id="db779-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="db779-113">Дополнительные сведения о наблюдении за производительностью hello приложения hello [портал Azure](http://portal.azure.com/), в разделе [как tooMonitor облачных служб](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="db779-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="db779-114">Дополнительные подробные рекомендации по методам ведения журнала и трассировки, а также использованию диагностики и других проблем tootroubleshoot методы и оптимизации приложений Azure см. в разделе [Устранение неполадок советы и рекомендации по разработке Azure Приложения](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="db779-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="db779-115">Включение мониторинга счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="db779-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="db779-116">Счетчики производительности по умолчанию отключены.</span><span class="sxs-lookup"><span data-stu-id="db779-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="db779-117">Приложение или задача запуска необходимо изменить диагностики по умолчанию hello агента tooinclude hello конкретных счетчиков производительности для конфигурации обратиться в toomonitor для каждого экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="db779-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="db779-118">Счетчики производительности, доступные в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="db779-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="db779-119">Azure предоставляет подмножество hello счетчики производительности, доступные для Windows Server, IIS и стека ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="db779-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="db779-120">Hello следующей таблице перечислены некоторые счетчики производительности hello особый интерес для приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="db779-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="db779-121">Категория счетчика: объект (экземпляр)</span><span class="sxs-lookup"><span data-stu-id="db779-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="db779-122">Имя счетчика</span><span class="sxs-lookup"><span data-stu-id="db779-122">Counter Name</span></span> | <span data-ttu-id="db779-123">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="db779-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db779-124">Исключения .NET CLR (*глобально*)</span><span class="sxs-lookup"><span data-stu-id="db779-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="db779-125">Число исключений/с</span><span class="sxs-lookup"><span data-stu-id="db779-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="db779-126">Счетчики производительности исключений</span><span class="sxs-lookup"><span data-stu-id="db779-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="db779-127">Память .NET CLR (*глобально*)</span><span class="sxs-lookup"><span data-stu-id="db779-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="db779-128">Время на сборку мусора, %</span><span class="sxs-lookup"><span data-stu-id="db779-128">% Time in GC</span></span> |<span data-ttu-id="db779-129">Счетчики производительности памяти</span><span class="sxs-lookup"><span data-stu-id="db779-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="db779-130">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="db779-130">ASP.NET</span></span> |<span data-ttu-id="db779-131">Перезапуски приложения</span><span class="sxs-lookup"><span data-stu-id="db779-131">Application Restarts</span></span> |<span data-ttu-id="db779-132">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-133">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="db779-133">ASP.NET</span></span> |<span data-ttu-id="db779-134">Время выполнения запроса</span><span class="sxs-lookup"><span data-stu-id="db779-134">Request Execution Time</span></span> |<span data-ttu-id="db779-135">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-136">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="db779-136">ASP.NET</span></span> |<span data-ttu-id="db779-137">Прерванные запросы</span><span class="sxs-lookup"><span data-stu-id="db779-137">Requests Disconnected</span></span> |<span data-ttu-id="db779-138">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-139">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="db779-139">ASP.NET</span></span> |<span data-ttu-id="db779-140">Перезапуски рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="db779-140">Worker Process Restarts</span></span> |<span data-ttu-id="db779-141">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-142">Приложения ASP.NET (**всего**)</span><span class="sxs-lookup"><span data-stu-id="db779-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="db779-143">Общее число запросов</span><span class="sxs-lookup"><span data-stu-id="db779-143">Requests Total</span></span> |<span data-ttu-id="db779-144">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-145">Приложения ASP.NET (**всего**)</span><span class="sxs-lookup"><span data-stu-id="db779-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="db779-146">Число запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="db779-146">Requests/Sec</span></span> |<span data-ttu-id="db779-147">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="db779-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="db779-149">Время выполнения запроса</span><span class="sxs-lookup"><span data-stu-id="db779-149">Request Execution Time</span></span> |<span data-ttu-id="db779-150">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="db779-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="db779-152">Время ожидания запроса</span><span class="sxs-lookup"><span data-stu-id="db779-152">Request Wait Time</span></span> |<span data-ttu-id="db779-153">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="db779-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="db779-155">Текущие запросы</span><span class="sxs-lookup"><span data-stu-id="db779-155">Requests Current</span></span> |<span data-ttu-id="db779-156">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="db779-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="db779-158">Запросы в очереди</span><span class="sxs-lookup"><span data-stu-id="db779-158">Requests Queued</span></span> |<span data-ttu-id="db779-159">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="db779-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="db779-161">Отклоненные запросы</span><span class="sxs-lookup"><span data-stu-id="db779-161">Requests Rejected</span></span> |<span data-ttu-id="db779-162">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-163">Память</span><span class="sxs-lookup"><span data-stu-id="db779-163">Memory</span></span> |<span data-ttu-id="db779-164">Доступный объем в МБ</span><span class="sxs-lookup"><span data-stu-id="db779-164">Available MBytes</span></span> |<span data-ttu-id="db779-165">Счетчики производительности памяти</span><span class="sxs-lookup"><span data-stu-id="db779-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="db779-166">Память</span><span class="sxs-lookup"><span data-stu-id="db779-166">Memory</span></span> |<span data-ttu-id="db779-167">Число байтов выделенной памяти</span><span class="sxs-lookup"><span data-stu-id="db779-167">Committed Bytes</span></span> |<span data-ttu-id="db779-168">Счетчики производительности памяти</span><span class="sxs-lookup"><span data-stu-id="db779-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="db779-169">Процессор(_всего)</span><span class="sxs-lookup"><span data-stu-id="db779-169">Processor(_Total)</span></span> |<span data-ttu-id="db779-170">% загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="db779-170">% Processor Time</span></span> |<span data-ttu-id="db779-171">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="db779-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="db779-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="db779-172">TCPv4</span></span> |<span data-ttu-id="db779-173">Ошибки подключения</span><span class="sxs-lookup"><span data-stu-id="db779-173">Connection Failures</span></span> |<span data-ttu-id="db779-174">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="db779-174">TCP Object</span></span> |
| <span data-ttu-id="db779-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="db779-175">TCPv4</span></span> |<span data-ttu-id="db779-176">Установлено подключений</span><span class="sxs-lookup"><span data-stu-id="db779-176">Connections Established</span></span> |<span data-ttu-id="db779-177">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="db779-177">TCP Object</span></span> |
| <span data-ttu-id="db779-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="db779-178">TCPv4</span></span> |<span data-ttu-id="db779-179">Сбросов подключений</span><span class="sxs-lookup"><span data-stu-id="db779-179">Connections Reset</span></span> |<span data-ttu-id="db779-180">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="db779-180">TCP Object</span></span> |
| <span data-ttu-id="db779-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="db779-181">TCPv4</span></span> |<span data-ttu-id="db779-182">Отправлено сегментов/с</span><span class="sxs-lookup"><span data-stu-id="db779-182">Segments Sent/sec</span></span> |<span data-ttu-id="db779-183">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="db779-183">TCP Object</span></span> |
| <span data-ttu-id="db779-184">Сетевой интерфейс (*)</span><span class="sxs-lookup"><span data-stu-id="db779-184">Network Interface(*)</span></span> |<span data-ttu-id="db779-185">Полученных байтов/с</span><span class="sxs-lookup"><span data-stu-id="db779-185">Bytes Received/sec</span></span> |<span data-ttu-id="db779-186">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="db779-186">Network Interface Object</span></span> |
| <span data-ttu-id="db779-187">Сетевой интерфейс (*)</span><span class="sxs-lookup"><span data-stu-id="db779-187">Network Interface(*)</span></span> |<span data-ttu-id="db779-188">Отправленных байтов/с</span><span class="sxs-lookup"><span data-stu-id="db779-188">Bytes Sent/sec</span></span> |<span data-ttu-id="db779-189">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="db779-189">Network Interface Object</span></span> |
| <span data-ttu-id="db779-190">Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="db779-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="db779-191">Полученных байтов/с</span><span class="sxs-lookup"><span data-stu-id="db779-191">Bytes Received/sec</span></span> |<span data-ttu-id="db779-192">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="db779-192">Network Interface Object</span></span> |
| <span data-ttu-id="db779-193">Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="db779-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="db779-194">Отправленных байтов/с</span><span class="sxs-lookup"><span data-stu-id="db779-194">Bytes Sent/sec</span></span> |<span data-ttu-id="db779-195">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="db779-195">Network Interface Object</span></span> |
| <span data-ttu-id="db779-196">Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="db779-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="db779-197">Всего байтов/с</span><span class="sxs-lookup"><span data-stu-id="db779-197">Bytes Total/sec</span></span> |<span data-ttu-id="db779-198">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="db779-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="db779-199">Создание и добавление приложения tooyour счетчики производительности</span><span class="sxs-lookup"><span data-stu-id="db779-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="db779-200">Azure имеет toocreate поддержки и изменять пользовательские счетчики производительности для веб-ролей и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="db779-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="db779-201">счетчики Hello возможно, используется монитор и tootrack поведения приложения.</span><span class="sxs-lookup"><span data-stu-id="db779-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="db779-202">Вы можете создавать пользовательские категории и описатели счетчиков производительности для задачи при запуске, веб-роли или рабочей роли с повышенными разрешениями, а также удалять их.</span><span class="sxs-lookup"><span data-stu-id="db779-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="db779-203">Код, который вносит изменения toocustom счетчики производительности должны быть повышенные разрешения toorun.</span><span class="sxs-lookup"><span data-stu-id="db779-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="db779-204">Если код hello в веб-роли или рабочей роли, hello роль должна содержать тег hello <Runtime executionContext="elevated" /> в hello ServiceDefinition.csdef-файла для роли tooinitialize hello должным образом.</span><span class="sxs-lookup"><span data-stu-id="db779-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="db779-205">Можно отправлять с помощью агента диагностики hello tooAzure хранения производительности счетчиков данных.</span><span class="sxs-lookup"><span data-stu-id="db779-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="db779-206">Hello стандартные данные счетчиков производительности формируется hello, обрабатываемых в Azure.</span><span class="sxs-lookup"><span data-stu-id="db779-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="db779-207">Данные пользовательских счетчиков производительности должны создаваться приложением веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="db779-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="db779-208">В разделе [типы счетчиков производительности](https://msdn.microsoft.com/library/z573042h.aspx) сведения о типах hello данных, которые могут храниться в пользовательские счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="db779-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="db779-209">Пример создания и установки данных пользовательских счетчиков производительности в веб-роли см. в статье [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) (Пример PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="db779-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="db779-210">Сохранение и просмотр данных счетчика производительности</span><span class="sxs-lookup"><span data-stu-id="db779-210">Store and view performance counter data</span></span>
<span data-ttu-id="db779-211">Azure кэширует данные счетчиков производительности вместе с другими диагностическими сведениями.</span><span class="sxs-lookup"><span data-stu-id="db779-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="db779-212">Эти данные доступны для удаленного мониторинга, пока экземпляр роли hello выполняется с помощью удаленного рабочего стола доступа tooview средства, такие как системный монитор.</span><span class="sxs-lookup"><span data-stu-id="db779-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="db779-213">toopersist hello данных за пределами экземпляра роли hello, hello диагностики агента необходимо перенести hello данных tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="db779-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="db779-214">Ограничение размера Hello hello кэшированных данных счетчиков производительности можно настроить в агент диагностики hello, или может быть настроен toobe часть общего ограничения для всех hello диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="db779-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="db779-215">Дополнительные сведения о размере буфера hello см. в разделе [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) и [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="db779-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="db779-216">В разделе [хранения и просмотра диагностических данных в хранилище Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) Общие сведения о настройке hello агента tootransfer данных tooa учетная запись хранения диагностики.</span><span class="sxs-lookup"><span data-stu-id="db779-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="db779-217">Каждый настроенный экземпляр счетчика производительности записывается с указанной частотой выборки и передаче данных выборки hello toohello учетной записи хранения плановым запросом передачи или запрос передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="db779-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="db779-218">Автоматическую передачу можно запланировать с периодичностью раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="db779-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="db779-219">Данные счетчиков производительности, передаваемых агентом диагностики hello хранится в таблице WADPerformanceCountersTable, в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="db779-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="db779-220">К этой таблице можно обращаться с помощью запросов в рамках стандартных методов API хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="db779-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="db779-221">В разделе [пример PerformanceCounters Microsoft Azure](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) пример запроса и отображения данных счетчиков производительности из таблицы WADPerformanceCountersTable hello.</span><span class="sxs-lookup"><span data-stu-id="db779-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="db779-222">В зависимости от частоты передачи агент диагностики hello и задержки очереди hello самые последние данные счетчиков производительности в учетной записи хранилища hello может быть устаревшим в несколько минут.</span><span class="sxs-lookup"><span data-stu-id="db779-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="db779-223">Включение счетчиков производительности с помощью файла конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="db779-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="db779-224">Используйте следующие счетчики производительности tooenable процедуры в приложении Azure hello.</span><span class="sxs-lookup"><span data-stu-id="db779-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db779-225">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="db779-225">Prerequisites</span></span>
<span data-ttu-id="db779-226">В этом разделе предполагается, что были импортированы hello монитор диагностики в приложении и были добавлены hello диагностики конфигурации файла tooyour решения Visual Studio (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и более поздних версий).</span><span class="sxs-lookup"><span data-stu-id="db779-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="db779-227">Дополнительные сведения отображены в шагах 1 и 2 статьи [Включение диагностики в облачных службах и виртуальных машинах Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="db779-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="db779-228">Шаг 1. Сбор и хранение данных счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="db779-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="db779-229">После добавления диагностики hello файл решения Visual Studio tooyour можно настроить hello сбор и хранение данных счетчиков производительности в приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="db779-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="db779-230">Это делается путем добавления файла диагностики toohello счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="db779-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="db779-231">Данные диагностики, включая счетчики производительности, сначала собираются в экземпляре hello.</span><span class="sxs-lookup"><span data-stu-id="db779-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="db779-232">Hello данные затем сохраненного toohello WADPerformanceCountersTable таблицу hello службы таблицы Azure, так вы также должны toospecify hello учетной записи хранения в приложении.</span><span class="sxs-lookup"><span data-stu-id="db779-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="db779-233">При тестировании приложения локально в эмуляторе вычислений hello, можно также хранить данные диагностики локально в hello эмулятор хранилища.</span><span class="sxs-lookup"><span data-stu-id="db779-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="db779-234">Перед сохранением диагностических данных, необходимо сначала перейти toohello [портал Azure](http://portal.azure.com/) и создать учетную запись классической хранилища.</span><span class="sxs-lookup"><span data-stu-id="db779-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="db779-235">Рекомендуется toolocate вашей учетной записи хранения в hello географическому расположению, как приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="db779-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="db779-236">С сохранением hello Azure приложений и учетную запись хранения находятся в Здравствуйте географическому расположению, предотвратить дополнительные затраты на внешнюю полосу пропускания и уменьшить задержку.</span><span class="sxs-lookup"><span data-stu-id="db779-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="db779-237">Добавьте файл диагностики toohello счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="db779-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="db779-238">Вы можете использовать самые разные счетчики.</span><span class="sxs-lookup"><span data-stu-id="db779-238">There are many counters you can use.</span></span> <span data-ttu-id="db779-239">Hello следующем примере показано несколько счетчиков производительности, которые рекомендуются для веб- и мониторинг рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="db779-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="db779-240">Откройте файл диагностики hello (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и более поздних версий) и добавьте следующий элемент DiagnosticMonitorConfiguration toohello hello:</span><span class="sxs-lookup"><span data-stu-id="db779-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="db779-241">атрибут bufferQuotaInMB Hello, который указывает hello максимальный объем хранилища файловой системы, которая доступна для hello типа собираемых данных (журналы Azure, журналы IIS, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="db779-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="db779-242">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="db779-242">hello default is 0.</span></span> <span data-ttu-id="db779-243">При достижении квоты hello старые данные hello удаляется по мере добавления новых данных.</span><span class="sxs-lookup"><span data-stu-id="db779-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="db779-244">Hello сумма всех свойств bufferQuotaInMB hello должна быть больше, чем значение hello атрибута OverallQuotaInMB hello.</span><span class="sxs-lookup"><span data-stu-id="db779-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="db779-245">Более подробное рассмотрение определения того, какой объем хранилища потребуется для hello сбор диагностических данных см. в разделе hello разделе настройки WAD [Устранение неполадок советы и рекомендации по разработке приложений Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="db779-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="db779-246">Hello scheduledTransferPeriod атрибут, который указывает hello интервал между запланированными передачами данных, округляется в сторону увеличения toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="db779-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="db779-247">В следующих примерах hello задается tooPT30M (30 минут).</span><span class="sxs-lookup"><span data-stu-id="db779-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="db779-248">Параметр hello передачи периода tooa малое значение, например 1 минуту, будет отрицательно влиять на производительность приложения в рабочей среде, но может быть полезным для просмотра диагностики быстрой работы при тестировании.</span><span class="sxs-lookup"><span data-stu-id="db779-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="db779-249">Hello запланированный период передачи должен быть достаточно мал tooensure, что диагностических данных не будет перезаписан в экземпляре hello, но достаточно велик, что он не повлияет на производительность приложения hello.</span><span class="sxs-lookup"><span data-stu-id="db779-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="db779-250">атрибут counterSpecifier Hello указывает toocollect счетчика производительности hello.</span><span class="sxs-lookup"><span data-stu-id="db779-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="db779-251">атрибут SampleRate содержит Hello указывает hello скорость, с которой счетчик производительности hello должны считываться, в данном случае 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="db779-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="db779-252">После добавления счетчиков производительности для hello, которые должны toocollect, сохраните изменения toohello диагностики.</span><span class="sxs-lookup"><span data-stu-id="db779-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="db779-253">Далее необходимо использовать учетную запись хранения toospecify hello, будут сохраняться данные диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="db779-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="db779-254">Укажите учетную запись хранения hello</span><span class="sxs-lookup"><span data-stu-id="db779-254">Specify hello storage account</span></span>
<span data-ttu-id="db779-255">toopersist вашей tooyour сведения диагностики хранилища Azure учетной записи, необходимо указать строку подключения в файле конфигурации (ServiceConfiguration.cscfg) службы.</span><span class="sxs-lookup"><span data-stu-id="db779-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="db779-256">Для Azure SDK 2.5 hello учетной записи хранилища можно задать в файле diagnostics.wadcfgx hello.</span><span class="sxs-lookup"><span data-stu-id="db779-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="db779-257">Эти инструкции применяются только tooAzure SDK 2.4 и ниже.</span><span class="sxs-lookup"><span data-stu-id="db779-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="db779-258">Для Azure SDK 2.5 hello учетной записи хранилища можно задать в файле diagnostics.wadcfgx hello.</span><span class="sxs-lookup"><span data-stu-id="db779-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="db779-259">строки подключения hello tooset:</span><span class="sxs-lookup"><span data-stu-id="db779-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="db779-260">Откройте файл ServiceConfiguration.Cloud.cscfg hello, с помощью любого текстового редактора и строка подключения hello набор для хранилища.</span><span class="sxs-lookup"><span data-stu-id="db779-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="db779-261">Hello *AccountName* и *AccountKey* значения находятся в hello портал Azure в мониторинга учетной записи хранения hello в списке ключей доступа.</span><span class="sxs-lookup"><span data-stu-id="db779-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="db779-262">Сохраните файл ServiceConfiguration.Cloud.cscfg hello.</span><span class="sxs-lookup"><span data-stu-id="db779-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="db779-263">Откройте файл ServiceConfiguration.Local.cscfg hello и убедитесь, что UseDevelopmentStorage tootrue.</span><span class="sxs-lookup"><span data-stu-id="db779-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="db779-264">Теперь, когда hello строки подключения заданы, приложение будет сохранять учетная запись хранения tooyour данных диагностики при развертывании приложения.</span><span class="sxs-lookup"><span data-stu-id="db779-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="db779-265">Сохраните и соберите свой проект, затем разверните приложение.</span><span class="sxs-lookup"><span data-stu-id="db779-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="db779-266">Шаг 2. (Необязательно) Создание пользовательских счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="db779-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="db779-267">В дополнение к этому toohello предварительно определенные счетчики производительности, можно добавить собственные пользовательские счетчики производительности toomonitor рабочих и веб-ролей.</span><span class="sxs-lookup"><span data-stu-id="db779-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="db779-268">Пользовательские счетчики производительности могут быть используется монитор и tootrack поведения приложения и может быть создано или удалены в задаче запуска, веб-роли или рабочей роли с повышенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="db779-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="db779-269">агент диагностики Azure Hello обновляет hello конфигурации счетчиков производительности из файла .wadcfg hello одну минуту, после запуска.</span><span class="sxs-lookup"><span data-stu-id="db779-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="db779-270">Если создать пользовательские счетчики производительности в метод OnStart hello и задачи запуска выполняются дольше, чем tooexecute одну минуту, пользователем счетчиков производительности будет не были созданы при агент Azure Diagnostics hello tooload их.</span><span class="sxs-lookup"><span data-stu-id="db779-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="db779-271">В этом случае система диагностики Azure будет надлежащим образом собирать все данные диагностики — за исключением данных пользовательских счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="db779-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="db779-272">tooresolve эту проблему, создайте hello счетчиков производительности в задачу запуска и перемещение метод OnStart toohello некоторые задачи запуска работать после создания hello счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="db779-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="db779-273">Выполните следующие шаги toocreate простой пользовательский счетчик производительности с именем «\MyCustomCounterCategory\MyButton1Counter» hello.</span><span class="sxs-lookup"><span data-stu-id="db779-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="db779-274">Откройте файл определения hello службы (CSDEF) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="db779-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="db779-275">Добавьте hello элемент toohello WebRole или WorkerRole элемент tooallow выполнения среды с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="db779-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="db779-276">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="db779-276">Save hello file.</span></span>
4. <span data-ttu-id="db779-277">Откройте файл диагностики hello (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и более поздних версий) и добавьте следующие toohello DiagnosticMonitorConfiguration hello</span><span class="sxs-lookup"><span data-stu-id="db779-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="db779-278">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="db779-278">Save hello file.</span></span>
6. <span data-ttu-id="db779-279">Создайте hello пользовательскую категорию счетчиков производительности в метод OnStart hello своей роли перед вызовом базы. Метод OnStart.</span><span class="sxs-lookup"><span data-stu-id="db779-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="db779-280">Hello следующий пример на C# создается пользовательская категория, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="db779-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="db779-281">Обновите счетчики hello внутри приложения.</span><span class="sxs-lookup"><span data-stu-id="db779-281">Update hello counters within your application.</span></span> <span data-ttu-id="db779-282">Следующий пример Hello обновляет пользовательский счетчик производительности для событий Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="db779-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="db779-283">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="db779-283">Save hello file.</span></span>  

<span data-ttu-id="db779-284">Теперь данных пользовательских счетчиков производительности собираются монитором диагностики Azure hello.</span><span class="sxs-lookup"><span data-stu-id="db779-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="db779-285">Шаг 3. Запрос данных счетчика производительности</span><span class="sxs-lookup"><span data-stu-id="db779-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="db779-286">После развертывания приложения и запущена, монитор диагностики hello начнет сбор данных счетчиков производительности и сохранение этой tooAzure хранения данных.</span><span class="sxs-lookup"><span data-stu-id="db779-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="db779-287">Используйте средства, такие как обозреватель серверов в Visual Studio [обозреватель хранилищ Azure](http://azurestorageexplorer.codeplex.com/), или [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) компании Cerebrata tooview hello данных счетчиков производительности в hello Таблица WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="db779-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="db779-288">Можно также программно использовать в запросах hello таблицы службы [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), или [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="db779-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="db779-289">Hello следующий пример на C# показан базовый запрос к таблице WADPerformanceCountersTable hello и сохраняет hello диагностики данных tooa CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="db779-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="db779-290">После hello счетчики производительности сохранены tooa CSV-файл, можно использовать hello построения диаграмм возможностей в Microsoft Excel или другие средства toovisualize hello данными.</span><span class="sxs-lookup"><span data-stu-id="db779-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="db779-291">Быть убедиться, что tooadd tooMicrosoft.WindowsAzure.Storage.dll ссылки, который входит в hello Azure SDK для .NET от октября 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="db779-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="db779-292">сборка Hello — установленных toohello % Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ каталог.</span><span class="sxs-lookup"><span data-stu-id="db779-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="db779-293">Сущности сопоставляют tooC # объектов с помощью пользовательского класса, производного от **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="db779-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="db779-294">Hello следующий код определяет класс сущностей, который представляет собой счетчик производительности в hello **WADPerformanceCountersTable** таблицы.</span><span class="sxs-lookup"><span data-stu-id="db779-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="db779-295">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db779-295">Next Steps</span></span>
[<span data-ttu-id="db779-296">Просмотрите дополнительные статьи о системе диагностику Azure</span><span class="sxs-lookup"><span data-stu-id="db779-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
