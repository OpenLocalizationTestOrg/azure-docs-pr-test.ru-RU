---
title: "Проверка трафика с использованием проверки потока IP-адресов с помощью Наблюдателя за сетями (Azure CLI) | Документация Майкрософт"
description: "В этой статье описывается, как проверить состояние передачи входящего и исходящего трафика виртуальной машины (разрешен или запрещен) с помощью Azure CLI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c5fe6c662b3ee2a443904b0f12cbfd495d9bc85e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="1f26d-103">Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) путем проверки потока IP-адресов (компонент Наблюдателя за сетями Azure)</span><span class="sxs-lookup"><span data-stu-id="1f26d-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1f26d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1f26d-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="1f26d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f26d-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="1f26d-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="1f26d-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="1f26d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1f26d-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="1f26d-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="1f26d-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="1f26d-109">Проверка IP-потока — это компонент Наблюдателя за сетями, позволяющий определить состояние (разрешен или запрещен) входящего и исходящего трафика виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1f26d-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="1f26d-110">В этом сценарии можно получить сведения о текущем состоянии взаимодействия виртуальной машины с внешним ресурсом или сервером.</span><span class="sxs-lookup"><span data-stu-id="1f26d-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="1f26d-111">Проверка потока IP-адресов позволяет убедиться, что правила группы безопасности сети настроены правильно, и устранить неполадки потоков, заблокированных правилами NSG.</span><span class="sxs-lookup"><span data-stu-id="1f26d-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="1f26d-112">Такая проверка также гарантирует, что NSG будет соответствующим образом блокировать трафик, который нужно заблокировать.</span><span class="sxs-lookup"><span data-stu-id="1f26d-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="1f26d-113">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="1f26d-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1f26d-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1f26d-114">Before you begin</span></span>

<span data-ttu-id="1f26d-115">В этом сценарии предполагается, что у вас уже есть Наблюдатель за сетями или что вы создали его в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="1f26d-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="1f26d-116">Предполагается также, что у вас имеется группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="1f26d-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="1f26d-117">Сценарий</span><span class="sxs-lookup"><span data-stu-id="1f26d-117">Scenario</span></span>

<span data-ttu-id="1f26d-118">В этом сценарии проверка потока IP-адресов используется, чтобы определить, может ли виртуальная машина обратиться к Bing по известному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="1f26d-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="1f26d-119">Если трафик отклоняется, возвращается правило безопасности, блокирующее трафик.</span><span class="sxs-lookup"><span data-stu-id="1f26d-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="1f26d-120">Дополнительные сведения о проверке потока IP-адресов см. в [этой статье](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f26d-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="1f26d-121">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1f26d-121">Get a VM</span></span>

<span data-ttu-id="1f26d-122">При проверке IP-потока тестируется входящий и исходящий трафик виртуальной машины по IP-адресу в удаленное расположение и из него.</span><span class="sxs-lookup"><span data-stu-id="1f26d-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="1f26d-123">Для командлета требуется идентификатор виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1f26d-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="1f26d-124">Если вы уже знаете идентификатор виртуальной машины, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="1f26d-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a><span data-ttu-id="1f26d-125">Получение сетевых карт</span><span class="sxs-lookup"><span data-stu-id="1f26d-125">Get the NICS</span></span>

<span data-ttu-id="1f26d-126">Вам понадобится IP-адрес сетевой карты на виртуальной машине. В этом примере мы получаем сетевые карты на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1f26d-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="1f26d-127">Если вы уже знаете IP-адрес, который необходимо протестировать на виртуальной машине, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="1f26d-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="1f26d-128">Выполнение проверки IP-потока</span><span class="sxs-lookup"><span data-stu-id="1f26d-128">Run IP flow verify</span></span>

<span data-ttu-id="1f26d-129">Теперь, когда у нас есть сведения, необходимые для выполнения командлета, мы выполним командлет `network watcher ip-flow-verify` для проверки трафика.</span><span class="sxs-lookup"><span data-stu-id="1f26d-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span></span> <span data-ttu-id="1f26d-130">В этом примере мы используем первый IP-адрес первой сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="1f26d-130">In this example, we are using the first IP address on the first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="1f26d-131">Для проверки IP-потока требуется выделение ресурса виртуальной машины для выполнения.</span><span class="sxs-lookup"><span data-stu-id="1f26d-131">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="1f26d-132">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="1f26d-132">Review Results</span></span>

<span data-ttu-id="1f26d-133">После выполнения командлет `network watcher ip-flow-verify` вернет результаты. Они представлены в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="1f26d-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="1f26d-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f26d-134">Next steps</span></span>

<span data-ttu-id="1f26d-135">Если трафик блокируется, чего не должно быть, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md). В ней содержатся сведения об отслеживании группы безопасности сети и определенных правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="1f26d-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="1f26d-136">Узнайте, как выполнить аудит параметров NSG, в статье [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="1f26d-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
