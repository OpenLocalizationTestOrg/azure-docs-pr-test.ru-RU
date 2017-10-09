---
title: "Примеры PowerShell виртуальной машины aaaAzure | Документы Microsoft"
description: "Примеры PowerShell для виртуальной машины Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 89fd26aa979687cdcdf9ae4e60be7d0d2eaeae91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-powershell-samples"></a>Примеры PowerShell для виртуальной машины Azure

Hello следующей таблице представлены примеры сценариев tooPowerShell ссылки, создание и управление виртуальными машинами Windows.

| | |
|---|---|
|**Создание виртуальных машин**||
| [Создание полностью настроенной виртуальной машины](./../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает группу ресурсов, виртуальную машину и все связанные ресурсы.|
| [Создание высокодоступной виртуальной машины](./../scripts/virtual-machines-windows-powershell-sample-create-nlb-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки.|
| [Создание виртуальной машины с помощью NGINX](./../scripts/virtual-machines-windows-powershell-sample-create-vm-iis.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает виртуальную машину и использует hello Azure пользовательский сценарий расширения tooinstall IIS. |
| [Создание виртуальной машины с IIS с помощью DSC](./../scripts/virtual-machines-windows-powershell-sample-create-iis-using-dsc.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает виртуальную машину и использует tooinstall расширения IIS для hello Azure требуемого состояния (DSC). |
| [Sample script to upload a VHD to Azure and create a new VM](./../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) (Пример скрипта для передачи VHD в Azure и создания виртуальной машины) | Uplaods локального виртуального жесткого диска файл tooAzure, создает и изображение из hello виртуального жесткого диска, а затем создает виртуальную Машину из этого образа. |
| [Создание виртуальной машины с помощью существующего управляемого диска ОС с использованием PowerShell](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает виртуальную машину путем подключения имеющегося управляемого диска как диска ОС. |
| [Создание виртуальной машины из моментального снимка с помощью PowerShell](./../scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает виртуальную машину из моментального снимка путем создания управляемого диска из моментального снимка и затем присоединив hello нового управляемого диск как диск ОС. |
|**Управление хранилищем**||
| [Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) (Создание управляемого диска на основе VHD-файла в учетной записи хранения в той же или другой подписке с помощью PowerShell) | Создание управляемого диска из специализированного VHD в качестве диска ОС или из VHD данных в качестве диска данных в той же или в другой подписке.  |
| [Create a managed disk from a snapshot with PowerShell](../scripts/virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json) (Создание управляемого диска из моментального снимка с помощью PowerShell) | Создание управляемого диска из моментального снимка. |
| [Скопируйте toosame управляемого диска или другой подписке](../scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Копии управляемых диск toosame или другой подписке, а в hello же регионе, что и родительский hello управляемого диска. 
| [Экспортировать моментальный снимок с учетной записью хранения tooa виртуального жесткого диска](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-storage-account.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Экспортирует управляемого моментального снимка с учетной записью хранения tooa VHD в другом регионе. |
| [Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell](../scripts/virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) (Создание моментального снимка на основе VHD для быстрого создания нескольких идентичных управляемых дисков с помощью PowerShell) | Создает моментальных снимков из VHD toocreate несколько управляемых идентичные диски из моментального снимка за короткий промежуток времени.  |
| [Копирование моментального снимка toosame или другой подписке](../scripts/virtual-machines-windows-powershell-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Копии моментальных снимков toosame или другую подписку только в hello же регионе, что hello родительского снимка. |
|**Защита виртуальных машин**||
| [Encrypt a Windows virtual machine with Azure PowerShell](./../scripts/virtual-machines-windows-powershell-sample-encrypt-vm.md?toc=%2fpowershell%2fazure%2ftoc.json) (Шифрование виртуальной машины Windows с помощью Azure PowerShell) | Создание Azure Key Vault, ключа шифрования и субъекта-службы. Шифрование виртуальной машины. |
|**Мониторинг виртуальных машин**||
| [Мониторинг виртуальной машины с помощью Operations Management Suite](./../scripts/virtual-machines-windows-powershell-sample-create-vm-oms.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Создает виртуальную машину, устанавливает агент Operations Management Suite hello и регистрирует hello виртуальной Машины в рабочей области OMS.  |
| | |

