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
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="ef00f-103">Изменение параметров шлюза локальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef00f-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="ef00f-104">Иногда hello параметры для изменения AddressPrefix или GatewayIPAddress шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef00f-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="ef00f-105">В этой статье показано, как toomodify параметры шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="ef00f-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="ef00f-106">Также можно изменить эти параметры с помощью другого метода, выбрав другой вариант из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="ef00f-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef00f-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ef00f-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="ef00f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef00f-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="ef00f-109">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="ef00f-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="ef00f-110"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ef00f-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="ef00f-111">Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ef00f-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ef00f-112">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ef00f-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="ef00f-113"><a name="ipaddprefix"></a>Изменение префиксов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="ef00f-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="ef00f-114"><a name="gwip"></a>Изменение IP-адреса шлюза hello</span><span class="sxs-lookup"><span data-stu-id="ef00f-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ef00f-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef00f-115">Next steps</span></span>

<span data-ttu-id="ef00f-116">Проверьте подключение шлюза.</span><span class="sxs-lookup"><span data-stu-id="ef00f-116">You can verify your gateway connection.</span></span> <span data-ttu-id="ef00f-117">См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ef00f-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>