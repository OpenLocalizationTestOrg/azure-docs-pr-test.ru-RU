---
title: "Проверка подключения с помощью службы \"Наблюдатель за сетями\" Azure (Azure CLI 2.0) | Документация Майкрософт"
description: "На этой странице объясняется, как использовать проверку подключения с помощью службы \"Наблюдатель за сетями\" в интерфейсе командной строки Azure CLI 2.0"
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
ms.openlocfilehash: c1deaa40bfda0bf3858ad56d3d6a90df34351278
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="2247d-103">Проверка возможности подключения с помощью службы Azure "Наблюдатель за сетями" в Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2247d-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2247d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2247d-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="2247d-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2247d-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="2247d-106">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="2247d-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="2247d-107">Узнайте, как проверить возможность прямого подключения TCP между виртуальной машиной и определенной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="2247d-107">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2247d-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2247d-108">Before you begin</span></span>

<span data-ttu-id="2247d-109">В данной статье предполагается, что у вас есть следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="2247d-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="2247d-110">экземпляр службы "Наблюдатель за сетями" в регионе, в котором нужно проверить возможность подключения;</span><span class="sxs-lookup"><span data-stu-id="2247d-110">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="2247d-111">виртуальные машины, возможность подключения к которым необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="2247d-111">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="2247d-112">Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="2247d-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="2247d-113">Информацию об установке расширения для виртуальной машины Windows см. в статье [Расширение виртуальной машины агента Наблюдателя за сетями для Windows](../virtual-machines/windows/extensions-nwa.md), а для виртуальной машины Linux — в статье [Расширение виртуальной машины агента Наблюдателя за сетями для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="2247d-113">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="2247d-114">Регистрация возможностей предварительной версии</span><span class="sxs-lookup"><span data-stu-id="2247d-114">Register the preview capability</span></span> 

<span data-ttu-id="2247d-115">Проверка возможности подключения в настоящее время поддерживается в общедоступной предварительной версии. Для использования этой функции ее необходимо зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="2247d-115">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="2247d-116">Для этого выполните следующий пример команды в интерфейсе командной строки.</span><span class="sxs-lookup"><span data-stu-id="2247d-116">To do this, run the following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="2247d-117">Чтобы проверить, была ли регистрация успешно завершена, выполните приведенную ниже команду интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="2247d-117">To verify the registration was successful, run the following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="2247d-118">Если компонент был правильно зарегистрирован, выходные данные должны выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2247d-118">If the feature was properly registered, the output should match the following:</span></span> 

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

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="2247d-119">Проверка возможности подключения к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="2247d-119">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="2247d-120">В этом примере проверяется возможность подключения к целевой виртуальной машине через порт 80.</span><span class="sxs-lookup"><span data-stu-id="2247d-120">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="2247d-121">Пример</span><span class="sxs-lookup"><span data-stu-id="2247d-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="2247d-122">Ответ</span><span class="sxs-lookup"><span data-stu-id="2247d-122">Response</span></span>

<span data-ttu-id="2247d-123">Следующий ответ взят из предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="2247d-123">The following response is from the previous example.</span></span>  <span data-ttu-id="2247d-124">В этом ответе параметр `ConnectionStatus` имеет значение **Unreachable** (Недоступно).</span><span class="sxs-lookup"><span data-stu-id="2247d-124">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="2247d-125">Как видите, все отправленные пробы завершились неудачей.</span><span class="sxs-lookup"><span data-stu-id="2247d-125">You can see that all the probes sent failed.</span></span> <span data-ttu-id="2247d-126">Попытка подключения завершилась сбоем в виртуальном модуле из-за пользовательского правила `NetworkSecurityRule` с именем **UserRule_Port80**, настроенного на блокировку входящего трафика на порту 80.</span><span class="sxs-lookup"><span data-stu-id="2247d-126">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="2247d-127">Эти сведения можно использовать для анализа проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="2247d-127">This information can be used to research connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="2247d-128">Проверка проблем с маршрутизацией</span><span class="sxs-lookup"><span data-stu-id="2247d-128">Validate routing issues</span></span>

<span data-ttu-id="2247d-129">В этом примере проверяется возможность подключения между виртуальной машиной и удаленной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="2247d-129">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="2247d-130">Пример</span><span class="sxs-lookup"><span data-stu-id="2247d-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="2247d-131">Ответ</span><span class="sxs-lookup"><span data-stu-id="2247d-131">Response</span></span>

<span data-ttu-id="2247d-132">В следующем примере состояние `connectionStatus` отображается как **Unreachable** (Недоступно).</span><span class="sxs-lookup"><span data-stu-id="2247d-132">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="2247d-133">В блоке `hops` в разделе `issues` видно, что трафик заблокирован из-за `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="2247d-133">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="2247d-134">Проверка задержки веб-сайта</span><span class="sxs-lookup"><span data-stu-id="2247d-134">Check website latency</span></span>

<span data-ttu-id="2247d-135">В следующем примере проверяется возможность подключения к веб-сайту.</span><span class="sxs-lookup"><span data-stu-id="2247d-135">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="2247d-136">Пример</span><span class="sxs-lookup"><span data-stu-id="2247d-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="2247d-137">Ответ</span><span class="sxs-lookup"><span data-stu-id="2247d-137">Response</span></span>

<span data-ttu-id="2247d-138">В следующем ответе видно, что параметр `connectionStatus` отображается со значением **Reachable** (Достижимо).</span><span class="sxs-lookup"><span data-stu-id="2247d-138">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="2247d-139">Когда подключение будет установлено, отобразятся значения задержки.</span><span class="sxs-lookup"><span data-stu-id="2247d-139">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="2247d-140">Проверка возможности подключения к конечной точке хранилища</span><span class="sxs-lookup"><span data-stu-id="2247d-140">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="2247d-141">В следующем примере проверяется возможность подключения с виртуальной машины к учетной записи хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2247d-141">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="2247d-142">Пример</span><span class="sxs-lookup"><span data-stu-id="2247d-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="2247d-143">Ответ</span><span class="sxs-lookup"><span data-stu-id="2247d-143">Response</span></span>

<span data-ttu-id="2247d-144">JSON-код ниже — это пример ответа на предыдущий командлет.</span><span class="sxs-lookup"><span data-stu-id="2247d-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="2247d-145">Так как проверка выполнена успешно, свойство `connectionStatus` отображается со значением **Reachable** (Достижимо).</span><span class="sxs-lookup"><span data-stu-id="2247d-145">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="2247d-146">Также отображаются сведения о числе прыжков, необходимых для доступа к BLOB-объекту в хранилище, а также о задержке.</span><span class="sxs-lookup"><span data-stu-id="2247d-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2247d-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2247d-147">Next steps</span></span>

<span data-ttu-id="2247d-148">Дополнительные сведения об автоматизации записи пакетов с помощью оповещений на виртуальной машине см. в статье, посвященной [созданию записи пакетов, активируемой с использованием оповещений](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="2247d-148">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="2247d-149">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2247d-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
