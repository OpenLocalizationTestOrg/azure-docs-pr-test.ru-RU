---
title: "шлюз виртуальной сети Azure aaaLegacy SKU | Документы Microsoft"
description: "Устаревшие SKU шлюзов виртуальной сети."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>Работа со SKU шлюза виртуальной сети (старые версии SKU)

Эта статья содержит сведения о hello прежних версий (старая) шлюз виртуальной сети SKU. прежних версий Hello SKU по-прежнему работать в обеих моделях развертывания для VPN-шлюзов, которые уже были созданы. Классический VPN-шлюзов продолжить toouse hello устаревших SKU, и для существующего шлюзов, так и для новых шлюзов. При создании нового диспетчера ресурсов VPN шлюзы, используйте новый шлюз hello SKU. Сведения о hello содержатся новых SKU [о VPN-шлюз](vpn-gateway-about-vpngateways.md).

## <a name="gwsku"></a>SKU шлюзов

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>Расчетная суммарная пропускная способность в зависимости от SKU

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>Поддерживаемые конфигурации в зависимости от SKU и типа VPN

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>Изменение размера SKU шлюза (изменение SKU шлюза)

Вы можете изменить размер номер SKU шлюза в hello родственного SKU. Например при наличии стандартном номере SKU, можно изменить размер tooa высокопроизводительные SKU. Не удается изменить размер VPN шлюзы между hello старого SKU и hello новых семейств SKU. Например не может перейти в стандартном номере SKU tooa VpnGw2 SKU. 

tooresize номер SKU шлюза для hello классической модели развертывания, hello используйте следующую команду:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

tooresize номер SKU шлюза для hello модели развертывания диспетчера ресурсов, используйте hello следующую команду:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Перенос toohello новый шлюз SKU

При работе с моделью развертывания диспетчера ресурсов hello можно перенести новый шлюз toohello номера SKU. При работе с hello классической модели развертывания, которые нельзя перенести toohello новых SKU и вместо этого необходимо продолжить toouse hello SKU прежних версий.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello новых SKU шлюза см. в разделе [SKU шлюза](vpn-gateway-about-vpngateways.md#gwsku).

Дополнительные сведения о параметрах конфигурации VPN-шлюза см. в [этой статье](vpn-gateway-about-vpn-gateway-settings.md).