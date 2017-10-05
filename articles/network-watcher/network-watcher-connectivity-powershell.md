---
title: "Проверка возможности подключения с помощью службы \"Наблюдатель за сетями Azure\" в PowerShell | Документация Майкрософт"
description: "На этой странице объясняется, как проверить возможность подключения с помощью службы \"Наблюдатель за сетями\" в PowerShell"
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
ms.openlocfilehash: a8f936cd23838759dc30b04688d3c6544e4895cc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="9bade-103">Проверка возможности подключения с помощью службы "Наблюдатель за сетями Azure" в PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bade-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9bade-104">Портал</span><span class="sxs-lookup"><span data-stu-id="9bade-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="9bade-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bade-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="9bade-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9bade-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="9bade-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="9bade-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="9bade-108">Узнайте, как проверить возможность прямого подключения TCP между виртуальной машиной и определенной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="9bade-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9bade-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9bade-109">Before you begin</span></span>

<span data-ttu-id="9bade-110">В данной статье предполагается, что у вас есть следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="9bade-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="9bade-111">экземпляр службы "Наблюдатель за сетями" в регионе, в котором нужно проверить возможность подключения;</span><span class="sxs-lookup"><span data-stu-id="9bade-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="9bade-112">виртуальные машины, возможность подключения к которым необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="9bade-112">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="9bade-113">Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="9bade-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="9bade-114">Информацию об установке расширения для виртуальной машины Windows см. в статье [Расширение виртуальной машины агента Наблюдателя за сетями для Windows](../virtual-machines/windows/extensions-nwa.md), а для виртуальной машины Linux — в статье [Расширение виртуальной машины агента Наблюдателя за сетями для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="9bade-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="9bade-115">Регистрация возможностей предварительной версии</span><span class="sxs-lookup"><span data-stu-id="9bade-115">Register the preview capability</span></span>

<span data-ttu-id="9bade-116">Возможность подключения сейчас поддерживается в общедоступной предварительной версии. Для использования этой функции компонент необходимо зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="9bade-116">Connectivity is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="9bade-117">Для этого выполните следующие командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bade-117">To do this, run the following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="9bade-118">Чтобы проверить, была ли регистрация успешно завершена, выполните приведенный ниже командлет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bade-118">To verify the registration was successful, run the following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="9bade-119">Если компонент был правильно зарегистрирован, выходные данные должны выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9bade-119">If the feature was properly registered, the output should match the following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="9bade-120">Проверка возможности подключения к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="9bade-120">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="9bade-121">В этом примере проверяется возможность подключения к целевой виртуальной машине через порт 80.</span><span class="sxs-lookup"><span data-stu-id="9bade-121">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="9bade-122">Пример</span><span class="sxs-lookup"><span data-stu-id="9bade-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="9bade-123">Ответ</span><span class="sxs-lookup"><span data-stu-id="9bade-123">Response</span></span>

<span data-ttu-id="9bade-124">Следующий ответ взят из предыдущего примера.</span><span class="sxs-lookup"><span data-stu-id="9bade-124">The following response is from the previous example.</span></span>  <span data-ttu-id="9bade-125">В этом ответе параметр `ConnectionStatus` имеет значение **Unreachable** (Недоступно).</span><span class="sxs-lookup"><span data-stu-id="9bade-125">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="9bade-126">Как видите, все отправленные пробы завершились неудачей.</span><span class="sxs-lookup"><span data-stu-id="9bade-126">You can see that all the probes sent failed.</span></span> <span data-ttu-id="9bade-127">Попытка подключения завершилась сбоем в виртуальном модуле из-за пользовательского правила `NetworkSecurityRule` с именем **UserRule_Port80**, настроенного на блокировку входящего трафика на порту 80.</span><span class="sxs-lookup"><span data-stu-id="9bade-127">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="9bade-128">Эти сведения можно использовать для анализа проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="9bade-128">This information can be used to research connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="9bade-129">Проверка проблем с маршрутизацией</span><span class="sxs-lookup"><span data-stu-id="9bade-129">Validate routing issues</span></span>

<span data-ttu-id="9bade-130">В этом примере проверяется возможность подключения между виртуальной машиной и удаленной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="9bade-130">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="9bade-131">Пример</span><span class="sxs-lookup"><span data-stu-id="9bade-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="9bade-132">Ответ</span><span class="sxs-lookup"><span data-stu-id="9bade-132">Response</span></span>

<span data-ttu-id="9bade-133">В следующем примере состояние `ConnectionStatus` отображается как **Unreachable** (Недоступно).</span><span class="sxs-lookup"><span data-stu-id="9bade-133">In the following example, the `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="9bade-134">В блоке `Hops` в разделе `Issues` видно, что трафик заблокирован из-за `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="9bade-134">In the `Hops` details, you can see under `Issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="9bade-135">Проверка задержки веб-сайта</span><span class="sxs-lookup"><span data-stu-id="9bade-135">Check website latency</span></span>

<span data-ttu-id="9bade-136">В следующем примере проверяется возможность подключения к веб-сайту.</span><span class="sxs-lookup"><span data-stu-id="9bade-136">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="9bade-137">Пример</span><span class="sxs-lookup"><span data-stu-id="9bade-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="9bade-138">Ответ</span><span class="sxs-lookup"><span data-stu-id="9bade-138">Response</span></span>

<span data-ttu-id="9bade-139">В следующем ответе видно, что параметр `ConnectionStatus` отображается со значением **Reachable** (Достижимо).</span><span class="sxs-lookup"><span data-stu-id="9bade-139">In the following response, you can see the `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="9bade-140">Когда подключение будет установлено, отобразятся значения задержки.</span><span class="sxs-lookup"><span data-stu-id="9bade-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="9bade-141">Проверка возможности подключения к конечной точке хранилища</span><span class="sxs-lookup"><span data-stu-id="9bade-141">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="9bade-142">В следующем примере проверяется возможность подключения между виртуальной машиной и учетной записью хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="9bade-142">The following example tests the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="9bade-143">Пример</span><span class="sxs-lookup"><span data-stu-id="9bade-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="9bade-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="9bade-144">Response</span></span>

<span data-ttu-id="9bade-145">JSON-код ниже — это пример ответа на предыдущий командлет.</span><span class="sxs-lookup"><span data-stu-id="9bade-145">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="9bade-146">Так как назначение доступно, для свойства `ConnectionStatus` отображается значение **Reachable** (Доступно).</span><span class="sxs-lookup"><span data-stu-id="9bade-146">As the destination is reachable, the `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="9bade-147">Также отображаются сведения о числе прыжков, необходимых для доступа к BLOB-объекту в хранилище, а также о задержке.</span><span class="sxs-lookup"><span data-stu-id="9bade-147">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="9bade-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bade-148">Next steps</span></span>

<span data-ttu-id="9bade-149">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9bade-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="9bade-150">Если трафик блокируется, чего не должно быть, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md). В ней содержатся сведения об отслеживании группы безопасности сети и определенных правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="9bade-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<!-- Image references -->














