---
title: "Устранение неполадок в Azure Наблюдатель сети tooresource aaaIntroduction | Документы Microsoft"
description: "Эта страница предоставляет общие сведения о возможности по устранению неполадок ресурсов Наблюдатель сети hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="37314-103">Устранение неполадок в Azure Наблюдатель сети tooresource введение</span><span class="sxs-lookup"><span data-stu-id="37314-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="37314-104">Шлюзы виртуальной сети обеспечивают связь между локальными ресурсами и другими виртуальными сетями в Azure.</span><span class="sxs-lookup"><span data-stu-id="37314-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="37314-105">Мониторинг этих шлюзов и их соединения является критическим tooensuring связи не нарушена.</span><span class="sxs-lookup"><span data-stu-id="37314-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="37314-106">Наблюдатель сети предоставляет возможность tootroubleshoot hello шлюзах виртуальной сети и подключения.</span><span class="sxs-lookup"><span data-stu-id="37314-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="37314-107">Это может вызываться через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="37314-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="37314-108">При вызове Наблюдатель сети Диагностика работоспособности hello hello шлюз виртуальной сети или подключений и соответствующие результаты возврата hello.</span><span class="sxs-lookup"><span data-stu-id="37314-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="37314-109">Этот запрос является долго выполняющаяся транзакция, hello результатов после завершения диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="37314-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![портал][2]

## <a name="results"></a><span data-ttu-id="37314-111">Результаты</span><span class="sxs-lookup"><span data-stu-id="37314-111">Results</span></span>

<span data-ttu-id="37314-112">Hello предварительные результаты, возвращаемые дают общее представление о работоспособности hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="37314-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="37314-113">Для ресурсов могут быть предоставлены подробные сведения, как показано в следующем разделе hello:</span><span class="sxs-lookup"><span data-stu-id="37314-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="37314-114">Hello ниже приведен hello значения, возвращаемые с hello устранения API.</span><span class="sxs-lookup"><span data-stu-id="37314-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="37314-115">**время начала** -это значение равно времени hello hello Устранение неполадок запуска при вызове API.</span><span class="sxs-lookup"><span data-stu-id="37314-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="37314-116">**время окончания** -это значение является время hello, завершения устранения неполадок hello.</span><span class="sxs-lookup"><span data-stu-id="37314-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="37314-117">**code** — имеет значение UnHealthy в случае обнаружения отдельной ошибки при диагностике.</span><span class="sxs-lookup"><span data-stu-id="37314-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="37314-118">**результаты** -результаты — это набор результатов, возвращаемый на hello соединения или hello шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="37314-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="37314-119">**Идентификатор** -это значение является типом ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="37314-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="37314-120">**Сводка** -это значение представляет собой сводку ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="37314-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="37314-121">**Подробные** -это значение содержит подробное описание ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="37314-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="37314-122">**recommendedActions** -это свойство представляет собой коллекцию tootake рекомендуемые действия.</span><span class="sxs-lookup"><span data-stu-id="37314-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="37314-123">**actionText** -это значение содержит текст hello, описывающий какие tootake действие.</span><span class="sxs-lookup"><span data-stu-id="37314-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="37314-124">**actionUri** -это значение содержит hello URI toodocumentation tooact.</span><span class="sxs-lookup"><span data-stu-id="37314-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="37314-125">**actionUriText** -это значение является краткое описание действия текста hello.</span><span class="sxs-lookup"><span data-stu-id="37314-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="37314-126">Hello следующие таблицы Показать hello ошибок типы (идентификатор в области результатов из списка hello), доступных, и если hello сбоя журнала.</span><span class="sxs-lookup"><span data-stu-id="37314-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="37314-127">Шлюз</span><span class="sxs-lookup"><span data-stu-id="37314-127">Gateway</span></span>

| <span data-ttu-id="37314-128">Тип ошибки</span><span class="sxs-lookup"><span data-stu-id="37314-128">Fault Type</span></span> | <span data-ttu-id="37314-129">Причина</span><span class="sxs-lookup"><span data-stu-id="37314-129">Reason</span></span> | <span data-ttu-id="37314-130">Журнал</span><span class="sxs-lookup"><span data-stu-id="37314-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="37314-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="37314-131">NoFault</span></span> | <span data-ttu-id="37314-132">Ошибка не обнаружена.</span><span class="sxs-lookup"><span data-stu-id="37314-132">When no error is detected.</span></span> |<span data-ttu-id="37314-133">Да</span><span class="sxs-lookup"><span data-stu-id="37314-133">Yes</span></span>|
| <span data-ttu-id="37314-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="37314-134">GatewayNotFound</span></span> | <span data-ttu-id="37314-135">Не удается найти шлюз или шлюз не подготовлен.</span><span class="sxs-lookup"><span data-stu-id="37314-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="37314-136">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-136">No</span></span>|
| <span data-ttu-id="37314-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="37314-137">PlannedMaintenance</span></span> |  <span data-ttu-id="37314-138">Выполняется обслуживание экземпляра шлюза.</span><span class="sxs-lookup"><span data-stu-id="37314-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="37314-139">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-139">No</span></span>|
| <span data-ttu-id="37314-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="37314-140">UserDrivenUpdate</span></span> | <span data-ttu-id="37314-141">Идет обновление, инициированное пользователем.</span><span class="sxs-lookup"><span data-stu-id="37314-141">When a user update is in progress.</span></span> <span data-ttu-id="37314-142">Это может быть операция изменения размера.</span><span class="sxs-lookup"><span data-stu-id="37314-142">This could be a resize operation.</span></span> | <span data-ttu-id="37314-143">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-143">No</span></span> |
| <span data-ttu-id="37314-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="37314-144">VipUnResponsive</span></span> | <span data-ttu-id="37314-145">Не удается связаться с hello первичного экземпляра hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="37314-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="37314-146">Это происходит, когда происходит сбой проверки работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="37314-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="37314-147">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-147">No</span></span> |
| <span data-ttu-id="37314-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="37314-148">PlatformInActive</span></span> | <span data-ttu-id="37314-149">Имеется проблема с платформой hello.</span><span class="sxs-lookup"><span data-stu-id="37314-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="37314-150">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-150">No</span></span>|
| <span data-ttu-id="37314-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="37314-151">ServiceNotRunning</span></span> | <span data-ttu-id="37314-152">базовая служба Hello не выполняется.</span><span class="sxs-lookup"><span data-stu-id="37314-152">hello underlying service is not running.</span></span> | <span data-ttu-id="37314-153">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-153">No</span></span>|
| <span data-ttu-id="37314-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="37314-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="37314-155">Подключения не существует в шлюзе hello.</span><span class="sxs-lookup"><span data-stu-id="37314-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="37314-156">Это всего лишь предупреждение.</span><span class="sxs-lookup"><span data-stu-id="37314-156">This is only a warning.</span></span>| <span data-ttu-id="37314-157">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-157">No</span></span>|
| <span data-ttu-id="37314-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="37314-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="37314-159">Подключения не установлены.</span><span class="sxs-lookup"><span data-stu-id="37314-159">Connections are not connected.</span></span> <span data-ttu-id="37314-160">Это всего лишь предупреждение.</span><span class="sxs-lookup"><span data-stu-id="37314-160">This is only a warning.</span></span>| <span data-ttu-id="37314-161">Да</span><span class="sxs-lookup"><span data-stu-id="37314-161">Yes</span></span>|
| <span data-ttu-id="37314-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="37314-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="37314-163">текущее использование ЦП шлюза Hello равно > 95%.</span><span class="sxs-lookup"><span data-stu-id="37314-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="37314-164">Да</span><span class="sxs-lookup"><span data-stu-id="37314-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="37314-165">Подключение</span><span class="sxs-lookup"><span data-stu-id="37314-165">Connection</span></span>

| <span data-ttu-id="37314-166">Тип ошибки</span><span class="sxs-lookup"><span data-stu-id="37314-166">Fault Type</span></span> | <span data-ttu-id="37314-167">Причина</span><span class="sxs-lookup"><span data-stu-id="37314-167">Reason</span></span> | <span data-ttu-id="37314-168">Журнал</span><span class="sxs-lookup"><span data-stu-id="37314-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="37314-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="37314-169">NoFault</span></span> | <span data-ttu-id="37314-170">Ошибка не обнаружена.</span><span class="sxs-lookup"><span data-stu-id="37314-170">When no error is detected.</span></span> |<span data-ttu-id="37314-171">Да</span><span class="sxs-lookup"><span data-stu-id="37314-171">Yes</span></span>|
| <span data-ttu-id="37314-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="37314-172">GatewayNotFound</span></span> | <span data-ttu-id="37314-173">Не удается найти шлюз или шлюз не подготовлен.</span><span class="sxs-lookup"><span data-stu-id="37314-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="37314-174">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-174">No</span></span>|
| <span data-ttu-id="37314-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="37314-175">PlannedMaintenance</span></span> | <span data-ttu-id="37314-176">Выполняется обслуживание экземпляра шлюза.</span><span class="sxs-lookup"><span data-stu-id="37314-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="37314-177">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-177">No</span></span>|
| <span data-ttu-id="37314-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="37314-178">UserDrivenUpdate</span></span> | <span data-ttu-id="37314-179">Идет обновление, инициированное пользователем.</span><span class="sxs-lookup"><span data-stu-id="37314-179">When a user update is in progress.</span></span> <span data-ttu-id="37314-180">Это может быть операция изменения размера.</span><span class="sxs-lookup"><span data-stu-id="37314-180">This could be a resize operation.</span></span>  | <span data-ttu-id="37314-181">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-181">No</span></span> |
| <span data-ttu-id="37314-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="37314-182">VipUnResponsive</span></span> | <span data-ttu-id="37314-183">Не удается связаться с hello первичного экземпляра hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="37314-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="37314-184">Это происходит, когда происходит сбой проверки работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="37314-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="37314-185">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-185">No</span></span> |
| <span data-ttu-id="37314-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="37314-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="37314-187">Отсутствует конфигурация подключения.</span><span class="sxs-lookup"><span data-stu-id="37314-187">Connection configuration is missing.</span></span> | <span data-ttu-id="37314-188">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-188">No</span></span> |
| <span data-ttu-id="37314-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="37314-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="37314-190">Hello соединение помечается как «отключенной».</span><span class="sxs-lookup"><span data-stu-id="37314-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="37314-191">Нет</span><span class="sxs-lookup"><span data-stu-id="37314-191">No</span></span>|
| <span data-ttu-id="37314-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="37314-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="37314-193">Hello базовой службы не имеет настроенного подключения hello.</span><span class="sxs-lookup"><span data-stu-id="37314-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="37314-194">Да</span><span class="sxs-lookup"><span data-stu-id="37314-194">Yes</span></span> |
| <span data-ttu-id="37314-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="37314-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="37314-196">соответствующая служба Hello помечается как standby.</span><span class="sxs-lookup"><span data-stu-id="37314-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="37314-197">Да</span><span class="sxs-lookup"><span data-stu-id="37314-197">Yes</span></span>|
| <span data-ttu-id="37314-198">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="37314-198">Authentication</span></span> | <span data-ttu-id="37314-199">Несоответствие предварительного ключа.</span><span class="sxs-lookup"><span data-stu-id="37314-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="37314-200">Да</span><span class="sxs-lookup"><span data-stu-id="37314-200">Yes</span></span>|
| <span data-ttu-id="37314-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="37314-201">PeerReachability</span></span> | <span data-ttu-id="37314-202">Hello одноранговых шлюз недоступен.</span><span class="sxs-lookup"><span data-stu-id="37314-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="37314-203">Да</span><span class="sxs-lookup"><span data-stu-id="37314-203">Yes</span></span>|
| <span data-ttu-id="37314-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="37314-204">IkePolicyMismatch</span></span> | <span data-ttu-id="37314-205">Hello одноранговых шлюза имеет IKE политики, которые не поддерживаются в Azure.</span><span class="sxs-lookup"><span data-stu-id="37314-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="37314-206">Да</span><span class="sxs-lookup"><span data-stu-id="37314-206">Yes</span></span>|
| <span data-ttu-id="37314-207">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="37314-207">WfpParse Error</span></span> | <span data-ttu-id="37314-208">Ошибка синтаксического анализа журнала WFP hello.</span><span class="sxs-lookup"><span data-stu-id="37314-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="37314-209">Да</span><span class="sxs-lookup"><span data-stu-id="37314-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="37314-210">Поддерживаемые типы шлюзов</span><span class="sxs-lookup"><span data-stu-id="37314-210">Supported Gateway types</span></span>

<span data-ttu-id="37314-211">Hello ниже перечислены hello поддержки показано, какие шлюзы и подключения поддерживаются в устранении неполадок Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="37314-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="37314-212">**Типы шлюзов**</span><span class="sxs-lookup"><span data-stu-id="37314-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="37314-213">Виртуальная частная сеть</span><span class="sxs-lookup"><span data-stu-id="37314-213">VPN</span></span>      | <span data-ttu-id="37314-214">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="37314-214">Supported</span></span>        |
|<span data-ttu-id="37314-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="37314-215">ExpressRoute</span></span> | <span data-ttu-id="37314-216">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="37314-216">Not Supported</span></span> |
|<span data-ttu-id="37314-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="37314-217">Hypernet</span></span> | <span data-ttu-id="37314-218">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="37314-218">Not Supported</span></span>|
|<span data-ttu-id="37314-219">**Типы VPN**</span><span class="sxs-lookup"><span data-stu-id="37314-219">**VPN types**</span></span> | |
|<span data-ttu-id="37314-220">На основе маршрутов</span><span class="sxs-lookup"><span data-stu-id="37314-220">Route Based</span></span> | <span data-ttu-id="37314-221">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="37314-221">Supported</span></span>|
|<span data-ttu-id="37314-222">На основе политик</span><span class="sxs-lookup"><span data-stu-id="37314-222">Policy Based</span></span> | <span data-ttu-id="37314-223">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="37314-223">Not Supported</span></span>|
|<span data-ttu-id="37314-224">**Типы подключений**</span><span class="sxs-lookup"><span data-stu-id="37314-224">**Connection types**</span></span>||
|<span data-ttu-id="37314-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="37314-225">IPSec</span></span>| <span data-ttu-id="37314-226">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="37314-226">Supported</span></span>|
|<span data-ttu-id="37314-227">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="37314-227">VNet2Vnet</span></span>| <span data-ttu-id="37314-228">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="37314-228">Supported</span></span>|
|<span data-ttu-id="37314-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="37314-229">ExpressRoute</span></span>| <span data-ttu-id="37314-230">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="37314-230">Not Supported</span></span>|
|<span data-ttu-id="37314-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="37314-231">Hypernet</span></span>| <span data-ttu-id="37314-232">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="37314-232">Not Supported</span></span>|
|<span data-ttu-id="37314-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="37314-233">VPNClient</span></span>| <span data-ttu-id="37314-234">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="37314-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="37314-235">Файлы журналов</span><span class="sxs-lookup"><span data-stu-id="37314-235">Log files</span></span>

<span data-ttu-id="37314-236">файлы журнала устранения неполадок Hello ресурсов хранятся в учетной записи хранения, после завершения устранения неполадок ресурсов.</span><span class="sxs-lookup"><span data-stu-id="37314-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="37314-237">Hello на иллюстрации показан пример hello содержимое вызова, который завершился ошибкой.</span><span class="sxs-lookup"><span data-stu-id="37314-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![ZIP-файл][1]

> [!NOTE]
> <span data-ttu-id="37314-239">В некоторых случаях только подмножество hello файлы журналов записывается toostorage.</span><span class="sxs-lookup"><span data-stu-id="37314-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="37314-240">Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="37314-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="37314-241">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="37314-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="37314-242">Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="37314-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="37314-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="37314-243">ConnectionStats.txt</span></span>

<span data-ttu-id="37314-244">Hello **ConnectionStats.txt** файл содержит общую статистику hello соединения, включая байты входящего и исходящего состояние подключения и подключения hello время hello.</span><span class="sxs-lookup"><span data-stu-id="37314-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="37314-245">Если toohello вызов hello, устранение неполадок API возвращает работоспособное, hello единственное возвращается в hello ZIP-файл — **ConnectionStats.txt** файла.</span><span class="sxs-lookup"><span data-stu-id="37314-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="37314-246">содержимое этого файла Hello, аналогичные toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="37314-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="37314-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="37314-247">CPUStats.txt</span></span>

<span data-ttu-id="37314-248">Hello **CPUStats.txt** файл содержит ЦП и памяти, доступной во время hello тестирования.</span><span class="sxs-lookup"><span data-stu-id="37314-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="37314-249">Hello этот файл содержит аналогичные toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="37314-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="37314-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="37314-250">IKEErrors.txt</span></span>

<span data-ttu-id="37314-251">Hello **IKEErrors.txt** файл содержит ошибки, найденные во время мониторинга IKE.</span><span class="sxs-lookup"><span data-stu-id="37314-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="37314-252">Hello следующем примере показано содержимое файла IKEErrors.txt hello.</span><span class="sxs-lookup"><span data-stu-id="37314-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="37314-253">Ошибки могут отличаться в зависимости от проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="37314-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="37314-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="37314-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="37314-255">Hello **Scrubbed wfpdiag.txt** файл журнала содержит журнал wfp hello.</span><span class="sxs-lookup"><span data-stu-id="37314-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="37314-256">В этом журнале регистрируется удаление пакетов, а также сбои протокола IKE и AuthIP.</span><span class="sxs-lookup"><span data-stu-id="37314-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="37314-257">Hello пример hello содержимое файла Scrubbed wfpdiag.txt hello.</span><span class="sxs-lookup"><span data-stu-id="37314-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="37314-258">В этом примере hello общего ключа соединения не был правильно, как видно из 3-й строки hello снизу hello.</span><span class="sxs-lookup"><span data-stu-id="37314-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="37314-259">Следующий пример Hello — просто фрагмент кода hello всего журнала, как hello журнал может быть длительное время, в зависимости от проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="37314-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="37314-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="37314-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="37314-261">Hello **wfpdiag.txt.sum** файл является журнал, содержащий буферов hello и обработанных событий.</span><span class="sxs-lookup"><span data-stu-id="37314-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="37314-262">Hello следующий пример — содержимое файла wfpdiag.txt.sum hello.</span><span class="sxs-lookup"><span data-stu-id="37314-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="37314-263">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37314-263">Next steps</span></span>

<span data-ttu-id="37314-264">Узнайте, как toodiagnose VPN-шлюзы и подключения через hello портала, посетив [Устранение неполадок шлюза - портал Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37314-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
