---
title: "Проверьте aaaverify трафика с потоком IP Наблюдатель сети Azure - PowerShell | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен, с помощью PowerShell tooor трафик от виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="5ef50-103">Проверьте, нельзя ли трафик разрешен или запрещен tooor из виртуальной Машины с потоком IP проверить компонент Наблюдатель сети Azure</span><span class="sxs-lookup"><span data-stu-id="5ef50-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5ef50-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ef50-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="5ef50-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ef50-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="5ef50-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="5ef50-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="5ef50-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5ef50-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="5ef50-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="5ef50-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="5ef50-109">Проверьте IP потока — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5ef50-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="5ef50-110">Этот сценарий является полезным tooget текущее состояние ли виртуальной машины могут взаимодействовать tooan внешнего ресурса или внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="5ef50-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="5ef50-111">Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG.</span><span class="sxs-lookup"><span data-stu-id="5ef50-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="5ef50-112">Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.</span><span class="sxs-lookup"><span data-stu-id="5ef50-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ef50-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5ef50-113">Before you begin</span></span>

<span data-ttu-id="5ef50-114">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети или иметь существующий экземпляр Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="5ef50-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="5ef50-115">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="5ef50-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="5ef50-116">Сценарий</span><span class="sxs-lookup"><span data-stu-id="5ef50-116">Scenario</span></span>

<span data-ttu-id="5ef50-117">Этот сценарий использует IP потока проверьте tooverify, если виртуальная машина может обмениваться информацией tooa известного Bing IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5ef50-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="5ef50-118">Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик.</span><span class="sxs-lookup"><span data-stu-id="5ef50-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="5ef50-119">Дополнительные сведения о потоке IP проверить, посетите toolearn [IP потока проверить Обзор](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5ef50-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="5ef50-120">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="5ef50-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="5ef50-121">Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="5ef50-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="5ef50-122">Hello `$networkWatcher` переменной передается toohello IP потока проверьте командлета.</span><span class="sxs-lookup"><span data-stu-id="5ef50-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="5ef50-123">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5ef50-123">Get a VM</span></span>

<span data-ttu-id="5ef50-124">Поток IP проверьте tooor трафика тесты из IP-адреса виртуальной машины tooor из удаленного места назначения.</span><span class="sxs-lookup"><span data-stu-id="5ef50-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="5ef50-125">Идентификатор виртуальной машины является обязательным для командлета hello.</span><span class="sxs-lookup"><span data-stu-id="5ef50-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="5ef50-126">Если вы уже знаете идентификатор hello toouse hello виртуальной машины, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="5ef50-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="5ef50-127">Получить hello сетевых Адаптеров</span><span class="sxs-lookup"><span data-stu-id="5ef50-127">Get hello NICS</span></span>

<span data-ttu-id="5ef50-128">в этом примере мы получить hello сетевых адаптеров на виртуальной машине требуется Hello IP-адрес сетевого адаптера на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="5ef50-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="5ef50-129">Если вы уже знаете hello IP адрес, о котором требуется tootest на виртуальной машине hello, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="5ef50-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="5ef50-130">Выполнение проверки IP-потока</span><span class="sxs-lookup"><span data-stu-id="5ef50-130">Run IP flow verify</span></span>

<span data-ttu-id="5ef50-131">Теперь, когда есть hello сведения, необходимые toorun hello командлета, запустим hello `Test-AzureRmNetworkWatcherIPFlow` командлет tootest hello трафика.</span><span class="sxs-lookup"><span data-stu-id="5ef50-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="5ef50-132">В этом примере мы используем hello первый IP-адрес первой hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="5ef50-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="5ef50-133">Проверьте потока IP требует, что toorun распределения ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="5ef50-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="5ef50-134">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="5ef50-134">Review Results</span></span>

<span data-ttu-id="5ef50-135">После выполнения команды `Test-AzureRmNetworkWatcherIPFlow` hello результаты возвращаются, hello следующий пример является hello результаты, возвращенные hello предыдущих шага.</span><span class="sxs-lookup"><span data-stu-id="5ef50-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="5ef50-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ef50-136">Next steps</span></span>

<span data-ttu-id="5ef50-137">Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.</span><span class="sxs-lookup"><span data-stu-id="5ef50-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













