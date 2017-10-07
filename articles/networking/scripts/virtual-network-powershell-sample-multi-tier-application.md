---
title: "Пример сценария PowerShell - aaaAzure создания сетей многоуровневые приложения | Документы Microsoft"
description: "Пример скрипта Azure PowerShell для создания сети для многоуровневых приложений."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Создание сети для многоуровневых приложений

В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями. Подсети интерфейса toohello трафика является ограниченной tooHTTP и SSH, при toohello трафика конечной подсети ограниченный tooMySQL, порт 3306. После выполнения скрипта hello имеется две виртуальные машины, по одному в каждой подсети, можно развернуть веб-сервера и программное обеспечение MySQL.

При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети. Каждая команда в таблице hello связывает toocommand документации.

| Команда | Примечания |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Создает виртуальную сеть Azure и интерфейсную подсеть. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Создает внутреннюю подсеть. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Создает виртуальными сетевыми интерфейсами и вкладывает их подсети виртуальной сети toohello внешнего и внутреннего интерфейса. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Создание группы безопасности сети (NSG), которые будут связанного toohello внешнего и внутреннего интерфейса подсети. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |Создаются правила NSG, разрешать или запрещать определенные порты toospecific подсетей. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Создает виртуальные машины и присоединяет tooeach сетевого Адаптера виртуальной Машины. Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Удаляет группу ресурсов и все содержащиеся в ней ресурсы. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
