---
title: "подключение aaaCheck с Наблюдатель сети Azure — PowerShell | Документы Microsoft"
description: "На этой странице объясняется способ подключения к tootest с Наблюдатель сети с помощью PowerShell"
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
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="56d94-103">Проверка возможности подключения с помощью службы "Наблюдатель за сетями Azure" в PowerShell</span><span class="sxs-lookup"><span data-stu-id="56d94-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="56d94-104">Портал</span><span class="sxs-lookup"><span data-stu-id="56d94-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="56d94-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56d94-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="56d94-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="56d94-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="56d94-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="56d94-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="56d94-108">Узнайте, как можно установить toouse tooverify подключения, если прямое подключение TCP от tooa виртуальной машины, заданный конечной точки.</span><span class="sxs-lookup"><span data-stu-id="56d94-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56d94-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="56d94-109">Before you begin</span></span>

<span data-ttu-id="56d94-110">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="56d94-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="56d94-111">Экземпляр Наблюдатель сети в регионе hello нужно toocheck подключения.</span><span class="sxs-lookup"><span data-stu-id="56d94-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="56d94-112">Виртуальные машины toocheck подключение.</span><span class="sxs-lookup"><span data-stu-id="56d94-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="56d94-113">Для проверки возможности подключения требуется расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="56d94-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="56d94-114">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="56d94-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="56d94-115">Регистрация возможностей предварительного просмотра hello</span><span class="sxs-lookup"><span data-stu-id="56d94-115">Register hello preview capability</span></span>

<span data-ttu-id="56d94-116">Подключение в данный момент общедоступной предварительной версии, toouse эту функцию, он должен toobe зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="56d94-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="56d94-117">toodo, выполнения hello следующий пример PowerShell:</span><span class="sxs-lookup"><span data-stu-id="56d94-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="56d94-118">tooverify hello регистрация прошла успешно, запустите следующий пример скрипта Powershell hello:</span><span class="sxs-lookup"><span data-stu-id="56d94-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="56d94-119">Если функции hello был правильно зарегистрирован, hello выходных данных должно совпадать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="56d94-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="56d94-120">Проверьте подключение tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="56d94-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="56d94-121">В этом примере проверяется подключение tooa целевой виртуальной машине через порт 80.</span><span class="sxs-lookup"><span data-stu-id="56d94-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="56d94-122">Пример</span><span class="sxs-lookup"><span data-stu-id="56d94-122">Example</span></span>

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

### <a name="response"></a><span data-ttu-id="56d94-123">Ответ</span><span class="sxs-lookup"><span data-stu-id="56d94-123">Response</span></span>

<span data-ttu-id="56d94-124">После ответа Hello — из предыдущего примера hello.</span><span class="sxs-lookup"><span data-stu-id="56d94-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="56d94-125">В данном ответе hello `ConnectionStatus` — **недостижимо**.</span><span class="sxs-lookup"><span data-stu-id="56d94-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="56d94-126">Вы увидите, что все hello Сбой отправки проб.</span><span class="sxs-lookup"><span data-stu-id="56d94-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="56d94-127">не удалось выполнить подключение Hello hello виртуального устройства из-за tooa настроенного пользователем `NetworkSecurityRule` с именем **UserRule_Port80**, настроен tooblock входящий трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="56d94-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="56d94-128">Эти сведения можно использовать tooresearch проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="56d94-128">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="56d94-129">Проверка проблем с маршрутизацией</span><span class="sxs-lookup"><span data-stu-id="56d94-129">Validate routing issues</span></span>

<span data-ttu-id="56d94-130">пример Hello проверяет подключение между виртуальной машиной и удаленной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="56d94-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="56d94-131">Пример</span><span class="sxs-lookup"><span data-stu-id="56d94-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="56d94-132">Ответ</span><span class="sxs-lookup"><span data-stu-id="56d94-132">Response</span></span>

<span data-ttu-id="56d94-133">В следующем примере hello, hello `ConnectionStatus` отображается как **недостижимо**.</span><span class="sxs-lookup"><span data-stu-id="56d94-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="56d94-134">В hello `Hops` сведения, можно увидеть в разделе `Issues` трафика hello заблокирована из-за tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="56d94-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

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

## <a name="check-website-latency"></a><span data-ttu-id="56d94-135">Проверка задержки веб-сайта</span><span class="sxs-lookup"><span data-stu-id="56d94-135">Check website latency</span></span>

<span data-ttu-id="56d94-136">Hello следующий пример проверяет веб-сайт tooa hello подключения.</span><span class="sxs-lookup"><span data-stu-id="56d94-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="56d94-137">Пример</span><span class="sxs-lookup"><span data-stu-id="56d94-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="56d94-138">Ответ</span><span class="sxs-lookup"><span data-stu-id="56d94-138">Response</span></span>

<span data-ttu-id="56d94-139">В следующих ответа hello, вы увидите hello `ConnectionStatus` показано, как **доступный**.</span><span class="sxs-lookup"><span data-stu-id="56d94-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="56d94-140">Когда подключение будет установлено, отобразятся значения задержки.</span><span class="sxs-lookup"><span data-stu-id="56d94-140">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="56d94-141">Проверьте подключение tooa конечную точку</span><span class="sxs-lookup"><span data-stu-id="56d94-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="56d94-142">Следующий пример Hello тестирует подключение hello из виртуальной машины учетной записи хранения tooa блога.</span><span class="sxs-lookup"><span data-stu-id="56d94-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="56d94-143">Пример</span><span class="sxs-lookup"><span data-stu-id="56d94-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="56d94-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="56d94-144">Response</span></span>

<span data-ttu-id="56d94-145">Hello следующий json-hello пример ответа из предыдущих командлета hello.</span><span class="sxs-lookup"><span data-stu-id="56d94-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="56d94-146">Здравствуйте, как назначение hello доступен, `ConnectionStatus` показано, как свойство **доступный**.</span><span class="sxs-lookup"><span data-stu-id="56d94-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="56d94-147">Предоставляются hello детали hello число прыжков необходимые tooreach hello хранилища больших двоичных объектов и задержки.</span><span class="sxs-lookup"><span data-stu-id="56d94-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="56d94-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56d94-148">Next steps</span></span>

<span data-ttu-id="56d94-149">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье, посвященной [проверке потока IP-адресов](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="56d94-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="56d94-150">Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.</span><span class="sxs-lookup"><span data-stu-id="56d94-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














