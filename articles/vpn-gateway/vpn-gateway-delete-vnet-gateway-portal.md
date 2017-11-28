---
title: "Удаление шлюза виртуальной сети с помощью портала Azure (модель Resource Manager) | Документация Майкрософт"
description: "Удаление шлюза виртуальной сети с помощью портала Azure в модели развертывания диспетчера ресурсов."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="fad04-103">Удаление шлюза виртуальной сети с помощью портала</span><span class="sxs-lookup"><span data-stu-id="fad04-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fad04-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="fad04-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="fad04-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fad04-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="fad04-106">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="fad04-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="fad04-107">Существует несколько разных подходов, которые можно применить, когда требуется удалить шлюз виртуальной сети для настройки VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="fad04-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="fad04-108">Если вы хотите все удалить и начать заново, как в случае с тестовой средой, то можете удалить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fad04-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="fad04-109">При удалении группы ресурсов удаляются все ресурсы в этой группе.</span><span class="sxs-lookup"><span data-stu-id="fad04-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="fad04-110">Этот метод рекомендуется, только если вы не хотите оставить какие-либо ресурсы из группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fad04-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="fad04-111">При таком подходе невозможно выборочно удалить только некоторые из ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fad04-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="fad04-112">Если вы хотите сохранить некоторые ресурсы в группе ресурсов, то удаление шлюза виртуальной сети немного усложняется.</span><span class="sxs-lookup"><span data-stu-id="fad04-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="fad04-113">Прежде чем удалить шлюз виртуальной сети, необходимо удалить все ресурсы, зависящие от него.</span><span class="sxs-lookup"><span data-stu-id="fad04-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="fad04-114">Выполняемые действия зависят от типа подключений, которые были созданы, и зависимых ресурсов для каждого подключения.</span><span class="sxs-lookup"><span data-stu-id="fad04-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="fad04-115">Удаление VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="fad04-115">Delete a VPN gateway</span></span>

<span data-ttu-id="fad04-116">Чтобы удалить шлюз виртуальной сети, необходимо сначала удалить каждый ресурс, относящийся к этому шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fad04-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="fad04-117">Ресурсы должны быть удалены в определенном порядке из-за зависимостей.</span><span class="sxs-lookup"><span data-stu-id="fad04-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="fad04-118">На этом этапе шлюз виртуальной сети будет удален.</span><span class="sxs-lookup"><span data-stu-id="fad04-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="fad04-119">Следующие шаги позволят вам удалить любые неиспользуемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fad04-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="fad04-120">Чтобы удалить шлюз локальной сети, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fad04-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="fad04-121">В области **Все ресурсы** найдите шлюзы локальной сети, которые были связаны с каждым подключением.</span><span class="sxs-lookup"><span data-stu-id="fad04-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="fad04-122">В колонке **Обзор** для шлюза локальной сети щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="fad04-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="fad04-123">Чтобы удалить ресурс с общедоступным IP-адресом для шлюза, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fad04-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="fad04-124">В области **Все ресурсы** найдите ресурс с общедоступным IP-адресом, связанный со шлюзом.</span><span class="sxs-lookup"><span data-stu-id="fad04-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="fad04-125">Если шлюз виртуальной сети работал в режиме "активный — активный", вы увидите два общедоступных IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="fad04-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="fad04-126">На странице **Обзор** для общедоступного IP-адреса щелкните **Удалить**, затем нажмите кнопку **Да** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fad04-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="fad04-127">Чтобы удалить подсеть шлюза, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="fad04-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="fad04-128">В области **Все ресурсы** найдите виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="fad04-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="fad04-129">В колонке **Подсети** щелкните **GatewaySubnet**, затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="fad04-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="fad04-130">Нажмите кнопку **Да**, чтобы подтвердить удаление подсети шлюза.</span><span class="sxs-lookup"><span data-stu-id="fad04-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="fad04-131"><a name="deleterg"></a>Удаление VPN-шлюза путем удаления группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="fad04-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="fad04-132">Если не требуется сохранить какие-либо ресурсы из группы ресурсов и вы просто хотите начать все заново, то вы можете удалить всю группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fad04-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="fad04-133">Это быстрый способ удалить все сразу.</span><span class="sxs-lookup"><span data-stu-id="fad04-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="fad04-134">Приведенные ниже инструкции относятся только к модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fad04-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="fad04-135">В области **Все ресурсы** найдите группу ресурсов и щелкните ее, чтобы открыть колонку.</span><span class="sxs-lookup"><span data-stu-id="fad04-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="fad04-136">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="fad04-136">Click **Delete**.</span></span> <span data-ttu-id="fad04-137">В колонке "Удаление" просмотрите задействованные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fad04-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="fad04-138">Убедитесь, что вы хотите удалить все эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fad04-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="fad04-139">Если это не так, следуйте инструкциям в разделе [Удаление VPN-шлюза](#deletegw) в начале этой статьи.</span><span class="sxs-lookup"><span data-stu-id="fad04-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="fad04-140">Чтобы продолжить, введите имя группы ресурсов, которую требуется удалить, а затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="fad04-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>