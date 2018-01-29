---
title: "Изменение префиксов IP-адресов шлюза локальной сети и IP-адреса VPN- шлюза | Azure | PowerShell | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как изменять префиксы IP-адресов для шлюза локальной сети с помощью PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 2a095b96a8c352abeca72640d37c0d629b447763
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Изменение параметров шлюза локальной сети с помощью PowerShell

Иногда такие параметры шлюза локальной сети, как AddressPrefix или GatewayIPAddress, могут изменяться. В этой статье описывается, как изменить параметры шлюза локальной сети. Эти параметры можно изменить с использованием другого метода, выбрав вариант из следующего списка:

> [!div class="op_single_selector"]
> * [портал Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [интерфейс командной строки Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Перед началом работы

Установите последнюю версию командлетов PowerShell для Azure Resource Manager. Дополнительные сведения об установке командлетов PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).

## <a name="ipaddprefix"></a>Изменение префиксов IP-адресов

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Изменение IP-адреса шлюза

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Проверьте подключение шлюза. См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).