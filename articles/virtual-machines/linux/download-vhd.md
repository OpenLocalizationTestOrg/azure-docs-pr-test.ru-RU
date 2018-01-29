---
title: "Скачивание виртуального жесткого диска Linux из Azure | Документация Майкрософт"
description: "Скачайте виртуальный жесткий диск Linux с помощью Azure CLI и портала Azure."
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
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Скачивание виртуального жесткого диска Linux из Azure

В этой статье описано, как скачать файл [виртуального жесткого диска (VHD) Linux](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) из Azure, используя Azure CLI и портал Azure. 

Виртуальные машины в Azure используют [диски](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) как место хранения операционной системы, приложений и данных. Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск. Диск операционной системы изначально создается из образа, при этом и диск операционной системы, и образ являются виртуальными жесткими дисками (VHD), расположенными в учетной записи хранения Azure. Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках.

Установите интерфейс командной строки [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), если это еще не сделано.

## <a name="stop-the-vm"></a>Остановка виртуальной машины

VHD невозможно скачать из Azure, если он подключен к запущенной виртуальной машине. Для скачивания VHD необходимо остановить виртуальную машину. Чтобы использовать VHD в качестве [образа](tutorial-custom-images.md) для создания других виртуальных машин с помощью новых дисков, необходимо отозвать и подготовить к использованию операционную систему, которая содержится в файле, и остановить виртуальную машину. Для использования VHD в качестве диска для нового экземпляра существующей виртуальной машины или диска данных необходимо просто остановить виртуальную машину и отменить ее выделение.

Чтобы использовать VHD как образ для создания других виртуальных машин, выполните следующие действия:

1. Используйте SSH, имя учетной записи и общедоступный IP-адрес виртуальной машины, чтобы подключиться к ней и отозвать ее. Параметр +user также удаляет последнюю подготовленную учетную запись пользователя. При вводе учетных данных в виртуальную машину оставьте параметр +user. В следующем примере удаляется последняя подготовленная учетная запись пользователя:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Войдите в свою учетную запись Azure с помощью команды [az login](https://docs.microsoft.com/cli/azure/#login).
3. Остановите виртуальную машину и отмените ее выделение.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Подготовьте виртуальную машину к использованию. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

Для использования VHD в качестве диска для нового экземпляра существующей виртуальной машины или диска данных выполните следующие действия:

1.  Войдите на [портал Azure](https://portal.azure.com/).
2.  В главном меню щелкните **Виртуальные машины**.
3.  Выберите виртуальную машину из списка.
4.  В колонке виртуальной машины нажмите кнопку **Остановить**.

    ![Остановка виртуальной машины](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Создание URL-адреса SAS

Чтобы скачать VHD-файл, необходимо создать [подписанный URL-адрес (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Когда этот URL-адрес создан, ему назначается срок действия.

1.  В меню колонки виртуальной машины щелкните **Диски**.
2.  Выберите диск операционной системы для виртуальной машины и щелкните **Экспорт**.
3.  Нажмите кнопку **Создать URL-адрес**.

    ![Создание URL-адреса](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Скачивание VHD

1.  Под созданным URL-адресом щелкните ссылку "Скачать VHD-файл".

    ![Скачивание VHD](./media/download-vhd/export-download.png)

2.  Чтобы начать скачивание, может потребоваться нажать кнопку **Сохранить** в браузере. По умолчанию VHD-файлу присваивается имя *abcd*.

    ![Нажатие кнопки "Сохранить" в браузере](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, как [передать пользовательский диск и создать на его основе виртуальную машину Linux с помощью Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Управление дисками Azure с помощью Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

