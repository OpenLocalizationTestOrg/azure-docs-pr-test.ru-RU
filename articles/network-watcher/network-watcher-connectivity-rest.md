---
title: "подключение aaaCheck с Наблюдатель сети Azure — портал Azure | Документы Microsoft"
description: "На этой странице объясняется, как toocheck подключения с Наблюдатель сети в hello портал Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="18f32-103">Убедитесь в наличии подключения с Наблюдатель сети Azure с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="18f32-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="18f32-104">Портал</span><span class="sxs-lookup"><span data-stu-id="18f32-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="18f32-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18f32-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="18f32-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="18f32-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="18f32-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="18f32-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="18f32-108">Узнайте, как можно установить toouse tooverify подключения, если прямое подключение TCP от tooa виртуальной машины, заданный конечной точки.</span><span class="sxs-lookup"><span data-stu-id="18f32-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="18f32-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="18f32-109">Before you begin</span></span>

<span data-ttu-id="18f32-110">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="18f32-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="18f32-111">Экземпляр Наблюдатель сети в регионе hello нужно toocheck подключения.</span><span class="sxs-lookup"><span data-stu-id="18f32-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="18f32-112">Виртуальные машины toocheck подключение.</span><span class="sxs-lookup"><span data-stu-id="18f32-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="18f32-113">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18f32-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="18f32-114">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="18f32-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="18f32-115">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="18f32-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="18f32-116">Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="18f32-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="18f32-117">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="18f32-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="18f32-118">Регистрация возможностей предварительного просмотра hello</span><span class="sxs-lookup"><span data-stu-id="18f32-118">Register hello preview capability</span></span>

<span data-ttu-id="18f32-119">Проверка возможности подключения находится в общедоступной предварительной версии, toouse эту функцию, он должен toobe зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="18f32-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="18f32-120">toodo, выполнения hello следующий пример PowerShell:</span><span class="sxs-lookup"><span data-stu-id="18f32-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="18f32-121">tooverify hello регистрация прошла успешно, запустите следующий пример скрипта Powershell hello:</span><span class="sxs-lookup"><span data-stu-id="18f32-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="18f32-122">Если функции hello был правильно зарегистрирован, hello выходных данных должно совпадать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="18f32-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="18f32-123">Вход с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="18f32-123">Log in with ARMClient</span></span>

<span data-ttu-id="18f32-124">Войдите в tooarmclient с учетными данными Azure.</span><span class="sxs-lookup"><span data-stu-id="18f32-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="18f32-125">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="18f32-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="18f32-126">Запустите следующий сценарий tooreturn hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="18f32-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="18f32-127">Эти сведения потребуются для подключения.</span><span class="sxs-lookup"><span data-stu-id="18f32-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="18f32-128">После кода Hello необходимые значения для hello следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="18f32-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="18f32-129">**subscriptionId** -hello toouse идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="18f32-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="18f32-130">**resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="18f32-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="18f32-131">Из hello следующие выходные данные, идентификатор hello hello виртуальной машины используется в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="18f32-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="18f32-132">Проверьте подключение tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="18f32-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="18f32-133">В этом примере проверяется подключение tooa целевой виртуальной машине через порт 80.</span><span class="sxs-lookup"><span data-stu-id="18f32-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="18f32-134">Пример</span><span class="sxs-lookup"><span data-stu-id="18f32-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="18f32-135">Так как эта операция имеет большую длину под управлением hello URI для hello результат возвращается в заголовок ответа hello как показано в hello после ответа:</span><span class="sxs-lookup"><span data-stu-id="18f32-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="18f32-136">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="18f32-136">**Important Values**</span></span>

* <span data-ttu-id="18f32-137">**Расположение** -это свойство содержит hello URI, где hello при результаты становятся hello операция завершена</span><span class="sxs-lookup"><span data-stu-id="18f32-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="18f32-138">Ответ</span><span class="sxs-lookup"><span data-stu-id="18f32-138">Response</span></span>

<span data-ttu-id="18f32-139">После ответа Hello — из предыдущего примера hello.</span><span class="sxs-lookup"><span data-stu-id="18f32-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="18f32-140">В данном ответе hello `ConnectionStatus` — **недостижимо**.</span><span class="sxs-lookup"><span data-stu-id="18f32-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="18f32-141">Вы увидите, что все hello Сбой отправки проб.</span><span class="sxs-lookup"><span data-stu-id="18f32-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="18f32-142">не удалось выполнить подключение Hello hello виртуального устройства из-за tooa настроенного пользователем `NetworkSecurityRule` с именем **UserRule_Port80**, настроен tooblock входящий трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="18f32-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="18f32-143">Эти сведения можно использовать tooresearch проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="18f32-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="18f32-144">Проверка проблем с маршрутизацией</span><span class="sxs-lookup"><span data-stu-id="18f32-144">Validate routing issues</span></span>

<span data-ttu-id="18f32-145">пример Hello проверяет подключение между виртуальной машиной и удаленной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="18f32-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="18f32-146">Пример</span><span class="sxs-lookup"><span data-stu-id="18f32-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="18f32-147">Так как эта операция имеет большую длину под управлением hello URI для hello результат возвращается в заголовок ответа hello как показано в hello после ответа:</span><span class="sxs-lookup"><span data-stu-id="18f32-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="18f32-148">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="18f32-148">**Important Values**</span></span>

* <span data-ttu-id="18f32-149">**Расположение** -это свойство содержит hello URI, где hello при результаты становятся hello операция завершена</span><span class="sxs-lookup"><span data-stu-id="18f32-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="18f32-150">Ответ</span><span class="sxs-lookup"><span data-stu-id="18f32-150">Response</span></span>

<span data-ttu-id="18f32-151">В следующем примере hello, hello `connectionStatus` отображается как **недостижимо**.</span><span class="sxs-lookup"><span data-stu-id="18f32-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="18f32-152">В hello `hops` сведения, можно увидеть в разделе `issues` трафика hello заблокирована из-за tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="18f32-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="18f32-153">Проверка задержки веб-сайта</span><span class="sxs-lookup"><span data-stu-id="18f32-153">Check website latency</span></span>

<span data-ttu-id="18f32-154">Hello следующий пример проверяет веб-сайт tooa hello подключения.</span><span class="sxs-lookup"><span data-stu-id="18f32-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="18f32-155">Пример</span><span class="sxs-lookup"><span data-stu-id="18f32-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="18f32-156">Так как эта операция имеет большую длину под управлением hello URI для hello результат возвращается в заголовок ответа hello как показано в hello после ответа:</span><span class="sxs-lookup"><span data-stu-id="18f32-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="18f32-157">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="18f32-157">**Important Values**</span></span>

* <span data-ttu-id="18f32-158">**Расположение** -это свойство содержит hello URI, где hello при результаты становятся hello операция завершена</span><span class="sxs-lookup"><span data-stu-id="18f32-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="18f32-159">Ответ</span><span class="sxs-lookup"><span data-stu-id="18f32-159">Response</span></span>

<span data-ttu-id="18f32-160">В следующих ответа hello, вы увидите hello `connectionStatus` показано, как **доступный**.</span><span class="sxs-lookup"><span data-stu-id="18f32-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="18f32-161">Когда подключение будет установлено, отобразятся значения задержки.</span><span class="sxs-lookup"><span data-stu-id="18f32-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="18f32-162">Проверьте подключение tooa конечную точку</span><span class="sxs-lookup"><span data-stu-id="18f32-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="18f32-163">Hello следующий пример проверяет подключение hello из виртуальной машины учетной записи хранения tooa блога.</span><span class="sxs-lookup"><span data-stu-id="18f32-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="18f32-164">Пример</span><span class="sxs-lookup"><span data-stu-id="18f32-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="18f32-165">Так как эта операция имеет большую длину под управлением hello URI для hello результат возвращается в заголовок ответа hello как показано в hello после ответа:</span><span class="sxs-lookup"><span data-stu-id="18f32-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="18f32-166">**Важные значения**</span><span class="sxs-lookup"><span data-stu-id="18f32-166">**Important Values**</span></span>

* <span data-ttu-id="18f32-167">**Расположение** -это свойство содержит hello URI, где hello при результаты становятся hello операция завершена</span><span class="sxs-lookup"><span data-stu-id="18f32-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="18f32-168">Ответ</span><span class="sxs-lookup"><span data-stu-id="18f32-168">Response</span></span>

<span data-ttu-id="18f32-169">Hello следующий пример — ответ hello запуск hello предыдущего вызова API.</span><span class="sxs-lookup"><span data-stu-id="18f32-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="18f32-170">Здравствуйте, как hello проверка прошла успешно, `connectionStatus` показано, как свойство **доступный**.</span><span class="sxs-lookup"><span data-stu-id="18f32-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="18f32-171">Предоставляются hello детали hello число прыжков необходимые tooreach hello хранилища больших двоичных объектов и задержки.</span><span class="sxs-lookup"><span data-stu-id="18f32-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="18f32-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18f32-172">Next steps</span></span>

<span data-ttu-id="18f32-173">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="18f32-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="18f32-174">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18f32-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














