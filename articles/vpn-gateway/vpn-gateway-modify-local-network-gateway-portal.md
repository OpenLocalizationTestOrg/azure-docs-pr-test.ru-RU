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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="3218a-103">Измените параметры шлюза локальной сети при помощи hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3218a-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="3218a-104">Иногда hello параметры для изменения AddressPrefix или GatewayIPAddress шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="3218a-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="3218a-105">В этой статье показано, как toomodify параметры шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="3218a-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="3218a-106">Также можно изменить эти параметры с помощью другого метода, выбрав другой вариант из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="3218a-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3218a-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="3218a-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="3218a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3218a-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="3218a-109">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="3218a-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="3218a-110"><a name="ipaddprefix"></a>Изменение префиксов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="3218a-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="3218a-111">При изменении префиксов IP-адресов, hello шаги, которые можно выполнить зависят от того, имеет ли шлюз локальной сети соединения.</span><span class="sxs-lookup"><span data-stu-id="3218a-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="3218a-112"><a name="gwip"></a>Изменение IP-адреса шлюза hello</span><span class="sxs-lookup"><span data-stu-id="3218a-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="3218a-113">Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется.</span><span class="sxs-lookup"><span data-stu-id="3218a-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="3218a-114">При изменении hello общедоступный IP-адрес hello шаги, которые можно выполнить зависят от того, имеет ли шлюз локальной сети соединения.</span><span class="sxs-lookup"><span data-stu-id="3218a-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3218a-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3218a-115">Next steps</span></span>

<span data-ttu-id="3218a-116">Проверьте подключение шлюза.</span><span class="sxs-lookup"><span data-stu-id="3218a-116">You can verify your gateway connection.</span></span> <span data-ttu-id="3218a-117">См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3218a-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>