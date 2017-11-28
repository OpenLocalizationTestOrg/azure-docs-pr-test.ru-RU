---
title: "Добавление виртуальной сети шлюза tooa виртуальной сети для ExpressRoute: PowerShell: Azure | Документы Microsoft"
description: "В этой статье описывается добавление tooan шлюза виртуальной сети, уже созданы диспетчера ресурсов виртуальной сети для ExpressRoute."
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
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="ae3f1-103">Настройка шлюза виртуальной сети для ExpressRoute с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae3f1-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae3f1-104">Resource Manager — портал Azure</span><span class="sxs-lookup"><span data-stu-id="ae3f1-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="ae3f1-105">Resource Manager — PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae3f1-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="ae3f1-106">Классическая модель: PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae3f1-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="ae3f1-107">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="ae3f1-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="ae3f1-108">В этой статье рассматриваются действия tooadd hello, масштабировать и удалить шлюз виртуальной сети (VNet) для существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="ae3f1-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="ae3f1-109">Hello этапах данной конфигурации предназначены специально для виртуальных сетей, которые были созданы с помощью модели развертывания диспетчера ресурсов hello, который будет использоваться в конфигурации ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae3f1-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="ae3f1-110">Дополнительные сведения о шлюзах виртуальных сетей и параметрах конфигурации шлюза для ExpressRoute см. в разделе [Сведения о шлюзах виртуальных сетей ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="ae3f1-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="ae3f1-111">Подготовка</span><span class="sxs-lookup"><span data-stu-id="ae3f1-111">Before beginning</span></span>
<span data-ttu-id="ae3f1-112">Убедитесь, что вы установили hello новые командлеты Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae3f1-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ae3f1-113">Если вы не установили hello новые командлеты, необходимо toodo так перед началом действия по настройке hello.</span><span class="sxs-lookup"><span data-stu-id="ae3f1-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="ae3f1-114">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae3f1-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ae3f1-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae3f1-115">Next steps</span></span>
<span data-ttu-id="ae3f1-116">После создания шлюза виртуальной сети hello, можно связать вашей виртуальной сети tooan канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae3f1-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="ae3f1-117">В разделе [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ae3f1-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

