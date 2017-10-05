---
title: "Решение \"Данные передачи\" в Log Analytics | Документация Майкрософт"
description: "Данные передачи — это объединенные сетевые данные и данные производительности, передаваемые с компьютеров с установленными агентами OMS, включая агенты Operations Manager и агенты, подключенные к Windows. Сетевые данные вместе с данными журнала помогают коррелировать данные."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: eb8ae80f91b9ecad666ab7a2257d99e5669f5b88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="4f269-104">Решение Wire Data 2.0 (предварительная версия) в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4f269-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Символ Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="4f269-106">Данные передачи — это объединенные сетевые данные и данные производительности, передаваемые с компьютеров с установленными агентами OMS, включая агенты Operations Manager и агенты, подключенные к Windows, а также агенты Linux.</span><span class="sxs-lookup"><span data-stu-id="4f269-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="4f269-107">Сетевые данные вместе с другими данными журнала помогают коррелировать данные.</span><span class="sxs-lookup"><span data-stu-id="4f269-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="4f269-108">Помимо агентов OMS, решение "Данные передачи" использует агенты зависимостей Майкрософт, установленные на компьютерах в вашей ИТ-инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="4f269-108">In addition to OMS agents, the Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="4f269-109">Агенты зависимостей отслеживают сетевые данные, отправляемые на эти компьютеры и с них, для сетевых уровней 2–3 в [модели OSI](https://en.wikipedia.org/wiki/OSI_model), включая различные используемые протоколы и порты.</span><span class="sxs-lookup"><span data-stu-id="4f269-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="4f269-110">Затем данные отправляются в Log Analytics с помощью агентов.</span><span class="sxs-lookup"><span data-stu-id="4f269-110">Data is then sent to Log Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="4f269-111">Нельзя добавить предыдущую версию решения "Данные передачи" в новые рабочие области.</span><span class="sxs-lookup"><span data-stu-id="4f269-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="4f269-112">Если у вас включено исходное решение "Данные передачи", вы можете продолжать его использовать.</span><span class="sxs-lookup"><span data-stu-id="4f269-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="4f269-113">Однако для использования Wire Data 2.0 необходимо сначала удалить исходную версию.</span><span class="sxs-lookup"><span data-stu-id="4f269-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="4f269-114">По умолчанию Log Analytics собирает зарегистрированные в журналах данные производительности ЦП, памяти, дисков и сети на основе показателей счетчиков, встроенных в Windows.</span><span class="sxs-lookup"><span data-stu-id="4f269-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="4f269-115">Процесс сбора сетевых и других данных выполняется в режиме реального времени для каждого агента, включая протоколы подсетей и протоколы уровня приложений, используемые компьютером.</span><span class="sxs-lookup"><span data-stu-id="4f269-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span> <span data-ttu-id="4f269-116">Дополнительные счетчики производительности можно добавить на странице "Параметры" на вкладке "Журналы".</span><span class="sxs-lookup"><span data-stu-id="4f269-116">You can add other performance counters on the Settings page on the Logs tab.</span></span>

<span data-ttu-id="4f269-117">Если вы использовали [sFlow](http://www.sflow.org/) или другое программное обеспечение с [протоколом etFlow от Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), передаваемые статистические данные будут вам знакомы.</span><span class="sxs-lookup"><span data-stu-id="4f269-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="4f269-118">Ниже перечислены некоторые типы встроенных запросов поиска в журналах.</span><span class="sxs-lookup"><span data-stu-id="4f269-118">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="4f269-119">агенты,предоставляющие данные передачи;</span><span class="sxs-lookup"><span data-stu-id="4f269-119">Agents that provide wire data</span></span>
- <span data-ttu-id="4f269-120">IP-адреса агентов, предоставляющих данные передачи;</span><span class="sxs-lookup"><span data-stu-id="4f269-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="4f269-121">исходящие подключения по IP-адресам;</span><span class="sxs-lookup"><span data-stu-id="4f269-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="4f269-122">количество байт, отправленных протоколами приложений;</span><span class="sxs-lookup"><span data-stu-id="4f269-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="4f269-123">количество байт, отправленных службой приложений;</span><span class="sxs-lookup"><span data-stu-id="4f269-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="4f269-124">количество байт, полученных различными протоколами;</span><span class="sxs-lookup"><span data-stu-id="4f269-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="4f269-125">общее количество отправленных и полученных байт по версии IP;</span><span class="sxs-lookup"><span data-stu-id="4f269-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="4f269-126">среднее время задержки для подключений, которые оценивались как надежные;</span><span class="sxs-lookup"><span data-stu-id="4f269-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="4f269-127">компьютерные процессы, которые инициировали или получали сетевой трафик;</span><span class="sxs-lookup"><span data-stu-id="4f269-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="4f269-128">объем сетевого трафика для процесса.</span><span class="sxs-lookup"><span data-stu-id="4f269-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="4f269-129">Выполняя поиск с помощью данных передачи, можно отфильтровать и сгруппировать данные, чтобы просмотреть сведения об основных агентах и основных протоколах.</span><span class="sxs-lookup"><span data-stu-id="4f269-129">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="4f269-130">Кроме того, можно узнать, когда определенные компьютеры (IP-адреса или MAC-адреса) взаимодействовали друг с другом, как долго длился процесс и сколько данных было отправлено. По сути вы просматриваете метаданные о сетевом трафике на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="4f269-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="4f269-131">Однако просмотр метаданных не всегда полезен для проведения глубокой диагностики.</span><span class="sxs-lookup"><span data-stu-id="4f269-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="4f269-132">Данные передачи в Log Analytics не являются полным отражением сетевых данных.</span><span class="sxs-lookup"><span data-stu-id="4f269-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="4f269-133">Поэтому они не предназначены для расширенного устранения неполадок на уровне пакетов.</span><span class="sxs-lookup"><span data-stu-id="4f269-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="4f269-134">Преимуществом использования агента (по сравнению с другими методами сбора) является отсутствие необходимости установки устройств, перенастройки сетевых коммутаторов или выполнения сложных настроек.</span><span class="sxs-lookup"><span data-stu-id="4f269-134">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="4f269-135">Данные передачи основаны на использовании агента — установите агент на компьютере, и он будет отслеживать свой собственный сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="4f269-135">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="4f269-136">Еще одно преимущество проявляется в случае, если нужно отслеживать рабочие нагрузки, выполняющиеся у поставщиков облачных служб, поставщиков услуг размещения или в Microsoft Azure, где пользователь не является владельцем уровня структуры.</span><span class="sxs-lookup"><span data-stu-id="4f269-136">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="4f269-137">Подключенные источники</span><span class="sxs-lookup"><span data-stu-id="4f269-137">Connected sources</span></span>

<span data-ttu-id="4f269-138">Решение "Данные передачи" получает данные от агента зависимостей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4f269-138">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="4f269-139">Агент зависимостей является зависимым от агента OMS ввиду подключений к Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f269-139">The Dependency Agent depends on the OMS Agent for its connections to Log Analytics.</span></span> <span data-ttu-id="4f269-140">Это означает, что сначала на сервере нужно установить и настроить агент OMS, после чего можно будет установить агент зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4f269-140">This means that a server must have the OMS Agent installed and configured first, and then you install the Dependency Agent.</span></span> <span data-ttu-id="4f269-141">В приведенной ниже таблице описаны подключенные источники, которые поддерживаются решением "Данные передачи".</span><span class="sxs-lookup"><span data-stu-id="4f269-141">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="4f269-142">**Подключенный источник**</span><span class="sxs-lookup"><span data-stu-id="4f269-142">**Connected source**</span></span> | <span data-ttu-id="4f269-143">**Поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="4f269-143">**Supported**</span></span> | <span data-ttu-id="4f269-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4f269-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f269-145">Агенты Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-145">Windows agents</span></span> | <span data-ttu-id="4f269-146">Да</span><span class="sxs-lookup"><span data-stu-id="4f269-146">Yes</span></span> | <span data-ttu-id="4f269-147">Решение "Данные передачи" анализирует и собирает данные из компьютеров агентов Windows.</span><span class="sxs-lookup"><span data-stu-id="4f269-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="4f269-148">Помимо [агента OMS](log-analytics-windows-agents.md) для агентов Windows необходим агент зависимостей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4f269-148">In addition to the [OMS Agent](log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="4f269-149">Полный список версий операционных систем см. в разделе [Поддерживаемые операционные системы](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems).</span><span class="sxs-lookup"><span data-stu-id="4f269-149">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="4f269-150">Агенты Linux</span><span class="sxs-lookup"><span data-stu-id="4f269-150">Linux agents</span></span> | <span data-ttu-id="4f269-151">Да</span><span class="sxs-lookup"><span data-stu-id="4f269-151">Yes</span></span> | <span data-ttu-id="4f269-152">Решение "Данные передачи" анализирует и собирает данные из компьютеров агентов Linux.</span><span class="sxs-lookup"><span data-stu-id="4f269-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="4f269-153">Помимо [агента OMS](log-analytics-linux-agents.md) для агентов Linux необходим агент зависимостей Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4f269-153">In addition to the [OMS Agent](log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="4f269-154">Полный список версий операционных систем см. в разделе [Поддерживаемые операционные системы](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems).</span><span class="sxs-lookup"><span data-stu-id="4f269-154">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="4f269-155">Группа управления System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="4f269-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="4f269-156">Да</span><span class="sxs-lookup"><span data-stu-id="4f269-156">Yes</span></span> | <span data-ttu-id="4f269-157">Решение "Данные передачи" анализирует и собирает данные из агентов Windows и Linux в подключенной [группе управления System Center Operations Manager](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="4f269-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="4f269-158">Требуется прямое подключение из агента System Center Operations Manager к Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f269-158">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> <span data-ttu-id="4f269-159">Данные пересылаются из группы управления в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f269-159">Data is forwarded from the management group to Log Analytics.</span></span> |
| <span data-ttu-id="4f269-160">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="4f269-160">Azure storage account</span></span> | <span data-ttu-id="4f269-161">Нет</span><span class="sxs-lookup"><span data-stu-id="4f269-161">No</span></span> | <span data-ttu-id="4f269-162">Решение "Данные передачи" собирает данные из компьютеров агента, поэтому данные из службы хранилища Azure не собираются.</span><span class="sxs-lookup"><span data-stu-id="4f269-162">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="4f269-163">В ОС Windows System Center Operations Manager и Log Analytics используют Microsoft Monitoring Agent для сбора и отправки данных.</span><span class="sxs-lookup"><span data-stu-id="4f269-163">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="4f269-164">В зависимости от контекста этот агент называется агентом System Center Operations Manager, агентом OMS, агентом Log Analytics, MMA или прямым агентом.</span><span class="sxs-lookup"><span data-stu-id="4f269-164">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="4f269-165">System Center Operations Manager и Log Analytics предоставляют немного разные версии MMA.</span><span class="sxs-lookup"><span data-stu-id="4f269-165">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="4f269-166">В каждой из этих версий предусмотрена возможность отправлять отчеты в System Center Operations Manager, Log Analytics или в оба решения.</span><span class="sxs-lookup"><span data-stu-id="4f269-166">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="4f269-167">В ОС Linux агент OMS для Linux собирает и отправляет данные в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f269-167">On Linux, the OMS Agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="4f269-168">"Данные передачи" можно использовать на серверах с прямыми агентами OMS или на серверах, подключенных к Log Analytics через группы управления System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="4f269-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="4f269-169">В этой статье мы будем называть все эти агенты — как в Linux, так и в Windows, подключенные к группе управления System Center Operations Manager или непосредственно к Log Analytics — _агентами OMS_.</span><span class="sxs-lookup"><span data-stu-id="4f269-169">In this article, references to all agents, whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Log Analytics are termed the _OMS agent_.</span></span> <span data-ttu-id="4f269-170">Имя конкретного развернутого агента будет использоваться, только если оно требуется в контексте.</span><span class="sxs-lookup"><span data-stu-id="4f269-170">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="4f269-171">Агент зависимостей самостоятельно не передает данные и не требует внесения изменений в брандмауэры или порты.</span><span class="sxs-lookup"><span data-stu-id="4f269-171">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="4f269-172">Данные в решении"Данные передачи" всегда передаются агентом OMS в Log Analytics, напрямую или через шлюз OMS.</span><span class="sxs-lookup"><span data-stu-id="4f269-172">The data in Wire Data is always transmitted by the OMS agent to Log Analytics, either directly or using the OMS Gateway.</span></span>

![Схема передачи данных агентами](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="4f269-174">Если вы являетесь пользователем System Center Operations Manager с группой управления, подключенной к Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="4f269-174">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="4f269-175">Если у ваших агентов System Center Operations Manager есть доступ к Log Analytics через Интернет, никаких дополнительных настроек не требуется.</span><span class="sxs-lookup"><span data-stu-id="4f269-175">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="4f269-176">Если у агентов System Center Operations Manager нет доступа к Log Analytics через Интернет, необходимо настроить шлюз OMS для работы с System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="4f269-176">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="4f269-177">При использовании Direct Agent необходимо настроить агент OMS для подключения к Log Analytics или шлюзу OMS.</span><span class="sxs-lookup"><span data-stu-id="4f269-177">If you are using the Direct Agent, you need to configure the OMS agent itself to connect to Log Analytics or to your OMS Gateway.</span></span> <span data-ttu-id="4f269-178">Шлюз OMS можно скачать в [Центре загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="4f269-178">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f269-179">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f269-179">Prerequisites</span></span>

- <span data-ttu-id="4f269-180">Требуется предложение решения [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing).</span><span class="sxs-lookup"><span data-stu-id="4f269-180">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="4f269-181">Если вы используете предыдущую версию решения "Данные передачи", сначала необходимо ее удалить.</span><span class="sxs-lookup"><span data-stu-id="4f269-181">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="4f269-182">Тем не менее все данные, зафиксированные с помощью исходного решения "Данные передачи", по-прежнему будут доступны в Wire Data 2.0 и для поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="4f269-182">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="4f269-183">Для установки или удаления агента зависимостей требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="4f269-183">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="4f269-184">Агент зависимостей нужно установить на компьютер с 64-разрядной операционной системой.</span><span class="sxs-lookup"><span data-stu-id="4f269-184">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="4f269-185">Операционные системы</span><span class="sxs-lookup"><span data-stu-id="4f269-185">Operating systems</span></span>

<span data-ttu-id="4f269-186">В следующих разделах представлены поддерживаемые операционные системы для агента зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4f269-186">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="4f269-187">Решение "Данные передачи" не поддерживает 32-разрядные архитектуры операционных систем.</span><span class="sxs-lookup"><span data-stu-id="4f269-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="4f269-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="4f269-188">Windows Server</span></span>

- <span data-ttu-id="4f269-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4f269-189">Windows Server 2016</span></span>
- <span data-ttu-id="4f269-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4f269-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="4f269-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4f269-191">Windows Server 2012</span></span>
- <span data-ttu-id="4f269-192">Windows Server 2008 R2 с пакетом обновления 1</span><span class="sxs-lookup"><span data-stu-id="4f269-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="4f269-193">Классические приложения Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-193">Windows desktop</span></span>

- <span data-ttu-id="4f269-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4f269-194">Windows 10</span></span>
- <span data-ttu-id="4f269-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="4f269-195">Windows 8.1</span></span>
- <span data-ttu-id="4f269-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="4f269-196">Windows 8</span></span>
- <span data-ttu-id="4f269-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="4f269-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="4f269-198">Red Hat Enterprise Linux, CentOS Linux и Oracle Linux (с ядром RHEL)</span><span class="sxs-lookup"><span data-stu-id="4f269-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="4f269-199">Поддерживаются только версии ядра по умолчанию и SMP для Linux.</span><span class="sxs-lookup"><span data-stu-id="4f269-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="4f269-200">Нестандартные версии ядра, такие как PAE и Xen, не поддерживаются ни в одном дистрибутиве Linux.</span><span class="sxs-lookup"><span data-stu-id="4f269-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="4f269-201">Например, система со строкой версии _2.6.16.21-0.8-xen_ не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4f269-201">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="4f269-202">Пользовательские ядра, включая повторные компиляции стандартных ядер, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4f269-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="4f269-203">Ядро CentOSPlus не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4f269-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="4f269-204">Oracle Unbreakable Enterprise Kernel (UEK) рассматривается в разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="4f269-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="4f269-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="4f269-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="4f269-206">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-206">**OS version**</span></span> | <span data-ttu-id="4f269-207">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-208">7.0</span><span class="sxs-lookup"><span data-stu-id="4f269-208">7.0</span></span> | <span data-ttu-id="4f269-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="4f269-209">3.10.0-123</span></span> |
| <span data-ttu-id="4f269-210">7.1.</span><span class="sxs-lookup"><span data-stu-id="4f269-210">7.1</span></span> | <span data-ttu-id="4f269-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="4f269-211">3.10.0-229</span></span> |
| <span data-ttu-id="4f269-212">7,2</span><span class="sxs-lookup"><span data-stu-id="4f269-212">7.2</span></span> | <span data-ttu-id="4f269-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="4f269-213">3.10.0-327</span></span> |
| <span data-ttu-id="4f269-214">7.3</span><span class="sxs-lookup"><span data-stu-id="4f269-214">7.3</span></span> | <span data-ttu-id="4f269-215">3.10.0–514</span><span class="sxs-lookup"><span data-stu-id="4f269-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="4f269-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="4f269-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="4f269-217">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-217">**OS version**</span></span> | <span data-ttu-id="4f269-218">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-219">6,0</span><span class="sxs-lookup"><span data-stu-id="4f269-219">6.0</span></span> | <span data-ttu-id="4f269-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="4f269-220">2.6.32-71</span></span> |
| <span data-ttu-id="4f269-221">6.1</span><span class="sxs-lookup"><span data-stu-id="4f269-221">6.1</span></span> | <span data-ttu-id="4f269-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="4f269-222">2.6.32-131</span></span> |
| <span data-ttu-id="4f269-223">6.2</span><span class="sxs-lookup"><span data-stu-id="4f269-223">6.2</span></span> | <span data-ttu-id="4f269-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="4f269-224">2.6.32-220</span></span> |
| <span data-ttu-id="4f269-225">6.3</span><span class="sxs-lookup"><span data-stu-id="4f269-225">6.3</span></span> | <span data-ttu-id="4f269-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="4f269-226">2.6.32-279</span></span> |
| <span data-ttu-id="4f269-227">6.4</span><span class="sxs-lookup"><span data-stu-id="4f269-227">6.4</span></span> | <span data-ttu-id="4f269-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="4f269-228">2.6.32-358</span></span> |
| <span data-ttu-id="4f269-229">6,5</span><span class="sxs-lookup"><span data-stu-id="4f269-229">6.5</span></span> | <span data-ttu-id="4f269-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="4f269-230">2.6.32-431</span></span> |
| <span data-ttu-id="4f269-231">6.6</span><span class="sxs-lookup"><span data-stu-id="4f269-231">6.6</span></span> | <span data-ttu-id="4f269-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="4f269-232">2.6.32-504</span></span> |
| <span data-ttu-id="4f269-233">6.7</span><span class="sxs-lookup"><span data-stu-id="4f269-233">6.7</span></span> | <span data-ttu-id="4f269-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="4f269-234">2.6.32-573</span></span> |
| <span data-ttu-id="4f269-235">6,8</span><span class="sxs-lookup"><span data-stu-id="4f269-235">6.8</span></span> | <span data-ttu-id="4f269-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="4f269-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="4f269-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="4f269-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="4f269-238">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-238">**OS version**</span></span> | <span data-ttu-id="4f269-239">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-240">5.8</span><span class="sxs-lookup"><span data-stu-id="4f269-240">5.8</span></span> | <span data-ttu-id="4f269-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="4f269-241">2.6.18-308</span></span> |
| <span data-ttu-id="4f269-242">5.9</span><span class="sxs-lookup"><span data-stu-id="4f269-242">5.9</span></span> | <span data-ttu-id="4f269-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="4f269-243">2.6.18-348</span></span> |
| <span data-ttu-id="4f269-244">5.10</span><span class="sxs-lookup"><span data-stu-id="4f269-244">5.10</span></span> | <span data-ttu-id="4f269-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="4f269-245">2.6.18-371</span></span> |
| <span data-ttu-id="4f269-246">5.11</span><span class="sxs-lookup"><span data-stu-id="4f269-246">5.11</span></span> | <span data-ttu-id="4f269-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="4f269-247">2.6.18-398</span></span> <br> <span data-ttu-id="4f269-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="4f269-248">2.6.18-400</span></span> <br><span data-ttu-id="4f269-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="4f269-249">2.6.18-402</span></span> <br><span data-ttu-id="4f269-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="4f269-250">2.6.18-404</span></span> <br><span data-ttu-id="4f269-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="4f269-251">2.6.18-406</span></span> <br> <span data-ttu-id="4f269-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="4f269-252">2.6.18-407</span></span> <br> <span data-ttu-id="4f269-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="4f269-253">2.6.18-408</span></span> <br> <span data-ttu-id="4f269-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="4f269-254">2.6.18-409</span></span> <br> <span data-ttu-id="4f269-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="4f269-255">2.6.18-410</span></span> <br> <span data-ttu-id="4f269-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="4f269-256">2.6.18-411</span></span> <br> <span data-ttu-id="4f269-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="4f269-257">2.6.18-412</span></span> <br> <span data-ttu-id="4f269-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="4f269-258">2.6.18-416</span></span> <br> <span data-ttu-id="4f269-259">2.6.18–417</span><span class="sxs-lookup"><span data-stu-id="4f269-259">2.6.18-417</span></span> <br> <span data-ttu-id="4f269-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="4f269-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="4f269-261">Oracle Enterprise Linux с Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="4f269-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="4f269-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="4f269-262">Oracle Linux 6</span></span>

| <span data-ttu-id="4f269-263">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-263">**OS version**</span></span> | <span data-ttu-id="4f269-264">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-265">6.2</span><span class="sxs-lookup"><span data-stu-id="4f269-265">6.2</span></span> | <span data-ttu-id="4f269-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="4f269-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="4f269-267">6.3</span><span class="sxs-lookup"><span data-stu-id="4f269-267">6.3</span></span> | <span data-ttu-id="4f269-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="4f269-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="4f269-269">6.4</span><span class="sxs-lookup"><span data-stu-id="4f269-269">6.4</span></span> | <span data-ttu-id="4f269-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="4f269-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="4f269-271">6,5</span><span class="sxs-lookup"><span data-stu-id="4f269-271">6.5</span></span> | <span data-ttu-id="4f269-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="4f269-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="4f269-273">6.6</span><span class="sxs-lookup"><span data-stu-id="4f269-273">6.6</span></span> | <span data-ttu-id="4f269-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="4f269-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="4f269-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="4f269-275">Oracle Linux 5</span></span>

| <span data-ttu-id="4f269-276">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-276">**OS version**</span></span> | <span data-ttu-id="4f269-277">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-278">5.8</span><span class="sxs-lookup"><span data-stu-id="4f269-278">5.8</span></span> | <span data-ttu-id="4f269-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="4f269-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="4f269-280">5.9</span><span class="sxs-lookup"><span data-stu-id="4f269-280">5.9</span></span> | <span data-ttu-id="4f269-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="4f269-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="4f269-282">5.10</span><span class="sxs-lookup"><span data-stu-id="4f269-282">5.10</span></span> | <span data-ttu-id="4f269-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="4f269-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="4f269-284">5.11</span><span class="sxs-lookup"><span data-stu-id="4f269-284">5.11</span></span> | <span data-ttu-id="4f269-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="4f269-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="4f269-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="4f269-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="4f269-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="4f269-287">SUSE Linux 11</span></span>

| <span data-ttu-id="4f269-288">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-288">**OS version**</span></span> | <span data-ttu-id="4f269-289">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-290">11</span><span class="sxs-lookup"><span data-stu-id="4f269-290">11</span></span> | <span data-ttu-id="4f269-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="4f269-291">2.6.27</span></span> |
| <span data-ttu-id="4f269-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="4f269-292">11 SP1</span></span> | <span data-ttu-id="4f269-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="4f269-293">2.6.32</span></span> |
| <span data-ttu-id="4f269-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="4f269-294">11 SP2</span></span> | <span data-ttu-id="4f269-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="4f269-295">3.0.13</span></span> |
| <span data-ttu-id="4f269-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="4f269-296">11 SP3</span></span> | <span data-ttu-id="4f269-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="4f269-297">3.0.76</span></span> |
| <span data-ttu-id="4f269-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="4f269-298">11 SP4</span></span> | <span data-ttu-id="4f269-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="4f269-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="4f269-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="4f269-300">SUSE Linux 10</span></span>

| <span data-ttu-id="4f269-301">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-301">**OS version**</span></span> | <span data-ttu-id="4f269-302">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="4f269-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="4f269-303">10 SP4</span></span> | <span data-ttu-id="4f269-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="4f269-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="4f269-305">Скачиваемые файлы агента зависимостей</span><span class="sxs-lookup"><span data-stu-id="4f269-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="4f269-306">**File**</span><span class="sxs-lookup"><span data-stu-id="4f269-306">**File**</span></span> | <span data-ttu-id="4f269-307">**ОС**</span><span class="sxs-lookup"><span data-stu-id="4f269-307">**OS**</span></span> | <span data-ttu-id="4f269-308">**Версия**</span><span class="sxs-lookup"><span data-stu-id="4f269-308">**Version**</span></span> | <span data-ttu-id="4f269-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="4f269-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="4f269-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="4f269-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="4f269-311">Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-311">Windows</span></span> | <span data-ttu-id="4f269-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="4f269-312">9.0.5</span></span> | <span data-ttu-id="4f269-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="4f269-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="4f269-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="4f269-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="4f269-315">Linux</span><span class="sxs-lookup"><span data-stu-id="4f269-315">Linux</span></span> | <span data-ttu-id="4f269-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="4f269-316">9.0.5</span></span> | <span data-ttu-id="4f269-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="4f269-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="4f269-318">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="4f269-318">Configuration</span></span>

<span data-ttu-id="4f269-319">Выполните следующие действия, чтобы настроить решение "Данные передачи" в своих рабочих областях.</span><span class="sxs-lookup"><span data-stu-id="4f269-319">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="4f269-320">Включите решение для анализа журналов действий из [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) или выполните инструкции из статьи [Добавление решений для управления Azure Log Analytics в рабочую область](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4f269-320">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="4f269-321">Установите агент зависимостей на каждом компьютере, где вы хотите получать данные.</span><span class="sxs-lookup"><span data-stu-id="4f269-321">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="4f269-322">Агент зависимостей может отслеживать ближайшие соседние подключения, поэтому необязательно выполнять установку агента на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="4f269-322">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="4f269-323">Установка агента зависимостей в Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-323">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="4f269-324">Для установки или удаления агента требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="4f269-324">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="4f269-325">Агент зависимостей устанавливается на компьютерах Windows с помощью файла InstallDependencyAgent-Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="4f269-325">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="4f269-326">Если запустить этот исполняемый файл без параметров, запустится мастер для установки в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="4f269-326">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="4f269-327">Выполните приведенные шаги, чтобы установить агент зависимостей на каждом компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="4f269-327">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="4f269-328">Установите агент OMS, выполнив инструкции в статье [Подключение компьютеров Windows к службе Log Analytics в Azure](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="4f269-328">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="4f269-329">Скачайте агент Windows, используя ссылку в предыдущем разделе, а затем запустите его с помощью команды InstallDependencyAgent Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="4f269-329">Download the Windows agent using the link in the previous section and then run it by using the following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="4f269-330">Следуйте инструкциям мастера для установки агента.</span><span class="sxs-lookup"><span data-stu-id="4f269-330">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="4f269-331">Если агент зависимостей не запускается, просмотрите подробные сведения об ошибке в записях журналов.</span><span class="sxs-lookup"><span data-stu-id="4f269-331">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="4f269-332">В агентах Windows каталогом журналов является %Programfiles%\Microsoft Dependency Agent\logs.</span><span class="sxs-lookup"><span data-stu-id="4f269-332">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="4f269-333">Командная строка Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-333">Windows command line</span></span>

<span data-ttu-id="4f269-334">Используйте параметры из следующей таблицы для установки из командной строки.</span><span class="sxs-lookup"><span data-stu-id="4f269-334">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="4f269-335">Чтобы просмотреть список параметров установки, запустите установщик с параметром /?</span><span class="sxs-lookup"><span data-stu-id="4f269-335">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="4f269-336">/? следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4f269-336">flag as follows.</span></span>

<span data-ttu-id="4f269-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="4f269-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="4f269-338">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="4f269-338">**Flag**</span></span> | <span data-ttu-id="4f269-339">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4f269-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="4f269-340">Получает список параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="4f269-340">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="4f269-341">Выполняет автоматическую установку без вывода сообщений для пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f269-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="4f269-342">Файлы для агента зависимостей Windows по умолчанию размещаются в папке C:\Program Files\Microsoft Dependency Agent.</span><span class="sxs-lookup"><span data-stu-id="4f269-342">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="4f269-343">Установка агента зависимостей в Linux</span><span class="sxs-lookup"><span data-stu-id="4f269-343">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="4f269-344">Для установки или настройки агента требуется доступ с правами привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f269-344">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="4f269-345">Агент зависимостей устанавливается на компьютерах Linux с помощью файла InstallDependencyAgent-Linux64.bin. Это скрипт оболочки с самоизвлекающимся двоичным файлом.</span><span class="sxs-lookup"><span data-stu-id="4f269-345">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="4f269-346">Вы можете запустить этот файл с помощью _sh_ или добавить разрешения на выполнение в сам файл.</span><span class="sxs-lookup"><span data-stu-id="4f269-346">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="4f269-347">Выполните приведение шаги, чтобы установить агент зависимостей на каждом компьютере Linux.</span><span class="sxs-lookup"><span data-stu-id="4f269-347">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="4f269-348">Установите агент OMS, выполнив инструкции, приведенные в статье [Подключение компьютеров Linux к Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4f269-348">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="4f269-349">Скачайте агент зависимостей Linux, используя ссылку в предыдущем разделе, установите его с правами привилегированного пользователя, а затем запустите с помощью команды InstallDependencyAgent-Linux64.bin.</span><span class="sxs-lookup"><span data-stu-id="4f269-349">Download the Linux Dependency agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="4f269-350">Если агент зависимостей не запускается, просмотрите подробные сведения об ошибке в записях журналов.</span><span class="sxs-lookup"><span data-stu-id="4f269-350">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="4f269-351">В агентах Linux каталог журналов находится в расположении /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="4f269-351">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="4f269-352">Чтобы просмотреть список параметров установки, запустите программу установки с параметров `-help` указанным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="4f269-352">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="4f269-353">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="4f269-353">**Flag**</span></span> | <span data-ttu-id="4f269-354">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4f269-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="4f269-355">Получает список параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="4f269-355">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="4f269-356">Выполняет автоматическую установку без вывода сообщений для пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f269-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="4f269-357">Проверяет разрешения и операционную систему, но не устанавливает агент.</span><span class="sxs-lookup"><span data-stu-id="4f269-357">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="4f269-358">Файлы для агента зависимостей размещаются в следующих каталогах.</span><span class="sxs-lookup"><span data-stu-id="4f269-358">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="4f269-359">**Файлы**</span><span class="sxs-lookup"><span data-stu-id="4f269-359">**Files**</span></span> | <span data-ttu-id="4f269-360">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="4f269-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-361">Основные файлы</span><span class="sxs-lookup"><span data-stu-id="4f269-361">Core files</span></span> | <span data-ttu-id="4f269-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="4f269-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="4f269-363">Файлы журналов</span><span class="sxs-lookup"><span data-stu-id="4f269-363">Log files</span></span> | <span data-ttu-id="4f269-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="4f269-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="4f269-365">Файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="4f269-365">Config files</span></span> | <span data-ttu-id="4f269-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="4f269-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="4f269-367">Исполняемые файлы службы</span><span class="sxs-lookup"><span data-stu-id="4f269-367">Service executable files</span></span> | <span data-ttu-id="4f269-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="4f269-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="4f269-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="4f269-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="4f269-370">Двоичные файлы хранилища</span><span class="sxs-lookup"><span data-stu-id="4f269-370">Binary storage files</span></span> | <span data-ttu-id="4f269-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="4f269-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="4f269-372">Примеры скриптов установки</span><span class="sxs-lookup"><span data-stu-id="4f269-372">Installation script examples</span></span>

<span data-ttu-id="4f269-373">Чтобы легко развернуть агент зависимостей сразу на нескольких серверах, можно использовать скрипт.</span><span class="sxs-lookup"><span data-stu-id="4f269-373">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="4f269-374">Для скачивания и установки агента зависимостей в Windows или Linux можно использовать приведенные ниже примеры скриптов.</span><span class="sxs-lookup"><span data-stu-id="4f269-374">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="4f269-375">Скрипт PowerShell для Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="4f269-376">Скрипт оболочки для Linux</span><span class="sxs-lookup"><span data-stu-id="4f269-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="4f269-377">Настройка требуемого состояния</span><span class="sxs-lookup"><span data-stu-id="4f269-377">Desired State Configuration</span></span>

<span data-ttu-id="4f269-378">Чтобы развернуть агент зависимостей посредством Desired State Configuration, можно использовать модуль xPSDesiredStateConfiguration и небольшой фрагмент кода, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4f269-378">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="4f269-379">Удаление агента зависимостей</span><span class="sxs-lookup"><span data-stu-id="4f269-379">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="4f269-380">Используйте следующие разделы для удаления агента зависимостей.</span><span class="sxs-lookup"><span data-stu-id="4f269-380">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="4f269-381">Удаление агента зависимостей в Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-381">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="4f269-382">Администратор может удалить агент зависимостей для Windows через панель управления.</span><span class="sxs-lookup"><span data-stu-id="4f269-382">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="4f269-383">Для удаления агента зависимостей администратор может также запустить файл %Programfiles%\Microsoft Dependency Agent\Uninstall.exe.</span><span class="sxs-lookup"><span data-stu-id="4f269-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="4f269-384">Удаление агента зависимостей в Linux</span><span class="sxs-lookup"><span data-stu-id="4f269-384">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="4f269-385">Чтобы полностью удалить агент зависимостей в Linux, необходимо удалить сам агент и соединитель, который автоматически устанавливается с агентом.</span><span class="sxs-lookup"><span data-stu-id="4f269-385">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="4f269-386">Удалить и то, и другое одновременно можно с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="4f269-386">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="4f269-387">Пакеты управления</span><span class="sxs-lookup"><span data-stu-id="4f269-387">Management packs</span></span>

<span data-ttu-id="4f269-388">Если решение "Данные передачи" активировано в рабочей области Log Analytics, то на все серверы в этой рабочей области отправляется пакет управления размером 300 КБ.</span><span class="sxs-lookup"><span data-stu-id="4f269-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="4f269-389">Если агенты System Center Operations Manager используются в [подключенной группе управления](log-analytics-om-agents.md), то пакет управления монитора зависимости развертывается из System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="4f269-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="4f269-390">Если агенты подключены напрямую, пакет управления доставляется с помощью Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f269-390">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="4f269-391">Пакет управления называется Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span><span class="sxs-lookup"><span data-stu-id="4f269-391">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="4f269-392">Он записывается в папку %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="4f269-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="4f269-393">Источник данных, используемый пакетом управления, — %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;Автоматически_созданный_идентификатор&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="4f269-393">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="4f269-394">Использование решения</span><span class="sxs-lookup"><span data-stu-id="4f269-394">Using the solution</span></span>

<span data-ttu-id="4f269-395">**Установка и настройка решения**</span><span class="sxs-lookup"><span data-stu-id="4f269-395">**Installing and configuring the solution**</span></span>

<span data-ttu-id="4f269-396">Для установки и настройки решений используйте указанные ниже данные.</span><span class="sxs-lookup"><span data-stu-id="4f269-396">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="4f269-397">Решение "Данные передачи" получает данные с компьютеров под управлением Windows Server 2012 R2, Windows 8.1 и более поздних операционных систем.</span><span class="sxs-lookup"><span data-stu-id="4f269-397">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="4f269-398">На компьютерах, с которых предполагается выполнять сбор данных передачи, необходимо установить Microsoft .NET Framework 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="4f269-398">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="4f269-399">Решение "Данные передачи" необходимо добавить в рабочую область Log Analytics, как описано в статье [Добавление решений для управления Azure Log Analytics в рабочую область](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4f269-399">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="4f269-400">Дополнительная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="4f269-400">There is no further configuration required.</span></span>
- <span data-ttu-id="4f269-401">Для просмотра данных передачи для конкретного решения это решение должно быть уже добавлено в рабочую область.</span><span class="sxs-lookup"><span data-stu-id="4f269-401">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="4f269-402">После установки агентов и решения в вашей рабочей области отобразится плитка Wire Data 2.0.</span><span class="sxs-lookup"><span data-stu-id="4f269-402">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="4f269-403">В настоящее время для просмотра данных передачи необходимо использовать портал OMS.</span><span class="sxs-lookup"><span data-stu-id="4f269-403">Currently, you must use the OMS portal to view wire data.</span></span> <span data-ttu-id="4f269-404">Эти данные нельзя просмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4f269-404">You cannot use the Azure portal to view wire data.</span></span>

![Плитка "Данные передачи"](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="4f269-406">Использование решения Wire Data 2.0</span><span class="sxs-lookup"><span data-stu-id="4f269-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="4f269-407">Чтобы открыть панель мониторинга решения "Данные передачи", на портале OMS щелкните плитку **Wire Data 2.0**.</span><span class="sxs-lookup"><span data-stu-id="4f269-407">In the OMS portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="4f269-408">Панель мониторинга содержит колонки, перечисленные в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="4f269-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="4f269-409">В каждой колонке содержится максимум 10 элементов, соответствующих таким указанным критериям, как область действия и диапазон времени.</span><span class="sxs-lookup"><span data-stu-id="4f269-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="4f269-410">Вы можете выполнить поиск по журналам, в результате которого возвращаются все записи, если щелкнуть заголовок колонки или **Показать все** в ее нижней части.</span><span class="sxs-lookup"><span data-stu-id="4f269-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="4f269-411">**Колонка**</span><span class="sxs-lookup"><span data-stu-id="4f269-411">**Blade**</span></span> | <span data-ttu-id="4f269-412">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4f269-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="4f269-413">Агенты, записывающие сетевой трафик</span><span class="sxs-lookup"><span data-stu-id="4f269-413">Agents capturing network traffic</span></span> | <span data-ttu-id="4f269-414">Отображает число агентов, которые записывают сетевой трафик, и показывает первые 10 компьютеров, записывающих сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="4f269-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="4f269-415">Щелкните количество, чтобы выполнить поиск по журналам: <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="4f269-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="4f269-416">Щелкните в списке компьютер, чтобы выполнить поиск по журналам и получить общее число записанных байт.</span><span class="sxs-lookup"><span data-stu-id="4f269-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="4f269-417">Локальные подсети</span><span class="sxs-lookup"><span data-stu-id="4f269-417">Local Subnets</span></span> | <span data-ttu-id="4f269-418">Показывает число локальных подсетей, которые обнаружили агенты.</span><span class="sxs-lookup"><span data-stu-id="4f269-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="4f269-419">Щелкните число, чтобы выполнить поиск по журналам: <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code>. В результате вы получите список всех подсетей и количество байт, отправленных в каждой из них.</span><span class="sxs-lookup"><span data-stu-id="4f269-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="4f269-420">Выберите подсеть в списке, чтобы выполнить поиск по журналам и получить общее число байт, отправленных в подсети.</span><span class="sxs-lookup"><span data-stu-id="4f269-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="4f269-421">Протоколы уровня приложений</span><span class="sxs-lookup"><span data-stu-id="4f269-421">Application-level Protocols</span></span> | <span data-ttu-id="4f269-422">Показывает количество используемых протоколов уровня приложений, обнаруженных агентами.</span><span class="sxs-lookup"><span data-stu-id="4f269-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="4f269-423">Щелкните количество, чтобы выполнить поиск по журналам: <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="4f269-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="4f269-424">Щелкните в списке протокол, чтобы выполнить поиск по журналам и получить общее число байт, отправленных с помощью протокола.</span><span class="sxs-lookup"><span data-stu-id="4f269-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Панель мониторинга "Данные передачи"](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="4f269-426">Используйте колонку **Агенты, записывающие сетевой трафик**, чтобы определить, какой процент пропускной способности сети используется компьютерами.</span><span class="sxs-lookup"><span data-stu-id="4f269-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="4f269-427">Эта колонка поможет найти самый _активный_ компьютер в среде.</span><span class="sxs-lookup"><span data-stu-id="4f269-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="4f269-428">Такие компьютеры могут быть перегружены, работать со сбоями либо использовать больше сетевых ресурсов, чем обычно.</span><span class="sxs-lookup"><span data-stu-id="4f269-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="4f269-430">Вы также можете использовать колонку **Локальные подсети**, чтобы определить объем сетевого трафика, проходящего через подсети.</span><span class="sxs-lookup"><span data-stu-id="4f269-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="4f269-431">Пользователи часто создают подсети для важных областей своих приложений.</span><span class="sxs-lookup"><span data-stu-id="4f269-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="4f269-432">Эта колонка позволяет просматривать такие области.</span><span class="sxs-lookup"><span data-stu-id="4f269-432">This blade offers a view into those areas.</span></span>

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="4f269-434">Колонка **Протоколы уровня приложений** помогает узнать, какие протоколы используются.</span><span class="sxs-lookup"><span data-stu-id="4f269-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="4f269-435">Например, вы ожидаете, что SSH не используется в вашей сетевой среде.</span><span class="sxs-lookup"><span data-stu-id="4f269-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="4f269-436">С помощью этой колонки можно быстро проверить, так ли это.</span><span class="sxs-lookup"><span data-stu-id="4f269-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="4f269-438">В этом примере можно просмотреть подробные сведения о SSH, чтобы узнать, какие компьютеры используют этот протокол и множество других сведений об обмене данными.</span><span class="sxs-lookup"><span data-stu-id="4f269-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![результаты поиска SSH](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="4f269-440">Также полезно знать об увеличении или уменьшении трафика по протоколу по прошествии времени.</span><span class="sxs-lookup"><span data-stu-id="4f269-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="4f269-441">Например, если объем данных, передаваемых приложением, увеличился, вам следует об этом знать.</span><span class="sxs-lookup"><span data-stu-id="4f269-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="4f269-442">Входные данные</span><span class="sxs-lookup"><span data-stu-id="4f269-442">Input data</span></span>

<span data-ttu-id="4f269-443">Данные передачи собирают метаданные о сетевом трафике с помощью включенных агентов.</span><span class="sxs-lookup"><span data-stu-id="4f269-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="4f269-444">Каждый агент передает данные примерно каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="4f269-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="4f269-445">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="4f269-445">Output data</span></span>

<span data-ttu-id="4f269-446">Для каждого типа входных данных создается запись с данными о типе _WireData_.</span><span class="sxs-lookup"><span data-stu-id="4f269-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="4f269-447">У этих записей есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4f269-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="4f269-448">Свойство</span><span class="sxs-lookup"><span data-stu-id="4f269-448">Property</span></span> | <span data-ttu-id="4f269-449">Описание</span><span class="sxs-lookup"><span data-stu-id="4f269-449">Description</span></span> |
|---|---|
| <span data-ttu-id="4f269-450">Компьютер</span><span class="sxs-lookup"><span data-stu-id="4f269-450">Computer</span></span> | <span data-ttu-id="4f269-451">Имя компьютера, на котором были собраны данные</span><span class="sxs-lookup"><span data-stu-id="4f269-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="4f269-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="4f269-452">TimeGenerated</span></span> | <span data-ttu-id="4f269-453">Время создания записи</span><span class="sxs-lookup"><span data-stu-id="4f269-453">Time of the record</span></span> |
| <span data-ttu-id="4f269-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="4f269-454">LocalIP</span></span> | <span data-ttu-id="4f269-455">IP-адрес локального компьютера</span><span class="sxs-lookup"><span data-stu-id="4f269-455">IP address of the local computer</span></span> |
| <span data-ttu-id="4f269-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="4f269-456">SessionState</span></span> | <span data-ttu-id="4f269-457">Подключен или отключен</span><span class="sxs-lookup"><span data-stu-id="4f269-457">Connected or disconnected</span></span> |
| <span data-ttu-id="4f269-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="4f269-458">ReceivedBytes</span></span> | <span data-ttu-id="4f269-459">Число полученных байт</span><span class="sxs-lookup"><span data-stu-id="4f269-459">Amount of bytes received</span></span> |
| <span data-ttu-id="4f269-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="4f269-460">ProtocolName</span></span> | <span data-ttu-id="4f269-461">Имя сетевого протокола, который используется</span><span class="sxs-lookup"><span data-stu-id="4f269-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="4f269-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="4f269-462">IPVersion</span></span> | <span data-ttu-id="4f269-463">Версия IP</span><span class="sxs-lookup"><span data-stu-id="4f269-463">IP version</span></span> |
| <span data-ttu-id="4f269-464">Направление</span><span class="sxs-lookup"><span data-stu-id="4f269-464">Direction</span></span> | <span data-ttu-id="4f269-465">Входящий или исходящий</span><span class="sxs-lookup"><span data-stu-id="4f269-465">Inbound or outbound</span></span> |
| <span data-ttu-id="4f269-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="4f269-466">MaliciousIP</span></span> | <span data-ttu-id="4f269-467">IP-адрес известного вредоносного источника</span><span class="sxs-lookup"><span data-stu-id="4f269-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="4f269-468">Severity</span><span class="sxs-lookup"><span data-stu-id="4f269-468">Severity</span></span> | <span data-ttu-id="4f269-469">Опасность потенциально вредоносной программы</span><span class="sxs-lookup"><span data-stu-id="4f269-469">Suspected malware severity</span></span> |
| <span data-ttu-id="4f269-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="4f269-470">RemoteIPCountry</span></span> | <span data-ttu-id="4f269-471">Страна удаленного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="4f269-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="4f269-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="4f269-472">ManagementGroupName</span></span> | <span data-ttu-id="4f269-473">Имя группы управления Operations Manager</span><span class="sxs-lookup"><span data-stu-id="4f269-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="4f269-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4f269-474">SourceSystem</span></span> | <span data-ttu-id="4f269-475">Источник, на котором были собраны данные</span><span class="sxs-lookup"><span data-stu-id="4f269-475">Source where data was collected</span></span> |
| <span data-ttu-id="4f269-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="4f269-476">SessionStartTime</span></span> | <span data-ttu-id="4f269-477">Время начала сеанса</span><span class="sxs-lookup"><span data-stu-id="4f269-477">Start time of session</span></span> |
| <span data-ttu-id="4f269-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="4f269-478">SessionEndTime</span></span> | <span data-ttu-id="4f269-479">Время окончания сеанса</span><span class="sxs-lookup"><span data-stu-id="4f269-479">End time of session</span></span> |
| <span data-ttu-id="4f269-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="4f269-480">LocalSubnet</span></span> | <span data-ttu-id="4f269-481">Подсеть, в которой были собраны данные</span><span class="sxs-lookup"><span data-stu-id="4f269-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="4f269-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="4f269-482">LocalPortNumber</span></span> | <span data-ttu-id="4f269-483">Номер локального порта</span><span class="sxs-lookup"><span data-stu-id="4f269-483">Local port number</span></span> |
| <span data-ttu-id="4f269-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="4f269-484">RemoteIP</span></span> | <span data-ttu-id="4f269-485">Удаленный IP-адрес, используемый удаленным компьютером</span><span class="sxs-lookup"><span data-stu-id="4f269-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="4f269-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="4f269-486">RemotePortNumber</span></span> | <span data-ttu-id="4f269-487">Номер порта, используемый удаленным IP-адресом</span><span class="sxs-lookup"><span data-stu-id="4f269-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="4f269-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="4f269-488">SessionID</span></span> | <span data-ttu-id="4f269-489">Уникальное значение, которое идентифицирует сеанс связи между двумя IP-адресами</span><span class="sxs-lookup"><span data-stu-id="4f269-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="4f269-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="4f269-490">SentBytes</span></span> | <span data-ttu-id="4f269-491">Число отправленных байт</span><span class="sxs-lookup"><span data-stu-id="4f269-491">Number of bytes sent</span></span> |
| <span data-ttu-id="4f269-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="4f269-492">TotalBytes</span></span> | <span data-ttu-id="4f269-493">Общее число байтов, отправленных в течение сеанса</span><span class="sxs-lookup"><span data-stu-id="4f269-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="4f269-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="4f269-494">ApplicationProtocol</span></span> | <span data-ttu-id="4f269-495">Тип используемого сетевого протокола</span><span class="sxs-lookup"><span data-stu-id="4f269-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="4f269-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="4f269-496">ProcessID</span></span> | <span data-ttu-id="4f269-497">Идентификатор процесса Windows</span><span class="sxs-lookup"><span data-stu-id="4f269-497">Windows process ID</span></span> |
| <span data-ttu-id="4f269-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="4f269-498">ProcessName</span></span> | <span data-ttu-id="4f269-499">Путь и имя файла процесса</span><span class="sxs-lookup"><span data-stu-id="4f269-499">Path and file name of the process</span></span> |
| <span data-ttu-id="4f269-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="4f269-500">RemoteIPLongitude</span></span> | <span data-ttu-id="4f269-501">Значение долготы IP</span><span class="sxs-lookup"><span data-stu-id="4f269-501">IP longitude value</span></span> |
| <span data-ttu-id="4f269-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="4f269-502">RemoteIPLatitude</span></span> | <span data-ttu-id="4f269-503">Значение широты IP</span><span class="sxs-lookup"><span data-stu-id="4f269-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="4f269-504">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f269-504">Next steps</span></span>

- <span data-ttu-id="4f269-505">[поиск в журналах](log-analytics-log-searches.md) , чтобы просмотреть подробные записи поиска данных передачи.</span><span class="sxs-lookup"><span data-stu-id="4f269-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
