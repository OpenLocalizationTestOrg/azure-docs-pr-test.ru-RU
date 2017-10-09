---
title: "aaaAzure образец скрипта CLI - toosame диски или другой подписке управляемых копии (перемещения) | Документы Microsoft"
description: "Azure CLI образец скрипта - toosame дисков управляемых копии (перемещения) или другой подписке"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: b1fa207bd6e05d7094be08855e7823e3b7686013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Скопируйте toosame управляемых дисков или другую подписку с CLI

Этот скрипт копирует toosame управляемого диска или другую подписку, но в hello же области. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующую команды toocreate нового управляемого диска в hello целевой подписки с помощью hello идентификатор источника hello управляемого диска. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Возвращает все свойства hello управляемого диска с помощью hello имя ресурса группы свойств и hello управляемого диска. Идентификатор свойства — используется toocopy hello управляемого диска toodifferent подписка.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Копирует управляемого диска путем создания нового управляемого диска в другую подписку, используя идентификатор и имя родительского hello управляемого диска.  |

## <a name="next-steps"></a>Дальнейшие действия

[Создание виртуальной машины на основе управляемого диска](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
