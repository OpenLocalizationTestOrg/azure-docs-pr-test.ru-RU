---
title: "aaaDownload Linux VHD из Azure | Документы Microsoft"
description: "Загрузите VHD Linux с помощью Azure CLI hello и hello портал Azure."
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
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Скачивание виртуального жесткого диска Linux из Azure

В этой статье вы узнаете, как toodownload [Linux виртуального жесткого диска (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello файл из Azure с помощью Azure CLI и на портале Azure. 

Виртуальные машины (VM Azure используется) [дисков](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toostore месте операционной системы, приложений и данных. Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск. диск операционной системы Hello изначально создается из образа, а hello диска операционной системы и образа hello, виртуальные жесткие диски хранятся в учетной записи хранилища Azure. Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.

Установите интерфейс командной строки [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), если это еще не сделано.

## <a name="stop-hello-vm"></a>Остановить hello виртуальной Машины

Не удается загрузить виртуальный жесткий ДИСК из Azure, если он подключен tooa запуск виртуальной Машины. Необходимо toostop hello toodownload виртуального жесткого диска для виртуальной Машины. Если требуется toouse VHD как [изображения](tutorial-custom-images.md) toocreate другие виртуальные машины с помощью новых дисков требуется toodeprovision и обобщения hello операционной системы, содержащихся в hello файла и остановить hello виртуальной Машины. hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, нужно только toostop, а освобождать hello виртуальной Машины.

toouse hello VHD как toocreate изображения других виртуальных машин, выполните следующие действия:

1. Использовать SSH, имя учетной записи hello и hello общедоступный IP-адрес tooit tooconnect hello виртуальной Машины и сделать. Здравствуйте, "+" пользователя параметра также приведет к удалению hello последняя подготовленного пользователя учетной записи. Если учетные данные учетной записи в toohello виртуальной Машины встраивание, пропустите это + параметр пользователя. Hello следующий пример удаляет hello последняя подготовленного пользователя учетной записи:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Войдите в tooyour учетная запись Azure с [входа az](https://docs.microsoft.com/cli/azure/#login).
3. Остановка и освобождать hello виртуальной Машины.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Обобщить hello виртуальной Машины. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

hello toouse виртуальный жесткий ДИСК как диск для нового экземпляра существующей ВМ или диск данных, выполните следующие действия.

1.  Войдите в toohello [портал Azure](https://portal.azure.com/).
2.  Hello концентратора меню **виртуальные машины**.
3.  Выберите hello виртуальной Машины из списка hello.
4.  В колонке hello для hello виртуальной Машины, нажмите кнопку **остановить**.

    ![Остановка виртуальной машины](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Создание URL-адреса SAS

toodownload hello VHD-файл, необходимо toogenerate [подписанного URL-адреса (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL-адрес. При формировании URL-адрес hello срок его действия назначается toohello URL-адрес.

1.  Hello колонка hello для hello виртуальной Машины в меню **дисков**.
2.  Выберите диск операционной системы hello для hello виртуальной Машины и нажмите кнопку **Экспорт**.
3.  Нажмите кнопку **Создать URL-адрес**.

    ![Создание URL-адреса](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Скачивание VHD

1.  В группе hello URL-адрес, созданный выберите загруженный файл VHD hello.

    ![Скачивание VHD](./media/download-vhd/export-download.png)

2.  Может потребоваться tooclick **Сохранить** в браузере toostart hello hello для загрузки. имя по умолчанию Hello hello VHD-файл — *abcd*.

    ![Нажмите кнопку "Сохранить" в браузере hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, каким образом слишком[передача и создание виртуальной Машины Linux с пользовательской диска с hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Управление дисками Azure hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

