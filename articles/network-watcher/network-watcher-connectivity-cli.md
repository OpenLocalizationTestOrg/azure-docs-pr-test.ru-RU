---
title: "подключение aaaCheck с Наблюдатель сети Azure — Azure CLI 2.0 | Документы Microsoft"
description: "На этой странице объясняется, как проверить подключение toouse с Наблюдатель сети с помощью Azure CLI 2.0"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="8195b-103">Проверка возможности подключения с помощью службы Azure "Наблюдатель за сетями" в Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8195b-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8195b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8195b-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="8195b-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8195b-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="8195b-106">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="8195b-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="8195b-107">Узнайте, как можно установить toouse tooverify подключения, если прямое подключение TCP от tooa виртуальной машины, заданный конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8195b-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8195b-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8195b-108">Before you begin</span></span>

<span data-ttu-id="8195b-109">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="8195b-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="8195b-110">Экземпляр Наблюдатель сети в регионе hello нужно toocheck подключения.</span><span class="sxs-lookup"><span data-stu-id="8195b-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="8195b-111">Виртуальные машины toocheck подключение.</span><span class="sxs-lookup"><span data-stu-id="8195b-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="8195b-112">Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="8195b-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="8195b-113">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="8195b-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="8195b-114">Регистрация возможностей предварительного просмотра hello</span><span class="sxs-lookup"><span data-stu-id="8195b-114">Register hello preview capability</span></span> 

<span data-ttu-id="8195b-115">Проверка возможности подключения находится в общедоступной предварительной версии, toouse эту функцию, он должен toobe зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="8195b-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="8195b-116">toodo, выполнения hello следующий образец CLI</span><span class="sxs-lookup"><span data-stu-id="8195b-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="8195b-117">tooverify hello регистрация прошла успешно, запустите следующую команду CLI hello:</span><span class="sxs-lookup"><span data-stu-id="8195b-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="8195b-118">Если функции hello был правильно зарегистрирован, hello выходных данных должно совпадать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8195b-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="8195b-119">Проверьте подключение tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8195b-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="8195b-120">В этом примере проверяется подключение tooa целевой виртуальной машине через порт 80.</span><span class="sxs-lookup"><span data-stu-id="8195b-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="8195b-121">Пример</span><span class="sxs-lookup"><span data-stu-id="8195b-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="8195b-122">Ответ</span><span class="sxs-lookup"><span data-stu-id="8195b-122">Response</span></span>

<span data-ttu-id="8195b-123">После ответа Hello — из предыдущего примера hello.</span><span class="sxs-lookup"><span data-stu-id="8195b-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="8195b-124">В данном ответе hello `ConnectionStatus` — **недостижимо**.</span><span class="sxs-lookup"><span data-stu-id="8195b-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="8195b-125">Вы увидите, что все hello Сбой отправки проб.</span><span class="sxs-lookup"><span data-stu-id="8195b-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="8195b-126">не удалось выполнить подключение Hello hello виртуального устройства из-за tooa настроенного пользователем `NetworkSecurityRule` с именем **UserRule_Port80**, настроен tooblock входящий трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="8195b-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="8195b-127">Эти сведения можно использовать tooresearch проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="8195b-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="8195b-128">Проверка проблем с маршрутизацией</span><span class="sxs-lookup"><span data-stu-id="8195b-128">Validate routing issues</span></span>

<span data-ttu-id="8195b-129">пример Hello проверяет подключение между виртуальной машиной и удаленной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="8195b-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="8195b-130">Пример</span><span class="sxs-lookup"><span data-stu-id="8195b-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="8195b-131">Ответ</span><span class="sxs-lookup"><span data-stu-id="8195b-131">Response</span></span>

<span data-ttu-id="8195b-132">В следующем примере hello, hello `connectionStatus` отображается как **недостижимо**.</span><span class="sxs-lookup"><span data-stu-id="8195b-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="8195b-133">В hello `hops` сведения, можно увидеть в разделе `issues` трафика hello заблокирована из-за tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="8195b-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="8195b-134">Проверка задержки веб-сайта</span><span class="sxs-lookup"><span data-stu-id="8195b-134">Check website latency</span></span>

<span data-ttu-id="8195b-135">Hello следующий пример проверяет веб-сайт tooa hello подключения.</span><span class="sxs-lookup"><span data-stu-id="8195b-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="8195b-136">Пример</span><span class="sxs-lookup"><span data-stu-id="8195b-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="8195b-137">Ответ</span><span class="sxs-lookup"><span data-stu-id="8195b-137">Response</span></span>

<span data-ttu-id="8195b-138">В следующих ответа hello, вы увидите hello `connectionStatus` показано, как **доступный**.</span><span class="sxs-lookup"><span data-stu-id="8195b-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="8195b-139">Когда подключение будет установлено, отобразятся значения задержки.</span><span class="sxs-lookup"><span data-stu-id="8195b-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="8195b-140">Проверьте подключение tooa конечную точку</span><span class="sxs-lookup"><span data-stu-id="8195b-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="8195b-141">Hello следующий пример проверяет подключение hello из виртуальной машины учетной записи хранения tooa блога.</span><span class="sxs-lookup"><span data-stu-id="8195b-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="8195b-142">Пример</span><span class="sxs-lookup"><span data-stu-id="8195b-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="8195b-143">Ответ</span><span class="sxs-lookup"><span data-stu-id="8195b-143">Response</span></span>

<span data-ttu-id="8195b-144">Hello следующий json-hello пример ответа из предыдущих командлета hello.</span><span class="sxs-lookup"><span data-stu-id="8195b-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="8195b-145">Здравствуйте, как hello проверка прошла успешно, `connectionStatus` показано, как свойство **доступный**.</span><span class="sxs-lookup"><span data-stu-id="8195b-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="8195b-146">Предоставляются hello детали hello число прыжков необходимые tooreach hello хранилища больших двоичных объектов и задержки.</span><span class="sxs-lookup"><span data-stu-id="8195b-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="8195b-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8195b-147">Next steps</span></span>

<span data-ttu-id="8195b-148">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="8195b-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="8195b-149">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8195b-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
