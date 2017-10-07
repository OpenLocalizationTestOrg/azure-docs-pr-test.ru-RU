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
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Настройка шлюза виртуальной сети для ExpressRoute с помощью PowerShell (классическая модель)
> [!div class="op_single_selector"]
> * [Resource Manager — PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Классическая модель: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Эта статья посвящена через hello tooadd действия, изменять размер и удалить шлюз виртуальной сети (VNet) для существующей виртуальной сети. Hello этапах данной конфигурации, специально предназначены для сети, которые были созданы с помощью hello **классической модели развертывания** и, которые будут использоваться в конфигурации ExpressRoute. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**О моделях развертывания Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Подготовка
Убедитесь, что вы установили hello командлетов Azure PowerShell, необходимые для этой конфигурации (версии 1.0.2 или более поздней версии). Если вы не установили hello командлеты, вам потребуется toodo так перед началом действия по настройке hello. Дополнительные сведения об установке Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
После создания шлюза виртуальной сети hello, можно связать вашей виртуальной сети tooan канал ExpressRoute. В разделе [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-classic.md).

