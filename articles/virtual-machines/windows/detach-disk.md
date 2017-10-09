---
title: "aaaDetach диск данных от виртуальной Машины Windows - Azure | Документы Microsoft"
description: "Узнайте, toodetach диск данных от виртуальной машины в Azure с помощью модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Toodetach данных места на диске из виртуальной машины Windows
Если диск данных, вложенные tooa виртуальной машины больше не нужен, можно легко отключить ее. Удаляет диск hello из hello виртуальной машины, но не удаляет его из хранилища.

> [!WARNING]
> Если отключить диск, он не удаляется автоматически. Если вы подписаны tooPremium хранилища, снова tooincur плата хранения для диска hello. Дополнительные сведения см. в разделе слишком[цены и выставление счетов при использовании хранилища Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Если требуется toouse hello существующие данные на диске hello, вам может быть повторно присоединена toohello одной виртуальной машине, так и любой другой.

## <a name="detach-a-data-disk-using-hello-portal"></a>Отсоединить диск данных с помощью портала hello
1. В концентраторе hello портала выберите **виртуальные машины**.
2. Выберите hello виртуальную машину с диска данных hello toodetach и щелкните **остановить** toodeallocate hello виртуальной Машины.
3. В колонке hello виртуальной машины, выберите **дисков**.
4. Вверху hello hello **дисков** колонке выберите **изменить**.
5. В hello **дисков** колонке toohello правому краю hello диск данных, что хотелось бы toodetach, щелкните hello ![изображение кнопки отсоединения](./media/detach-disk/detach.png) «отсоединить».
5. После удаления диска hello щелкните Сохранить hello верхней части колонки hello.
6. В колонке hello виртуальную машину, щелкните **Обзор** и нажмите кнопку hello **запустить** кнопку вверху hello hello toorestart hello колонке виртуальной Машины.



Hello диск остается в хранилище, но больше не tooa подключенных виртуальных машин.

## <a name="detach-a-data-disk-using-powershell"></a>Отключение диска данных с помощью PowerShell
В этом примере hello первая команда получает hello виртуальной машины с именем **MyVM07** в hello **RG11** группы ресурсов с помощью командлета Get-AzureRmVM hello. Здравствуйте, команда сохраняет hello виртуальной машины в hello **$VirtualMachine** переменной.

Вторая команда Hello удаляет hello диск данных, с именем DataDisk3 из hello виртуальной машины.

Последняя команда Hello обновляет состояние hello для hello виртуальной машины toocomplete hello процесс удаления диска данных hello.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Дополнительные сведения см. в разделе [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Дальнейшие действия
Если требуется диск данных tooreuse hello, только что [присоединить ее tooanother виртуальной Машины](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

