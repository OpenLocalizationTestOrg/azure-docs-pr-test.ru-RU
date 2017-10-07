---
title: "aaaWire решение данных в службе анализа журналов | Документы Microsoft"
description: "Данные передачи — это объединенные сетевые данные и данные производительности, передаваемые с компьютеров с установленными агентами OMS, включая агенты Operations Manager и агенты, подключенные к Windows. Сетевые данные вместе с данным вашего журнала toohelp корреляцию данных."
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
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="3b25d-104">Решение Wire Data 2.0 (предварительная версия) в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3b25d-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Символ Wire Data](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="3b25d-106">Данные передачи — это объединенные сетевые данные и данные производительности, передаваемые с компьютеров с установленными агентами OMS, включая агенты Operations Manager и агенты, подключенные к Windows, а также агенты Linux.</span><span class="sxs-lookup"><span data-stu-id="3b25d-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="3b25d-107">Сетевые данные вместе с вашей toohelp данные журнала корреляцию данных.</span><span class="sxs-lookup"><span data-stu-id="3b25d-107">Network data is combined with your other log data toohelp you correlate data.</span></span>

<span data-ttu-id="3b25d-108">Кроме агентов tooOMS hello решение для данных передачи использует агенты Microsoft зависимостей, устанавливаемого на компьютерах в ИТ-инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="3b25d-108">In addition tooOMS agents, hello Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="3b25d-109">Tooand зависимостей агенты монитора сети данных, отправляемых с компьютеров сети уровней 2 – 3 в hello [модели OSI](https://en.wikipedia.org/wiki/OSI_model), включая hello различные используемые протоколы и порты.</span><span class="sxs-lookup"><span data-stu-id="3b25d-109">Dependency Agents monitor network data sent tooand from your computers for network levels 2-3 in hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), including hello various protocols and ports used.</span></span> <span data-ttu-id="3b25d-110">Затем данные отправляются tooLog аналитика с помощью агентов.</span><span class="sxs-lookup"><span data-stu-id="3b25d-110">Data is then sent tooLog Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="3b25d-111">Не удается добавить hello предыдущей версии решения toonew hello данные передачи областей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-111">You cannot add hello previous version of hello Wire Data solution toonew workspaces.</span></span> <span data-ttu-id="3b25d-112">Если исходные данные передачи решение hello включена, можно продолжить toouse его.</span><span class="sxs-lookup"><span data-stu-id="3b25d-112">If you have hello original Wire Data solution enabled, you can continue toouse it.</span></span> <span data-ttu-id="3b25d-113">Однако toouse 2.0 передачи данных, необходимо сначала удалить исходную версию hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-113">However, toouse Wire Data 2.0, you must first remove hello original version.</span></span>

<span data-ttu-id="3b25d-114">По умолчанию Log Analytics собирает зарегистрированные в журналах данные производительности ЦП, памяти, дисков и сети на основе показателей счетчиков, встроенных в Windows.</span><span class="sxs-lookup"><span data-stu-id="3b25d-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="3b25d-115">Сбора сетевых и других данных выполняется режиме реального времени для каждого агента, включая протоколы подсетей и протоколы уровня приложений, используемого компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by hello computer.</span></span> <span data-ttu-id="3b25d-116">На странице параметров hello вкладка "журналы" hello, можно добавить другие счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="3b25d-116">You can add other performance counters on hello Settings page on hello Logs tab.</span></span>

<span data-ttu-id="3b25d-117">Если вы использовали [sFlow](http://www.sflow.org/) или другое программное обеспечение с [протоколом NetFlow от Cisco](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), затем hello статистику и данные, вы видите из данных передачи будут знакомы tooyou.</span><span class="sxs-lookup"><span data-stu-id="3b25d-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then hello statistics and data you see from wire data will be familiar tooyou.</span></span>

<span data-ttu-id="3b25d-118">Ниже перечислены некоторые типы встроенных запросов поиска журналов hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-118">Some of hello types of built-in Log search queries include:</span></span>

- <span data-ttu-id="3b25d-119">агенты,предоставляющие данные передачи;</span><span class="sxs-lookup"><span data-stu-id="3b25d-119">Agents that provide wire data</span></span>
- <span data-ttu-id="3b25d-120">IP-адреса агентов, предоставляющих данные передачи;</span><span class="sxs-lookup"><span data-stu-id="3b25d-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="3b25d-121">исходящие подключения по IP-адресам;</span><span class="sxs-lookup"><span data-stu-id="3b25d-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="3b25d-122">количество байт, отправленных протоколами приложений;</span><span class="sxs-lookup"><span data-stu-id="3b25d-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="3b25d-123">количество байт, отправленных службой приложений;</span><span class="sxs-lookup"><span data-stu-id="3b25d-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="3b25d-124">количество байт, полученных различными протоколами;</span><span class="sxs-lookup"><span data-stu-id="3b25d-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="3b25d-125">общее количество отправленных и полученных байт по версии IP;</span><span class="sxs-lookup"><span data-stu-id="3b25d-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="3b25d-126">среднее время задержки для подключений, которые оценивались как надежные;</span><span class="sxs-lookup"><span data-stu-id="3b25d-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="3b25d-127">компьютерные процессы, которые инициировали или получали сетевой трафик;</span><span class="sxs-lookup"><span data-stu-id="3b25d-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="3b25d-128">объем сетевого трафика для процесса.</span><span class="sxs-lookup"><span data-stu-id="3b25d-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="3b25d-129">При поиске с помощью данных передачи, можно фильтровать и hello группы данных tooview сведения об основных агентах и основных протоколах.</span><span class="sxs-lookup"><span data-stu-id="3b25d-129">When you search using wire data, you can filter and group data tooview information about hello top agents and top protocols.</span></span> <span data-ttu-id="3b25d-130">Кроме того, можно узнать, когда определенные компьютеры (IP-адреса или MAC-адреса) взаимодействовали друг с другом, как долго длился процесс и сколько данных было отправлено. По сути вы просматриваете метаданные о сетевом трафике на основе поиска.</span><span class="sxs-lookup"><span data-stu-id="3b25d-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="3b25d-131">Однако просмотр метаданных не всегда полезен для проведения глубокой диагностики.</span><span class="sxs-lookup"><span data-stu-id="3b25d-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="3b25d-132">Данные передачи в Log Analytics не являются полным отражением сетевых данных.</span><span class="sxs-lookup"><span data-stu-id="3b25d-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="3b25d-133">Поэтому они не предназначены для расширенного устранения неполадок на уровне пакетов.</span><span class="sxs-lookup"><span data-stu-id="3b25d-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="3b25d-134">Здравствуйте, преимуществом использования агента hello, по сравнению с tooother методов сбора, не имеют tooinstall устройств, перенастройки коммутаторов сети или выполнения сложных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="3b25d-134">hello advantage of using hello agent, compared tooother collection methods, is that you don't have tooinstall appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="3b25d-135">Данные передачи — это просто на основе агентов — hello агент устанавливается на компьютере, и он будет отслеживать свой собственный сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="3b25d-135">Wire data is simply agent-based—you install hello agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="3b25d-136">Еще одним преимуществом использования удобно, если нужно toomonitor рабочие нагрузки, выполняющиеся у поставщиков облачных служб или поставщика услуг размещения Microsoft Azure, где пользователь hello не является владельцем уровня структуры hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-136">Another advantage is when you want toomonitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where hello user doesn't own hello fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="3b25d-137">Подключенные источники</span><span class="sxs-lookup"><span data-stu-id="3b25d-137">Connected sources</span></span>

<span data-ttu-id="3b25d-138">Данные передачи получает данные из hello агента Microsoft зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-138">Wire Data gets its data from hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="3b25d-139">Hello агент зависимостей зависит от hello агента OMS для ее подключения tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b25d-139">hello Dependency Agent depends on hello OMS Agent for its connections tooLog Analytics.</span></span> <span data-ttu-id="3b25d-140">Это означает, что сервер должен иметь hello OMS агент установлен и настроен первый, и затем установить агент зависимостей hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-140">This means that a server must have hello OMS Agent installed and configured first, and then you install hello Dependency Agent.</span></span> <span data-ttu-id="3b25d-141">Hello следующей таблице описаны hello подключенных источников, которые поддерживает решение для данных передачи hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-141">hello following table describes hello connected sources that hello Wire Data solution supports.</span></span>

| <span data-ttu-id="3b25d-142">**Подключенный источник**</span><span class="sxs-lookup"><span data-stu-id="3b25d-142">**Connected source**</span></span> | <span data-ttu-id="3b25d-143">**Поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="3b25d-143">**Supported**</span></span> | <span data-ttu-id="3b25d-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3b25d-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b25d-145">Агенты Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-145">Windows agents</span></span> | <span data-ttu-id="3b25d-146">Да</span><span class="sxs-lookup"><span data-stu-id="3b25d-146">Yes</span></span> | <span data-ttu-id="3b25d-147">Решение "Данные передачи" анализирует и собирает данные из компьютеров агентов Windows.</span><span class="sxs-lookup"><span data-stu-id="3b25d-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="3b25d-148">В дополнение toohello [агента OMS](log-analytics-windows-agents.md), агентов Windows требуют hello агента Microsoft зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-148">In addition toohello [OMS Agent](log-analytics-windows-agents.md), Windows agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="3b25d-149">В разделе hello [поддерживаемые операционные системы](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) полный список версий операционной системы.</span><span class="sxs-lookup"><span data-stu-id="3b25d-149">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="3b25d-150">Агенты Linux</span><span class="sxs-lookup"><span data-stu-id="3b25d-150">Linux agents</span></span> | <span data-ttu-id="3b25d-151">Да</span><span class="sxs-lookup"><span data-stu-id="3b25d-151">Yes</span></span> | <span data-ttu-id="3b25d-152">Решение "Данные передачи" анализирует и собирает данные из компьютеров агентов Linux.</span><span class="sxs-lookup"><span data-stu-id="3b25d-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="3b25d-153">В дополнение toohello [агента OMS](log-analytics-linux-agents.md), агенты Linux требуется hello агента Microsoft зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-153">In addition toohello [OMS Agent](log-analytics-linux-agents.md), Linux agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="3b25d-154">В разделе hello [поддерживаемые операционные системы](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) полный список версий операционной системы.</span><span class="sxs-lookup"><span data-stu-id="3b25d-154">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="3b25d-155">Группа управления System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3b25d-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="3b25d-156">Да</span><span class="sxs-lookup"><span data-stu-id="3b25d-156">Yes</span></span> | <span data-ttu-id="3b25d-157">Решение "Данные передачи" анализирует и собирает данные из агентов Windows и Linux в подключенной [группе управления System Center Operations Manager](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="3b25d-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="3b25d-158">Прямое подключение от tooLog компьютера агента System Center Operations Manager hello аналитика является обязательным.</span><span class="sxs-lookup"><span data-stu-id="3b25d-158">A direct connection from hello System Center Operations Manager agent computer tooLog Analytics is required.</span></span> <span data-ttu-id="3b25d-159">Данные будут отправлены из tooLog группы управления hello Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b25d-159">Data is forwarded from hello management group tooLog Analytics.</span></span> |
| <span data-ttu-id="3b25d-160">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3b25d-160">Azure storage account</span></span> | <span data-ttu-id="3b25d-161">Нет</span><span class="sxs-lookup"><span data-stu-id="3b25d-161">No</span></span> | <span data-ttu-id="3b25d-162">Данные передачи собирает данные от компьютеров агентов, поэтому нет данных от него toocollect из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3b25d-162">Wire Data collects data from agent computers, so there is no data from it toocollect from Azure Storage.</span></span> |

<span data-ttu-id="3b25d-163">В Windows hello агента наблюдения Майкрософт (MMA) используется как System Center Operations Manager, так и служба аналитики журналов toogather и отправлять данные.</span><span class="sxs-lookup"><span data-stu-id="3b25d-163">On Windows, hello Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics toogather and send data.</span></span> <span data-ttu-id="3b25d-164">В зависимости от контекста hello агента hello называется hello агента System Center Operations Manager, агент OMS, аналитика агента журнала, MMA или Direct Agent.</span><span class="sxs-lookup"><span data-stu-id="3b25d-164">Depending on hello context, hello agent is called hello System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="3b25d-165">System Center Operations Manager и анализа журналов предоставляют несколько разных версий hello MMA.</span><span class="sxs-lookup"><span data-stu-id="3b25d-165">System Center Operations Manager and Log Analytics provide slightly different versions of hello MMA.</span></span> <span data-ttu-id="3b25d-166">Каждый эти версии можно отчет tooSystem Center Operations Manager, tooLog Analytics или tooboth.</span><span class="sxs-lookup"><span data-stu-id="3b25d-166">These versions can each report tooSystem Center Operations Manager, tooLog Analytics, or tooboth.</span></span>

<span data-ttu-id="3b25d-167">В Linux hello агента OMS для Linux собирает и отправляет данные tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b25d-167">On Linux, hello OMS Agent for Linux gathers and sends data tooLog Analytics.</span></span> <span data-ttu-id="3b25d-168">Данные передачи можно использовать на серверах с установленными агентами OMS прямой или на серверах, подключенных tooLog Analytics через группы управления System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3b25d-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached tooLog Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="3b25d-169">В этой статье, ссылается на агенты tooall ли Linux или Windows, ли tooa подключенной группы управления System Center Operations Manager или напрямую tooLog аналитика называется hello _агента OMS_.</span><span class="sxs-lookup"><span data-stu-id="3b25d-169">In this article, references tooall agents, whether Linux or Windows, whether connected tooa System Center Operations Manager management group or directly tooLog Analytics are termed hello _OMS agent_.</span></span> <span data-ttu-id="3b25d-170">Мы будем использовать имя конкретного развертывания hello агента hello только в том случае, если он необходим для контекста.</span><span class="sxs-lookup"><span data-stu-id="3b25d-170">We'll use hello specific deployment name of hello agent only if it's needed for context.</span></span>

<span data-ttu-id="3b25d-171">Hello агент зависимостей не передает сами все данные и не требует изменения toofirewalls ни порты.</span><span class="sxs-lookup"><span data-stu-id="3b25d-171">hello Dependency Agent does not transmit any data itself, and it does not require any changes toofirewalls or ports.</span></span> <span data-ttu-id="3b25d-172">Hello в данных передачи всегда передачи данных по tooLog агента OMS hello аналитики, либо непосредственно или с помощью OMS шлюза "hello".</span><span class="sxs-lookup"><span data-stu-id="3b25d-172">hello data in Wire Data is always transmitted by hello OMS agent tooLog Analytics, either directly or using hello OMS Gateway.</span></span>

![Схема передачи данных агентами](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="3b25d-174">Если вы являетесь пользователем System Center Operations Manager с tooLog подключено групп управления аналитика:</span><span class="sxs-lookup"><span data-stu-id="3b25d-174">If you are a System Center Operations Manager user with a management group connected tooLog Analytics:</span></span>

- <span data-ttu-id="3b25d-175">Без дополнительных настроек не требуется, когда агенты System Center Operations Manager можно получить доступ к hello Internet tooconnect tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b25d-175">No additional configuration is required when your System Center Operations Manager agents can access hello Internet tooconnect tooLog Analytics.</span></span>
- <span data-ttu-id="3b25d-176">Необходимо toowork шлюза OMS hello tooconfigure с System Center Operations Manager агентов System Center Operations Manager нет доступа к службе анализа журналов через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-176">You need tooconfigure hello OMS Gateway toowork with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over hello Internet.</span></span>

<span data-ttu-id="3b25d-177">При использовании hello Direct Agent необходим tooconfigure hello OMS самого агента tooconnect tooLog Analytics tooyour OMS шлюза.</span><span class="sxs-lookup"><span data-stu-id="3b25d-177">If you are using hello Direct Agent, you need tooconfigure hello OMS agent itself tooconnect tooLog Analytics or tooyour OMS Gateway.</span></span> <span data-ttu-id="3b25d-178">Можно загрузить hello шлюза OMS hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=52666).</span><span class="sxs-lookup"><span data-stu-id="3b25d-178">You can download hello OMS Gateway from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b25d-179">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3b25d-179">Prerequisites</span></span>

- <span data-ttu-id="3b25d-180">Требуется hello [аналитика](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) предложение решения.</span><span class="sxs-lookup"><span data-stu-id="3b25d-180">Requires hello [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="3b25d-181">Если вы используете предыдущую версию hello hello решение для данных передачи, необходимо сначала удалить его.</span><span class="sxs-lookup"><span data-stu-id="3b25d-181">If you're using hello previous version of hello Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="3b25d-182">Тем не менее все данные, полученные через hello исходное решение для передачи данных по-прежнему доступна в 2.0 передачи данных и поиска журналов.</span><span class="sxs-lookup"><span data-stu-id="3b25d-182">However, all data captured through hello original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="3b25d-183">Права администратора, необходимые tooinstall или удалите hello агент зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-183">Administrator privileges are required tooinstall or uninstall hello Dependency Agent.</span></span>
- <span data-ttu-id="3b25d-184">Hello зависимостей агент должен устанавливаться на компьютер с 64-разрядной операционной системе.</span><span class="sxs-lookup"><span data-stu-id="3b25d-184">hello Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="3b25d-185">Операционные системы</span><span class="sxs-lookup"><span data-stu-id="3b25d-185">Operating systems</span></span>

<span data-ttu-id="3b25d-186">Hello следующих разделах перечислены hello поддерживаемые операционные системы для hello агент зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-186">hello following sections list hello supported operating systems for hello Dependency Agent.</span></span> <span data-ttu-id="3b25d-187">Решение "Данные передачи" не поддерживает 32-разрядные архитектуры операционных систем.</span><span class="sxs-lookup"><span data-stu-id="3b25d-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="3b25d-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="3b25d-188">Windows Server</span></span>

- <span data-ttu-id="3b25d-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3b25d-189">Windows Server 2016</span></span>
- <span data-ttu-id="3b25d-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3b25d-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="3b25d-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3b25d-191">Windows Server 2012</span></span>
- <span data-ttu-id="3b25d-192">Windows Server 2008 R2 с пакетом обновления 1</span><span class="sxs-lookup"><span data-stu-id="3b25d-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="3b25d-193">Классические приложения Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-193">Windows desktop</span></span>

- <span data-ttu-id="3b25d-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="3b25d-194">Windows 10</span></span>
- <span data-ttu-id="3b25d-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3b25d-195">Windows 8.1</span></span>
- <span data-ttu-id="3b25d-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="3b25d-196">Windows 8</span></span>
- <span data-ttu-id="3b25d-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3b25d-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="3b25d-198">Red Hat Enterprise Linux, CentOS Linux и Oracle Linux (с ядром RHEL)</span><span class="sxs-lookup"><span data-stu-id="3b25d-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="3b25d-199">Поддерживаются только версии ядра по умолчанию и SMP для Linux.</span><span class="sxs-lookup"><span data-stu-id="3b25d-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="3b25d-200">Нестандартные версии ядра, такие как PAE и Xen, не поддерживаются ни в одном дистрибутиве Linux.</span><span class="sxs-lookup"><span data-stu-id="3b25d-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="3b25d-201">Например, в системе с выпуска строку hello _2.6.16.21-0.8-xen_ не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3b25d-201">For example, a system with hello release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="3b25d-202">Пользовательские ядра, включая повторные компиляции стандартных ядер, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="3b25d-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="3b25d-203">Ядро CentOSPlus не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="3b25d-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="3b25d-204">Oracle Unbreakable Enterprise Kernel (UEK) рассматривается в разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="3b25d-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="3b25d-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="3b25d-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="3b25d-206">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-206">**OS version**</span></span> | <span data-ttu-id="3b25d-207">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-208">7.0</span><span class="sxs-lookup"><span data-stu-id="3b25d-208">7.0</span></span> | <span data-ttu-id="3b25d-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="3b25d-209">3.10.0-123</span></span> |
| <span data-ttu-id="3b25d-210">7.1.</span><span class="sxs-lookup"><span data-stu-id="3b25d-210">7.1</span></span> | <span data-ttu-id="3b25d-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="3b25d-211">3.10.0-229</span></span> |
| <span data-ttu-id="3b25d-212">7,2</span><span class="sxs-lookup"><span data-stu-id="3b25d-212">7.2</span></span> | <span data-ttu-id="3b25d-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="3b25d-213">3.10.0-327</span></span> |
| <span data-ttu-id="3b25d-214">7.3</span><span class="sxs-lookup"><span data-stu-id="3b25d-214">7.3</span></span> | <span data-ttu-id="3b25d-215">3.10.0–514</span><span class="sxs-lookup"><span data-stu-id="3b25d-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="3b25d-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="3b25d-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="3b25d-217">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-217">**OS version**</span></span> | <span data-ttu-id="3b25d-218">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-219">6,0</span><span class="sxs-lookup"><span data-stu-id="3b25d-219">6.0</span></span> | <span data-ttu-id="3b25d-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="3b25d-220">2.6.32-71</span></span> |
| <span data-ttu-id="3b25d-221">6.1</span><span class="sxs-lookup"><span data-stu-id="3b25d-221">6.1</span></span> | <span data-ttu-id="3b25d-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="3b25d-222">2.6.32-131</span></span> |
| <span data-ttu-id="3b25d-223">6.2</span><span class="sxs-lookup"><span data-stu-id="3b25d-223">6.2</span></span> | <span data-ttu-id="3b25d-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="3b25d-224">2.6.32-220</span></span> |
| <span data-ttu-id="3b25d-225">6.3</span><span class="sxs-lookup"><span data-stu-id="3b25d-225">6.3</span></span> | <span data-ttu-id="3b25d-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="3b25d-226">2.6.32-279</span></span> |
| <span data-ttu-id="3b25d-227">6.4</span><span class="sxs-lookup"><span data-stu-id="3b25d-227">6.4</span></span> | <span data-ttu-id="3b25d-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="3b25d-228">2.6.32-358</span></span> |
| <span data-ttu-id="3b25d-229">6,5</span><span class="sxs-lookup"><span data-stu-id="3b25d-229">6.5</span></span> | <span data-ttu-id="3b25d-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="3b25d-230">2.6.32-431</span></span> |
| <span data-ttu-id="3b25d-231">6.6</span><span class="sxs-lookup"><span data-stu-id="3b25d-231">6.6</span></span> | <span data-ttu-id="3b25d-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="3b25d-232">2.6.32-504</span></span> |
| <span data-ttu-id="3b25d-233">6.7</span><span class="sxs-lookup"><span data-stu-id="3b25d-233">6.7</span></span> | <span data-ttu-id="3b25d-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="3b25d-234">2.6.32-573</span></span> |
| <span data-ttu-id="3b25d-235">6,8</span><span class="sxs-lookup"><span data-stu-id="3b25d-235">6.8</span></span> | <span data-ttu-id="3b25d-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="3b25d-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="3b25d-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="3b25d-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="3b25d-238">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-238">**OS version**</span></span> | <span data-ttu-id="3b25d-239">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-240">5.8</span><span class="sxs-lookup"><span data-stu-id="3b25d-240">5.8</span></span> | <span data-ttu-id="3b25d-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="3b25d-241">2.6.18-308</span></span> |
| <span data-ttu-id="3b25d-242">5.9</span><span class="sxs-lookup"><span data-stu-id="3b25d-242">5.9</span></span> | <span data-ttu-id="3b25d-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="3b25d-243">2.6.18-348</span></span> |
| <span data-ttu-id="3b25d-244">5.10</span><span class="sxs-lookup"><span data-stu-id="3b25d-244">5.10</span></span> | <span data-ttu-id="3b25d-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="3b25d-245">2.6.18-371</span></span> |
| <span data-ttu-id="3b25d-246">5.11</span><span class="sxs-lookup"><span data-stu-id="3b25d-246">5.11</span></span> | <span data-ttu-id="3b25d-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="3b25d-247">2.6.18-398</span></span> <br> <span data-ttu-id="3b25d-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="3b25d-248">2.6.18-400</span></span> <br><span data-ttu-id="3b25d-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="3b25d-249">2.6.18-402</span></span> <br><span data-ttu-id="3b25d-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="3b25d-250">2.6.18-404</span></span> <br><span data-ttu-id="3b25d-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="3b25d-251">2.6.18-406</span></span> <br> <span data-ttu-id="3b25d-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="3b25d-252">2.6.18-407</span></span> <br> <span data-ttu-id="3b25d-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="3b25d-253">2.6.18-408</span></span> <br> <span data-ttu-id="3b25d-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="3b25d-254">2.6.18-409</span></span> <br> <span data-ttu-id="3b25d-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="3b25d-255">2.6.18-410</span></span> <br> <span data-ttu-id="3b25d-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="3b25d-256">2.6.18-411</span></span> <br> <span data-ttu-id="3b25d-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="3b25d-257">2.6.18-412</span></span> <br> <span data-ttu-id="3b25d-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="3b25d-258">2.6.18-416</span></span> <br> <span data-ttu-id="3b25d-259">2.6.18–417</span><span class="sxs-lookup"><span data-stu-id="3b25d-259">2.6.18-417</span></span> <br> <span data-ttu-id="3b25d-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="3b25d-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="3b25d-261">Oracle Enterprise Linux с Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="3b25d-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="3b25d-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="3b25d-262">Oracle Linux 6</span></span>

| <span data-ttu-id="3b25d-263">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-263">**OS version**</span></span> | <span data-ttu-id="3b25d-264">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-265">6.2</span><span class="sxs-lookup"><span data-stu-id="3b25d-265">6.2</span></span> | <span data-ttu-id="3b25d-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="3b25d-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="3b25d-267">6.3</span><span class="sxs-lookup"><span data-stu-id="3b25d-267">6.3</span></span> | <span data-ttu-id="3b25d-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="3b25d-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="3b25d-269">6.4</span><span class="sxs-lookup"><span data-stu-id="3b25d-269">6.4</span></span> | <span data-ttu-id="3b25d-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="3b25d-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="3b25d-271">6,5</span><span class="sxs-lookup"><span data-stu-id="3b25d-271">6.5</span></span> | <span data-ttu-id="3b25d-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="3b25d-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="3b25d-273">6.6</span><span class="sxs-lookup"><span data-stu-id="3b25d-273">6.6</span></span> | <span data-ttu-id="3b25d-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="3b25d-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="3b25d-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="3b25d-275">Oracle Linux 5</span></span>

| <span data-ttu-id="3b25d-276">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-276">**OS version**</span></span> | <span data-ttu-id="3b25d-277">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-278">5.8</span><span class="sxs-lookup"><span data-stu-id="3b25d-278">5.8</span></span> | <span data-ttu-id="3b25d-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="3b25d-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="3b25d-280">5.9</span><span class="sxs-lookup"><span data-stu-id="3b25d-280">5.9</span></span> | <span data-ttu-id="3b25d-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="3b25d-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="3b25d-282">5.10</span><span class="sxs-lookup"><span data-stu-id="3b25d-282">5.10</span></span> | <span data-ttu-id="3b25d-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="3b25d-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="3b25d-284">5.11</span><span class="sxs-lookup"><span data-stu-id="3b25d-284">5.11</span></span> | <span data-ttu-id="3b25d-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="3b25d-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="3b25d-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="3b25d-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="3b25d-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="3b25d-287">SUSE Linux 11</span></span>

| <span data-ttu-id="3b25d-288">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-288">**OS version**</span></span> | <span data-ttu-id="3b25d-289">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-290">11</span><span class="sxs-lookup"><span data-stu-id="3b25d-290">11</span></span> | <span data-ttu-id="3b25d-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="3b25d-291">2.6.27</span></span> |
| <span data-ttu-id="3b25d-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="3b25d-292">11 SP1</span></span> | <span data-ttu-id="3b25d-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="3b25d-293">2.6.32</span></span> |
| <span data-ttu-id="3b25d-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="3b25d-294">11 SP2</span></span> | <span data-ttu-id="3b25d-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="3b25d-295">3.0.13</span></span> |
| <span data-ttu-id="3b25d-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="3b25d-296">11 SP3</span></span> | <span data-ttu-id="3b25d-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="3b25d-297">3.0.76</span></span> |
| <span data-ttu-id="3b25d-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="3b25d-298">11 SP4</span></span> | <span data-ttu-id="3b25d-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="3b25d-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="3b25d-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="3b25d-300">SUSE Linux 10</span></span>

| <span data-ttu-id="3b25d-301">**Версия ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-301">**OS version**</span></span> | <span data-ttu-id="3b25d-302">**Версия ядра**</span><span class="sxs-lookup"><span data-stu-id="3b25d-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="3b25d-303">10 SP4</span></span> | <span data-ttu-id="3b25d-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="3b25d-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="3b25d-305">Скачиваемые файлы агента зависимостей</span><span class="sxs-lookup"><span data-stu-id="3b25d-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="3b25d-306">**File**</span><span class="sxs-lookup"><span data-stu-id="3b25d-306">**File**</span></span> | <span data-ttu-id="3b25d-307">**ОС**</span><span class="sxs-lookup"><span data-stu-id="3b25d-307">**OS**</span></span> | <span data-ttu-id="3b25d-308">**Версия**</span><span class="sxs-lookup"><span data-stu-id="3b25d-308">**Version**</span></span> | <span data-ttu-id="3b25d-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="3b25d-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="3b25d-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="3b25d-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="3b25d-311">Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-311">Windows</span></span> | <span data-ttu-id="3b25d-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="3b25d-312">9.0.5</span></span> | <span data-ttu-id="3b25d-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="3b25d-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="3b25d-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="3b25d-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="3b25d-315">Linux</span><span class="sxs-lookup"><span data-stu-id="3b25d-315">Linux</span></span> | <span data-ttu-id="3b25d-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="3b25d-316">9.0.5</span></span> | <span data-ttu-id="3b25d-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="3b25d-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="3b25d-318">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="3b25d-318">Configuration</span></span>

<span data-ttu-id="3b25d-319">Выполните следующие шаги tooconfigure hello данные передачи решения для рабочих областей hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-319">Perform hello following steps tooconfigure hello Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="3b25d-320">Включить решение hello анализа журналов действий из hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3b25d-320">Enable hello Activity Log Analytics solution from hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="3b25d-321">Установите агент зависимостей hello на каждом компьютере, где вы хотите tooget данные.</span><span class="sxs-lookup"><span data-stu-id="3b25d-321">Install hello Dependency Agent on each computer where you want tooget data.</span></span> <span data-ttu-id="3b25d-322">Hello агент зависимостей можно отслеживать соседей tooimmediate соединения, поэтому может не требоваться агента на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="3b25d-322">hello Dependency Agent can monitor connections tooimmediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-hello-dependency-agent-on-windows"></a><span data-ttu-id="3b25d-323">Установка агента зависимостей hello в Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-323">Install hello Dependency Agent on Windows</span></span>

<span data-ttu-id="3b25d-324">Права администратора не требуется tooinstall или удалите агент hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-324">Administrator privileges are required tooinstall or uninstall hello agent.</span></span>

<span data-ttu-id="3b25d-325">Hello зависимостей агент устанавливается на компьютерах под управлением Windows через InstallDependencyAgent Windows.exe.</span><span class="sxs-lookup"><span data-stu-id="3b25d-325">hello Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="3b25d-326">Если запустить этот исполняемый файл без параметров, запускается мастер интерактивно выполните tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3b25d-326">If you run this executable file without any options, it starts a wizard that you can follow tooinstall interactively.</span></span>

<span data-ttu-id="3b25d-327">Используйте следующие шаги tooinstall hello зависимостей агента на каждом компьютере под управлением Windows hello:</span><span class="sxs-lookup"><span data-stu-id="3b25d-327">Use hello following steps tooinstall hello Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="3b25d-328">Установка агента OMS hello с помощью инструкций hello в [toohello компьютеров Windows подключения службы анализа журналов в Azure](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="3b25d-328">Install hello OMS Agent by using hello instructions at [Connect Windows computers toohello Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="3b25d-329">Скачать агент Windows hello, с помощью ссылки hello в предыдущем разделе hello и запустите его с помощью hello следующую команду: InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="3b25d-329">Download hello Windows agent using hello link in hello previous section and then run it by using hello following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="3b25d-330">Выполните приветствия мастера tooinstall hello агента.</span><span class="sxs-lookup"><span data-stu-id="3b25d-330">Follow hello wizard tooinstall hello agent.</span></span>
4. <span data-ttu-id="3b25d-331">При сбое toostart hello агент зависимостей в журнале hello подробные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="3b25d-331">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="3b25d-332">Для агентов Windows hello каталог журнала находится в %Programfiles%\Microsoft Agent\logs зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-332">On Windows agents, hello log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="3b25d-333">Командная строка Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-333">Windows command line</span></span>

<span data-ttu-id="3b25d-334">Используйте параметры из hello следующую таблицу tooinstall из командной строки.</span><span class="sxs-lookup"><span data-stu-id="3b25d-334">Use options from hello following table tooinstall from a command line.</span></span> <span data-ttu-id="3b25d-335">Список флагов установки hello, запустите установщик hello с помощью hello toosee /?</span><span class="sxs-lookup"><span data-stu-id="3b25d-335">toosee a list of hello installation flags, run hello installer by using hello /?</span></span> <span data-ttu-id="3b25d-336">/? следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3b25d-336">flag as follows.</span></span>

<span data-ttu-id="3b25d-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="3b25d-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="3b25d-338">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="3b25d-338">**Flag**</span></span> | <span data-ttu-id="3b25d-339">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3b25d-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="3b25d-340">Получение списка параметров командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-340">Get a list of hello command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="3b25d-341">Выполняет автоматическую установку без вывода сообщений для пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b25d-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="3b25d-342">Файлы для агента зависимостей Windows hello, помещаются в C:\Program Files\Microsoft зависимостей агента по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3b25d-342">Files for hello Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-hello-dependency-agent-on-linux"></a><span data-ttu-id="3b25d-343">Установить агент зависимостей hello в Linux</span><span class="sxs-lookup"><span data-stu-id="3b25d-343">Install hello Dependency Agent on Linux</span></span>

<span data-ttu-id="3b25d-344">Корневой доступ является обязательным tooinstall или настройки агента hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-344">Root access is required tooinstall or configure hello agent.</span></span>

<span data-ttu-id="3b25d-345">Hello зависимостей агент устанавливается на компьютеров Linux с помощью InstallDependencyAgent Linux64.bin, сценарий оболочки с самораспаковывающийся двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="3b25d-345">hello Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="3b25d-346">Можно выполнять с помощью файла hello _sh_ или добавьте выполнение сам файл toohello разрешения.</span><span class="sxs-lookup"><span data-stu-id="3b25d-346">You can run hello file by using _sh_ or add execute permissions toohello file itself.</span></span>

<span data-ttu-id="3b25d-347">Используйте следующие шаги tooinstall hello зависимостей агента на каждом компьютере Linux hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-347">Use hello following steps tooinstall hello Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="3b25d-348">Установка агента OMS hello с помощью инструкций hello в [сбора данных и управления ими с компьютеров Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3b25d-348">Install hello OMS Agent by using hello instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="3b25d-349">Скачать агент Linux зависимостей hello, с помощью ссылки hello в предыдущем разделе hello и затем установить его как корневой элемент с помощью hello следующую команду: sh InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="3b25d-349">Download hello Linux Dependency agent using hello link in hello previous section and then install it as root by using hello following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="3b25d-350">При сбое toostart hello агент зависимостей в журнале hello подробные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="3b25d-350">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="3b25d-351">На агентах Linux — каталог журнала hello: /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="3b25d-351">On Linux agents, hello log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="3b25d-352">Список флагов установки hello, запустите программу установки hello с hello toosee `-help` флаг следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3b25d-352">toosee a list of hello installation flags, run hello installation program with hello `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="3b25d-353">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="3b25d-353">**Flag**</span></span> | <span data-ttu-id="3b25d-354">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3b25d-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="3b25d-355">Получение списка параметров командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-355">Get a list of hello command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="3b25d-356">Выполняет автоматическую установку без вывода сообщений для пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b25d-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="3b25d-357">Проверьте разрешения и hello операционной системы, но не устанавливать агент hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-357">Check permissions and hello operating system but do not install hello agent.</span></span> |

<span data-ttu-id="3b25d-358">Файлы для hello агент зависимостей помещаются в hello следующие каталоги:</span><span class="sxs-lookup"><span data-stu-id="3b25d-358">Files for hello Dependency Agent are placed in hello following directories:</span></span>

| <span data-ttu-id="3b25d-359">**Файлы**</span><span class="sxs-lookup"><span data-stu-id="3b25d-359">**Files**</span></span> | <span data-ttu-id="3b25d-360">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="3b25d-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-361">Основные файлы</span><span class="sxs-lookup"><span data-stu-id="3b25d-361">Core files</span></span> | <span data-ttu-id="3b25d-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="3b25d-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="3b25d-363">Файлы журналов</span><span class="sxs-lookup"><span data-stu-id="3b25d-363">Log files</span></span> | <span data-ttu-id="3b25d-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="3b25d-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="3b25d-365">Файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="3b25d-365">Config files</span></span> | <span data-ttu-id="3b25d-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="3b25d-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="3b25d-367">Исполняемые файлы службы</span><span class="sxs-lookup"><span data-stu-id="3b25d-367">Service executable files</span></span> | <span data-ttu-id="3b25d-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="3b25d-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="3b25d-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="3b25d-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="3b25d-370">Двоичные файлы хранилища</span><span class="sxs-lookup"><span data-stu-id="3b25d-370">Binary storage files</span></span> | <span data-ttu-id="3b25d-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="3b25d-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="3b25d-372">Примеры скриптов установки</span><span class="sxs-lookup"><span data-stu-id="3b25d-372">Installation script examples</span></span>

<span data-ttu-id="3b25d-373">tooeasily развертывание hello зависимостей агент на нескольких серверах одновременно, он помогает toouse сценария.</span><span class="sxs-lookup"><span data-stu-id="3b25d-373">tooeasily deploy hello Dependency Agent on many servers at once, it helps toouse a script.</span></span> <span data-ttu-id="3b25d-374">Можно использовать следующие примеры toodownload сценария hello и установить агент зависимостей hello на Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="3b25d-374">You can use hello following script examples toodownload and install hello Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="3b25d-375">Скрипт PowerShell для Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="3b25d-376">Скрипт оболочки для Linux</span><span class="sxs-lookup"><span data-stu-id="3b25d-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="3b25d-377">Настройка требуемого состояния</span><span class="sxs-lookup"><span data-stu-id="3b25d-377">Desired State Configuration</span></span>

<span data-ttu-id="3b25d-378">hello toodeploy агент зависимостей посредством настройки требуемого состояния можно использовать модуль xPSDesiredStateConfiguration hello и большой объем кода hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3b25d-378">toodeploy hello Dependency Agent via Desired State Configuration, you can use hello xPSDesiredStateConfiguration module and a bit of code like hello following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

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
### <a name="uninstall-hello-dependency-agent"></a><span data-ttu-id="3b25d-379">Удаление hello агенту зависимостей</span><span class="sxs-lookup"><span data-stu-id="3b25d-379">Uninstall hello Dependency Agent</span></span>

<span data-ttu-id="3b25d-380">Используйте следующие разделы toohelp, удалите агент зависимостей hello hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-380">Use hello following sections toohelp you remove hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-windows"></a><span data-ttu-id="3b25d-381">Удаление агента зависимостей в ОС Windows hello</span><span class="sxs-lookup"><span data-stu-id="3b25d-381">Uninstall hello Dependency Agent on Windows</span></span>

<span data-ttu-id="3b25d-382">Администратор может удалить hello зависимостей агент для Windows с панели управления.</span><span class="sxs-lookup"><span data-stu-id="3b25d-382">An administrator can uninstall hello Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="3b25d-383">Администратор также можно запустить %Programfiles%\Microsoft Agent\Uninstall.exe зависимостей toouninstall hello агент зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe toouninstall hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-linux"></a><span data-ttu-id="3b25d-384">Удаление hello агент зависимостей в Linux</span><span class="sxs-lookup"><span data-stu-id="3b25d-384">Uninstall hello Dependency Agent on Linux</span></span>

<span data-ttu-id="3b25d-385">Удаление toocompletely Здравствуйте агент зависимостей от Linux, необходимо удалить самого агента hello и hello соединитель, который автоматически устанавливается вместе с агентом hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-385">toocompletely uninstall hello Dependency Agent from Linux, you must remove hello agent itself and hello connector, which is installed automatically with hello agent.</span></span> <span data-ttu-id="3b25d-386">Можно удалить с помощью hello, выполнив одну команду:</span><span class="sxs-lookup"><span data-stu-id="3b25d-386">You can uninstall both by using hello following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="3b25d-387">Пакеты управления</span><span class="sxs-lookup"><span data-stu-id="3b25d-387">Management packs</span></span>

<span data-ttu-id="3b25d-388">При активации в рабочей области аналитики журналов данных передачи пакета управления 300 КБ отправляется tooall серверов Windows hello в этой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3b25d-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent tooall hello Windows servers in that workspace.</span></span> <span data-ttu-id="3b25d-389">Если вы используете System Center Operations Manager агентов в [подключенной группе управления](log-analytics-om-agents.md), hello монитор зависимостей пакета управления, развернутых из System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3b25d-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), hello Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="3b25d-390">Если непосредственно подключенные агенты hello, аналитика журналов доставляет hello пакета управления.</span><span class="sxs-lookup"><span data-stu-id="3b25d-390">If hello agents are directly connected, Log Analytics delivers hello management pack.</span></span>

<span data-ttu-id="3b25d-391">пакет управления Hello называется Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span><span class="sxs-lookup"><span data-stu-id="3b25d-391">hello management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="3b25d-392">Он записывается в папку %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="3b25d-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="3b25d-393">— Hello источника данных, который использует пакет управления hello: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="3b25d-393">hello data source that hello management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-hello-solution"></a><span data-ttu-id="3b25d-394">С помощью решения hello</span><span class="sxs-lookup"><span data-stu-id="3b25d-394">Using hello solution</span></span>

<span data-ttu-id="3b25d-395">**Установка и настройка решения hello**</span><span class="sxs-lookup"><span data-stu-id="3b25d-395">**Installing and configuring hello solution**</span></span>

<span data-ttu-id="3b25d-396">Используйте следующие сведения tooinstall hello и настроить решение hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-396">Use hello following information tooinstall and configure hello solution.</span></span>

- <span data-ttu-id="3b25d-397">решение для данных передачи Hello получает данные с компьютеров под управлением Windows Server 2012 R2, Windows 8.1 и более поздних операционных системах.</span><span class="sxs-lookup"><span data-stu-id="3b25d-397">hello Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="3b25d-398">На компьютеры, где требуется tooacquire передачи данных из требуется Microsoft .NET Framework 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3b25d-398">Microsoft .NET Framework 4.0 or later is required on computers where you want tooacquire wire data from.</span></span>
- <span data-ttu-id="3b25d-399">Добавление hello данные передачи решения tooyour анализа журналов рабочей области с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="3b25d-399">Add hello Wire Data solution tooyour Log Analytics workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="3b25d-400">Дополнительная настройка не требуется.</span><span class="sxs-lookup"><span data-stu-id="3b25d-400">There is no further configuration required.</span></span>
- <span data-ttu-id="3b25d-401">Tooview передачи данных для конкретного решения, вы должны toohave hello решение уже добавлен tooyour рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3b25d-401">If you want tooview wire data for a specific solution, you need toohave hello solution already added tooyour workspace.</span></span>

<span data-ttu-id="3b25d-402">После установлены агенты и установке решения hello, Плитка hello 2.0 передачи данных отображается в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3b25d-402">After you have agents installed and you install hello solution, hello Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="3b25d-403">В настоящее время необходимо использовать данные передачи tooview портала OMS hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-403">Currently, you must use hello OMS portal tooview wire data.</span></span> <span data-ttu-id="3b25d-404">Нельзя использовать hello Azure портала tooview передачи данных.</span><span class="sxs-lookup"><span data-stu-id="3b25d-404">You cannot use hello Azure portal tooview wire data.</span></span>

![Плитка "Данные передачи"](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a><span data-ttu-id="3b25d-406">С помощью решения hello 2.0 передачи данных</span><span class="sxs-lookup"><span data-stu-id="3b25d-406">Using hello Wire Data 2.0 solution</span></span>

<span data-ttu-id="3b25d-407">На портале OMS hello щелкните hello **передачи данных 2.0** плитки tooopen hello передачи данных мониторинга.</span><span class="sxs-lookup"><span data-stu-id="3b25d-407">In hello OMS portal, click hello **Wire Data 2.0** tile tooopen hello Wire Data dashboard.</span></span> <span data-ttu-id="3b25d-408">панель мониторинга Hello включает hello колонок в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="3b25d-408">hello dashboard includes hello blades in hello following table.</span></span> <span data-ttu-id="3b25d-409">Каждой колонки перечислены вверх too10 сузьте указан, в колонке критерий hello области и временной диапазон.</span><span class="sxs-lookup"><span data-stu-id="3b25d-409">Each blade lists up too10 items matching that blade's criteria for hello specified scope and time range.</span></span> <span data-ttu-id="3b25d-410">Можно выполнить поиск журнала, который возвращает все записи, нажав кнопку **все** hello нижней части колонки hello или щелкнув заголовок колонки hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-410">You can run a log search that returns all records by clicking **See all** at hello bottom of hello blade or by clicking hello blade header.</span></span>

| <span data-ttu-id="3b25d-411">**Колонка**</span><span class="sxs-lookup"><span data-stu-id="3b25d-411">**Blade**</span></span> | <span data-ttu-id="3b25d-412">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3b25d-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="3b25d-413">Агенты, записывающие сетевой трафик</span><span class="sxs-lookup"><span data-stu-id="3b25d-413">Agents capturing network traffic</span></span> | <span data-ttu-id="3b25d-414">Показывает количество hello агенты, которые записи сетевого трафика и перечисляет hello top 10 компьютеров, которые захватываемых трафика.</span><span class="sxs-lookup"><span data-stu-id="3b25d-414">Shows hello number of agents that are capturing network traffic and lists hello top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="3b25d-415">Щелкните номер toorun hello поиска журналов для <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span><span class="sxs-lookup"><span data-stu-id="3b25d-415">Click hello number toorun a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="3b25d-416">Выберите компьютер в списке toorun hello поиска журналов, возвращая hello общее число записанных байтов.</span><span class="sxs-lookup"><span data-stu-id="3b25d-416">Click a computer in hello list toorun a log search returning hello total number of bytes captured.</span></span> |
| <span data-ttu-id="3b25d-417">Локальные подсети</span><span class="sxs-lookup"><span data-stu-id="3b25d-417">Local Subnets</span></span> | <span data-ttu-id="3b25d-418">Показывает количество hello в локальной подсети, которые обнаружены агенты.</span><span class="sxs-lookup"><span data-stu-id="3b25d-418">Shows hello number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="3b25d-419">Щелкните номер toorun hello поиска журналов для <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> , в которой перечислены все подсети с hello количеством байтов, отправленных в каждый из них.</span><span class="sxs-lookup"><span data-stu-id="3b25d-419">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with hello number of bytes sent over each one.</span></span> <span data-ttu-id="3b25d-420">Выберите подсеть в списке toorun hello поиска журналов, возвращая hello общее число байтов, отправленных в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-420">Click a subnet in hello list toorun a log search returning hello total number of bytes sent over hello subnet.</span></span> |
| <span data-ttu-id="3b25d-421">Протоколы уровня приложений</span><span class="sxs-lookup"><span data-stu-id="3b25d-421">Application-level Protocols</span></span> | <span data-ttu-id="3b25d-422">Показывает номер hello протоколы уровня приложений используется, как обнаруженный агентами.</span><span class="sxs-lookup"><span data-stu-id="3b25d-422">Shows hello number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="3b25d-423">Щелкните номер toorun hello поиска журналов для <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span><span class="sxs-lookup"><span data-stu-id="3b25d-423">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="3b25d-424">Щелкните toorun протокола поиска журналов, возвращая hello общее число байтов, отправленных по протоколу hello.</span><span class="sxs-lookup"><span data-stu-id="3b25d-424">Click a protocol toorun a log search returning hello total number of bytes sent using hello protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Панель мониторинга "Данные передачи"](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="3b25d-426">Можно использовать hello **агенты, записывающие сетевой трафик** toodetermine колонки, какую часть пропускной способности сети, потребляемый компьютеров.</span><span class="sxs-lookup"><span data-stu-id="3b25d-426">You can use hello **Agents capturing network traffic** blade toodetermine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="3b25d-427">Эта колонка позволяет легко найти hello _chattiest_ компьютера в среде.</span><span class="sxs-lookup"><span data-stu-id="3b25d-427">This blade can help you easily find hello _chattiest_ computer in your environment.</span></span> <span data-ttu-id="3b25d-428">Такие компьютеры могут быть перегружены, работать со сбоями либо использовать больше сетевых ресурсов, чем обычно.</span><span class="sxs-lookup"><span data-stu-id="3b25d-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="3b25d-430">Аналогичным образом можно использовать hello **в локальных подсетях** toodetermine колонки, объем сетевого трафика, перемещение по подсетей.</span><span class="sxs-lookup"><span data-stu-id="3b25d-430">Similarly, you can use hello **Local Subnets** blade toodetermine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="3b25d-431">Пользователи часто создают подсети для важных областей своих приложений.</span><span class="sxs-lookup"><span data-stu-id="3b25d-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="3b25d-432">Эта колонка позволяет просматривать такие области.</span><span class="sxs-lookup"><span data-stu-id="3b25d-432">This blade offers a view into those areas.</span></span>

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="3b25d-434">Hello **протоколы уровня приложений** колонке полезно потому, что бывает полезно знать протоколы используется.</span><span class="sxs-lookup"><span data-stu-id="3b25d-434">hello **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="3b25d-435">Например можно предположить, настоящий SSH toonot в сетевой среде.</span><span class="sxs-lookup"><span data-stu-id="3b25d-435">For example, you might expect SSH toonot be in use in your network environment.</span></span> <span data-ttu-id="3b25d-436">Просмотр данных, доступных в колонке hello быстро подтвердить или не опровергает ваши ожидания.</span><span class="sxs-lookup"><span data-stu-id="3b25d-436">Viewing information available in hello blade can quickly confirm or disprove your expectation.</span></span>

![Пример поиска по журналам](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="3b25d-438">В этом примере можно было бы глубже изучить SSH сведения toosee компьютеры, на которых используется SSH и множество других сведений о связи.</span><span class="sxs-lookup"><span data-stu-id="3b25d-438">In this example, you could drill-into SSH details toosee which computers are using SSH and many other communication details.</span></span>

![результаты поиска SSH](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="3b25d-440">Это также полезно tooknow Если трафик протокола увеличивается или уменьшается во времени.</span><span class="sxs-lookup"><span data-stu-id="3b25d-440">It's also useful tooknow if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="3b25d-441">Например если возрастает hello объем данных, передаваемых приложением, могут быть то, что следует обратить внимание, или, может оказаться внимания.</span><span class="sxs-lookup"><span data-stu-id="3b25d-441">For example, if hello amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="3b25d-442">Входные данные</span><span class="sxs-lookup"><span data-stu-id="3b25d-442">Input data</span></span>

<span data-ttu-id="3b25d-443">Метаданные о сетевом трафике, с помощью hello агенты, которые вы включили собирает данные передачи.</span><span class="sxs-lookup"><span data-stu-id="3b25d-443">Wire data collects metadata about network traffic using hello agents that you have enabled.</span></span> <span data-ttu-id="3b25d-444">Каждый агент передает данные примерно каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="3b25d-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="3b25d-445">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="3b25d-445">Output data</span></span>

<span data-ttu-id="3b25d-446">Для каждого типа входных данных создается запись с данными о типе _WireData_.</span><span class="sxs-lookup"><span data-stu-id="3b25d-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="3b25d-447">Данные передачи записи имеют свойства, показанные в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="3b25d-447">WireData records have properties shown in hello following table:</span></span>

| <span data-ttu-id="3b25d-448">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b25d-448">Property</span></span> | <span data-ttu-id="3b25d-449">Описание</span><span class="sxs-lookup"><span data-stu-id="3b25d-449">Description</span></span> |
|---|---|
| <span data-ttu-id="3b25d-450">Компьютер</span><span class="sxs-lookup"><span data-stu-id="3b25d-450">Computer</span></span> | <span data-ttu-id="3b25d-451">Имя компьютера, на котором были собраны данные</span><span class="sxs-lookup"><span data-stu-id="3b25d-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="3b25d-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="3b25d-452">TimeGenerated</span></span> | <span data-ttu-id="3b25d-453">Время записи hello</span><span class="sxs-lookup"><span data-stu-id="3b25d-453">Time of hello record</span></span> |
| <span data-ttu-id="3b25d-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="3b25d-454">LocalIP</span></span> | <span data-ttu-id="3b25d-455">IP-адрес локального компьютера hello</span><span class="sxs-lookup"><span data-stu-id="3b25d-455">IP address of hello local computer</span></span> |
| <span data-ttu-id="3b25d-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="3b25d-456">SessionState</span></span> | <span data-ttu-id="3b25d-457">Подключен или отключен</span><span class="sxs-lookup"><span data-stu-id="3b25d-457">Connected or disconnected</span></span> |
| <span data-ttu-id="3b25d-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="3b25d-458">ReceivedBytes</span></span> | <span data-ttu-id="3b25d-459">Число полученных байт</span><span class="sxs-lookup"><span data-stu-id="3b25d-459">Amount of bytes received</span></span> |
| <span data-ttu-id="3b25d-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="3b25d-460">ProtocolName</span></span> | <span data-ttu-id="3b25d-461">Имя hello сетевой протокол, используемый</span><span class="sxs-lookup"><span data-stu-id="3b25d-461">Name of hello network protocol used</span></span> |
| <span data-ttu-id="3b25d-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="3b25d-462">IPVersion</span></span> | <span data-ttu-id="3b25d-463">Версия IP</span><span class="sxs-lookup"><span data-stu-id="3b25d-463">IP version</span></span> |
| <span data-ttu-id="3b25d-464">Направление</span><span class="sxs-lookup"><span data-stu-id="3b25d-464">Direction</span></span> | <span data-ttu-id="3b25d-465">Входящий или исходящий</span><span class="sxs-lookup"><span data-stu-id="3b25d-465">Inbound or outbound</span></span> |
| <span data-ttu-id="3b25d-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="3b25d-466">MaliciousIP</span></span> | <span data-ttu-id="3b25d-467">IP-адрес известного вредоносного источника</span><span class="sxs-lookup"><span data-stu-id="3b25d-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="3b25d-468">Severity</span><span class="sxs-lookup"><span data-stu-id="3b25d-468">Severity</span></span> | <span data-ttu-id="3b25d-469">Опасность потенциально вредоносной программы</span><span class="sxs-lookup"><span data-stu-id="3b25d-469">Suspected malware severity</span></span> |
| <span data-ttu-id="3b25d-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="3b25d-470">RemoteIPCountry</span></span> | <span data-ttu-id="3b25d-471">Страна hello удаленный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="3b25d-471">Country of hello remote IP address</span></span> |
| <span data-ttu-id="3b25d-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="3b25d-472">ManagementGroupName</span></span> | <span data-ttu-id="3b25d-473">Имя группы управления Operations Manager hello</span><span class="sxs-lookup"><span data-stu-id="3b25d-473">Name of hello Operations Manager management group</span></span> |
| <span data-ttu-id="3b25d-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="3b25d-474">SourceSystem</span></span> | <span data-ttu-id="3b25d-475">Источник, на котором были собраны данные</span><span class="sxs-lookup"><span data-stu-id="3b25d-475">Source where data was collected</span></span> |
| <span data-ttu-id="3b25d-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="3b25d-476">SessionStartTime</span></span> | <span data-ttu-id="3b25d-477">Время начала сеанса</span><span class="sxs-lookup"><span data-stu-id="3b25d-477">Start time of session</span></span> |
| <span data-ttu-id="3b25d-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="3b25d-478">SessionEndTime</span></span> | <span data-ttu-id="3b25d-479">Время окончания сеанса</span><span class="sxs-lookup"><span data-stu-id="3b25d-479">End time of session</span></span> |
| <span data-ttu-id="3b25d-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="3b25d-480">LocalSubnet</span></span> | <span data-ttu-id="3b25d-481">Подсеть, в которой были собраны данные</span><span class="sxs-lookup"><span data-stu-id="3b25d-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="3b25d-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="3b25d-482">LocalPortNumber</span></span> | <span data-ttu-id="3b25d-483">Номер локального порта</span><span class="sxs-lookup"><span data-stu-id="3b25d-483">Local port number</span></span> |
| <span data-ttu-id="3b25d-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="3b25d-484">RemoteIP</span></span> | <span data-ttu-id="3b25d-485">Удаленный IP-адрес, используемый hello удаленного компьютера</span><span class="sxs-lookup"><span data-stu-id="3b25d-485">Remote IP address used by hello remote computer</span></span> |
| <span data-ttu-id="3b25d-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="3b25d-486">RemotePortNumber</span></span> | <span data-ttu-id="3b25d-487">Номер порта, используемый hello удаленный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="3b25d-487">Port number used by hello remote IP address</span></span> |
| <span data-ttu-id="3b25d-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="3b25d-488">SessionID</span></span> | <span data-ttu-id="3b25d-489">Уникальное значение, которое идентифицирует сеанс связи между двумя IP-адресами</span><span class="sxs-lookup"><span data-stu-id="3b25d-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="3b25d-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="3b25d-490">SentBytes</span></span> | <span data-ttu-id="3b25d-491">Число отправленных байт</span><span class="sxs-lookup"><span data-stu-id="3b25d-491">Number of bytes sent</span></span> |
| <span data-ttu-id="3b25d-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="3b25d-492">TotalBytes</span></span> | <span data-ttu-id="3b25d-493">Общее число байтов, отправленных в течение сеанса</span><span class="sxs-lookup"><span data-stu-id="3b25d-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="3b25d-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="3b25d-494">ApplicationProtocol</span></span> | <span data-ttu-id="3b25d-495">Тип используемого сетевого протокола</span><span class="sxs-lookup"><span data-stu-id="3b25d-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="3b25d-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="3b25d-496">ProcessID</span></span> | <span data-ttu-id="3b25d-497">Идентификатор процесса Windows</span><span class="sxs-lookup"><span data-stu-id="3b25d-497">Windows process ID</span></span> |
| <span data-ttu-id="3b25d-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="3b25d-498">ProcessName</span></span> | <span data-ttu-id="3b25d-499">Путь и имя файла процесса hello</span><span class="sxs-lookup"><span data-stu-id="3b25d-499">Path and file name of hello process</span></span> |
| <span data-ttu-id="3b25d-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="3b25d-500">RemoteIPLongitude</span></span> | <span data-ttu-id="3b25d-501">Значение долготы IP</span><span class="sxs-lookup"><span data-stu-id="3b25d-501">IP longitude value</span></span> |
| <span data-ttu-id="3b25d-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="3b25d-502">RemoteIPLatitude</span></span> | <span data-ttu-id="3b25d-503">Значение широты IP</span><span class="sxs-lookup"><span data-stu-id="3b25d-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="3b25d-504">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b25d-504">Next steps</span></span>

- <span data-ttu-id="3b25d-505">[Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробные записи поиска передачи данных.</span><span class="sxs-lookup"><span data-stu-id="3b25d-505">[Search logs](log-analytics-log-searches.md) tooview detailed wire data search records.</span></span>
