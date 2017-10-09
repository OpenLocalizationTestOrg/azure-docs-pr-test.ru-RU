---
title: "aaaAzure образец скрипта PowerShell - создание моментального снимка из VHD toocreate несколько идентичных управляемых дисков в небольшой промежуток времени | Документы Microsoft"
description: "Сценарий Azure PowerShell пример — создание моментального снимка из VHD toocreate несколько идентичных управляемых дисков в небольшой промежуток времени"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Создание моментального снимка из VHD toocreate несколько идентичных управляемых дисков в небольшой промежуток времени с помощью PowerShell

Этот сценарий создает моментальный снимок из VHD-файла в учетной записи хранения в той же или другой подписке. Использовать этот сценарий tooimport моментальный снимок специализированные tooa виртуальный жесткий ДИСК (не обобщенный или командой Sysprep), а затем использовать несколько идентичных дисков управляемого toocreate hello моментального снимка в небольшой промежуток времени. Кроме того, используйте моментальный снимок данных виртуального жесткого диска tooa tooimport, а затем использовать несколько дисков, управляемых toocreate hello моментального снимка в небольшой промежуток времени. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate управляемого диска из VHD в другую подписку. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Создает конфигурацию диска, которая используется для создания диска. Он включает тип хранилища, расположение, идентификатор учетной записи хранилища hello, где хранится hello родительского виртуального жесткого диска ресурса и URI VHD hello родительского виртуального жесткого диска. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров. |

## <a name="next-steps"></a>Дальнейшие действия

[Создание управляемого диска из моментального снимка](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Создание виртуальной машины путем подключения управляемого диска как диска ОС](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
