---
title: "aaaCreate копию управляемых диска Azure для резервного копирования | Документы Microsoft"
description: "Узнайте, как toocreate копию toouse Azure управляемого диска для диска обратно вверх или устранения неполадок проблемы."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Создание копии виртуального жесткого диска, хранящегося в виде управляемого диска Azure, с помощью управляемых моментальных снимков
Снимок управляемых диск для резервного копирования или создать диск управляемых из моментального снимка hello и присоединить ее tootroubleshoot виртуальной машины tooa теста. Управляемый моментальный снимок — это полная копия управляемого диска виртуальной машины на определенный момент времени. Он создает копию виртуального жесткого диска только для чтения и по умолчанию сохраняет ее в качестве управляемого диска уровня "Стандартный". Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Дополнительные сведения о ценах см. на странице [с ценами на службу хранилища Azure](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Перед началом работы
При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello. Запустите hello следующие tooinstall команды.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Скопируйте hello виртуального жесткого диска с помощью моментального снимка
Используйте hello портал Azure или tootake PowerShell моментальный снимок hello управляемого диска.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Использование Azure портала tootake моментального снимка 

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Начиная с левого верхнего угла hello, нажмите кнопку **New** и выполните поиск **моментального снимка**.
3. В колонке hello моментального снимка, щелкните **создать**.
4. Введите **имя** для hello моментального снимка.
5. Выберите существующую [группы ресурсов](../../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую. 
6. Выберите расположение центра обработки данных Azure.  
7. Для **исходный диск**, выберите hello toosnapshot управляемого диска.
8. Выберите hello **тип счета** toouse toostore hello снимка. Мы рекомендуем тип **Standard_LRS**, если вам не требуется хранить моментальный снимок на высокопроизводительном диске.
9. Щелкните **Создать**.

### <a name="use-powershell-tootake-a-snapshot"></a>Используйте PowerShell tootake моментального снимка
Hello следующее показано, как tooget hello VHD на диске toobe копируются, создания hello конфигураций моментального снимка и снимок hello диска с помощью командлета New-AzureRmSnapshot hello<!--Add link toocmdlet when available-->. 

1. Задайте некоторые параметры. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Замените значения параметров hello:
  -  «myResourceGroup» с группой ресурсов виртуальной Машины hello.
  -  «southeastasia» с место снимок управляемых хранимых географическое расположение hello. <!---How do you look these up? -->
  -  «ContosoMD_datadisk1» с именем hello, которые должны toocopy диска VHD hello.
  -  «ContosoMD_datadisk1_snapshot1» с hello именем, вы должны toouse для hello новый моментальный снимок.

2. Получение hello VHD диск toobe копируются.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Создайте моментальный снимок конфигурации, hello. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Снимок "hello".

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Если план toouse hello моментального снимка toocreate диск управляемых и присоединить ее к виртуальной Машине, должен toobe высокопроизводительной, используйте параметр hello `-AccountType Premium_LRS` с помощью команды New-AzureRmSnapshot hello. параметр Hello создает hello моментальных снимков, чтобы оно хранится как диск управляемых Premium. Управляемые диски уровня "Премиум" дороже, чем управляемые диски уровня "Стандартный". Поэтому, прежде чем использовать этот параметр, убедитесь, что вам действительно необходим управляемый диск уровня "Премиум".


