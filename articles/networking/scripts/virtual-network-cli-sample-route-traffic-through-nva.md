---
title: "Пример сценария CLI aaaAzure - трафик через сеть виртуального устройства | Документы Microsoft"
description: "Пример скрипта Azure CLI. Маршрутизация трафика через виртуальный сетевой модуль брандмауэра."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Маршрутизация трафика через виртуальный сетевой модуль

В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями. Он также создает виртуальную Машину с IP-пересылка включена tooroute трафик между двумя подсетями hello. После выполнения сценария hello можно развернуть сетевое программное обеспечение, таких как брандмауэр toohello виртуальной Машины.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Пример скрипта


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети. Каждая команда в таблице hello связывает toocommand документации.

| Команда | Примечания |
|---|---|
| [az group create](/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az network vnet create](/cli/azure/network/vnet#create) | Создает виртуальную сеть Azure и интерфейсную подсеть. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Создает внутреннюю подсеть и подсеть DMZ. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello. |
| [az network nic create](/cli/azure/network/nic#create) | Создает виртуальный сетевой интерфейс и включает IP-пересылку для него. |
| [az network nsg create](/cli/azure/network/nsg#create) | Создает группу безопасности сети (NSG). |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) | Создает правила NSG, позволяющими toohello ВМ входящие порты HTTP и HTTPS. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)| Связывает hello Nsg и toosubnets таблицы маршрутов. |
| [az network route-table create](/cli/azure/network/route-table#create)| Создает таблицу маршрутов для всех маршрутов. |
| [az network route-table route create](/cli/azure/network/route-table/route#create)| Создает маршруты tooroute трафика между подсетями и hello Интернета через hello виртуальной Машины. |
| [az vm create](/cli/azure/vm#create) | Создает виртуальную машину и присоединяет hello tooit сетевого Адаптера. Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора. |
| [az group delete](/cli/azure/group#delete) | Удаляет группу ресурсов и все содержащиеся в ней ресурсы. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](/cli/azure/overview).

Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md)
