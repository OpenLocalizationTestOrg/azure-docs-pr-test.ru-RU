---
title: "aaaAzure образец скрипта CLI - монтирования диска операционной системы | Документы Microsoft"
description: "Пример скрипта Azure CLI. Подключение диска операционной системы"
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
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Устранение неполадок диска операционной системы виртуальных машин

Этот сценарий подключает hello диск операционной системы виртуальной машины, сбоя или проблемный как данных диска tooa второй виртуальной машины. Это может быть полезно при устранении неполадок с дисками или восстановлении данных. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az vm show](https://docs.microsoft.com/cli/azure/vm#show) | Возвращает список виртуальных машин. В этом случае параметр запроса hello является диск операционной системы виртуальной машины используется tooreturn hello. Затем это значение добавляется имя переменной tooa «uri». |
| [az vm delete](https://docs.microsoft.com/cli/azure/vm#delete) | Удаляет виртуальную машину. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Создает виртуальную машину.  |
| [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Присоединяет диск tooa виртуальной машины. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Возвращает hello IP-адреса виртуальной машины. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
