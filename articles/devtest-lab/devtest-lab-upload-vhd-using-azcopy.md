---
title: "Отправка VHD-файла в Azure Labs DevTest с помощью AzCopy | Документация Майкрософт"
description: "Отправка VHD-файла в учетную запись хранения лаборатории с помощью AzCopy"
services: devtest-lab,virtual-machines
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: v-craic
ms.openlocfilehash: 11a9d03e62c674c4311c74f78e4cb2e709940941
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a>Отправка VHD-файла в учетную запись хранения лаборатории с помощью AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

В Azure DevTest Labs с помощью VHD-файлов можно создать пользовательские образы, используемые для подготовки виртуальных машин. Ниже приведены пошаговые инструкции по отправке VHD-файла в учетную запись хранения лаборатории с помощью служебной программы командной строки AzCopy. После отправки VHD-файла переходите к разделу [Дальнейшие действия](#next-steps), где перечислены несколько статей, в которых описывается создание пользовательского образа из загруженного VHD-файла. Дополнительные сведения о дисках и виртуальных жестких дисках в Azure см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> AzCopy является служебной программой командной строки только для Windows.

## <a name="step-by-step-instructions"></a>Пошаговые инструкции

Ниже приведены пошаговые инструкции по отправке VHD-файла в Azure DevTest Labs с помощью [AzCopy](http://aka.ms/downloadazcopy). 

1. Узнайте имя учетной записи хранения лаборатории с помощью портала Azure.

1. Войдите на [портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.

1. Из списка лабораторий выберите нужную лабораторию.  

1. В колонке лаборатории выберите **Конфигурация**. 

1. В колонке **Configuration** (Конфигурация) лаборатории выберите **Custom images (VHDs)** (Пользовательские образы (VHD)).

1. В колонке **Custom images** (Пользовательские образы) выберите **+Add** (+ Добавить). 

1. В колонке **Custom images** (Пользовательские образы) выберите **VHD**.

1. В колонке **VHD** щелкните **Upload a VHD file using PowerShell** (Отправить VHD-файл с помощью PowerShell).

    ![Отправка VHD с помощью PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. В колонке **Upload an image using PowerShell** (Отправка образа с помощью PowerShell) отображается вызов командлета **Add-AzureVhd**. Первый параметр (*Назначение*) содержит URI для контейнера больших двоичных объектов (*отправки*) в следующем формате:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Запишите полный URI, так как он понадобится вам дальше.

1. Отправьте VHD-файл с помощью AzCopy.
 
1. [Скачайте и установите последнюю версию AzCopy](http://aka.ms/downloadazcopy).

1. Откройте окно командной строки и перейдите к каталогу установки AzCopy. При необходимости можно добавить место установки AzCopy к системному пути. По умолчанию AzCopy устанавливается в следующий каталог:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Используя ключ учетной записи и URI контейнера больших двоичных объектов, выполните следующую команду в командной строке. Значение *vhdFileName* должно быть заключено в кавычки. В зависимости от размера VHD-файла и скорости подключения процесс передачи файла может занять длительное время.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Дальнейшие действия

- [Управление пользовательскими образами Azure DevTest Labs для создания виртуальных машин](devtest-lab-create-template.md)
- [Создание пользовательского образа из VHD-файла с помощью PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)