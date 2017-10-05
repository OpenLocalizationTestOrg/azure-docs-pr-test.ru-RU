---
title: "Устранение неполадок шлюза виртуальной сети и подключений с помощью Наблюдателя за сетями Azure (REST) | Документация Майкрософт"
description: "На этой странице объясняется, как в службе наблюдения за сетями Azure с помощью REST устранять неполадки шлюза виртуальной сети и подключений"
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="2ac0f-103">Устранение неполадок шлюза виртуальной сети и подключений, используя Наблюдатель за сетями Azure</span><span class="sxs-lookup"><span data-stu-id="2ac0f-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2ac0f-104">Портал</span><span class="sxs-lookup"><span data-stu-id="2ac0f-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="2ac0f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ac0f-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="2ac0f-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="2ac0f-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="2ac0f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2ac0f-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="2ac0f-108">REST API</span><span class="sxs-lookup"><span data-stu-id="2ac0f-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="2ac0f-109">Наблюдатель за сетями предоставляет множество возможностей, так как он позволяет проанализировать сетевые ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="2ac0f-110">Одна из этих возможностей — устранение неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="2ac0f-111">Процедуру устранения неполадок с ресурсами можно вызывать с помощью портала, PowerShell, интерфейса командной строки или API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="2ac0f-112">При вызове Наблюдатель за сетями проверяет работоспособность шлюза виртуальной сети или подключения и возвращает результаты.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="2ac0f-113">В этой статье вы ознакомитесь с разными задачами управления, доступными в настоящее время для устранения неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="2ac0f-114">**Устранение неполадок шлюза виртуальной сети**</span><span class="sxs-lookup"><span data-stu-id="2ac0f-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="2ac0f-115">**Устранение неполадок подключений**</span><span class="sxs-lookup"><span data-stu-id="2ac0f-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="2ac0f-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2ac0f-116">Before you begin</span></span>

<span data-ttu-id="2ac0f-117">Чтобы вызвать REST API при помощи PowerShell, потребуется ARMClient.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="2ac0f-118">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="2ac0f-119">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="2ac0f-120">Список поддерживаемых типов шлюзов см. в разделе [Поддерживаемые типы шлюзов](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="2ac0f-121">Обзор</span><span class="sxs-lookup"><span data-stu-id="2ac0f-121">Overview</span></span>

<span data-ttu-id="2ac0f-122">Средство устранения неполадок Наблюдатель за сетями позволяет устранить неполадки в работе шлюзов виртуальной сети и подключений.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="2ac0f-123">При запросе на устранение неполадок в ресурсах запрашиваются и проверяются журналы.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="2ac0f-124">По завершении проверки возвращаются результаты.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="2ac0f-125">Запросы к API устранения неполадок выполняются долго, поэтому для возвращения результатов может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="2ac0f-126">Журналы хранятся в контейнере учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="2ac0f-127">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="2ac0f-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="2ac0f-128">Устранение неполадок шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="2ac0f-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="2ac0f-129">Запрос POST на устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2ac0f-129">POST the troubleshoot request</span></span>

<span data-ttu-id="2ac0f-130">В следующем примере запрашивается состояние шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="2ac0f-131">Поскольку эта операция выполняется долго, URI для запроса операции и URI результата возвращаются в заголовке ответа, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="2ac0f-132">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="2ac0f-132">**Important Values**</span></span>

* <span data-ttu-id="2ac0f-133">**Azure-AsyncOperation** (Асинхронная операция Azure) — это свойство содержит URI для запроса асинхронной операции устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="2ac0f-134">**Location** (Расположение) — это свойство содержит универсальный код ресурса (URI), где находятся результаты после выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="2ac0f-135">Запрос на выполнение асинхронной операции</span><span class="sxs-lookup"><span data-stu-id="2ac0f-135">Query the async operation for completion</span></span>

<span data-ttu-id="2ac0f-136">Используйте URI операций, чтобы запросить ход выполнения операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="2ac0f-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="2ac0f-137">Во время выполнения операции ответ показывает состояние **InProgress** (Выполняется), как видно в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="2ac0f-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="2ac0f-138">После завершения операции состояние изменится на **Succeeded** (Успешно).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="2ac0f-139">Получение результатов</span><span class="sxs-lookup"><span data-stu-id="2ac0f-139">Retrieve the results</span></span>

<span data-ttu-id="2ac0f-140">После того как возвратится состояние **Succeeded**, вызовите метод GET на URI operationResult, чтобы получить результаты.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="2ac0f-141">Следующие ответы являются примерами стандартного ограниченного ответа, который возвращается при запросе результатов устранения неполадок шлюза.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="2ac0f-142">См. раздел [Анализ результатов](#understanding-the-results), чтобы понять значения свойств в ответе.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="2ac0f-143">Устранение неполадок подключений</span><span class="sxs-lookup"><span data-stu-id="2ac0f-143">Troubleshoot Connections</span></span>

<span data-ttu-id="2ac0f-144">В следующем примере запрашивается состояние подключения.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="2ac0f-145">Невозможно запустить операцию устранения неполадок подключения и соответствующих шлюзов в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="2ac0f-146">Прежде чем запускать операцию, необходимо дождаться завершения ее выполнения для предыдущего ресурса.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="2ac0f-147">Поскольку эта операция выполняется долго, в заголовке ответа возвращаются URI для запроса операции и URI результата, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="2ac0f-148">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="2ac0f-148">**Important Values**</span></span>

* <span data-ttu-id="2ac0f-149">**Azure-AsyncOperation** (Асинхронная операция Azure) — это свойство содержит URI для запроса асинхронной операции устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="2ac0f-150">**Location** (Расположение) — это свойство содержит универсальный код ресурса (URI), где находятся результаты после выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="2ac0f-151">Запрос на выполнение асинхронной операции</span><span class="sxs-lookup"><span data-stu-id="2ac0f-151">Query the async operation for completion</span></span>

<span data-ttu-id="2ac0f-152">Используйте URI операций, чтобы запросить ход выполнения операции, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="2ac0f-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="2ac0f-153">Во время выполнения операции ответ показывает состояние **InProgress** (Выполняется), как видно в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="2ac0f-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="2ac0f-154">После завершения операции состояние изменится на **Succeeded** (Успешно).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="2ac0f-155">Следующие ответы являются примерами стандартного ответа, который возвращается при запросе результатов устранения неполадок подключения.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="2ac0f-156">Получение результатов</span><span class="sxs-lookup"><span data-stu-id="2ac0f-156">Retrieve the results</span></span>

<span data-ttu-id="2ac0f-157">После того как возвратится состояние **Succeeded**, вызовите метод GET на URI operationResult, чтобы получить результаты.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="2ac0f-158">Следующие ответы являются примерами стандартного ответа, который возвращается при запросе результатов устранения неполадок подключения.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="2ac0f-159">Анализ результатов</span><span class="sxs-lookup"><span data-stu-id="2ac0f-159">Understanding the results</span></span>

<span data-ttu-id="2ac0f-160">Текст действий содержит общие рекомендации по устранению проблемы.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="2ac0f-161">Если для устранения проблемы можно что-то сделать, предоставляется ссылка на дополнительные инструкции.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="2ac0f-162">Если дополнительных рекомендаций нет, в ответе указывается URL-адрес, открыв который можно отправить запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="2ac0f-163">Дополнительные сведения о свойствах ответа, а также о данных, которые он содержит, см. в статье [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md) (Обзор устранения неполадок наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="2ac0f-164">Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="2ac0f-165">Кроме того, можно использовать такое средство, как Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="2ac0f-166">Дополнительные сведения об обозревателе хранилищ см. на [этой странице](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="2ac0f-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ac0f-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ac0f-167">Next steps</span></span>

<span data-ttu-id="2ac0f-168">Если изменены параметры, которые мешают VPN-подключению, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md), чтобы найти сведения о группах безопасности сети и соответствующие правила безопасности.</span><span class="sxs-lookup"><span data-stu-id="2ac0f-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
