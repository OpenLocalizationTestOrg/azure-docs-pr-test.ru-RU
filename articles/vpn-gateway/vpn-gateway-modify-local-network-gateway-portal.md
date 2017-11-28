---
title: "Изменение префиксов IP-адресов шлюза локальной сети и IP-адреса VPN-шлюза | Azure | Портал | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как изменять префиксы IP-адресов для шлюза локальной сети с помощью портала Azure."
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
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="5828c-103">Изменение параметров шлюза локальной сети с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5828c-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="5828c-104">Иногда такие параметры шлюза локальной сети, как AddressPrefix или GatewayIPAddress, могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="5828c-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="5828c-105">В этой статье описывается, как изменить параметры шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="5828c-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="5828c-106">Эти параметры можно изменить с использованием другого метода, выбрав вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="5828c-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5828c-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5828c-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="5828c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5828c-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="5828c-109">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5828c-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="5828c-110"><a name="ipaddprefix"></a>Изменение префиксов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="5828c-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="5828c-111">При изменении префиксов IP-адресов выполняемые действия зависят от того, имеет ли шлюз локальной сети подключение.</span><span class="sxs-lookup"><span data-stu-id="5828c-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="5828c-112"><a name="gwip"></a>Изменение IP-адреса шлюза</span><span class="sxs-lookup"><span data-stu-id="5828c-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="5828c-113">Если общедоступный IP-адрес VPN-устройства, к которому вы хотите подключиться, изменился, измените шлюз локальной сети в соответствии с изменениями.</span><span class="sxs-lookup"><span data-stu-id="5828c-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="5828c-114">При изменении общедоступного IP-адреса выполняемые действия зависят от того, имеет ли шлюз локальной сети подключение.</span><span class="sxs-lookup"><span data-stu-id="5828c-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5828c-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5828c-115">Next steps</span></span>

<span data-ttu-id="5828c-116">Проверьте подключение шлюза.</span><span class="sxs-lookup"><span data-stu-id="5828c-116">You can verify your gateway connection.</span></span> <span data-ttu-id="5828c-117">См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5828c-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>