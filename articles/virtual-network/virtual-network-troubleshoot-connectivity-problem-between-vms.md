---
title: "проблемы с подключением aaaTroubleshooting между виртуальными машинами Azure | Документы Microsoft"
description: "Узнайте, как tooTroubleshoot hello проблем с подключением между виртуальными машинами Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="5b362-103">Устранение проблем с подключением между виртуальными машинами Azure</span><span class="sxs-lookup"><span data-stu-id="5b362-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="5b362-104">Могут возникнуть проблемы с подключением между виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="5b362-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="5b362-105">В этой статье приведены по устранению неполадок toohelp действия при решении этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="5b362-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="5b362-106">Симптом</span><span class="sxs-lookup"><span data-stu-id="5b362-106">Symptom</span></span>

<span data-ttu-id="5b362-107">ВМ Azure не удается подключиться tooanother виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="5b362-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="5b362-108">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="5b362-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="5b362-109">Проверьте, если сетевой Адаптер настроен неправильно</span><span class="sxs-lookup"><span data-stu-id="5b362-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="5b362-110">Проверьте, если сетевой трафик блокируется NSG или UDR</span><span class="sxs-lookup"><span data-stu-id="5b362-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="5b362-111">Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5b362-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="5b362-112">Проверьте ли ВМ приложение или служба прослушивает порт hello</span><span class="sxs-lookup"><span data-stu-id="5b362-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="5b362-113">Проверьте, вызвана ли проблема hello SNAT</span><span class="sxs-lookup"><span data-stu-id="5b362-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="5b362-114">Проверка ли трафик блокируется в списках управления доступом для hello классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5b362-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="5b362-115">Проверка ли hello конечная точка создана для hello классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5b362-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="5b362-116">Не удается tooconnect tooa ВМ сетевую папку</span><span class="sxs-lookup"><span data-stu-id="5b362-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="5b362-117">Подключения между Vnet</span><span class="sxs-lookup"><span data-stu-id="5b362-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="5b362-118">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="5b362-118">Troubleshooting steps</span></span>

<span data-ttu-id="5b362-119">Выполните эти шаги tootroubleshoot hello проблему.</span><span class="sxs-lookup"><span data-stu-id="5b362-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="5b362-120">Проверьте, устранена ли проблема hello после каждого шага.</span><span class="sxs-lookup"><span data-stu-id="5b362-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="5b362-121">Шаг 1: Проверьте, если сетевой Адаптер настроен неправильно</span><span class="sxs-lookup"><span data-stu-id="5b362-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="5b362-122">Выполните [как tooreset сетевой интерфейс для виртуальной Машины Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="5b362-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="5b362-123">Если проблема hello возникает после изменения hello сетевого интерфейса (NIC), выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5b362-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="5b362-124">**Виртуальные машины Mulit-NIC**</span><span class="sxs-lookup"><span data-stu-id="5b362-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="5b362-125">Добавьте сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="5b362-125">Add a NIC.</span></span>
2. <span data-ttu-id="5b362-126">Устранение проблем hello в hello неверный сетевой Адаптер или удалить неверный сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="5b362-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="5b362-127">Затем readd hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="5b362-127">Then readd hello NIC.</span></span>

<span data-ttu-id="5b362-128">Дополнительные сведения см. в разделе [tooor интерфейсы сети Добавить удалить из виртуальной машины](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="5b362-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="5b362-129">**Виртуальные машины с одним сетевым интерфейсом**</span><span class="sxs-lookup"><span data-stu-id="5b362-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="5b362-130">Повторное развертывание виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="5b362-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="5b362-131">Повторное развертывание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="5b362-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="5b362-132">Шаг 2: Проверьте, если сетевой трафик блокируется NSG или UDR</span><span class="sxs-lookup"><span data-stu-id="5b362-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="5b362-133">Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику.</span><span class="sxs-lookup"><span data-stu-id="5b362-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="5b362-134">Шаг 3: Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5b362-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="5b362-135">Отключите брандмауэр hello и затем hello результата теста.</span><span class="sxs-lookup"><span data-stu-id="5b362-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="5b362-136">Если hello проблему, проверьте параметры hello в брандмауэре hello и снова включите.</span><span class="sxs-lookup"><span data-stu-id="5b362-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="5b362-137">Шаг 4: Проверка ли ВМ приложение или служба прослушивает порт hello</span><span class="sxs-lookup"><span data-stu-id="5b362-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="5b362-138">Можно использовать один из следующих методов toocheck ли виртуальная машина приложение или служба прослушивает порт hello hello</span><span class="sxs-lookup"><span data-stu-id="5b362-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="5b362-139">Выполните следующие команды toocheck ли сервер Здравствуй прослушивает этот порт hello.</span><span class="sxs-lookup"><span data-stu-id="5b362-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="5b362-140">**Виртуальные машины Windows**</span><span class="sxs-lookup"><span data-stu-id="5b362-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="5b362-141">**Виртуальные машины Linux**</span><span class="sxs-lookup"><span data-stu-id="5b362-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="5b362-142">Запустите hello **Telnet** на hello порт hello tootest tooitself ВМ.</span><span class="sxs-lookup"><span data-stu-id="5b362-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="5b362-143">В случае сбоя проверки hello приложение или служба не toolisten настроенный порт hello.</span><span class="sxs-lookup"><span data-stu-id="5b362-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="5b362-144">Шаг 5: Проверьте, вызвана ли проблема hello SNAT</span><span class="sxs-lookup"><span data-stu-id="5b362-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="5b362-145">В некоторых сценариях hello ВМ помещается за решение балансировки нагрузки, которое имеет зависимость ресурсов за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="5b362-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="5b362-146">В этих сценариях при возникновении проблем временное подключение hello проблема может быть вызвана по [нехватку портов SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="5b362-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="5b362-147">проблема tooresolve hello, Создание виртуального IP-адреса (или ILPIP для классической) для каждой виртуальной Машины, балансировщиком нагрузки hello и защиту с NSG или списка управления Доступом.</span><span class="sxs-lookup"><span data-stu-id="5b362-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="5b362-148">Шаг 6: Проверка ли трафик блокируется в списках управления доступом для hello классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5b362-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="5b362-149">Список управления Доступом предоставляет разрешения tooselectively возможность hello или запрещать трафик для конечной точки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5b362-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="5b362-150">Дополнительные сведения см. в разделе [управление hello ACL в конечной точке](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5b362-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="5b362-151">Шаг 7: Проверка ли hello конечная точка создана для hello классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5b362-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="5b362-152">Все виртуальные машины, созданные в Azure с помощью hello классической модели развертывания, могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в hello, же облака службы или виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5b362-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="5b362-153">Тем не менее для компьютеров на других виртуальных сетей требуются конечные точки toodirect hello входящего сетевого трафика tooa виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5b362-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="5b362-154">Дополнительные сведения см. в разделе [как tooset настройке конечных точек](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="5b362-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="5b362-155">Шаг 8: Не удается tooconnect tooa ВМ сетевую папку</span><span class="sxs-lookup"><span data-stu-id="5b362-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="5b362-156">Если не удается tooconnect tooa ВМ сетевую папку, hello проблема может вызываться недоступен сетевых адаптеров в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5b362-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="5b362-157">toodelete hello недоступен сетевых адаптеров см. в разделе [как toodelete hello недоступен сетевых адаптеров](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="5b362-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="5b362-158">Шаг 9: Подключения между Vnet</span><span class="sxs-lookup"><span data-stu-id="5b362-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="5b362-159">Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику.</span><span class="sxs-lookup"><span data-stu-id="5b362-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="5b362-160">Также можно проверить конфигурацию виртуальной сети внутри [здесь](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="5b362-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="5b362-161">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="5b362-161">Need help?</span></span> <span data-ttu-id="5b362-162">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="5b362-162">Contact support.</span></span>
<span data-ttu-id="5b362-163">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="5b362-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
