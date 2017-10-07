---
title: "aaaUpload VHD-файл tooAzure DevTest Labs, с помощью AzCopy | Документы Microsoft"
description: "Отправка VHD файл toolab учетной записи хранилища с помощью AzCopy"
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Отправка VHD файл toolab учетной записи хранилища с помощью AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

В Azure DevTest Labs VHD-файлы могут быть используется toocreate пользовательские образы, которые являются tooprovision используемых виртуальных машин. Hello следующие шаги описывают с помощью программы командной строки tooupload hello AzCopy учетную запись хранения лаборатории файл виртуального жесткого диска tooa. После отправки вашего VHD-файла, hello [дальнейшие действия раздела](#next-steps) перечислены некоторые статей, которые показывают, как toocreate пользовательского образа из hello отправили файл виртуального жесткого диска. См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).

> [!NOTE] 
>  
> AzCopy является служебной программой командной строки только для Windows.

## <a name="step-by-step-instructions"></a>Пошаговые инструкции

Здравствуйте, следуя обход действия можно выполнить с помощью Отправка VHD файлов tooAzure DevTest Labs с помощью [AzCopy](http://aka.ms/downloadazcopy). 

1. Получите имя hello hello лаборатории учетной записи хранилища с помощью портала Azure hello:

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.

1. Выберите из списка hello лабораториям hello требуемой лаборатории.  

1. В колонке hello лаборатории выберите **конфигурации**. 

1. В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.

1. На hello **пользовательских образов** колонке выберите **+ добавить**. 

1. На hello **настраиваемое изображение** колонке выберите **VHD**.

1. На hello **VHD** колонке выберите **отправить VHD с помощью PowerShell**.

    ![Отправка VHD с помощью PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Hello **отправить изображение с помощью PowerShell** колонке отображает toohello вызов **Add-AzureVhd** командлета. Здравствуйте, первый параметр (*назначения*) содержит hello URI контейнера больших двоичных объектов (*отправляет*) в кодировке hello:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Запишите hello полный URI, поскольку он используется в последующих шагах.

1. Отправьте файл виртуального жесткого диска hello, с помощью AzCopy.
 
1. [Загрузите и установите последнюю версию hello AzCopy](http://aka.ms/downloadazcopy).

1. Откройте окно командной строки и перейдите в каталог установки toohello AzCopy. При необходимости можно добавить hello AzCopy tooyour системы путь установки. По умолчанию AzCopy — установленных toohello следующий каталог:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. С помощью hello контейнера учетной записи хранилища ключей и BLOB-объект URI, запустите следующую команду в командной строке hello hello. Hello *vhdFileName* значение должно toobe в кавычки. Hello процесс передачи файла виртуального жесткого диска может быть длительное время, в зависимости от размера hello hello VHD-файл и скорость подключения.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Дальнейшие действия

- [Создание пользовательского образа в Azure DevTest Labs файла виртуального жесткого диска с помощью портала Azure hello](devtest-lab-create-template.md)
- [Создание пользовательского образа из VHD-файла с помощью PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)