---
title: "Общие сведения об агенте виртуальной машины aaaAzure | Документы Microsoft"
description: "Обзор агента виртуальной машины Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Обзор агента виртуальной машины Azure

Hello агент виртуальной машины Microsoft Azure (агент ВМ) является защищенным, простое процессом, который управляет взаимодействием виртуальной Машины с hello Azure Fabric Controller. Hello агент виртуальной Машины имеет основной роли в Включение и выполнении расширения виртуальных машин Azure. Расширения виртуальной машины дают возможность выполнить дополнительные действия по настройке виртуальных машин после развертывания, например установить и настроить программное обеспечение. Расширения виртуальных машин также включение функции восстановления, например, сбросить пароль администратора hello виртуальной машины. Без hello агента ВМ Azure невозможно запустить расширения виртуальной машины.

В этом документе описаны установки, обнаружения и удаления hello агент виртуальной машины Azure.

## <a name="install-hello-vm-agent"></a>Установить агент ВМ hello

### <a name="azure-gallery-image"></a>Образ из коллекции Azure

Hello агента ВМ Azure устанавливается по умолчанию на любой виртуальной машине Windows, развернутых из образа Azure коллекции. При развертывании образа Azure коллекции из hello портала, PowerShell, интерфейс командной строки или шаблонов диспетчера ресурсов Azure, установить приветствия также является агента ВМ Azure. 

### <a name="manual-installation"></a>Ручная установка

агент виртуальной Машины Windows Hello можно установить вручную с помощью пакета установщика Windows. Ручная установка может потребоваться при создании пользовательского образа виртуальной машины, который будет развернут в Azure. hello toomanually установки агента виртуальной Машины Windows, загрузка установщика агента ВМ hello из этого расположения [загрузки агента ВМ Windows Azure](http://go.microsoft.com/fwlink/?LinkID=394789). 

Hello агент виртуальной Машины можно установить, дважды щелкнув файл установщика windows hello. Для автоматической или автоматической установки агента ВМ hello выполните следующую команду hello.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Обнаружить hello агент виртуальной Машины

### <a name="powershell"></a>PowerShell

модуль PowerShell диспетчера ресурсов Azure Hello можно использовать tooretrieve сведения о виртуальных машинах Azure. Под управлением `Get-AzureRmVM` возвращает довольно много информации, включая состояние для hello агента ВМ Azure подготовки hello.

```PowerShell
Get-AzureRmVM
```

Hello ниже приведен только подмножество hello `Get-AzureRmVM` выходных данных. Обратите внимание hello `ProvisionVMAgent` свойство вложено в `OSProfile`, это свойство может быть toodetermine используется, если агент виртуальной Машины hello было toohello развернутой виртуальной машины.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

Привет, выполнив сценарий может быть используется tooreturn краткий список имен виртуальных машин и состояние hello hello агент виртуальной Машины.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>Обнаружение вручную

При регистрации в tooa виртуальной Машине Windows Azure, диспетчер задач может быть используется tooexamine запущенных процессов. toocheck для hello агента ВМ Azure, откройте диспетчер задач > вкладку подробности hello и найдите имя процесса `WindowsAzureGuestAgent.exe`. Присутствие этого процесса Hello указывает, что установлен агент ВМ, hello.

## <a name="upgrade-hello-vm-agent"></a>Обновление hello агент виртуальной Машины

Hello Azure VM агент для Windows обновляется автоматически. Как новые виртуальные машины в развернутой tooAzure, они получают последнюю версию агента ВМ hello. Пользовательские образы виртуальных Машин следует вручную, добавив новые tooinclude hello новый агент виртуальной Машины.
