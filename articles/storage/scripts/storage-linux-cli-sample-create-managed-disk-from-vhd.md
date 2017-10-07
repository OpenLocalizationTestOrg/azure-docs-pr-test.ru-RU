---
title: "aaaAzure образец скрипта CLI - Создание управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке | Документы Microsoft"
description: "Сценарий Azure CLI пример — создание управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке"
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
ms.openlocfilehash: 1e792fdbb7daea92bf6a6589a5d8aab5b9b5a670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Создание управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке с CLI

Этот скрипт создает управляемого диска из VHD-файла в учетную запись хранилища в hello одной подписке. Используйте этот скрипт tooimport специальных (не обобщенный или командой Sysprep) виртуального жесткого диска toomanaged ОС диска toocreate виртуальной машины. Или использовать его tooimport диск данных виртуального жесткого диска toomanaged данных. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate управляемого диска с виртуального жесткого диска. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Создает управляемый диска с использованием URI виртуального жесткого диска в учетной записи хранения в hello одной подписке |

## <a name="next-steps"></a>Дальнейшие действия

[Создание виртуальной машины путем подключения управляемого диска как диска ОС](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Установить дополнительную виртуальную машину и управляемых дисков CLI образцы скриптов можно найти в hello [документации виртуальной Машине Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
