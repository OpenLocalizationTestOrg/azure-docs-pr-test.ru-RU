---
title: "Изменить префиксов IP-адресов шлюза локальной сети hello и адрес IP-адрес шлюза VPN hello | Azure | CLI | Документы Microsoft"
description: "В этой статье описывается изменение префиксов IP-адресов для шлюза локальной сети с помощью hello Azure CLI."
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="8b10f-103">Измените параметры шлюза локальной сети при помощи hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b10f-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="8b10f-104">Иногда изменение параметров hello префикс адреса шлюза локальной сети или IP-адрес шлюза.</span><span class="sxs-lookup"><span data-stu-id="8b10f-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="8b10f-105">В этой статье показано, как toomodify параметры шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="8b10f-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="8b10f-106">Также можно изменить эти параметры с помощью другого метода, выбрав другой вариант из hello после списка:</span><span class="sxs-lookup"><span data-stu-id="8b10f-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b10f-107">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="8b10f-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="8b10f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b10f-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="8b10f-109">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8b10f-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="8b10f-110"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8b10f-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="8b10f-111">Установите последнюю версию hello hello команды CLI (2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="8b10f-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="8b10f-112">Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8b10f-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="8b10f-113"><a name="ipaddprefix"></a>Изменение префиксов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="8b10f-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="8b10f-114"><a name="gwip"></a>Изменение IP-адреса шлюза hello</span><span class="sxs-lookup"><span data-stu-id="8b10f-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8b10f-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b10f-115">Next steps</span></span>

<span data-ttu-id="8b10f-116">Проверьте подключение шлюза.</span><span class="sxs-lookup"><span data-stu-id="8b10f-116">You can verify your gateway connection.</span></span> <span data-ttu-id="8b10f-117">См. статью [Проверка подключения шлюза](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8b10f-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

