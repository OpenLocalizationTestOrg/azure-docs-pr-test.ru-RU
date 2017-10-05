---
title: "Настройка шлюза виртуальной сети для ExpressRoute с помощью PowerShell в Azure (классическая модель) | Документация Майкрософт"
description: "Узнайте, как настроить шлюз виртуальной сети для виртуальной сети на основе классической модели развертывания с помощью командлетов PowerShell для настройки ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="83f24-103">Настройка шлюза виртуальной сети для ExpressRoute с помощью PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="83f24-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="83f24-104">Resource Manager — PowerShell</span><span class="sxs-lookup"><span data-stu-id="83f24-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="83f24-105">Классическая модель: PowerShell</span><span class="sxs-lookup"><span data-stu-id="83f24-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="83f24-106">Видео — портал Azure</span><span class="sxs-lookup"><span data-stu-id="83f24-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="83f24-107">Эта статья содержит инструкции по добавлению, изменению размера и удалению шлюза виртуальной сети для существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="83f24-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="83f24-108">Приведенные действия по настройке предназначены для виртуальных сетей, созданных с помощью **классической модели развертывания** , которые будут использоваться в конфигурации ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="83f24-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="83f24-109">**О моделях развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="83f24-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="83f24-110">Подготовка</span><span class="sxs-lookup"><span data-stu-id="83f24-110">Before beginning</span></span>
<span data-ttu-id="83f24-111">Убедитесь, что вы установили командлеты Azure PowerShell, необходимые для этой конфигурации (1.0.2 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="83f24-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="83f24-112">Если вы еще не установили эти командлеты, необходимо сделать это перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="83f24-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="83f24-113">Дополнительную информацию об установке Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="83f24-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="83f24-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83f24-114">Next steps</span></span>
<span data-ttu-id="83f24-115">После создания шлюза виртуальной сети вы можете связать виртуальную сеть с каналом ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="83f24-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="83f24-116">Ознакомьтесь со статьей [Связывание виртуальной сети с каналом ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="83f24-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

