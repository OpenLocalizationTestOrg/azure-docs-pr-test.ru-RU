---
title: "Изменить префиксов IP-адресов шлюза локальной сети hello и адрес IP-адрес шлюза VPN hello | Azure | PowerShell | Документы Microsoft"
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
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Изменение параметров шлюза локальной сети с помощью PowerShell

Иногда hello параметры для изменения AddressPrefix или GatewayIPAddress шлюза локальной сети. В этой статье показано, как toomodify параметры шлюза локальной сети. Также можно изменить эти параметры с помощью другого метода, выбрав другой вариант из hello после списка:

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Интерфейс командной строки Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Перед началом работы

Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) Дополнительные сведения об установке командлетов PowerShell hello.

## <a name="ipaddprefix"></a>Изменение префиксов IP-адресов

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Изменение IP-адреса шлюза hello

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Проверьте подключение шлюза. См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).