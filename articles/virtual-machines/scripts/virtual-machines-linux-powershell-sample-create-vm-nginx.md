---
title: "aaaAzure образец скрипта PowerShell - NGINX | Документы Microsoft"
description: "Пример сценария Azure PowerShell для NGINX."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 017a4853e400f8f544a3f92771adaf468b5dee76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-nginx-vm-with-powershell"></a>Создание виртуальной машины NGINX с помощью PowerShell

Этот скрипт создает виртуальную машину Azure, а затем использует hello виртуальной машины Azure настраиваемое расширение скриптов tooinstall NGINX. После выполнения сценария hello, можно получить доступ к демонстрационной веб-сайта на общедоступный IP-адрес hello hello виртуальной машины.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.ps1 "Create VM NGINX")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate hello развертывания hello. Каждый элемент в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Создает конфигурацию подсети. Эта конфигурация используется с hello процесс создания виртуальной сети. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Создает виртуальную сеть. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Создает общедоступный IP-адрес. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Создает конфигурацию правил группы безопасности сети. Такая настройка является toocreate используется правило NSG при создании hello NSG. |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Создает группу безопасности сети. |
| [Get-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | Возвращает сведения о подсети. Эта информация используется при создании сетевого интерфейса. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Создает сетевой интерфейс. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Создает конфигурацию виртуальной машины. Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора. Конфигурация Hello используется во время создания виртуальной Машины. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Создайте виртуальную машину. |
| [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) | Добавьте виртуальную машину toohello расширения виртуальной Машины. В этом образце hello расширение пользовательского скрипта является используется tooinstall NGINX. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Удаляет группу ресурсов и все ресурсы, содержащиеся в ней. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
