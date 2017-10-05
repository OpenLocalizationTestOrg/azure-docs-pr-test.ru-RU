---
title: "Общие сведения об устранении неполадок ресурсов в Наблюдателе за сетями Azure | Документация Майкрософт"
description: "Эта страница содержит обзор возможностей Наблюдателя за сетями по устранению неполадок."
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="97d38-103">Общие сведения об устранении неполадок ресурсов в Наблюдателе за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="97d38-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="97d38-104">Шлюзы виртуальной сети обеспечивают связь между локальными ресурсами и другими виртуальными сетями в Azure.</span><span class="sxs-lookup"><span data-stu-id="97d38-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="97d38-105">Мониторинг этих шлюзов и их подключений крайне важен для обеспечения бесперебойной связи.</span><span class="sxs-lookup"><span data-stu-id="97d38-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="97d38-106">Наблюдатель за сетями дает возможность устранять неполадки шлюзов виртуальной сети и их подключений.</span><span class="sxs-lookup"><span data-stu-id="97d38-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="97d38-107">Процедуру устранения неполадок можно вызывать с помощью портала, PowerShell, интерфейса командной строки или API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="97d38-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="97d38-108">При вызове Наблюдатель за сетями диагностирует работоспособность шлюза виртуальной сети или подключения и возвращает соответствующие результаты.</span><span class="sxs-lookup"><span data-stu-id="97d38-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="97d38-109">Этот запрос является долго выполняющейся транзакцией, результаты которой возвращаются после завершения диагностики.</span><span class="sxs-lookup"><span data-stu-id="97d38-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![портал][2]

## <a name="results"></a><span data-ttu-id="97d38-111">Результаты</span><span class="sxs-lookup"><span data-stu-id="97d38-111">Results</span></span>

<span data-ttu-id="97d38-112">Полученные предварительные результаты дают общее представление о работоспособности ресурса.</span><span class="sxs-lookup"><span data-stu-id="97d38-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="97d38-113">Можно получить более подробную информацию о ресурсах, как показано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="97d38-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="97d38-114">В следующем списке приведены значения, возвращаемые API устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="97d38-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="97d38-115">**startTime** — это значение представляет собой время начала вызова API устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="97d38-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="97d38-116">**endTime** — это значение представляет собой время завершения устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="97d38-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="97d38-117">**code** — имеет значение UnHealthy в случае обнаружения отдельной ошибки при диагностике.</span><span class="sxs-lookup"><span data-stu-id="97d38-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="97d38-118">**results** — результаты представляют собой набор данных, возвращаемых для подключения или шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="97d38-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="97d38-119">**id** — это значение представляет собой тип ошибки.</span><span class="sxs-lookup"><span data-stu-id="97d38-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="97d38-120">**summary** — это значение представляет собой сводку по ошибке.</span><span class="sxs-lookup"><span data-stu-id="97d38-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="97d38-121">**detailed** — это значение содержит подробное описание ошибки.</span><span class="sxs-lookup"><span data-stu-id="97d38-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="97d38-122">**recommendedActions** — это свойство представляет собой набор рекомендуемых действий.</span><span class="sxs-lookup"><span data-stu-id="97d38-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="97d38-123">**actionText** — это значение содержит текст, описывающий, какие действия следует предпринять.</span><span class="sxs-lookup"><span data-stu-id="97d38-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="97d38-124">**actionUri** — это значение содержит универсальный код ресурса (URI) для документации о том, как действовать.</span><span class="sxs-lookup"><span data-stu-id="97d38-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="97d38-125">**actionUriText** — это значение представляет собой краткое описание действий.</span><span class="sxs-lookup"><span data-stu-id="97d38-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="97d38-126">В следующих таблицах показаны различные типы ошибок (идентификатор в результатах из приведенного выше списка), которые могут произойти, и указано, приводит ли ошибка к созданию журнала.</span><span class="sxs-lookup"><span data-stu-id="97d38-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="97d38-127">Шлюз</span><span class="sxs-lookup"><span data-stu-id="97d38-127">Gateway</span></span>

| <span data-ttu-id="97d38-128">Тип ошибки</span><span class="sxs-lookup"><span data-stu-id="97d38-128">Fault Type</span></span> | <span data-ttu-id="97d38-129">Причина</span><span class="sxs-lookup"><span data-stu-id="97d38-129">Reason</span></span> | <span data-ttu-id="97d38-130">Журнал</span><span class="sxs-lookup"><span data-stu-id="97d38-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="97d38-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="97d38-131">NoFault</span></span> | <span data-ttu-id="97d38-132">Ошибка не обнаружена.</span><span class="sxs-lookup"><span data-stu-id="97d38-132">When no error is detected.</span></span> |<span data-ttu-id="97d38-133">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-133">Yes</span></span>|
| <span data-ttu-id="97d38-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="97d38-134">GatewayNotFound</span></span> | <span data-ttu-id="97d38-135">Не удается найти шлюз или шлюз не подготовлен.</span><span class="sxs-lookup"><span data-stu-id="97d38-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="97d38-136">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-136">No</span></span>|
| <span data-ttu-id="97d38-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="97d38-137">PlannedMaintenance</span></span> |  <span data-ttu-id="97d38-138">Выполняется обслуживание экземпляра шлюза.</span><span class="sxs-lookup"><span data-stu-id="97d38-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="97d38-139">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-139">No</span></span>|
| <span data-ttu-id="97d38-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="97d38-140">UserDrivenUpdate</span></span> | <span data-ttu-id="97d38-141">Идет обновление, инициированное пользователем.</span><span class="sxs-lookup"><span data-stu-id="97d38-141">When a user update is in progress.</span></span> <span data-ttu-id="97d38-142">Это может быть операция изменения размера.</span><span class="sxs-lookup"><span data-stu-id="97d38-142">This could be a resize operation.</span></span> | <span data-ttu-id="97d38-143">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-143">No</span></span> |
| <span data-ttu-id="97d38-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="97d38-144">VipUnResponsive</span></span> | <span data-ttu-id="97d38-145">Не удается связаться с первичным экземпляром шлюза.</span><span class="sxs-lookup"><span data-stu-id="97d38-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="97d38-146">Это происходит при сбое пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="97d38-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="97d38-147">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-147">No</span></span> |
| <span data-ttu-id="97d38-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="97d38-148">PlatformInActive</span></span> | <span data-ttu-id="97d38-149">Существует проблема с платформой.</span><span class="sxs-lookup"><span data-stu-id="97d38-149">There is an issue with the platform.</span></span> | <span data-ttu-id="97d38-150">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-150">No</span></span>|
| <span data-ttu-id="97d38-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="97d38-151">ServiceNotRunning</span></span> | <span data-ttu-id="97d38-152">Базовая служба не выполняется.</span><span class="sxs-lookup"><span data-stu-id="97d38-152">The underlying service is not running.</span></span> | <span data-ttu-id="97d38-153">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-153">No</span></span>|
| <span data-ttu-id="97d38-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="97d38-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="97d38-155">У шлюза нет подключений.</span><span class="sxs-lookup"><span data-stu-id="97d38-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="97d38-156">Это всего лишь предупреждение.</span><span class="sxs-lookup"><span data-stu-id="97d38-156">This is only a warning.</span></span>| <span data-ttu-id="97d38-157">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-157">No</span></span>|
| <span data-ttu-id="97d38-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="97d38-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="97d38-159">Подключения не установлены.</span><span class="sxs-lookup"><span data-stu-id="97d38-159">Connections are not connected.</span></span> <span data-ttu-id="97d38-160">Это всего лишь предупреждение.</span><span class="sxs-lookup"><span data-stu-id="97d38-160">This is only a warning.</span></span>| <span data-ttu-id="97d38-161">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-161">Yes</span></span>|
| <span data-ttu-id="97d38-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="97d38-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="97d38-163">Текущее использование ЦП шлюза превышает 95 %.</span><span class="sxs-lookup"><span data-stu-id="97d38-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="97d38-164">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="97d38-165">Подключение</span><span class="sxs-lookup"><span data-stu-id="97d38-165">Connection</span></span>

| <span data-ttu-id="97d38-166">Тип ошибки</span><span class="sxs-lookup"><span data-stu-id="97d38-166">Fault Type</span></span> | <span data-ttu-id="97d38-167">Причина</span><span class="sxs-lookup"><span data-stu-id="97d38-167">Reason</span></span> | <span data-ttu-id="97d38-168">Журнал</span><span class="sxs-lookup"><span data-stu-id="97d38-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="97d38-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="97d38-169">NoFault</span></span> | <span data-ttu-id="97d38-170">Ошибка не обнаружена.</span><span class="sxs-lookup"><span data-stu-id="97d38-170">When no error is detected.</span></span> |<span data-ttu-id="97d38-171">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-171">Yes</span></span>|
| <span data-ttu-id="97d38-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="97d38-172">GatewayNotFound</span></span> | <span data-ttu-id="97d38-173">Не удается найти шлюз или шлюз не подготовлен.</span><span class="sxs-lookup"><span data-stu-id="97d38-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="97d38-174">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-174">No</span></span>|
| <span data-ttu-id="97d38-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="97d38-175">PlannedMaintenance</span></span> | <span data-ttu-id="97d38-176">Выполняется обслуживание экземпляра шлюза.</span><span class="sxs-lookup"><span data-stu-id="97d38-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="97d38-177">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-177">No</span></span>|
| <span data-ttu-id="97d38-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="97d38-178">UserDrivenUpdate</span></span> | <span data-ttu-id="97d38-179">Идет обновление, инициированное пользователем.</span><span class="sxs-lookup"><span data-stu-id="97d38-179">When a user update is in progress.</span></span> <span data-ttu-id="97d38-180">Это может быть операция изменения размера.</span><span class="sxs-lookup"><span data-stu-id="97d38-180">This could be a resize operation.</span></span>  | <span data-ttu-id="97d38-181">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-181">No</span></span> |
| <span data-ttu-id="97d38-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="97d38-182">VipUnResponsive</span></span> | <span data-ttu-id="97d38-183">Не удается связаться с первичным экземпляром шлюза.</span><span class="sxs-lookup"><span data-stu-id="97d38-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="97d38-184">Это происходит при сбое пробы работоспособности.</span><span class="sxs-lookup"><span data-stu-id="97d38-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="97d38-185">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-185">No</span></span> |
| <span data-ttu-id="97d38-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="97d38-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="97d38-187">Отсутствует конфигурация подключения.</span><span class="sxs-lookup"><span data-stu-id="97d38-187">Connection configuration is missing.</span></span> | <span data-ttu-id="97d38-188">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-188">No</span></span> |
| <span data-ttu-id="97d38-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="97d38-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="97d38-190">Подключение отмечено как "разъединенное".</span><span class="sxs-lookup"><span data-stu-id="97d38-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="97d38-191">Нет</span><span class="sxs-lookup"><span data-stu-id="97d38-191">No</span></span>|
| <span data-ttu-id="97d38-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="97d38-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="97d38-193">Для базовой службы не настроено подключение.</span><span class="sxs-lookup"><span data-stu-id="97d38-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="97d38-194">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-194">Yes</span></span> |
| <span data-ttu-id="97d38-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="97d38-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="97d38-196">Базовая служба помечена как ждущая.</span><span class="sxs-lookup"><span data-stu-id="97d38-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="97d38-197">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-197">Yes</span></span>|
| <span data-ttu-id="97d38-198">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="97d38-198">Authentication</span></span> | <span data-ttu-id="97d38-199">Несоответствие предварительного ключа.</span><span class="sxs-lookup"><span data-stu-id="97d38-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="97d38-200">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-200">Yes</span></span>|
| <span data-ttu-id="97d38-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="97d38-201">PeerReachability</span></span> | <span data-ttu-id="97d38-202">Одноранговый шлюз недоступен.</span><span class="sxs-lookup"><span data-stu-id="97d38-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="97d38-203">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-203">Yes</span></span>|
| <span data-ttu-id="97d38-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="97d38-204">IkePolicyMismatch</span></span> | <span data-ttu-id="97d38-205">У однорангового шлюза имеются политики IKE, которые не поддерживаются в Azure.</span><span class="sxs-lookup"><span data-stu-id="97d38-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="97d38-206">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-206">Yes</span></span>|
| <span data-ttu-id="97d38-207">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="97d38-207">WfpParse Error</span></span> | <span data-ttu-id="97d38-208">Ошибка при анализе журнала WFP.</span><span class="sxs-lookup"><span data-stu-id="97d38-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="97d38-209">Да</span><span class="sxs-lookup"><span data-stu-id="97d38-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="97d38-210">Поддерживаемые типы шлюзов</span><span class="sxs-lookup"><span data-stu-id="97d38-210">Supported Gateway types</span></span>

<span data-ttu-id="97d38-211">В следующем списке показано, какие шлюзы и подключения поддерживаются при устранении неполадок с наблюдателем за сетями.</span><span class="sxs-lookup"><span data-stu-id="97d38-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="97d38-212">**Типы шлюзов**</span><span class="sxs-lookup"><span data-stu-id="97d38-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="97d38-213">Виртуальная частная сеть</span><span class="sxs-lookup"><span data-stu-id="97d38-213">VPN</span></span>      | <span data-ttu-id="97d38-214">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="97d38-214">Supported</span></span>        |
|<span data-ttu-id="97d38-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="97d38-215">ExpressRoute</span></span> | <span data-ttu-id="97d38-216">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="97d38-216">Not Supported</span></span> |
|<span data-ttu-id="97d38-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="97d38-217">Hypernet</span></span> | <span data-ttu-id="97d38-218">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="97d38-218">Not Supported</span></span>|
|<span data-ttu-id="97d38-219">**Типы VPN**</span><span class="sxs-lookup"><span data-stu-id="97d38-219">**VPN types**</span></span> | |
|<span data-ttu-id="97d38-220">На основе маршрутов</span><span class="sxs-lookup"><span data-stu-id="97d38-220">Route Based</span></span> | <span data-ttu-id="97d38-221">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="97d38-221">Supported</span></span>|
|<span data-ttu-id="97d38-222">На основе политик</span><span class="sxs-lookup"><span data-stu-id="97d38-222">Policy Based</span></span> | <span data-ttu-id="97d38-223">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="97d38-223">Not Supported</span></span>|
|<span data-ttu-id="97d38-224">**Типы подключений**</span><span class="sxs-lookup"><span data-stu-id="97d38-224">**Connection types**</span></span>||
|<span data-ttu-id="97d38-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="97d38-225">IPSec</span></span>| <span data-ttu-id="97d38-226">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="97d38-226">Supported</span></span>|
|<span data-ttu-id="97d38-227">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="97d38-227">VNet2Vnet</span></span>| <span data-ttu-id="97d38-228">Поддерживаются</span><span class="sxs-lookup"><span data-stu-id="97d38-228">Supported</span></span>|
|<span data-ttu-id="97d38-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="97d38-229">ExpressRoute</span></span>| <span data-ttu-id="97d38-230">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="97d38-230">Not Supported</span></span>|
|<span data-ttu-id="97d38-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="97d38-231">Hypernet</span></span>| <span data-ttu-id="97d38-232">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="97d38-232">Not Supported</span></span>|
|<span data-ttu-id="97d38-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="97d38-233">VPNClient</span></span>| <span data-ttu-id="97d38-234">Не поддерживается</span><span class="sxs-lookup"><span data-stu-id="97d38-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="97d38-235">Файлы журналов</span><span class="sxs-lookup"><span data-stu-id="97d38-235">Log files</span></span>

<span data-ttu-id="97d38-236">После того, как устранение неполадок ресурсов завершено, файлы журнала устранения неполадок ресурсов сохраняются в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="97d38-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="97d38-237">На следующем рисунке приведен пример содержимого вызова, который завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="97d38-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![ZIP-файл][1]

> [!NOTE]
> <span data-ttu-id="97d38-239">В некоторых случаях только подмножество файлов журнала записывается в хранилище.</span><span class="sxs-lookup"><span data-stu-id="97d38-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="97d38-240">Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="97d38-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="97d38-241">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="97d38-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="97d38-242">Дополнительные сведения о Storage Explorer можно найти по следующей ссылке: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="97d38-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="97d38-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="97d38-243">ConnectionStats.txt</span></span>

<span data-ttu-id="97d38-244">Файл **ConnectionStats.txt** содержит общую статистику подключения, включая количество полученных и отправленных байтов, состояние подключения и время, когда подключение было установлено.</span><span class="sxs-lookup"><span data-stu-id="97d38-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="97d38-245">Если вызов к API устранения неполадок возвращает значение, указывающее на работоспособное состояние, то в ZIP-файле возвращается только файл **ConnectionStats.txt**.</span><span class="sxs-lookup"><span data-stu-id="97d38-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="97d38-246">Содержимое этого файла имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="97d38-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="97d38-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="97d38-247">CPUStats.txt</span></span>

<span data-ttu-id="97d38-248">Файл **CPUStats.txt** содержит данные об использовании ЦП и памяти, доступных во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="97d38-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="97d38-249">Пример содержимого этого файла приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="97d38-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="97d38-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="97d38-250">IKEErrors.txt</span></span>

<span data-ttu-id="97d38-251">Файл **IKEErrors.txt** содержит все ошибки протокола IKE, обнаруженные во время мониторинга.</span><span class="sxs-lookup"><span data-stu-id="97d38-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="97d38-252">В следующем примере показано содержимое файла IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="97d38-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="97d38-253">Ошибки могут быть разными в зависимости от проблемы.</span><span class="sxs-lookup"><span data-stu-id="97d38-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="97d38-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="97d38-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="97d38-255">Файл журнала **Scrubbed-wfpdiag.txt** содержит журнал WFP.</span><span class="sxs-lookup"><span data-stu-id="97d38-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="97d38-256">В этом журнале регистрируется удаление пакетов, а также сбои протокола IKE и AuthIP.</span><span class="sxs-lookup"><span data-stu-id="97d38-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="97d38-257">В следующем примере показано содержимое файла Scrubbed-wfpdiag.txt.</span><span class="sxs-lookup"><span data-stu-id="97d38-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="97d38-258">В данном примере общий ключ подключения неправилен, как видно в третьей строке снизу.</span><span class="sxs-lookup"><span data-stu-id="97d38-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="97d38-259">Ниже приведен только фрагмент журнала, так как журнал может быть большим, в зависимости от проблемы.</span><span class="sxs-lookup"><span data-stu-id="97d38-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="97d38-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="97d38-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="97d38-261">Файл **wfpdiag.txt.sum** — это журнал, содержащий информацию о буферах и обработанных событиях.</span><span class="sxs-lookup"><span data-stu-id="97d38-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="97d38-262">Ниже приведен пример содержимого файла wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="97d38-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="97d38-263">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97d38-263">Next steps</span></span>

<span data-ttu-id="97d38-264">Узнайте, как диагностировать VPN-шлюзы и подключения с помощью портала, посетив страницу [Устранение неполадок шлюза — портал Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="97d38-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
