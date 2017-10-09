---
title: "Проверьте aaaVerify трафика с потоком IP Наблюдатель сети Azure - REST | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен трафик tooor из виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="7c4bc-103">Проверка состояния входящего и исходящего трафика (разрешен или запрещен) путем проверки IP-потока (компонент Наблюдателя за сетями Azure)</span><span class="sxs-lookup"><span data-stu-id="7c4bc-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7c4bc-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7c4bc-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="7c4bc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c4bc-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="7c4bc-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="7c4bc-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="7c4bc-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7c4bc-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="7c4bc-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="7c4bc-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="7c4bc-109">Проверьте IP потока — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="7c4bc-110">Hello проверку можно провести для входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="7c4bc-111">Этот сценарий является полезным tooget текущее состояние ли виртуальной машины могут взаимодействовать tooan внешнего ресурса или внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="7c4bc-112">Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="7c4bc-113">Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c4bc-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7c4bc-114">Before you begin</span></span>

<span data-ttu-id="7c4bc-115">ARMclient — используется toocall hello REST API с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="7c4bc-116">Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="7c4bc-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="7c4bc-117">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7c4bc-118">Сценарий</span><span class="sxs-lookup"><span data-stu-id="7c4bc-118">Scenario</span></span>

<span data-ttu-id="7c4bc-119">В этом сценарии используется tooverify проверьте потока IP, если виртуальная машина может обмениваться информацией машины tooanother через порт 443.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="7c4bc-120">Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="7c4bc-121">Посетите toolearn Дополнительные сведения о IP потока проверьте, [IP потока проверить Обзор](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7c4bc-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="7c4bc-122">В рамках этого сценария вы:</span><span class="sxs-lookup"><span data-stu-id="7c4bc-122">In this scenario, you:</span></span>

* <span data-ttu-id="7c4bc-123">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c4bc-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="7c4bc-124">Вызов проверки IP-потока</span><span class="sxs-lookup"><span data-stu-id="7c4bc-124">Call IP flow verify</span></span>
* <span data-ttu-id="7c4bc-125">проверите результаты;</span><span class="sxs-lookup"><span data-stu-id="7c4bc-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="7c4bc-126">выполните вход с помощью ARMClient;</span><span class="sxs-lookup"><span data-stu-id="7c4bc-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="7c4bc-127">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7c4bc-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="7c4bc-128">Запустите следующий сценарий tooreturn hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="7c4bc-129">Hello следующий код должен значений для переменных hello.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="7c4bc-130">**subscriptionId** -hello toouse идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="7c4bc-131">**resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="7c4bc-132">Hello сведения, необходимые — идентификатор hello в тип hello `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="7c4bc-133">Hello результаты должны быть примерно toohello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="7c4bc-133">hello results should be similar toohello following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="7c4bc-134">Вызов проверки IP-потока</span><span class="sxs-lookup"><span data-stu-id="7c4bc-134">Call IP flow Verify</span></span>

<span data-ttu-id="7c4bc-135">Hello следующий пример создает запрос tooverify hello трафика для указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="7c4bc-136">Hello ответ возвращается, если трафик hello или запрещен трафик hello.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="7c4bc-137">Если он запрещен трафик также возвращает какие блоки правило hello трафика.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="7c4bc-138">Проверьте потока IP требует, что выделена hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="7c4bc-139">Hello сценарий требует ресурсов hello идентификатор виртуальной машины и сетевой интерфейсной платы на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="7c4bc-140">Эти значения предоставляются hello предшествующих выходных данных.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="7c4bc-141">Для всех ОСТАЛЬНЫХ Наблюдатель сети вызовы hello имя группы ресурсов в запросе hello, что URI является hello, содержащей экземпляр hello Наблюдатель сети, не hello ресурсы при выполнении hello диагностических действий на.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a><span data-ttu-id="7c4bc-142">Основные сведения о результатах hello</span><span class="sxs-lookup"><span data-stu-id="7c4bc-142">Understanding hello results</span></span>

<span data-ttu-id="7c4bc-143">Hello вы получаете вы узнаете, разрешен или запрещен трафик hello.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="7c4bc-144">Hello ответа выглядит как один из следующих примеров hello.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="7c4bc-145">**Разрешен**</span><span class="sxs-lookup"><span data-stu-id="7c4bc-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="7c4bc-146">**Запрещен**</span><span class="sxs-lookup"><span data-stu-id="7c4bc-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="7c4bc-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c4bc-147">Next steps</span></span>

<span data-ttu-id="7c4bc-148">Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn Дополнительные сведения о группах безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="7c4bc-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












