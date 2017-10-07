---
title: "Пример сценария CLI - Экспорт копирования моментальных снимков с учетной записью хранения tooa VHD в другом регионе aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI - Экспорт копирования моментальных снимков с учетной записью хранения tooa виртуального жесткого диска в тот же или другой подписке"
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Экспорт» или «копировать управляемый снимки с учетной записью хранения tooa VHD в другом регионе с CLI

Этот сценарий экспортирует учетную запись хранения tooa управляемого моментального снимка в другом регионе. Сначала генерации hello универсальный код Ресурса SAS hello моментальных снимков и использует его toocopy его tooa учетной записи хранилища в другом регионе. Используйте эту резервную копию toomaintain сценария управляемого диски в другом регионе для аварийного восстановления. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующую toogenerate команды универсальный код Ресурса SAS для управляемых hello моментального снимка и копий моментальных снимков tooa учетной записи хранилища с помощью универсального кода Ресурса SAS. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Создает локальный tooon SAS только для чтения, используется toocopy основной учетной записи хранилища tooa файл виртуального жесткого диска или загрузите его  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Асинхронно копирует большой двоичный объект из одного tooanother учетной записи хранилища |

## <a name="next-steps"></a>Дальнейшие действия

[Создание управляемого диска на основе VHD](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Создание виртуальной машины на основе управляемого диска](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
