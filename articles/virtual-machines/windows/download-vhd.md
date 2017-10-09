---
title: "aaaDownload виртуального жесткого диска Windows из Azure | Документы Microsoft"
description: "Загрузка виртуального жесткого диска в Windows с помощью портала Azure hello."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Скачивание виртуального жесткого диска Windows из Azure

В этой статье вы узнаете, как toodownload [Windows виртуального жесткого диска (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) файл из Azure с помощью hello портал Azure. 

Виртуальные машины (VM Azure используется) [дисков](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore месте операционной системы, приложений и данных. Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск. диск операционной системы Hello изначально создается из образа, а hello диска операционной системы и образа hello, виртуальные жесткие диски хранятся в учетной записи хранилища Azure. Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.

## <a name="stop-hello-vm"></a>Остановить hello виртуальной Машины

Не удается загрузить виртуальный жесткий ДИСК из Azure, если он подключен tooa запуск виртуальной Машины. Необходимо toostop hello toodownload виртуального жесткого диска для виртуальной Машины. Если требуется VHD как toouse [изображения](tutorial-custom-images.md) toocreate использовать другие виртуальные машины с помощью новых дисков [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello операционной системы, содержащихся в файле hello и затем остановить hello виртуальной Машины. hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, нужно только toostop, а освобождать hello виртуальной Машины.

toouse hello VHD как toocreate изображения других виртуальных машин, выполните следующие действия:

1.  Если это еще не сделано, войдите в toohello [портал Azure](https://portal.azure.com/).
2.  [Подключение виртуальной Машины toohello](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  На hello виртуальной Машины откройте окно командной строки hello с правами администратора.
4.  Измените каталог hello слишком*%windir%\system32\sysprep* и запустите sysprep.exe.
5.  В средство подготовки системы диалоговое окно «hello», выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что **Generalize** выбран.
6.  В разделе "Параметры завершения работы" выберите **Завершение работы** и нажмите кнопку **ОК**. 

hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, выполните следующие действия.

1.  Hello концентратора в hello портала Azure выберите команду меню **виртуальные машины**.
2.  Выберите hello виртуальной Машины из списка hello.
3.  В колонке hello для hello виртуальной Машины, нажмите кнопку **остановить**.

    ![Остановка виртуальной машины](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Создание URL-адреса SAS

toodownload hello VHD-файл, необходимо toogenerate [подписанного URL-адреса (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL-адрес. При формировании URL-адрес hello срок его действия назначается toohello URL-адрес.

1.  Hello колонка hello для hello виртуальной Машины в меню **дисков**.
2.  Выберите диск операционной системы hello для hello виртуальной Машины и нажмите кнопку **Экспорт**.
3.  Задайте время истечения срока действия hello hello URL-адрес слишком*36000*.
4.  Нажмите кнопку **Создать URL-адрес**.

    ![Создание URL-адреса](./media/download-vhd/export-generate.png)

> [!NOTE]
> время истечения срока действия Hello увеличено с tooprovide по умолчанию hello достаточное количество времени, toodownload hello большой VHD-файл для операционной системы Windows Server. Можно ожидать VHD-файл, содержащий несколько toodownload часов в зависимости от подключения к tootake операционной системы Windows Server hello. Если вы загружаете VHD для диска с данными, достаточно времени по умолчанию hello. 
> 
> 

## <a name="download-vhd"></a>Скачивание VHD

1.  В группе hello URL-адрес, созданный выберите загруженный файл VHD hello.

    ![Скачивание VHD](./media/download-vhd/export-download.png)

2.  Может потребоваться tooclick **Сохранить** в браузере toostart hello hello для загрузки. имя по умолчанию Hello hello VHD-файл — *abcd*.

    ![Нажмите кнопку "Сохранить" в браузере hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, каким образом слишком[передать файл виртуального жесткого диска tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Создание управляемых дисков из неуправляемых дисков в учетной записи хранения](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [Управление дисками Azure с помощью PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

