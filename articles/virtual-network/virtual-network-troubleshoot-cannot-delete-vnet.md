---
title: "Не удается удалить виртуальную сеть в Azure | Документация Майкрософт"
description: "Узнайте, как устранить проблему, когда невозможно удалить виртуальную сеть в Azure."
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
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="df1a8-103">Устранение неполадок: не удалось удалить виртуальную сеть в Azure</span><span class="sxs-lookup"><span data-stu-id="df1a8-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="df1a8-104">При попытке удаления виртуальной сети в Microsoft Azure могут возникать ошибки.</span><span class="sxs-lookup"><span data-stu-id="df1a8-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="df1a8-105">В этой статье приведены действия по устранению этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="df1a8-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="df1a8-106">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="df1a8-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="df1a8-107">[Проверьте, работает ли шлюз виртуальной сети в виртуальной сети](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="df1a8-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="df1a8-108">[Проверьте, работает ли шлюз приложений в виртуальной сети](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="df1a8-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="df1a8-109">[Проверьте, включена ли доменная служба Active Directory Azure в виртуальной сети](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="df1a8-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="df1a8-110">[Проверьте, подключена ли виртуальная сеть к другому ресурсу](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="df1a8-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="df1a8-111">[Проверьте, работает ли виртуальная машина в виртуальной сети](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="df1a8-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="df1a8-112">[Проверьте, зависла ли виртуальная сеть в состоянии миграции](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="df1a8-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="df1a8-113">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="df1a8-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="df1a8-114">Проверка работы шлюза виртуальной сети в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="df1a8-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="df1a8-115">Чтобы удалить виртуальную сеть, сначала необходимо удалить шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="df1a8-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="df1a8-116">Для классических виртуальных сетей перейдите на страницу **обзора** классической виртуальной сети на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="df1a8-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="df1a8-117">В разделе **VPN-подключения**, если шлюз работает в виртуальной сети, отобразится IP-адрес шлюза.</span><span class="sxs-lookup"><span data-stu-id="df1a8-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Проверка работы шлюза](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="df1a8-119">Для виртуальных сетей перейдите на страницу **обзора** виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="df1a8-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="df1a8-120">Проверьте **подключенные устройства** шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="df1a8-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Проверка подключенных устройств](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="df1a8-122">Прежде чем удалить шлюз, сначала необходимо удалить объекты **подключений** в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="df1a8-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="df1a8-123">Проверка работы шлюза приложений в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="df1a8-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="df1a8-124">Перейдите на страницу **обзора** виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="df1a8-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="df1a8-125">Проверьте **подключенные устройства** шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="df1a8-125">Check the **Connected devices** for the application gateway.</span></span>

![Проверка подключенных устройств](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="df1a8-127">Прежде чем удалить виртуальную сеть, необходимо удалить шлюз приложений (если имеется).</span><span class="sxs-lookup"><span data-stu-id="df1a8-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="df1a8-128">Проверка, включена ли доменная служба Active Directory Azure в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="df1a8-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="df1a8-129">Если доменная служба Active Directory включена и подключена к виртуальной сети, вы не сможете удалить эту виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="df1a8-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Проверка подключенных устройств](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="df1a8-131">Чтобы отключить службу, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="df1a8-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="df1a8-132">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="df1a8-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="df1a8-133">В области слева выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df1a8-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="df1a8-134">Выберите каталог Azure Active Directory (Azure AD), в котором включена доменная служба Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df1a8-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="df1a8-135">Перейдите на вкладку **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="df1a8-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="df1a8-136">В разделе **Доменные службы** установите для параметра **Включение доменных служб для этого каталога** значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="df1a8-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="df1a8-137">Проверка, подключена ли виртуальная сеть к другому ресурсу</span><span class="sxs-lookup"><span data-stu-id="df1a8-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="df1a8-138">Проверьте наличие каналов связи, соединений и пирингов виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="df1a8-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="df1a8-139">Любой из этих элементов может вызвать сбой удаления виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="df1a8-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="df1a8-140">Рекомендуемый порядок удаления выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="df1a8-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="df1a8-141">Подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="df1a8-141">Gateway connections</span></span>
2. <span data-ttu-id="df1a8-142">Шлюзы</span><span class="sxs-lookup"><span data-stu-id="df1a8-142">Gateways</span></span>
3. <span data-ttu-id="df1a8-143">IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="df1a8-143">IPs</span></span>
4. <span data-ttu-id="df1a8-144">Пиринги виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="df1a8-144">Virtual network peerings</span></span>
5. <span data-ttu-id="df1a8-145">Среда службы приложений (ASE).</span><span class="sxs-lookup"><span data-stu-id="df1a8-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="df1a8-146">Проверка работы виртуальной машины в виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="df1a8-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="df1a8-147">Убедитесь, что в виртуальной сети нет виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="df1a8-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="df1a8-148">Проверка, зависла ли виртуальная сеть в состоянии миграции</span><span class="sxs-lookup"><span data-stu-id="df1a8-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="df1a8-149">Если виртуальная сеть зависла в состоянии миграции, ее нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="df1a8-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="df1a8-150">Выполните следующую команду, чтобы прервать миграцию, а затем удалите виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="df1a8-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="df1a8-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df1a8-151">Next steps</span></span>

- [<span data-ttu-id="df1a8-152">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="df1a8-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="df1a8-153">Виртуальная сеть Azure: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="df1a8-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)