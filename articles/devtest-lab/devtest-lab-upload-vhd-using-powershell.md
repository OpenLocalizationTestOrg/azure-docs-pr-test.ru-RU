---
title: "aaaUpload VHD-файл tooAzure DevTest Labs, с помощью PowerShell | Документы Microsoft"
description: "Отправка VHD файл toolab учетной записи хранилища с помощью PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>Отправка VHD файл toolab учетной записи хранилища с помощью PowerShell

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

В Azure DevTest Labs VHD-файлы могут быть используется toocreate пользовательские образы, которые являются tooprovision используемых виртуальных машин. Hello следующие шаги описывают с помощью PowerShell tooupload учетную запись хранения лаборатории файл виртуального жесткого диска tooa. После отправки вашего VHD-файла, hello [дальнейшие действия раздела](#next-steps) перечислены некоторые статей, которые показывают, как toocreate пользовательского образа из hello отправили файл виртуального жесткого диска. См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).

## <a name="step-by-step-instructions"></a>Пошаговые инструкции

Здравствуйте, следуя обход действия можно выполнить с помощью Отправка VHD файлов tooAzure DevTest Labs, с помощью PowerShell. 

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.

1. Выберите из списка hello лабораториям hello требуемой лаборатории.  

1. В колонке hello лаборатории выберите **конфигурации**. 

1. В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.

1. На hello **пользовательских образов** колонке выберите **+ добавить**. 

1. На hello **настраиваемое изображение** колонке выберите **VHD**.

1. На hello **VHD** колонке выберите **отправить VHD с помощью PowerShell**.

    ![Отправка VHD с помощью PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. На hello **отправить изображение с помощью PowerShell** колонки, копирования hello созданный скрипт PowerShell tooa текстовый редактор.

1. Изменение hello **LocalFilePath** параметр hello **Add-AzureVhd** командлет toopoint toohello расположение файла виртуального жесткого диска, который необходимо tooupload hello.

1. В командной строке PowerShell выполните hello **Add-AzureVhd** командлета (с hello изменения **LocalFilePath** параметр).

> [!WARNING] 
> 
> Hello процесс передачи файла виртуального жесткого диска может быть длительное время, в зависимости от размера hello hello VHD-файл и скорость подключения.

## <a name="next-steps"></a>Дальнейшие действия

- [Создание пользовательского образа в Azure DevTest Labs файла виртуального жесткого диска с помощью портала Azure hello](devtest-lab-create-template.md)
- [Создание пользовательского образа из VHD-файла с помощью PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
