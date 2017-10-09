---
title: "сценарий CLI aaaAzure пример — создание сети многоуровневых приложений | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание сети для многоуровневых приложений."
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Создание сети для многоуровневых приложений

В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями. Подсети интерфейса toohello трафика является ограниченной tooHTTP и SSH, при toohello трафика конечной подсети ограниченный tooMySQL, порт 3306. После выполнения скрипта hello имеется две виртуальные машины, по одному в каждой подсети, можно развернуть веб-сервера и программное обеспечение MySQL.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Пример скрипта


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

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
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Создает внутреннюю подсеть. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello. |
| [az network nic create](/cli/azure/network/nic#create) | Создает виртуальными сетевыми интерфейсами и вкладывает их подсети виртуальной сети toohello внешнего и внутреннего интерфейса. |
| [az network nsg create](/cli/azure/network/nsg#create) | Создание группы безопасности сети (NSG), которые будут связанного toohello внешнего и внутреннего интерфейса подсети. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Создаются правила NSG, разрешать или запрещать определенные порты toospecific подсетей. |
| [az vm create](/cli/azure/vm#create) | Создает виртуальные машины и присоединяет tooeach сетевого Адаптера виртуальной Машины. Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора. |
| [az group delete](/cli/azure/group#delete) | Удаляет группу ресурсов и все содержащиеся в ней ресурсы. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](/cli/azure/overview).

Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md)
