---
title: "Использование счетчиков производительности в системе диагностики Azure | Документация Майкрософт"
description: "Использование счетчиков производительности в облачных службах Azure или на виртуальной машине для обнаружения и решения проблем с производительностью."
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
ms.openlocfilehash: 2cf765cb034725199127c547a9b8b997a4a6089c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="d3d26-103">Создание и использование счетчиков производительности в приложении Azure</span><span class="sxs-lookup"><span data-stu-id="d3d26-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="d3d26-104">В этой статье рассматриваются преимущества счетчиков производительности, а также описан способ их добавления в приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="d3d26-105">Счетчики можно использовать для сбора данных, а также обнаружения и устранения проблем с производительностью системы и приложений.</span><span class="sxs-lookup"><span data-stu-id="d3d26-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="d3d26-106">Кроме этого, данные счетчиков производительности для Windows Server, IIS и ASP.NET можно собирать и использовать для определения работоспособности веб-ролей, рабочих ролей Azure и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d3d26-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="d3d26-107">Вы также можете создавать и использовать настраиваемые счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="d3d26-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="d3d26-108">Вы можете проверить данные счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="d3d26-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="d3d26-109">Непосредственно на узле приложения с помощью системного монитора через удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="d3d26-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="d3d26-110">Используя службу System Center Operations Manager с помощью пакета управления Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="d3d26-111">С помощью других средств мониторинга, которые получают доступ к диагностическим данным, передаваемым в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="d3d26-112">Дополнительные сведения см. в статье [Хранение и просмотр диагностических данных в службе хранилища Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3d26-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="d3d26-113">Дополнительные сведения о мониторинге производительности приложения на [портале Azure](http://portal.azure.com/) см. в статье [Мониторинг облачных служб](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="d3d26-113">For more information on monitoring the performance of your application in the [Azure portal](http://portal.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="d3d26-114">Дополнительные сведения о создании стратегии ведения журналов и трассировки, а также об использовании средств диагностики и других методик для устранения неполадок и оптимизации приложений Azure см. на странице [с рекомендациями по разработке приложений Azure](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3d26-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="d3d26-115">Включение мониторинга счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="d3d26-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="d3d26-116">Счетчики производительности по умолчанию отключены.</span><span class="sxs-lookup"><span data-stu-id="d3d26-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="d3d26-117">Приложение или задача при запуске должны изменить конфигурацию агента диагностики по умолчанию, чтобы включить определенные счетчики производительности, которые необходимо отслеживать для каждого экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="d3d26-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="d3d26-118">Счетчики производительности, доступные в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d3d26-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="d3d26-119">Azure предлагает набор счетчиков производительности для Windows Server, IIS и стека ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d3d26-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="d3d26-120">В следующей таблице перечислены некоторые счетчики производительности для приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="d3d26-121">Категория счетчика: объект (экземпляр)</span><span class="sxs-lookup"><span data-stu-id="d3d26-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="d3d26-122">Имя счетчика</span><span class="sxs-lookup"><span data-stu-id="d3d26-122">Counter Name</span></span> | <span data-ttu-id="d3d26-123">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="d3d26-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d3d26-124">Исключения .NET CLR (*глобально*)</span><span class="sxs-lookup"><span data-stu-id="d3d26-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="d3d26-125">Число исключений/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="d3d26-126">Счетчики производительности исключений</span><span class="sxs-lookup"><span data-stu-id="d3d26-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="d3d26-127">Память .NET CLR (*глобально*)</span><span class="sxs-lookup"><span data-stu-id="d3d26-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="d3d26-128">Время на сборку мусора, %</span><span class="sxs-lookup"><span data-stu-id="d3d26-128">% Time in GC</span></span> |<span data-ttu-id="d3d26-129">Счетчики производительности памяти</span><span class="sxs-lookup"><span data-stu-id="d3d26-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="d3d26-130">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d3d26-130">ASP.NET</span></span> |<span data-ttu-id="d3d26-131">Перезапуски приложения</span><span class="sxs-lookup"><span data-stu-id="d3d26-131">Application Restarts</span></span> |<span data-ttu-id="d3d26-132">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-133">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d3d26-133">ASP.NET</span></span> |<span data-ttu-id="d3d26-134">Время выполнения запроса</span><span class="sxs-lookup"><span data-stu-id="d3d26-134">Request Execution Time</span></span> |<span data-ttu-id="d3d26-135">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-136">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d3d26-136">ASP.NET</span></span> |<span data-ttu-id="d3d26-137">Прерванные запросы</span><span class="sxs-lookup"><span data-stu-id="d3d26-137">Requests Disconnected</span></span> |<span data-ttu-id="d3d26-138">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-139">ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d3d26-139">ASP.NET</span></span> |<span data-ttu-id="d3d26-140">Перезапуски рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="d3d26-140">Worker Process Restarts</span></span> |<span data-ttu-id="d3d26-141">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-142">Приложения ASP.NET (**всего**)</span><span class="sxs-lookup"><span data-stu-id="d3d26-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="d3d26-143">Общее число запросов</span><span class="sxs-lookup"><span data-stu-id="d3d26-143">Requests Total</span></span> |<span data-ttu-id="d3d26-144">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-145">Приложения ASP.NET (**всего**)</span><span class="sxs-lookup"><span data-stu-id="d3d26-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="d3d26-146">Число запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="d3d26-146">Requests/Sec</span></span> |<span data-ttu-id="d3d26-147">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="d3d26-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="d3d26-149">Время выполнения запроса</span><span class="sxs-lookup"><span data-stu-id="d3d26-149">Request Execution Time</span></span> |<span data-ttu-id="d3d26-150">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="d3d26-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="d3d26-152">Время ожидания запроса</span><span class="sxs-lookup"><span data-stu-id="d3d26-152">Request Wait Time</span></span> |<span data-ttu-id="d3d26-153">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="d3d26-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="d3d26-155">Текущие запросы</span><span class="sxs-lookup"><span data-stu-id="d3d26-155">Requests Current</span></span> |<span data-ttu-id="d3d26-156">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="d3d26-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="d3d26-158">Запросы в очереди</span><span class="sxs-lookup"><span data-stu-id="d3d26-158">Requests Queued</span></span> |<span data-ttu-id="d3d26-159">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="d3d26-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="d3d26-161">Отклоненные запросы</span><span class="sxs-lookup"><span data-stu-id="d3d26-161">Requests Rejected</span></span> |<span data-ttu-id="d3d26-162">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-163">Память</span><span class="sxs-lookup"><span data-stu-id="d3d26-163">Memory</span></span> |<span data-ttu-id="d3d26-164">Доступный объем в МБ</span><span class="sxs-lookup"><span data-stu-id="d3d26-164">Available MBytes</span></span> |<span data-ttu-id="d3d26-165">Счетчики производительности памяти</span><span class="sxs-lookup"><span data-stu-id="d3d26-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="d3d26-166">Память</span><span class="sxs-lookup"><span data-stu-id="d3d26-166">Memory</span></span> |<span data-ttu-id="d3d26-167">Число байтов выделенной памяти</span><span class="sxs-lookup"><span data-stu-id="d3d26-167">Committed Bytes</span></span> |<span data-ttu-id="d3d26-168">Счетчики производительности памяти</span><span class="sxs-lookup"><span data-stu-id="d3d26-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="d3d26-169">Процессор(_всего)</span><span class="sxs-lookup"><span data-stu-id="d3d26-169">Processor(_Total)</span></span> |<span data-ttu-id="d3d26-170">% загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="d3d26-170">% Processor Time</span></span> |<span data-ttu-id="d3d26-171">Счетчики производительности для ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d3d26-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="d3d26-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="d3d26-172">TCPv4</span></span> |<span data-ttu-id="d3d26-173">Ошибки подключения</span><span class="sxs-lookup"><span data-stu-id="d3d26-173">Connection Failures</span></span> |<span data-ttu-id="d3d26-174">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="d3d26-174">TCP Object</span></span> |
| <span data-ttu-id="d3d26-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="d3d26-175">TCPv4</span></span> |<span data-ttu-id="d3d26-176">Установлено подключений</span><span class="sxs-lookup"><span data-stu-id="d3d26-176">Connections Established</span></span> |<span data-ttu-id="d3d26-177">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="d3d26-177">TCP Object</span></span> |
| <span data-ttu-id="d3d26-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="d3d26-178">TCPv4</span></span> |<span data-ttu-id="d3d26-179">Сбросов подключений</span><span class="sxs-lookup"><span data-stu-id="d3d26-179">Connections Reset</span></span> |<span data-ttu-id="d3d26-180">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="d3d26-180">TCP Object</span></span> |
| <span data-ttu-id="d3d26-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="d3d26-181">TCPv4</span></span> |<span data-ttu-id="d3d26-182">Отправлено сегментов/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-182">Segments Sent/sec</span></span> |<span data-ttu-id="d3d26-183">Объект TCP</span><span class="sxs-lookup"><span data-stu-id="d3d26-183">TCP Object</span></span> |
| <span data-ttu-id="d3d26-184">Сетевой интерфейс (*)</span><span class="sxs-lookup"><span data-stu-id="d3d26-184">Network Interface(*)</span></span> |<span data-ttu-id="d3d26-185">Полученных байтов/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-185">Bytes Received/sec</span></span> |<span data-ttu-id="d3d26-186">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3d26-186">Network Interface Object</span></span> |
| <span data-ttu-id="d3d26-187">Сетевой интерфейс (*)</span><span class="sxs-lookup"><span data-stu-id="d3d26-187">Network Interface(*)</span></span> |<span data-ttu-id="d3d26-188">Отправленных байтов/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-188">Bytes Sent/sec</span></span> |<span data-ttu-id="d3d26-189">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3d26-189">Network Interface Object</span></span> |
| <span data-ttu-id="d3d26-190">Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="d3d26-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="d3d26-191">Полученных байтов/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-191">Bytes Received/sec</span></span> |<span data-ttu-id="d3d26-192">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3d26-192">Network Interface Object</span></span> |
| <span data-ttu-id="d3d26-193">Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="d3d26-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="d3d26-194">Отправленных байтов/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-194">Bytes Sent/sec</span></span> |<span data-ttu-id="d3d26-195">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3d26-195">Network Interface Object</span></span> |
| <span data-ttu-id="d3d26-196">Сетевой интерфейс (сетевой адаптер шины виртуальной машины Microsoft _2)</span><span class="sxs-lookup"><span data-stu-id="d3d26-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="d3d26-197">Всего байтов/с</span><span class="sxs-lookup"><span data-stu-id="d3d26-197">Bytes Total/sec</span></span> |<span data-ttu-id="d3d26-198">Объект сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3d26-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="d3d26-199">Создание пользовательских счетчиков производительности и добавление их в приложение</span><span class="sxs-lookup"><span data-stu-id="d3d26-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="d3d26-200">В Azure можно создавать и изменять пользовательские счетчики производительности для веб-ролей и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="d3d26-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="d3d26-201">Счетчики могут использоваться для отслеживания определенного поведения приложения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="d3d26-202">Вы можете создавать пользовательские категории и описатели счетчиков производительности для задачи при запуске, веб-роли или рабочей роли с повышенными разрешениями, а также удалять их.</span><span class="sxs-lookup"><span data-stu-id="d3d26-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="d3d26-203">Для выполнения кода, который вносит изменения в пользовательские счетчики производительности, нужны разрешения более высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="d3d26-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="d3d26-204">Если код относится к веб-роли или рабочей роли, для правильной инициализации такая роль должна содержать тег <Runtime executionContext="elevated" /> в файле ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="d3d26-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
>
>

<span data-ttu-id="d3d26-205">Данные пользовательских счетчиков производительности можно отправить в хранилище Azure с помощью агента диагностики.</span><span class="sxs-lookup"><span data-stu-id="d3d26-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="d3d26-206">Стандартные данные счетчиков производительности создаются процессами Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="d3d26-207">Данные пользовательских счетчиков производительности должны создаваться приложением веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="d3d26-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="d3d26-208">Сведения о типах данных, которые могут храниться в пользовательских счетчиках производительности, см. в статье [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) (Типы счетчиков производительности).</span><span class="sxs-lookup"><span data-stu-id="d3d26-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="d3d26-209">Пример создания и установки данных пользовательских счетчиков производительности в веб-роли см. в статье [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) (Пример PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="d3d26-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="d3d26-210">Сохранение и просмотр данных счетчика производительности</span><span class="sxs-lookup"><span data-stu-id="d3d26-210">Store and view performance counter data</span></span>
<span data-ttu-id="d3d26-211">Azure кэширует данные счетчиков производительности вместе с другими диагностическими сведениями.</span><span class="sxs-lookup"><span data-stu-id="d3d26-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="d3d26-212">Эти данные можно отслеживать удаленно во время выполнения экземпляра роли, используя удаленный доступ к рабочему столу для запуска таких средств, как системный монитор.</span><span class="sxs-lookup"><span data-stu-id="d3d26-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="d3d26-213">Чтобы сохранить данные за пределами экземпляра роли, агент диагностики должен передать их в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="d3d26-214">Ограничение размера кэшированных данных счетчиков производительности можно задать в мониторе диагностики. Это ограничение также можно настроить как часть общего ограничения для всех диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="d3d26-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="d3d26-215">Дополнительные сведения о задании размера буфера см. в статьях о свойствах [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) и [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3d26-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="d3d26-216">Общие сведения о настройке агента диагностики для передачи данных в учетную запись хранения см. в статье [Хранение и просмотр диагностических данных в службе хранилища Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3d26-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="d3d26-217">Каждый настроенный экземпляр счетчика производительности записывается с указанной частотой выборки. При этом данные передаются в учетную запись хранения в результате запланированного запроса на передачу или по требованию.</span><span class="sxs-lookup"><span data-stu-id="d3d26-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="d3d26-218">Автоматическую передачу можно запланировать с периодичностью раз в минуту.</span><span class="sxs-lookup"><span data-stu-id="d3d26-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="d3d26-219">Данные счетчиков производительности, переданные агентом диагностики, хранятся в таблице WADPerformanceCountersTable в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="d3d26-220">К этой таблице можно обращаться с помощью запросов в рамках стандартных методов API хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="d3d26-221">Пример запроса и отображения данных счетчиков производительности из таблицы WADPerformanceCountersTable см. в статье [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) (Пример PerformanceCounters Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="d3d26-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="d3d26-222">В зависимости от частоты передачи агента диагностики и задержки очереди самые последние данные счетчиков производительности в учетной записи хранения могут быть устаревшими на несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d3d26-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="d3d26-223">Включение счетчиков производительности с помощью файла конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="d3d26-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="d3d26-224">Чтобы включить счетчики производительности в приложении Azure, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="d3d26-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3d26-225">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3d26-225">Prerequisites</span></span>
<span data-ttu-id="d3d26-226">При работе с этой статьей предполагается, что вы импортировали монитор диагностики в свое приложение и добавили файл конфигурации в решение Visual Studio (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и выше).</span><span class="sxs-lookup"><span data-stu-id="d3d26-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="d3d26-227">Дополнительные сведения отображены в шагах 1 и 2 статьи [Включение диагностики в облачных службах и виртуальных машинах Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d3d26-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="d3d26-228">Шаг 1. Сбор и хранение данных счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="d3d26-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="d3d26-229">После добавления файла диагностики в решение Visual Studio можно настроить сбор и хранение данных счетчиков производительности в приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-229">After you have added the diagnostics file to your Visual Studio solution, you can configure the collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="d3d26-230">Это можно сделать, добавив счетчики производительности в файл диагностики.</span><span class="sxs-lookup"><span data-stu-id="d3d26-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="d3d26-231">Данные диагностики, включая счетчики производительности, сначала собираются на уровне экземпляра.</span><span class="sxs-lookup"><span data-stu-id="d3d26-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="d3d26-232">Затем данные сохраняются в таблице WADPerformanceCountersTable службы Azure, поэтому необходимо также указать в своем приложении учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="d3d26-233">При проверке приложения локально в эмуляторе вычислений можно также сохранить данные диагностики локально в эмуляторе хранилища.</span><span class="sxs-lookup"><span data-stu-id="d3d26-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="d3d26-234">Прежде чем сохранять данные диагностики, необходимо перейти на [портал Azure](http://portal.azure.com/) и создать классическую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-234">Before you store diagnostics data, you must first go to the [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="d3d26-235">Мы рекомендуем разместить учетную запись хранения в том же географическом местоположении, что и приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-235">A best practice is to locate your storage account in the same geo-location as your Azure application.</span></span> <span data-ttu-id="d3d26-236">Таким образом вы не будете оплачивать дополнительные расходы за пропускную способность, а также уменьшите задержки.</span><span class="sxs-lookup"><span data-stu-id="d3d26-236">By keeping the Azure application and storage account are in the same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="d3d26-237">Добавление счетчиков производительности в файл диагностики</span><span class="sxs-lookup"><span data-stu-id="d3d26-237">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="d3d26-238">Вы можете использовать самые разные счетчики.</span><span class="sxs-lookup"><span data-stu-id="d3d26-238">There are many counters you can use.</span></span> <span data-ttu-id="d3d26-239">В следующем примере приведено несколько счетчиков производительности, рекомендованных для мониторинга веб-ролей и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="d3d26-239">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="d3d26-240">Откройте файл диагностики (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и выше) и добавьте к элементу DiagnosticMonitorConfiguration следующий код:</span><span class="sxs-lookup"><span data-stu-id="d3d26-240">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
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

<span data-ttu-id="d3d26-241">Атрибут bufferQuotaInMB, который указывает максимальный объем хранилища файловой системы, доступной для типа собираемых данных (журналы Azure, журналы IIS и т. д.).</span><span class="sxs-lookup"><span data-stu-id="d3d26-241">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="d3d26-242">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="d3d26-242">The default is 0.</span></span> <span data-ttu-id="d3d26-243">При достижении квоты самые старые данные удаляются по мере добавления новых.</span><span class="sxs-lookup"><span data-stu-id="d3d26-243">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="d3d26-244">Сумма всех свойств bufferQuotaInMB должна быть больше значения атрибута OverallQuotaInMB.</span><span class="sxs-lookup"><span data-stu-id="d3d26-244">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="d3d26-245">Более подробные сведения о способах определения требуемого объема хранилища для сбора данных диагностики см. в разделе "Настройки WAD" статьи [Рекомендации по устранению неполадок при разработке приложений Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3d26-245">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="d3d26-246">Атрибут scheduledTransferPeriod, который указывает интервал между запланированными передачами данных, округлен до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="d3d26-246">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="d3d26-247">В следующих примерах для него указывается значение PT30M (30 минут).</span><span class="sxs-lookup"><span data-stu-id="d3d26-247">In the following examples, it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="d3d26-248">Определение для периода передачи небольшого значения, например 1 минуты, отрицательно повлияет на производительность приложения в рабочей среде, но может оказаться полезным для быстрой оценки диагностических данных во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="d3d26-248">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="d3d26-249">Период запланированного перемещения должен быть достаточно небольшим, чтобы данные диагностики не переопределялись на экземпляре, однако достаточно большим, чтобы не влиять на производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-249">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="d3d26-250">Атрибут counterSpecifier позволяет добавить счетчик производительности, данные которого будут собираться.</span><span class="sxs-lookup"><span data-stu-id="d3d26-250">The counterSpecifier attribute specifies the performance counter to collect.</span></span> <span data-ttu-id="d3d26-251">Атрибут sampleRate позволяет задать частоту выборки для счетчика производительности. В нашем случае это 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="d3d26-251">The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="d3d26-252">После добавления счетчиков производительности, данные которых будут собираться, сохраните изменения в файле диагностики.</span><span class="sxs-lookup"><span data-stu-id="d3d26-252">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="d3d26-253">Затем необходимо указать учетную запись хранения, в которую будут сохраняться данные диагностики.</span><span class="sxs-lookup"><span data-stu-id="d3d26-253">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="d3d26-254">Укажите учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="d3d26-254">Specify the storage account</span></span>
<span data-ttu-id="d3d26-255">Чтобы сохранить данные диагностики в учетной записи хранения Azure, необходимо указать строку подключения в файле конфигурации службы (ServiceConfiguration.cscfg).</span><span class="sxs-lookup"><span data-stu-id="d3d26-255">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="d3d26-256">В пакете Azure SDK 2.5 учетную запись хранения можно указать в файле diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="d3d26-256">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="d3d26-257">Эти инструкции применяются только к пакету Azure SDK 2.4 и ниже.</span><span class="sxs-lookup"><span data-stu-id="d3d26-257">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="d3d26-258">В пакете Azure SDK 2.5 учетную запись хранения можно указать в файле diagnostics.wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="d3d26-258">For Azure SDK 2.5, the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="d3d26-259">Чтобы настроить строки подключения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d3d26-259">To set the connection strings:</span></span>

1. <span data-ttu-id="d3d26-260">Откройте файл ServiceConfiguration.Cloud.cscfg в любом текстовом редакторе и настройте строку подключения для хранилища.</span><span class="sxs-lookup"><span data-stu-id="d3d26-260">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="d3d26-261">Значения *AccountName* и *AccountKey* можно найти на портале Azure. Для этого откройте раздел "Ключи доступа" на панели мониторинга учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-261">The *AccountName* and *AccountKey* values are found in the Azure portal in the storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="d3d26-262">Сохраните файл ServiceConfiguration.Cloud.cscfg.</span><span class="sxs-lookup"><span data-stu-id="d3d26-262">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="d3d26-263">Откройте файл ServiceConfiguration.Local.cscfg и убедитесь, что для параметра UseDevelopmentStorage задано значение True.</span><span class="sxs-lookup"><span data-stu-id="d3d26-263">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="d3d26-264">Теперь, когда заданы строки подключения, приложение будет сохранять данные диагностики в учетной записи хранения при развертывании приложения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-264">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="d3d26-265">Сохраните и соберите свой проект, затем разверните приложение.</span><span class="sxs-lookup"><span data-stu-id="d3d26-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="d3d26-266">Шаг 2. (Необязательно) Создание пользовательских счетчиков производительности</span><span class="sxs-lookup"><span data-stu-id="d3d26-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="d3d26-267">Помимо предварительно заданных счетчиков производительности можно добавить собственные счетчики производительности для мониторинга веб-ролей и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="d3d26-267">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="d3d26-268">Пользовательские счетчики производительности могут использоваться для отслеживания и мониторинга поведения, связанного с приложением, и могут создаваться или удаляться в задаче запуска, веб-роли или рабочей роли с повышенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="d3d26-268">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="d3d26-269">Агент диагностики Azure обновляет конфигурацию счетчиков производительности из файла .wadcfg через минуту после запуска.</span><span class="sxs-lookup"><span data-stu-id="d3d26-269">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="d3d26-270">Если вы создаете пользовательские счетчики производительности в методе OnStart, а на выполнение задач запуска требуется более одной минуты, счетчики не будут созданы при попытке агента диагностики Azure загрузить их.</span><span class="sxs-lookup"><span data-stu-id="d3d26-270">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="d3d26-271">В этом случае система диагностики Azure будет надлежащим образом собирать все данные диагностики — за исключением данных пользовательских счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="d3d26-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="d3d26-272">Чтобы устранить эту проблему, создайте счетчики производительности в задаче при запуске или переместите некоторые задачи запуска в метод OnStart после создания счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="d3d26-272">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="d3d26-273">Выполните следующие действия для создания простого настраиваемого счетчика производительности с именем "\MyCustomCounterCategory\MyButton1Counter":</span><span class="sxs-lookup"><span data-stu-id="d3d26-273">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="d3d26-274">Откройте файл определения службы (CSDEF) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d3d26-274">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="d3d26-275">Добавьте элемент Runtime в элемент WebRole или WorkerRole, чтобы разрешить выполнение с повышенными правами:</span><span class="sxs-lookup"><span data-stu-id="d3d26-275">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="d3d26-276">Сохраните файл .</span><span class="sxs-lookup"><span data-stu-id="d3d26-276">Save the file.</span></span>
4. <span data-ttu-id="d3d26-277">Откройте файл диагностики (diagnostics.wadcfg в пакете SDK 2.4 и ниже или diagnostics.wadcfgx в пакете SDK 2.5 и выше) и добавьте в элемент DiagnosticMonitorConfiguration следующий код:</span><span class="sxs-lookup"><span data-stu-id="d3d26-277">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="d3d26-278">Сохраните файл .</span><span class="sxs-lookup"><span data-stu-id="d3d26-278">Save the file.</span></span>
6. <span data-ttu-id="d3d26-279">Создайте категорию настраиваемого счетчика производительности в методе OnStart роли, прежде чем вызвать base.OnStart.</span><span class="sxs-lookup"><span data-stu-id="d3d26-279">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="d3d26-280">В следующем примере C# создается пользовательская категория, если она еще не существует:</span><span class="sxs-lookup"><span data-stu-id="d3d26-280">The following C# example creates a custom category, if it does not already exist:</span></span>

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
7. <span data-ttu-id="d3d26-281">Обновите счетчики в приложении.</span><span class="sxs-lookup"><span data-stu-id="d3d26-281">Update the counters within your application.</span></span> <span data-ttu-id="d3d26-282">В следующем примере выполняется обновление пользовательского счетчика производительности для событий Button1_Click:</span><span class="sxs-lookup"><span data-stu-id="d3d26-282">The following example updates a custom performance counter on Button1_Click events:</span></span>

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
8. <span data-ttu-id="d3d26-283">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="d3d26-283">Save the file.</span></span>  

<span data-ttu-id="d3d26-284">Теперь данные пользовательских счетчиков производительности собирает монитор диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-284">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="d3d26-285">Шаг 3. Запрос данных счетчика производительности</span><span class="sxs-lookup"><span data-stu-id="d3d26-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="d3d26-286">После развертывания и запуска приложения монитор диагностики начнет собирать данные счетчиков производительности и сохранять их в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d3d26-286">Once your application is deployed and running, the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="d3d26-287">Для просмотра данных счетчиков производительности в таблице WADPerformanceCountersTable используйте такие средства: обозреватель сервера в Visual Studio, [обозреватель хранилища Azure](http://azurestorageexplorer.codeplex.com/) или [диспетчер диагностики Azure](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) от Cerebrata.</span><span class="sxs-lookup"><span data-stu-id="d3d26-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="d3d26-288">Вы можете также программно запросить службу таблиц с использованием запросов [C#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md) или [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="d3d26-288">You can also programmatically query the Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="d3d26-289">В примере на C# показан базовый запрос таблицы WADPerformanceCountersTable с сохранением данных диагностики в CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="d3d26-289">The following C# example shows a basic query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="d3d26-290">После сохранения данных счетчиков производительности в CSV-файл можно использовать возможности построения графиков в Microsoft Excel или любом другом средстве для визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="d3d26-290">Once the performance counters are saved to a CSV file, you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="d3d26-291">Не забудьте добавить ссылку на библиотеку Microsoft.WindowsAzure.Storage.dll, которая включена в пакет Azure SDK для .NET в версии с октября 2012 г.</span><span class="sxs-lookup"><span data-stu-id="d3d26-291">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="d3d26-292">Эта сборка устанавливается в каталог %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\.</span><span class="sxs-lookup"><span data-stu-id="d3d26-292">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
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

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
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

<span data-ttu-id="d3d26-293">Сущности сопоставляются с объектами C# с помощью настраиваемого класса, производного от **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="d3d26-293">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="d3d26-294">Приведенный ниже код определяет класс сущностей, который является счетчиком производительности в таблице **WADPerformanceCountersTable** .</span><span class="sxs-lookup"><span data-stu-id="d3d26-294">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d3d26-295">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3d26-295">Next Steps</span></span>
[<span data-ttu-id="d3d26-296">Просмотрите дополнительные статьи о системе диагностику Azure</span><span class="sxs-lookup"><span data-stu-id="d3d26-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
