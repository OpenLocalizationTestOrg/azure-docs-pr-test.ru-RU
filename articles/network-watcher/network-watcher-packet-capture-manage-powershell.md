---
title: "снимки aaaManage пакетов с Наблюдатель сети Azure — PowerShell | Документы Microsoft"
description: "На этой странице объясняется, как пакет приветствия toomanage захвата функция Наблюдатель сети с помощью PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="45d1a-103">Управление записью пакетов с помощью Наблюдателя за сетями Azure в PowerShell</span><span class="sxs-lookup"><span data-stu-id="45d1a-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="45d1a-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="45d1a-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="45d1a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45d1a-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="45d1a-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="45d1a-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="45d1a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="45d1a-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="45d1a-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="45d1a-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="45d1a-109">Захват пакетов Наблюдатель сети позволяет tooand toocreate отслеживания сеансов tootrack трафик от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="45d1a-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="45d1a-110">Можно записать только трафик hello нужные фильтры предоставляются для tooensure сеанс отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="45d1a-111">Захват пакетов помогает аномалий toodiagnose сети как реактивный, так и заранее.</span><span class="sxs-lookup"><span data-stu-id="45d1a-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="45d1a-112">Другим пользователям включать сбор статистики сети, получение сведений о сети вторжений, toodebug клиент сервер, связи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="45d1a-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="45d1a-113">Из-за захват пакетов может tooremotely триггера, эта возможность облегчает нагрузку hello выполнения захват пакетов на нужный машины hello, чтобы экономить время и вручную.</span><span class="sxs-lookup"><span data-stu-id="45d1a-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="45d1a-114">В этой статье описывается hello задачи управления, которые в настоящее время доступны для получения пакетов.</span><span class="sxs-lookup"><span data-stu-id="45d1a-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="45d1a-115">**Запуск записи пакета**</span><span class="sxs-lookup"><span data-stu-id="45d1a-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="45d1a-116">**Прекращение записи пакета**</span><span class="sxs-lookup"><span data-stu-id="45d1a-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="45d1a-117">**Удаление записи пакета**</span><span class="sxs-lookup"><span data-stu-id="45d1a-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="45d1a-118">**Скачивание записи пакета**</span><span class="sxs-lookup"><span data-stu-id="45d1a-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="45d1a-119">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="45d1a-119">Before you begin</span></span>

<span data-ttu-id="45d1a-120">В этой статье предполагается, что hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="45d1a-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="45d1a-121">Экземпляр Наблюдатель сети в регионе hello нужно toocreate захват пакетов</span><span class="sxs-lookup"><span data-stu-id="45d1a-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="45d1a-122">Виртуальная машина с пакет приветствия записать расширение включено.</span><span class="sxs-lookup"><span data-stu-id="45d1a-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45d1a-123">Для записи пакетов необходимо расширение виртуальной машины `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="45d1a-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="45d1a-124">Установка расширения hello на виртуальной Машине Windows на сайте [расширение виртуальной машины агента Наблюдатель сети Azure для Windows](../virtual-machines/windows/extensions-nwa.md) и виртуальной Машине Linux см. по адресу [расширение виртуальной машины агента Наблюдатель сети Azure для Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="45d1a-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="45d1a-125">Установка расширения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="45d1a-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="45d1a-126">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="45d1a-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="45d1a-127">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="45d1a-127">Step 2</span></span>

<span data-ttu-id="45d1a-128">Hello следующий пример извлекает hello сведений о расширении необходимости toorun hello `Set-AzureRmVMExtension` командлета.</span><span class="sxs-lookup"><span data-stu-id="45d1a-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="45d1a-129">Этот командлет устанавливает на hello гостевой виртуальной машине агент захвата пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="45d1a-130">Hello `Set-AzureRmVMExtension` командлет может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="45d1a-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="45d1a-131">Для виртуальных машин Windows:</span><span class="sxs-lookup"><span data-stu-id="45d1a-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="45d1a-132">Для виртуальных машин Linux:</span><span class="sxs-lookup"><span data-stu-id="45d1a-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="45d1a-133">Hello следующий пример является успешный ответ после выполнения hello `Set-AzureRmVMExtension` командлета.</span><span class="sxs-lookup"><span data-stu-id="45d1a-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="45d1a-134">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="45d1a-134">Step 3</span></span>

<span data-ttu-id="45d1a-135">tooensure, hello агент установлен, запустите hello `Get-AzureRmVMExtension` командлета и передайте ему имя виртуальной машины hello и имя расширения hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="45d1a-136">Следующий образец Hello приведен пример ответа hello, запуск`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="45d1a-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="45d1a-137">Запуск записи пакета</span><span class="sxs-lookup"><span data-stu-id="45d1a-137">Start a packet capture</span></span>

<span data-ttu-id="45d1a-138">После hello предыдущего выполнения действий, hello пакет отслеживания агент устанавливается на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="45d1a-139">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="45d1a-139">Step 1</span></span>

<span data-ttu-id="45d1a-140">Hello следующим шагом является экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="45d1a-141">Эта переменная передается toohello `New-AzureRmNetworkWatcherPacketCapture` командлет на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="45d1a-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="45d1a-142">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="45d1a-142">Step 2</span></span>

<span data-ttu-id="45d1a-143">Получите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="45d1a-143">Retrieve a storage account.</span></span> <span data-ttu-id="45d1a-144">Эта учетная запись хранения — файл записи пакетов используется toostore hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="45d1a-145">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="45d1a-145">Step 3</span></span>

<span data-ttu-id="45d1a-146">Фильтры можно использовать toolimit hello данные, которые хранятся с захватом пакетов hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="45d1a-147">Hello следующий пример устанавливает два фильтра.</span><span class="sxs-lookup"><span data-stu-id="45d1a-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="45d1a-148">Собирает одного фильтра исходящих TCP-трафик только с локального IP-адреса 10.0.0.3 toodestination порты 20, 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="45d1a-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="45d1a-149">второй фильтр Hello собирает только трафик UDP.</span><span class="sxs-lookup"><span data-stu-id="45d1a-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="45d1a-150">Для записи пакетов можно определить несколько фильтров.</span><span class="sxs-lookup"><span data-stu-id="45d1a-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="45d1a-151">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="45d1a-151">Step 4</span></span>

<span data-ttu-id="45d1a-152">Запустите hello `New-AzureRmNetworkWatcherPacketCapture` командлет toostart hello пакет отслеживания процесс, передавая ему необходимые hello значения, полученные в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="45d1a-153">Hello следующий пример является hello ожидалось результатов выполнения hello `New-AzureRmNetworkWatcherPacketCapture` командлета.</span><span class="sxs-lookup"><span data-stu-id="45d1a-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="45d1a-154">Получение записи пакета</span><span class="sxs-lookup"><span data-stu-id="45d1a-154">Get a packet capture</span></span>

<span data-ttu-id="45d1a-155">Под управлением hello `Get-AzureRmNetworkWatcherPacketCapture` , получает hello состояние выполняющегося или завершенного отслеживания пакетов.</span><span class="sxs-lookup"><span data-stu-id="45d1a-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="45d1a-156">Hello ниже приведен вывод hello hello `Get-AzureRmNetworkWatcherPacketCapture` командлета.</span><span class="sxs-lookup"><span data-stu-id="45d1a-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="45d1a-157">Hello следующий пример — после завершения записи hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="45d1a-158">Hello значение PacketCaptureStatus остановлена с StopReason TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="45d1a-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="45d1a-159">Это значение показывает, что захват пакетов hello прошла успешно и время его запуска.</span><span class="sxs-lookup"><span data-stu-id="45d1a-159">This value shows that hello packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="45d1a-160">Прекращение записи пакета</span><span class="sxs-lookup"><span data-stu-id="45d1a-160">Stop a packet capture</span></span>

<span data-ttu-id="45d1a-161">Запустив hello `Stop-AzureRmNetworkWatcherPacketCapture` командлета, если записи сеанса выполняется она остановлена.</span><span class="sxs-lookup"><span data-stu-id="45d1a-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="45d1a-162">Hello командлет не возвращает ответа при выполнялись в момент записи сеанса или существующего сеанса, который уже был остановлен.</span><span class="sxs-lookup"><span data-stu-id="45d1a-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="45d1a-163">Удаление записи пакета</span><span class="sxs-lookup"><span data-stu-id="45d1a-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="45d1a-164">Удаление захват пакетов не приводит к удалению файла hello в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="45d1a-165">Скачивание записи пакета</span><span class="sxs-lookup"><span data-stu-id="45d1a-165">Download a packet capture</span></span>

<span data-ttu-id="45d1a-166">После завершения сеанса записи пакета файл записи hello может быть загруженного tooblob хранилища или tooa локальный файл на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="45d1a-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="45d1a-167">место хранения Hello hello захват пакетов определяется при создании сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="45d1a-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="45d1a-168">Tooaccess удобное средство их записывать файлы, сохраненные tooa учетную запись хранения является обозреватель хранилищ Microsoft Azure, которую можно загрузить здесь: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="45d1a-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="45d1a-169">При указании учетной записи хранилища пакетов отслеживания файлы сохраняются tooa учетной записи хранилища в hello следующие расположения:</span><span class="sxs-lookup"><span data-stu-id="45d1a-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="45d1a-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45d1a-170">Next steps</span></span>

<span data-ttu-id="45d1a-171">Узнайте, как снимки tooautomate пакетов с оповещениями виртуальной машины, просмотрев [создать получения оповещений триггеру пакетов](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="45d1a-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="45d1a-172">Сведения о состоянии (разрешен или запрещен) входящего и исходящего трафика виртуальной машины см. в статье [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md) (Проверка потока IP-адресов).</span><span class="sxs-lookup"><span data-stu-id="45d1a-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














