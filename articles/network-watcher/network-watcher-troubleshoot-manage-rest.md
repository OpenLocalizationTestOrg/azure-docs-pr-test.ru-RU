---
title: "aaaTroubleshoot шлюз виртуальной сети и подключения с помощью Наблюдатель сети Azure - REST | Документы Microsoft"
description: "На этой странице объясняется, как tootroubleshoot шлюзах виртуальной сети и подключения с помощью Наблюдатель сети Azure REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="2f1a8-103">Устранение неполадок шлюза виртуальной сети и подключений, используя Наблюдатель за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="2f1a8-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2f1a8-104">Портал</span><span class="sxs-lookup"><span data-stu-id="2f1a8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="2f1a8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f1a8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="2f1a8-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="2f1a8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="2f1a8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2f1a8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="2f1a8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="2f1a8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="2f1a8-109">Наблюдатель сети предоставляет множество возможностей, по отношению к сетевым ресурсам в Azure toounderstanding.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="2f1a8-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="2f1a8-111">Устранение неполадок ресурсов можно вызвать через портал hello, PowerShell, CLI или REST API.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="2f1a8-112">При вызове Наблюдатель сети проверяет работоспособность hello шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="2f1a8-113">В этой статье описывается hello различными задачами управления, доступных в данный момент сведения об устранении неполадок ресурса.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="2f1a8-114">**Устранение неполадок шлюза виртуальной сети**</span><span class="sxs-lookup"><span data-stu-id="2f1a8-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="2f1a8-115">**Устранение неполадок подключений**</span><span class="sxs-lookup"><span data-stu-id="2f1a8-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="2f1a8-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2f1a8-116">Before you begin</span></span>

<span data-ttu-id="2f1a8-117">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="2f1a8-118">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="2f1a8-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="2f1a8-119">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="2f1a8-120">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="2f1a8-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="2f1a8-121">Обзор</span><span class="sxs-lookup"><span data-stu-id="2f1a8-121">Overview</span></span>

<span data-ttu-id="2f1a8-122">Устранение неполадок Наблюдатель сети предоставляет возможность hello Устранение неполадок, возникающих со шлюзами виртуальной сети и подключения.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="2f1a8-123">При запросе ресурсов toohello Устранение неполадок, журналы запросов и проверен.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="2f1a8-124">После завершения проверки hello результатов.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="2f1a8-125">Hello устранения API запросов являются длинными выполняемых запросов, это может занять несколько минут tooreturn результат.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="2f1a8-126">Журналы хранятся в контейнере учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="2f1a8-127">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="2f1a8-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="2f1a8-128">Устранение неполадок шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="2f1a8-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="2f1a8-129">POST hello Диагностика запроса</span><span class="sxs-lookup"><span data-stu-id="2f1a8-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="2f1a8-130">Здравствуйте, следующий пример запросов hello состояние шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="2f1a8-131">Так как эта операция велика запущен, hello URI для выполнения запросов к операции hello и hello URI для hello результат возвращается в заголовке ответа hello, как показано в hello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="2f1a8-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="2f1a8-132">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="2f1a8-132">**Important Values**</span></span>

* <span data-ttu-id="2f1a8-133">**Azure AsyncOperation** -это свойство содержит hello URI tooquery hello Async Устранение неполадок с операцией</span><span class="sxs-lookup"><span data-stu-id="2f1a8-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="2f1a8-134">**Расположение** -это свойство содержит hello URI, где hello при результаты становятся hello операция завершена</span><span class="sxs-lookup"><span data-stu-id="2f1a8-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="2f1a8-135">Hello асинхронные операции для завершения запроса</span><span class="sxs-lookup"><span data-stu-id="2f1a8-135">Query hello async operation for completion</span></span>

<span data-ttu-id="2f1a8-136">Введите URI tooquery hello операций hello ход выполнения операции hello в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="2f1a8-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="2f1a8-137">Во время операции hello hello показан ответ **InProgress** как видно в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="2f1a8-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="2f1a8-138">Операция hello при изменениях состояния завершения hello слишком**успешно**.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="2f1a8-139">Получить результаты hello</span><span class="sxs-lookup"><span data-stu-id="2f1a8-139">Retrieve hello results</span></span>

<span data-ttu-id="2f1a8-140">Когда возвращается состояние hello **успешно**, на hello operationResult URI tooretrieve hello результаты вызова метод GET.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="2f1a8-141">Hello следующие ответы приведены примеры типичных ограниченной ответ возвращается, если запрос к результатам hello устранения неполадок шлюза.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="2f1a8-142">В разделе [основные сведения о результатах hello](#understanding-the-results) tooget разъяснение к какие свойства hello в ответ означают hello.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="2f1a8-143">Устранение неполадок подключений</span><span class="sxs-lookup"><span data-stu-id="2f1a8-143">Troubleshoot Connections</span></span>

<span data-ttu-id="2f1a8-144">Следующий пример запросов hello состояние соединения Hello.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-144">hello following example queries hello status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> <span data-ttu-id="2f1a8-145">Устранение неполадок с операцией для Hello не может выполняться параллельно на подключение и его соответствующие шлюзов.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="2f1a8-146">Hello операция должна быть завершена предыдущих toorunning ее на предыдущий ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="2f1a8-147">Так как это долго выполняющаяся транзакция, в заголовке ответа hello, hello URI для выполнения запросов к операции hello и hello URI для hello результат возвращается как показано в hello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="2f1a8-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="2f1a8-148">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="2f1a8-148">**Important Values**</span></span>

* <span data-ttu-id="2f1a8-149">**Azure AsyncOperation** -это свойство содержит hello URI tooquery hello Async Устранение неполадок с операцией</span><span class="sxs-lookup"><span data-stu-id="2f1a8-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="2f1a8-150">**Расположение** -это свойство содержит hello URI, где hello при результаты становятся hello операция завершена</span><span class="sxs-lookup"><span data-stu-id="2f1a8-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="2f1a8-151">Hello асинхронные операции для завершения запроса</span><span class="sxs-lookup"><span data-stu-id="2f1a8-151">Query hello async operation for completion</span></span>

<span data-ttu-id="2f1a8-152">Введите URI tooquery hello операций hello ход выполнения операции hello в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="2f1a8-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="2f1a8-153">Во время операции hello hello показан ответ **InProgress** как видно в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="2f1a8-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="2f1a8-154">По завершении операции hello hello состояние изменяется слишком**успешно**.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="2f1a8-155">Hello следующие ответы приведены примеры типичных ответ возвращается, если запрос к результатам hello Устранение неполадок при подключении.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="2f1a8-156">Получить результаты hello</span><span class="sxs-lookup"><span data-stu-id="2f1a8-156">Retrieve hello results</span></span>

<span data-ttu-id="2f1a8-157">Когда возвращается состояние hello **успешно**, на hello operationResult URI tooretrieve hello результаты вызова метод GET.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="2f1a8-158">Hello следующие ответы приведены примеры типичных ответ возвращается, если запрос к результатам hello Устранение неполадок при подключении.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a><span data-ttu-id="2f1a8-159">Основные сведения о результатах hello</span><span class="sxs-lookup"><span data-stu-id="2f1a8-159">Understanding hello results</span></span>

<span data-ttu-id="2f1a8-160">текст Hello действия даются общие рекомендации по как tooresolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="2f1a8-161">Если действие может устранить проблему hello, ссылка предоставляется с Дополнительные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="2f1a8-162">В случае hello которых нет Дополнительные рекомендации, ответ hello предоставляет tooopen URL-адрес hello обращение в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="2f1a8-163">Дополнительные сведения о свойствах hello ответа hello и которые не включены [Общие сведения об устранении Наблюдатель сети](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2f1a8-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="2f1a8-164">Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="2f1a8-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="2f1a8-165">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="2f1a8-166">Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="2f1a8-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f1a8-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f1a8-167">Next steps</span></span>

<span data-ttu-id="2f1a8-168">Если параметры были изменены, остановите подключения VPN, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, возможно, в вопросе.</span><span class="sxs-lookup"><span data-stu-id="2f1a8-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
