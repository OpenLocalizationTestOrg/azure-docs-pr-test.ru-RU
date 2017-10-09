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
# <a name="verify-a-vpn-gateway-connection"></a>Проверка подключения VPN-шлюза

В этой статье показано, как tooverify шлюза VPN-подключения для классического hello и модели развертывания диспетчера ресурсов.

## <a name="azure-portal"></a>Портал Azure

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a>PowerShell

tooverify шлюза VPN-подключения для hello диспетчера ресурсов развертывания модели с помощью PowerShell, установите последнюю версию hello hello [командлеты PowerShell диспетчера ресурсов Azure](/powershell/azure/overview).

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a>Инфраструктура CLI Azure

tooverify шлюза VPN-подключения для hello диспетчера ресурсов развертывания модели с помощью Azure CLI, установите последнюю версию hello hello [команды CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 или более поздней версии).

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a>Портал Azure (классическая модель)

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a>PowerShell (классическая модель)

tooverify шлюза VPN-подключение для hello классического развертывания модели с помощью PowerShell, установите последние версии hello hello командлетов Azure PowerShell. Быть убедиться, что hello toodownload и установить [управления службами](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) модуля. Используйте «Add-AzureAccount» toolog в toohello классической модели развертывания.

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

* Можно добавить виртуальные машины tooyour виртуальных сетей. Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
