---
title: "aaaUse a Windows, устранение неполадок виртуальной Машины с помощью Azure PowerShell | Документы Microsoft"
description: "Узнайте, как проблемы tootroubleshoot виртуальной Машины Windows в Azure путем подключения восстановление tooa диска hello ОС виртуальной Машины с помощью Azure PowerShell"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Устранение неполадок виртуальной Машины Windows путем присоединения восстановление tooa диска hello ОС виртуальной Машины с помощью Azure PowerShell
Если на виртуальной машине (ВМ) в Azure, возникает ошибка загрузки или диск, может потребоваться tooperform устранения неполадок на виртуальном жестком диске hello сам. Распространенным примером будет обновление отказавшего приложения, которое предотвращает hello виртуальной Машины может tooboot успешно. Этой статьи сведения о том, как Azure PowerShell tooconnect toouse toofix вашего виртуального жесткого диска для виртуальной Машины Windows tooanother ошибок, повторно создать исходной виртуальной Машины.


## <a name="recovery-process-overview"></a>Обзор процесса восстановления
Поиск и устранение неполадок Hello выглядит следующим образом:

1. Удалите hello ВМ возникновения проблемы, поддержание hello виртуальных жестких дисков.
2. Присоединение и подключить виртуальный жесткий диск hello tooanother виртуальной Машины Windows для устранения неполадок.
3. Подключите toohello Устранение неполадок виртуальной Машины. Изменение файлов или выполните любые средства toofix проблемы на hello исходный виртуальный жесткий диск.
4. Отключите образ и отсоединить виртуальный жесткий диск hello из hello, устранение неполадок виртуальной Машины.
5. Создайте виртуальную Машину с помощью hello исходный виртуальный жесткий диск.

Убедитесь, что [hello последнюю версию Azure PowerShell](/powershell/azure/overview) установлен и вход tooyour подписки:

```powershell
Login-AzureRMAccount
```

В hello следующих примерах замените имена параметров собственные значения. Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.


## <a name="determine-boot-issues"></a>Выявление проблем при загрузке
Можно просмотреть снимок экрана ВМ в Azure toohelp устранения неполадок загрузки. На этом снимке экрана может помочь определить, почему tooboot сбоя виртуальной Машины. Hello следующий пример возвращает экрана приветствия из виртуальной Машины Windows с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Просмотрите почему hello виртуальной Машины происходит сбой tooboot toodetermine экрана приветствия. Обратите внимание на соответствующие сообщения об ошибках или коды ошибок.


## <a name="view-existing-virtual-hard-disk-details"></a>Просмотр сведений для существующего виртуального жесткого диска
Перед тем как присоединить tooanother вашего виртуального жесткого диска виртуальной Машины, необходимо имя hello tooidentify hello виртуального жесткого диска (VHD).

Hello следующий пример получает сведения для виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Найдите `Vhd URI` внутри hello `StorageProfile` части hello предшествующий команда hello в выходных данных. Hello примере усеченные выходных данных ниже показаны hello `Vhd URI` концу hello hello блок кода:

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>Удаление существующей виртуальной машины
Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure. Виртуальный жесткий диск является местом hello операционной системы, приложения и конфигурации. Hello самой ВМ — точно так же метаданные, которые определяет hello размер или расположение и ссылки на ресурсы, такие как виртуальный жесткий диск или виртуальный сетевой адаптер (NIC). Каждый виртуальный жесткий диск содержит аренды, назначенный при присоединении tooa виртуальной Машины. Несмотря на то, что диски с данными может быть присоединенные и отсоединенные даже в том случае, когда выполняется hello виртуальной Машины, диска ОС hello отключить невозможно, пока удаляется hello ресурса виртуальной Машины. Аренда Hello продолжается tooassociate hello ОС диска с виртуальной Машиной даже в том случае, если этой виртуальной Машины находится в состоянии остановки и освобождается.

Здравствуйте, первый шаг toorecover ВМ — toodelete hello ВМ сам ресурс. Удаление hello ВМ оставляет hello виртуальных жестких дисков в вашей учетной записи хранилища. После hello удаления виртуальной Машины присоединения hello виртуальный жесткий диск tooanother ВМ tootroubleshoot и устранение ошибок hello.

Следующий пример удаляет Hello hello виртуальной Машины с именем `myVM` из группы ресурсов hello с именем `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Подождите, пока hello ВМ закончит удаление перед присоединением tooanother hello виртуальный жесткий диск виртуальной Машины. Аренда Hello hello виртуальный жесткий диск, который связывает его с hello виртуальной Машины должен toobe выпуска перед тем как присоединить tooanother hello виртуальный жесткий диск виртуальной Машины.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Подключить существующий виртуальный жесткий диск tooanother виртуальной Машины
Для Здравствуйте рядом шагах, для устранения неполадок используется другой виртуальной Машиной. Подключить существующий виртуальный жесткий диск toothis hello Устранение неполадок виртуальной Машины toobrowse и изменить содержимое диска hello. Этот процесс позволяет toocorrect все ошибки конфигурации или Просмотр дополнительных приложений или файлы журналов, например системы. Выберите или создайте другой toouse виртуальной Машины для устранения неполадок.

При присоединении hello существующий виртуальный жесткий диск, укажите диск toohello hello URL-адрес, полученный на предыдущем hello `Get-AzureRmVM` команды. Hello примере присоединяет существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Добавление диска требует toospecify hello размер диска hello. Здравствуйте, как мы подключить существующий диск, `-DiskSizeInGB` указывается как `$null`. Это значение обеспечивает hello данных диск подключен правильно и без hello требуется toodetermine hello значение true, размер диска данных.


## <a name="mount-hello-attached-data-disk"></a>Подключить hello подключенный диск данных

1. Устранение неполадок виртуальной Машины, используя соответствующие учетные данные hello tooyour протокола удаленного рабочего СТОЛА. Hello следующем примере загружаются RDP-файл подключения hello для виртуальной Машины с именем hello `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`и загружает его слишком`C:\Users\ops\Documents`»

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. диск данных Hello автоматически обнаружены и подсоединен. Просмотрите список hello букву диска hello присоединенных томах toodetermine следующим образом:

    ```powershell
    Get-Disk
    ```

    Следующий пример выходных данных Hello показывает hello виртуального жесткого диска, подключенного диска **2**. (Можно также использовать `Get-Volume` букву диска hello tooview):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Устранение неполадок на исходном виртуальном жестком диске
С hello существующий виртуальный жесткий диск подключен теперь можно выполнять обслуживание и действия по устранению неполадок при необходимости. После разрешения проблемы hello продолжите hello следующие шаги.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Отключение и отсоединение исходного виртуального жесткого диска
После разрешения ошибки, можно отключить и отсоединение hello существующий виртуальный жесткий диск от виртуальной Машины по устранению неполадок. Расположение виртуального жесткого диска нельзя использовать с любой другой ВМ до освобождения аренды hello присоединение toohello hello виртуального жесткого диска, устранение неполадок виртуальной Машины.

1. Из в рамках вашего сеанса RDP отсоединить диск данных hello на виртуальной Машине восстановления. Требуется номер диска hello из hello предыдущих `Get-Disk` командлета. Затем с помощью `Set-Disk` tooset hello диск как:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Подтвердите hello диск теперь задан как вне сети с помощью `Get-Disk` еще раз. Hello в выводе следующего примера показаны hello диск теперь задан как вне сети:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. Выйдите из сеанса RDP. Удалите из свой сеанс Azure PowerShell hello виртуального жесткого диска из hello, устранение неполадок виртуальной Машины.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Создание виртуальной машины из исходного жесткого диска
использовать ВМ с исходного виртуального жесткого диска, toocreate [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). шаблон фактического JSON Hello находится в hello по ссылке:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

шаблон Hello развертывания ВМ в существующей виртуальной сети, с помощью hello URL-адрес VHD из hello ранее команд. Hello примере развертывает hello шаблона toohello ресурсов группы с именем `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Hello ответов запрашивает hello шаблона, такие как имя виртуальной Машины, тип операционной системы и размер виртуальной Машины. Hello `osDiskVhdUri` Здравствуйте, же, как уже используется при присоединении hello существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины.


## <a name="re-enable-boot-diagnostics"></a>Восстановление диагностики загрузки

При создании ВМ из hello существующий виртуальный жесткий диск, диагностика загрузки может не быть доступной. Hello следующий пример включает hello диагностического расширения для виртуальной Машины с именем hello `myVMDeployed` в группе ресурсов hello с именем `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Дальнейшие действия
Если возникают проблемы с подключением tooyour виртуальной Машины, см. раздел [tooan подключений RDP, устранение неполадок виртуальной Машины Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Для устранения проблем с доступом к приложениям, выполняющимся на виртуальной машине, прочитайте статью [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Дополнительные сведения об использовании Resource Manager вы найдете в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
