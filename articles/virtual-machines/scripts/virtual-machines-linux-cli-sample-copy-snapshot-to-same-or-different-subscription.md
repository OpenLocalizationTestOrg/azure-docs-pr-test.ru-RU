---
title: "Пример сценария CLI - копии (перемещения) снимок toosame управляемого диска или другой подписке с CLI aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI - копии (перемещения) снимок toosame управляемого диска или другой подписке с CLI"
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Скопировать моментальный снимок toosame управляемого диска или другой подписке с CLI

Этот скрипт копирует моментальный снимок toosame управляемого диска или другую подписку. Используйте этот скрипт toomove toodifferent подписки на моментальные снимки в hello же регионе, что hello родительского снимка.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующую toocreate команд моментального снимка в hello целевой подписки с помощью hello идентификатор моментального снимка источника hello. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Возвращает все свойства hello моментального снимка с использованием имени hello и свойства группы ресурсов hello моментального снимка. Идентификатор свойства — это используемые toocopy hello моментального снимка toodifferent подписка.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | Здравствуйте моментального снимка путем создания моментального снимка в другую подписку, используя идентификатор и имя копии hello родительского снимка.  |

## <a name="next-steps"></a>Дальнейшие действия

[Создание виртуальной машины на основе моментального снимка](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
