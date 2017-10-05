---
title: "Добавление шлюза виртуальной сети в виртуальную сеть для канала ExpressRoute с помощью PowerShell в Azure | Документация Майкрософт"
description: "В этой статье рассматривается добавление шлюза виртуальной сети в уже созданную виртуальную сеть Resource Manager для ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="794da-103">Настройка шлюза виртуальной сети для ExpressRoute с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="794da-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="794da-104">Resource Manager — портал Azure</span><span class="sxs-lookup"><span data-stu-id="794da-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="794da-105">Resource Manager — PowerShell</span><span class="sxs-lookup"><span data-stu-id="794da-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="794da-106">Классическая модель: PowerShell</span><span class="sxs-lookup"><span data-stu-id="794da-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="794da-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="794da-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="794da-108">В ней описывается добавление, изменение размера и удаление шлюза виртуальной сети для существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="794da-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="794da-109">Приведенные действия по настройке предназначены для виртуальных сетей, созданных с помощью модели развертывания Resource Manager, которые будут использоваться в конфигурации ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="794da-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="794da-110">Дополнительные сведения о шлюзах виртуальных сетей и параметрах конфигурации шлюза для ExpressRoute см. в разделе [Сведения о шлюзах виртуальных сетей ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="794da-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="794da-111">Подготовка</span><span class="sxs-lookup"><span data-stu-id="794da-111">Before beginning</span></span>
<span data-ttu-id="794da-112">Убедитесь, что у вас установлена последняя версия командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="794da-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="794da-113">Если вы еще не установили ее, необходимо сделать это перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="794da-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="794da-114">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="794da-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="794da-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="794da-115">Next steps</span></span>
<span data-ttu-id="794da-116">После создания шлюза виртуальной сети вы можете связать виртуальную сеть с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="794da-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="794da-117">Ознакомьтесь со статьей [Связывание виртуальной сети с каналом ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="794da-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

