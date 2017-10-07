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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>Настройка шлюза виртуальной сети для ExpressRoute с помощью PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager — портал Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager — PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Классическая модель: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

В этой статье рассматриваются действия tooadd hello, масштабировать и удалить шлюз виртуальной сети (VNet) для существующей виртуальной сети. Hello этапах данной конфигурации предназначены специально для виртуальных сетей, которые были созданы с помощью модели развертывания диспетчера ресурсов hello, который будет использоваться в конфигурации ExpressRoute. Дополнительные сведения о шлюзах виртуальных сетей и параметрах конфигурации шлюза для ExpressRoute см. в разделе [Сведения о шлюзах виртуальных сетей ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Подготовка
Убедитесь, что вы установили hello новые командлеты Azure PowerShell. Если вы не установили hello новые командлеты, необходимо toodo так перед началом действия по настройке hello. Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
После создания шлюза виртуальной сети hello, можно связать вашей виртуальной сети tooan канал ExpressRoute. В разделе [связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-arm.md).

