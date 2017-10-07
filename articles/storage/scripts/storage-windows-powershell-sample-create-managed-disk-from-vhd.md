---
title: "aaaAzure образец скрипта PowerShell - Создание управляемого диска из VHD-файла в учетную запись хранилища в подписке на одном или разных | Документы Microsoft"
description: "Пример сценария Azure PowerShell для создания управляемого диска из VHD-файла в учетной записи хранения в той же или другой подписке."
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Создание управляемого диска из VHD-файла в учетной записи хранения в той же или другой подписке с помощью PowerShell

Этот сценарий создает управляемый диск на основе VHD-файла в учетной записи хранения в той же или другой подписке. Используйте этот скрипт tooimport специальных (не обобщенный или командой Sysprep) виртуального жесткого диска toomanaged ОС диска toocreate виртуальной машины. Кроме того используйте tooimport диск данных виртуального жесткого диска toomanaged данных. 

Не создавайте несколько идентичных управляемых дисков из VHD-файла за небольшой промежуток времени. toocreate управляемых дисков из VHD-файл, создается моментальный снимок большого двоичного объекта hello VHD-файл и будет используется toocreate управляемых дисков. Только один большой двоичный объект может быть создано в минуту, которое вызывает сбои при создании диска из-за toothrottling. tooavoid повтор, создайте [управляемого моментального снимка из файла виртуального жесткого диска hello](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) и затем используйте hello управляемых toocreate моментального снимка несколько дисков, управляемых за короткий промежуток времени. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует следующие команды toocreate управляемого диска из VHD в другую подписку. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Создает конфигурацию диска, которая используется для создания диска. Он включает тип хранилища, расположение, идентификатор hello учетной записи хранилища хранения hello родительского виртуального жесткого диска, hello родительского виртуального жесткого диска VHD URI ресурса. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Создает диск с помощью конфигурации диска, имени диска и имени группы ресурсов, которые передаются в качестве параметров. |

## <a name="next-steps"></a>Дальнейшие действия

[Создание виртуальной машины путем подключения управляемого диска как диска ОС](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).

Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
