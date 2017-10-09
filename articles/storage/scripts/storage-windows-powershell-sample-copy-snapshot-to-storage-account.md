---
title: "Пример сценария PowerShell - Экспорт копирования моментальных снимков с учетной записью хранения tooa VHD в другом регионе aaaAzure | Документы Microsoft"
description: "Azure образец скрипта PowerShell - Экспорт копирования моментальных снимков с учетной записью хранения tooa VHD в одном другом регионе"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Экспорт» или «копировать управляемый снимки с учетной записью хранения tooa VHD в другом регионе с помощью PowerShell

Этот сценарий экспортирует учетную запись хранения tooa управляемого моментального снимка в другом регионе. Сначала генерации hello универсальный код Ресурса SAS hello моментальных снимков и использует его toocopy его tooa учетной записи хранилища в другом регионе. Используйте эту резервную копию toomaintain сценария управляемого диски в другом регионе для аварийного восстановления.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующую toogenerate команды универсальный код Ресурса SAS для управляемых hello моментального снимка и копий моментальных снимков tooa учетной записи хранилища с помощью универсального кода Ресурса SAS. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Создает универсальный код Ресурса SAS для снимок, который используется toocopy его tooa учетной записи хранилища. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Создает контекст учетной записи хранилища с помощью hello имя учетной записи и ключа. Этот контекст может быть используется tooperform операций чтения и записи на учетную запись хранения hello. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Здравствуйте, копии базового VHD учетной записи хранения tooa моментальных снимков |

## <a name="next-steps"></a>Дальнейшие действия

[Создание управляемого диска на основе VHD](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Создание виртуальной машины на основе управляемого диска](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
