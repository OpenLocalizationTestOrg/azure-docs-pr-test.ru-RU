---
title: "Образец скрипта CLI - aaaAzure распределяет нагрузку между несколькими веб-сайтов с hello Azure CLI | Документы Microsoft"
description: "Пример сценария Azure CLI - распределяет нагрузку между несколькими toohello веб-сайтов одной виртуальной машине"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Балансировка нагрузки на нескольких веб-сайтах

Этот пример сценария создает виртуальную сеть с двумя виртуальными машинами, которые входят в группу доступности. Балансировщик нагрузки направляет трафик для двух разных IP-адреса toohello двух виртуальных машин. После выполнения скрипта hello можно развернуть web server программного обеспечения toohello виртуальных машин и размещать несколько веб-сайтов, каждая из которых свой IP-адрес.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной сети, подсистема балансировки нагрузки и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Создает виртуальную сеть и подсеть Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Создает службу Azure Load Balancer. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Создает зонд подсистемы балансировки нагрузки. Зонд подсистемы балансировки нагрузки является используется toomonitor каждой виртуальной Машины в наборе балансировки нагрузки hello. Если все виртуальные Машины, становится недоступной, трафик не перенаправленное toohello виртуальной Машины. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Создает правило подсистемы балансировки нагрузки. В этом примере создается правило для порта 80. HTTP-трафик поступает на hello балансировки нагрузки, это перенаправленное tooport 80 один из виртуальных машин hello в набор балансировки нагрузки hello. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Создайте интерфейсный IP-адрес для hello подсистемы балансировки нагрузки. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Создает внутренний пул адресов. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети и подсети. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Создает группу доступности. Наборы доступности обеспечения бесперебойной работы приложения, распределяя hello виртуальных машин между физическими ресурсами, таким образом, что в случае сбоя всего набора hello не влияют. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Создает IP-конфигурацию. Необходимо иметь возможность Microsoft.Network/AllowMultipleIpConfigurationsPerNic hello включена для вашей подписки. Только одна конфигурация может быть определен как hello основной IP-конфигурации каждого сетевого Адаптера, с помощью hello--флаг сделать основным. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG. Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
