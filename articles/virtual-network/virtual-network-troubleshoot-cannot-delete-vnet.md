---
title: "aaaCannot удалить виртуальную сеть в Azure | Документы Microsoft"
description: "Узнайте, как tootroubleshoot hello проблему, в котором не удается удалить виртуальную сеть в Azure."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="124bb-103">Устранение неполадок: Не удалось выполнить toodelete виртуальной сети в Azure</span><span class="sxs-lookup"><span data-stu-id="124bb-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="124bb-104">Могут возникать ошибки, при попытке toodelete виртуальной сети в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="124bb-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="124bb-105">В этой статье приведены по устранению неполадок toohelp действия при решении этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="124bb-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="124bb-106">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="124bb-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="124bb-107">[Проверьте, работает ли шлюз виртуальной сети в виртуальной сети hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="124bb-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="124bb-108">[Проверьте, работает ли шлюз приложений в виртуальной сети hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="124bb-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="124bb-109">[Проверьте, включен ли доменные службы Active Directory Azure в виртуальной сети hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="124bb-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="124bb-110">[Проверить, является ли виртуальной сети hello подключенных tooother ресурсов](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="124bb-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="124bb-111">[Проверьте, работает ли по-прежнему виртуальной машины в виртуальной сети hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="124bb-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="124bb-112">[Проверьте, повторяется ли hello виртуальной сети миграции](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="124bb-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="124bb-113">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="124bb-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="124bb-114">Проверьте, работает ли шлюз виртуальной сети в виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="124bb-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="124bb-115">tooremove hello виртуальной сети, необходимо сначала удалить шлюз виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="124bb-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="124bb-116">Для классических виртуальных сетей, go toohello **Обзор** страницы приветствия классической виртуальной сети в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="124bb-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="124bb-117">В hello **VPN-подключений** статьи, если hello шлюз работает в виртуальной сети hello, вы увидите hello IP адрес шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="124bb-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Проверка работы шлюза](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="124bb-119">Для виртуальных сетей go toohello **Обзор** страницы приветствия виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="124bb-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="124bb-120">Проверьте **подключенных устройств** для hello шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="124bb-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Проверьте hello подключенного устройства](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="124bb-122">Перед удалением hello шлюз, сначала удаляйте **подключения** объектов в hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="124bb-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="124bb-123">Проверьте, работает ли шлюз приложений в виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="124bb-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="124bb-124">Go toohello **Обзор** страницы приветствия виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="124bb-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="124bb-125">Проверьте hello **подключенных устройств** для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="124bb-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Проверьте hello подключенного устройства](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="124bb-127">Если шлюз приложений, необходимо удалить перед удалением виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="124bb-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="124bb-128">Проверьте, включен ли доменные службы Active Directory Azure в виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="124bb-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="124bb-129">Если включен и подключен toohello виртуальной сети hello доменные службы Active Directory, нельзя удалить эту виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="124bb-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Проверьте hello подключенного устройства](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="124bb-131">toodisable Здравствуйте службы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="124bb-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="124bb-132">Go toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="124bb-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="124bb-133">Выберите в левой области hello **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="124bb-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="124bb-134">Выберите каталог hello Azure Active Directory (Azure AD), который имеет доменные службы Active Directory включена.</span><span class="sxs-lookup"><span data-stu-id="124bb-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="124bb-135">Выберите hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="124bb-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="124bb-136">В разделе **доменных служб**, измените hello **Включение доменных служб для этого каталога** параметр слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="124bb-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="124bb-137">Проверить, является ли виртуальной сети hello подключенных tooother ресурсов</span><span class="sxs-lookup"><span data-stu-id="124bb-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="124bb-138">Проверьте наличие каналов связи, соединений и пирингов виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="124bb-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="124bb-139">Любой из них может привести к toofail удаления виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="124bb-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="124bb-140">Hello удаления Рекомендуемый порядок выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="124bb-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="124bb-141">Подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="124bb-141">Gateway connections</span></span>
2. <span data-ttu-id="124bb-142">Шлюзы</span><span class="sxs-lookup"><span data-stu-id="124bb-142">Gateways</span></span>
3. <span data-ttu-id="124bb-143">IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="124bb-143">IPs</span></span>
4. <span data-ttu-id="124bb-144">Пиринги виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="124bb-144">Virtual network peerings</span></span>
5. <span data-ttu-id="124bb-145">Среда службы приложений (ASE).</span><span class="sxs-lookup"><span data-stu-id="124bb-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="124bb-146">Проверьте, работает ли по-прежнему виртуальной машины в виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="124bb-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="124bb-147">Убедитесь, что виртуальные машины не находится в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="124bb-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="124bb-148">Проверьте, повторяется ли hello виртуальной сети миграции</span><span class="sxs-lookup"><span data-stu-id="124bb-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="124bb-149">Если виртуальная сеть hello застряла в состоянии миграции, его нельзя удалить.</span><span class="sxs-lookup"><span data-stu-id="124bb-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="124bb-150">Запустите hello, следующая команда tooabort hello миграции, а затем удалите hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="124bb-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="124bb-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="124bb-151">Next steps</span></span>

- [<span data-ttu-id="124bb-152">Виртуальная сеть Azure</span><span class="sxs-lookup"><span data-stu-id="124bb-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="124bb-153">Виртуальная сеть Azure: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="124bb-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)