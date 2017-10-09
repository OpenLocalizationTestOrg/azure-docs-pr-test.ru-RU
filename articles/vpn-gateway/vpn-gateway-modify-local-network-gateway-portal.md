---
title: "Изменить префиксов IP-адресов шлюза локальной сети hello и адрес IP-адрес шлюза VPN hello | Azure | Портал | Документы Microsoft"
description: "В этой статье описывается изменение префиксов IP-адресов для шлюза локальной сети с помощью портала Azure hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Измените параметры шлюза локальной сети при помощи hello портал Azure

Иногда hello параметры для изменения AddressPrefix или GatewayIPAddress шлюза локальной сети. В этой статье показано, как toomodify параметры шлюза локальной сети. Также можно изменить эти параметры с помощью другого метода, выбрав другой вариант из hello после списка:

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [Интерфейс командной строки Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Изменение префиксов IP-адресов

При изменении префиксов IP-адресов, hello шаги, которые можно выполнить зависят от того, имеет ли шлюз локальной сети соединения.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Изменение IP-адреса шлюза hello

Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется. При изменении hello общедоступный IP-адрес hello шаги, которые можно выполнить зависят от того, имеет ли шлюз локальной сети соединения.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Проверьте подключение шлюза. См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).