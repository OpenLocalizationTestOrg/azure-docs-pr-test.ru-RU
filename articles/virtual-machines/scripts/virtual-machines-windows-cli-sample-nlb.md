---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server 2016 с помощью балансировщика сетевой нагрузки | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server 2016 с помощью балансировщика сетевой нагрузки"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 916204d2b94868057b824feee7b7d032c66382f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a>Балансировка нагрузки для трафика между высокодоступными виртуальными машинами

Этот пример скрипта позволяет создать все необходимые компоненты для запуска нескольких виртуальных машин Ubuntu, настроенных в высокодоступной конфигурации с балансировкой нагрузки. После выполнения этого сценария будут созданы три виртуальные машины, которые будут добавлены в группу доступности Azure. Доступ к ним можно будет получить через Azure Load Balancer.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Быстрое создание виртуальной машины")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Описание скрипта

Для создания группы ресурсов, виртуальной машины, группы доступности, балансировщика нагрузки и всех связанных ресурсов этот скрипт использует следующие команды. Для каждой команды в таблице приведены ссылки на соответствующую документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Создает виртуальную сеть и подсеть Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Создает балансировщик сетевой нагрузки Azure. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Создает пробу балансировщика сетевой нагрузки. Она используется для отслеживания каждой виртуальной машины в наборе балансировщика сетевой нагрузки. Если любая виртуальная машина становится недоступной, к ней не направляется трафик. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Создает правило балансировщика сетевой нагрузки. В этом примере создается правило для порта 80. Так как трафик HTTP поступает в балансировщик сетевой нагрузки, он перенаправляется на порт 80 одной из виртуальных машин в наборе балансировщика сетевой нагрузки. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Создает правило преобразования сетевых адресов (NAT) балансировщика сетевой нагрузки.  Правила NAT сопоставляют порт балансировщика сетевой нагрузки с портом виртуальной машины. В этом примере создается правило NAT для SSH-трафика на каждой виртуальной машине в наборе балансировщика сетевой нагрузки.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Создает группу безопасности сети (NSG), которая выполняет роль периметра безопасности между Интернетом и виртуальной машиной. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Создает правило NSG, разрешающее входящий трафик. В этом примере открывается порт 22 для трафика SSH. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Создает виртуальную сетевую карту и подключает ее к виртуальной сети, подсети и группе безопасности сети. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Создает группу доступности. Группы доступности обеспечивают непрерывную работу приложения, распределяя виртуальные машины по физическим ресурсам. Таким образом, в случае сбоя он не затронет весь набор ресурсов. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети. Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Windows](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
