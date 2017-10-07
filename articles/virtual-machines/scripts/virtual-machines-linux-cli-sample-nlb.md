---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины Linux с балансировкой сетевой Нагрузки | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью NLB"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a>Создание высокодоступной виртуальной машины

В этом примере сценария создается все необходимое toorun несколько Ubuntu виртуальных машин, настроенных в высокой доступности и загрузить сбалансированной конфигурации. После выполнения скрипта hello, будет иметь три виртуальные машины присоединены к домену tooan группе доступности Azure и доступный с помощью подсистемы балансировки нагрузки Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Создает виртуальную сеть и подсеть Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Создает балансировщик сетевой нагрузки Azure. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Создает пробу балансировщика сетевой нагрузки. Проверка балансировкой сетевой Нагрузки является используется toomonitor каждой виртуальной Машины в наборе балансировки сетевой Нагрузки hello. Если все виртуальные Машины, становится недоступной, трафик не перенаправленное toohello виртуальной Машины. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Создает правило балансировщика сетевой нагрузки. В этом примере создается правило для порта 80. HTTP-трафик поступает на hello балансировки сетевой Нагрузки, это перенаправленное tooport 80 один из виртуальных машин hello в наборе балансировки сетевой Нагрузки hello. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Создает правило преобразования сетевых адресов (NAT) балансировщика сетевой нагрузки.  Правила преобразования сетевых адресов сопоставление порта hello порт tooa балансировки сетевой Нагрузки на виртуальной Машине. В этом образце правило NAT создается для SSH tooeach трафик виртуальной Машины в наборе балансировки сетевой Нагрузки hello.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Создание группы безопасности сети (NSG), который является границей безопасности между виртуальными машинами hello Интернет» и «hello. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Создает правило NSG tooallow входящий трафик. В этом примере открывается порт 22 для трафика SSH. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети, подсети и NSG. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Создает группу доступности. Наборы доступности обеспечения бесперебойной работы приложения, распределяя hello виртуальных машин между физическими ресурсами, таким образом, что в случае сбоя всего набора hello не влияют. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG. Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
