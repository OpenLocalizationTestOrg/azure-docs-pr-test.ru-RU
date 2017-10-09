---
title: "Пример сценария PowerShell - tooVMs трафика балансировки нагрузки для обеспечения высокой доступности aaaAzure | Документы Microsoft"
description: "Azure образец скрипта PowerShell - tooVMs трафика балансировки нагрузки для обеспечения высокой доступности"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Загрузить tooVMs Балансировка трафика для обеспечения высокой доступности

В этом примере сценария создается все необходимое toorun нескольких виртуальных машинах, настроенных в высокой доступности и загрузить сбалансированной конфигурации. После выполнения скрипта hello, будет иметь три виртуальные машины присоединены к домену tooan группе доступности Azure и доступный с помощью подсистемы балансировки нагрузки Azure.

При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Создает конфигурацию подсети. Эта конфигурация используется с hello процесс создания виртуальной сети. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Создает виртуальную сеть и подсеть Azure. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Создает подсистему балансировки нагрузки Azure. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Создает зонд подсистемы балансировки нагрузки. Зонд подсистемы балансировки нагрузки является используется toomonitor каждой виртуальной Машины в наборе балансировки нагрузки hello. Если все виртуальные Машины, становится недоступной, трафик не перенаправленное toohello виртуальной Машины. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Создает правило подсистемы балансировки нагрузки. В этом примере создается правило для порта 80. HTTP-трафик поступает на hello балансировки нагрузки, это перенаправленное tooport 80 один из виртуальных машин hello в набор балансировки нагрузки hello. |
| [New-AzureRmLoadBalancerInboundNatRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Создает правило преобразования сетевых адресов (NAT) подсистемы балансировки нагрузки.  Правила преобразования сетевых адресов сопоставление порта порта tooa подсистемы балансировки нагрузки hello на виртуальной Машине. В этом образце правило NAT создается для SSH tooeach трафик виртуальной Машины в наборе балансировки нагрузки hello.  |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Создание группы безопасности сети (NSG), который является границей безопасности между виртуальными машинами hello Интернет» и «hello. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Создает правило NSG tooallow входящий трафик. В этом примере открывается порт 22 для трафика SSH. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети, подсети и NSG. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Создает группу доступности. Наборы доступности обеспечения бесперебойной работы приложения, распределяя hello виртуальных машин между физическими ресурсами, таким образом, что в случае сбоя всего набора hello не влияют. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Создает конфигурацию виртуальной машины. Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора. Конфигурация Hello используется во время создания виртуальной Машины. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG. Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
