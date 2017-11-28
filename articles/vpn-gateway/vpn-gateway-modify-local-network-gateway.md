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
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="16df8-103">Изменение параметров шлюза локальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="16df8-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="16df8-104">Иногда такие параметры шлюза локальной сети, как AddressPrefix или GatewayIPAddress, могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="16df8-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="16df8-105">В этой статье описывается, как изменить параметры шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="16df8-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="16df8-106">Эти параметры можно изменить с использованием другого метода, выбрав вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="16df8-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="16df8-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="16df8-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="16df8-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="16df8-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="16df8-109">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="16df8-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="16df8-110"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="16df8-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="16df8-111">Установите последнюю версию командлетов PowerShell для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16df8-111">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="16df8-112">Дополнительные сведения об установке командлетов PowerShell см. в статье [Как установить и настроить Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="16df8-112">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <span data-ttu-id="16df8-113"><a name="ipaddprefix"></a>Изменение префиксов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="16df8-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="16df8-114"><a name="gwip"></a>Изменение IP-адреса шлюза</span><span class="sxs-lookup"><span data-stu-id="16df8-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="16df8-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16df8-115">Next steps</span></span>

<span data-ttu-id="16df8-116">Проверьте подключение шлюза.</span><span class="sxs-lookup"><span data-stu-id="16df8-116">You can verify your gateway connection.</span></span> <span data-ttu-id="16df8-117">См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="16df8-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>