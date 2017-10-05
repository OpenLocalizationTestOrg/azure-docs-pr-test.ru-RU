---
title: "Устранение проблем с подключением между виртуальными машинами Azure | Документация Майкрософт"
description: "Сведения об устранении проблем с подключениями между виртуальными машинами Azure."
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
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="9c87f-103">Устранение проблем с подключением между виртуальными машинами Azure</span><span class="sxs-lookup"><span data-stu-id="9c87f-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="9c87f-104">Могут возникнуть проблемы с подключением между виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="9c87f-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="9c87f-105">В этой статье приведены действия по устранению этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="9c87f-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="9c87f-106">Симптом</span><span class="sxs-lookup"><span data-stu-id="9c87f-106">Symptom</span></span>

<span data-ttu-id="9c87f-107">ВМ Azure не удается подключиться к другой виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="9c87f-107">An Azure VM cannot connect to another Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="9c87f-108">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="9c87f-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="9c87f-109">Проверьте, если сетевой Адаптер настроен неправильно</span><span class="sxs-lookup"><span data-stu-id="9c87f-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="9c87f-110">Проверьте, если сетевой трафик блокируется NSG или UDR</span><span class="sxs-lookup"><span data-stu-id="9c87f-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="9c87f-111">Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9c87f-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. <span data-ttu-id="9c87f-112">[Проверьте, прослушивается ли порт приложением или службой виртуальной машины](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port).</span><span class="sxs-lookup"><span data-stu-id="9c87f-112">[Check whether VM app or service is listening on the port](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)</span></span>
5. <span data-ttu-id="9c87f-113">[Проверьте, не вызвана ли проблема SNAT](#step-5-check-whether-the-problem-is-caused-by-snat).</span><span class="sxs-lookup"><span data-stu-id="9c87f-113">[Check whether the problem is caused by SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)</span></span>
6. <span data-ttu-id="9c87f-114">[Проверьте, блокируется ли трафик классической виртуальной машины списками управления доступом (ACL)](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm).</span><span class="sxs-lookup"><span data-stu-id="9c87f-114">[Check whether traffic is blocked by ACLs for the classic VM](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)</span></span>
7. <span data-ttu-id="9c87f-115">[Проверьте, создана ли конечная точка классической виртуальной машины](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm).</span><span class="sxs-lookup"><span data-stu-id="9c87f-115">[Check whether the endpoint is created for the classic VM](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)</span></span>
8. [<span data-ttu-id="9c87f-116">Не удается подключиться к общей сетевой папке виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9c87f-116">Unable to connect to a VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="9c87f-117">Подключения между Vnet</span><span class="sxs-lookup"><span data-stu-id="9c87f-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="9c87f-118">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="9c87f-118">Troubleshooting steps</span></span>

<span data-ttu-id="9c87f-119">Чтобы устранить проблему, выполните действия ниже,</span><span class="sxs-lookup"><span data-stu-id="9c87f-119">Follow these steps to troubleshoot the problem.</span></span> <span data-ttu-id="9c87f-120">Проверьте, устранена ли проблема после каждого шага.</span><span class="sxs-lookup"><span data-stu-id="9c87f-120">Check whether the problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="9c87f-121">Шаг 1: Проверьте, если сетевой Адаптер настроен неправильно</span><span class="sxs-lookup"><span data-stu-id="9c87f-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="9c87f-122">Выполните [сброс сетевого интерфейса для виртуальной Машины Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="9c87f-122">Follow [How to reset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="9c87f-123">Если изменение конфигурации сетевого интерфейса не решило проблему, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9c87f-123">If the problem occurs after you modify the network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="9c87f-124">**Виртуальные машины Mulit-NIC**</span><span class="sxs-lookup"><span data-stu-id="9c87f-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="9c87f-125">Добавьте сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="9c87f-125">Add a NIC.</span></span>
2. <span data-ttu-id="9c87f-126">Устраните проблемы в неверный сетевой Адаптер или удалить неверный сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="9c87f-126">Fix the problems in the bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="9c87f-127">Затем readd сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="9c87f-127">Then readd the NIC.</span></span>

<span data-ttu-id="9c87f-128">Дополнительные сведения см. в статье [Добавление или удаление сетевых интерфейсов виртуальных машин](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="9c87f-128">For more information, see [Add network interfaces to or remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="9c87f-129">**Виртуальные машины с одним сетевым интерфейсом**</span><span class="sxs-lookup"><span data-stu-id="9c87f-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="9c87f-130">Повторное развертывание виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="9c87f-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="9c87f-131">Повторное развертывание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="9c87f-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="9c87f-132">Шаг 2: Проверьте, если сетевой трафик блокируется NSG или UDR</span><span class="sxs-lookup"><span data-stu-id="9c87f-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="9c87f-133">Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) для идентификации при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику.</span><span class="sxs-lookup"><span data-stu-id="9c87f-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="9c87f-134">Шаг 3: Проверьте, если сетевой трафик блокируется брандмауэром виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9c87f-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="9c87f-135">Отключите брандмауэр и проверьте результат.</span><span class="sxs-lookup"><span data-stu-id="9c87f-135">Disable the firewall, and then test the result.</span></span> <span data-ttu-id="9c87f-136">Если проблема будет устранена, проверьте параметры брандмауэра и повторно включить.</span><span class="sxs-lookup"><span data-stu-id="9c87f-136">If the problem is resolved, validate the settings in the firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a><span data-ttu-id="9c87f-137">Шаг 4. Проверка прослушивания порта приложением или службой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9c87f-137">Step 4: Check whether VM app or service is listening on the port</span></span>

<span data-ttu-id="9c87f-138">Можно использовать один из следующих методов для проверки ли виртуальная машина приложение или служба прослушивает порт</span><span class="sxs-lookup"><span data-stu-id="9c87f-138">You can use one of the following methods to check whether VM Application or Service is listening on the port</span></span>

- <span data-ttu-id="9c87f-139">Чтобы проверить, прослушивается ли порт сервером, выполните команды ниже.</span><span class="sxs-lookup"><span data-stu-id="9c87f-139">Run the following commands to check whether the server is listening on that port.</span></span>

<span data-ttu-id="9c87f-140">**Виртуальные машины Windows**</span><span class="sxs-lookup"><span data-stu-id="9c87f-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="9c87f-141">**Виртуальные машины Linux**</span><span class="sxs-lookup"><span data-stu-id="9c87f-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="9c87f-142">Запустите **Telnet** команду на виртуальной Машине для тестирования порт на самого себя.</span><span class="sxs-lookup"><span data-stu-id="9c87f-142">Run the **Telnet** command on the VM to itself to test the port.</span></span> <span data-ttu-id="9c87f-143">Если тест не пройден, приложение или служба не настроен для прослушивания порта.</span><span class="sxs-lookup"><span data-stu-id="9c87f-143">If the test fails, application or service is not configured to listen on the port.</span></span>

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a><span data-ttu-id="9c87f-144">Шаг 5. Проверка проблемы из-за SNAT</span><span class="sxs-lookup"><span data-stu-id="9c87f-144">Step 5: Check whether the problem is caused by SNAT</span></span>

<span data-ttu-id="9c87f-145">В некоторых сценариях ВМ помещается за решение балансировки нагрузки, которое имеет зависимость ресурсов за пределами Azure.</span><span class="sxs-lookup"><span data-stu-id="9c87f-145">In some scenarios, the VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="9c87f-146">Проблемы с промежуточными соединениями в этих сценариях могут возникать из-за [нехватки портов SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="9c87f-146">In these scenarios, if you experience intermittent connection problems, the problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="9c87f-147">Чтобы устранить проблему, создайте виртуальный IP-адрес (или ILPIP для классической) для каждой виртуальной Машины, в которой находится за подсистемой балансировки нагрузки и защиты с NSG или ACL.</span><span class="sxs-lookup"><span data-stu-id="9c87f-147">To resolve the issue, create a VIP (or ILPIP for classic) for each VM that is behind the Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a><span data-ttu-id="9c87f-148">Шаг 6. Проверка блокировки трафика классической виртуальной машины списками управления доступом</span><span class="sxs-lookup"><span data-stu-id="9c87f-148">Step 6: Check whether traffic is blocked by ACLs for the classic VM</span></span>

<span data-ttu-id="9c87f-149">Список ACL дает возможность выборочно разрешать или блокировать трафик для конечной точки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9c87f-149">An ACL provides the ability to selectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="9c87f-150">Дополнительные сведения см. в разделе [Управление ACL для конечной точки](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="9c87f-150">For more information, see [Manage the ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a><span data-ttu-id="9c87f-151">Шаг 7. Проверка наличия конечной точки классической виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9c87f-151">Step 7: Check whether the endpoint is created for the classic VM</span></span>

<span data-ttu-id="9c87f-152">Все виртуальные машины, созданные в Azure с помощью классической модели развертывания могут автоматически взаимодействовать через канал частной сети с другими виртуальными машинами в той же облачной службе или виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9c87f-152">All VMs that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="9c87f-153">Однако компьютерам в других виртуальных сетях требуются конечные точки, чтобы направить входящий трафик к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9c87f-153">However, computers on other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="9c87f-154">Дополнительные сведения см. в статье [Настройка конечных точек в классической виртуальной машине Windows в Azure](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="9c87f-154">For more information, see [How to set up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a><span data-ttu-id="9c87f-155">Шаг 8: Не удается подключиться к общей сетевой папке виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9c87f-155">Step 8: Unable to connect to a VM network share</span></span>

<span data-ttu-id="9c87f-156">Если не удается подключиться к общей сетевой папке виртуальной Машины, проблема может вызываться недоступен сетевых адаптеров в виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="9c87f-156">If you are unable to connect to a VM network share, the problem can be caused by unavailable NICs in the VM.</span></span> <span data-ttu-id="9c87f-157">Сведения об удалении недоступных сетевых интерфейсов см. в [этом разделе](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics).</span><span class="sxs-lookup"><span data-stu-id="9c87f-157">To delete the unavailable NICs, see [How to delete the unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="9c87f-158">Шаг 9: Подключения между Vnet</span><span class="sxs-lookup"><span data-stu-id="9c87f-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="9c87f-159">Использовать [проверить поток сети наблюдателя IP](../network-watcher/network-watcher-ip-flow-verify-overview.md) и [NSG ведение журнала потока](../network-watcher/network-watcher-nsg-flow-logging-overview.md) для идентификации при наличии группы безопасности сети или определяемые пользователем маршрута, который мешает трафику.</span><span class="sxs-lookup"><span data-stu-id="9c87f-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="9c87f-160">Также можно проверить конфигурацию виртуальной сети внутри [здесь](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="9c87f-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="9c87f-161">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="9c87f-161">Need help?</span></span> <span data-ttu-id="9c87f-162">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="9c87f-162">Contact support.</span></span>
<span data-ttu-id="9c87f-163">Если вам все еще нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="9c87f-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>