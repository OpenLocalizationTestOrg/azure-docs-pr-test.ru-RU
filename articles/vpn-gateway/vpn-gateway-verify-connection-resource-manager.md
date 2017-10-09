---
title: "подключение VPN-шлюз aaaVerify | Документы Microsoft"
description: "В этой статье показано, как tooverify a виртуального сетевого подключения VPN-шлюз."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="c4de3-103">Проверка подключения VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="c4de3-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="c4de3-104">В этой статье показано, как tooverify шлюза VPN-подключения для классического hello и модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c4de3-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="c4de3-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c4de3-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="c4de3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4de3-106">PowerShell</span></span>

<span data-ttu-id="c4de3-107">tooverify шлюза VPN-подключения для hello диспетчера ресурсов развертывания модели с помощью PowerShell, установите последнюю версию hello hello [командлеты PowerShell диспетчера ресурсов Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4de3-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="c4de3-108">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="c4de3-108">Azure CLI</span></span>

<span data-ttu-id="c4de3-109">tooverify шлюза VPN-подключения для hello диспетчера ресурсов развертывания модели с помощью Azure CLI, установите последнюю версию hello hello [команды CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="c4de3-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="c4de3-110">Портал Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c4de3-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="c4de3-111">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c4de3-111">PowerShell (classic)</span></span>

<span data-ttu-id="c4de3-112">tooverify шлюза VPN-подключение для hello классического развертывания модели с помощью PowerShell, установите последние версии hello hello командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4de3-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c4de3-113">Быть убедиться, что hello toodownload и установить [управления службами](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) модуля.</span><span class="sxs-lookup"><span data-stu-id="c4de3-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="c4de3-114">Используйте «Add-AzureAccount» toolog в toohello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c4de3-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c4de3-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4de3-115">Next steps</span></span>

* <span data-ttu-id="c4de3-116">Можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c4de3-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c4de3-117">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4de3-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
