---
title: "aaaAttach tooa диска данных виртуальной Машины с Linux | Документы Microsoft"
description: "Как tooa диск tooattach новых или существующих данных виртуальных Машин Linux в Azure портала с помощью hello hello модели развертывания диспетчера ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Как tooattach данных на диске tooa виртуальных Машин Linux в hello портал Azure
В этой статье показано, как tooattach новые и существующие диски виртуальной машины через портал Azure hello tooa Linux. Вы также можете [присоединения tooa диска данных виртуальной Машины Windows в hello портал Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Вы можете toouse либо дисков Azure управляемых или неуправляемых дисков. Управляемый диски обрабатываются hello платформы Azure и не требуют toostore любые предварительные и расположение их. Неуправляемые диски требуют учетную запись хранения и применения некоторых [квот и ограничений](../../azure-subscription-service-limits.md#storage-limits). Дополнительные сведения об Управляемых дисках Azure см. в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).

Прежде чем присоединять tooyour дисков виртуальной Машины, ознакомьтесь со следующими советами:

* размер Hello hello виртуальной машины определяет число дисков, можно присоединить. Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* toouse хранилище Premium необходимо виртуальную машину серии DS или GS-series. Эти виртуальные машины позволяют использовать диски уровня "Премиум" и "Стандартный". Хранилище Premium доступно в определенных регионах. Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Машины toovirtual присоединенные диски находятся фактически VHD-файлов, хранящихся в Azure. Дополнительную информацию см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Найти hello виртуальную машину
1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Hello концентратора меню **виртуальные машины**.
3. Выберите виртуальную машину hello из списка hello.
4. toohello виртуальной машины, в колонке **Essentials**, нажмите кнопку **дисков**.
   
    ![Открытие параметров диска](./media/attach-disk-portal/find-disk-settings.png)

Продолжайте, следуя указаниям по подключению [управляемого](#use-azure-managed-disks) или [неуправляемого диска](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Использование Управляемых дисков Azure

### <a name="attach-a-new-disk"></a>Подключение нового диска

1. На hello **дисков** колонка, щелкните **+ добавить диск данных**.
2. Щелкните раскрывающееся меню hello для **имя** и выберите **создать диск**:

    ![Создание управляемого диска Azure](./media/attach-disk-portal/create-new-md.png)

3. Введите имя управляемого диска. Просмотрите параметры по умолчанию hello, обновление при необходимости и щелкните **создать**.
   
   ![Просмотр параметров диска](./media/attach-disk-portal/create-new-md-settings.png)

4. Нажмите кнопку **Сохранить** toocreate hello управляемого диска и обновление конфигурации виртуальной Машины hello:

   ![Сохранение нового управляемого диска Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**. Как управляемый дисков в ресурсе верхнего уровня, диск hello появится в корне hello группа ресурсов «hello»:

   ![Управляемый диск Azure в группе ресурсов](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Подключение существующего диска
1. На hello **дисков** колонка, щелкните **+ добавить диск данных**.
2. Щелкните раскрывающееся меню hello для **имя** tooview список существующих управляемых диски доступны tooyour подписки Azure. Выберите hello управляемый tooattach диска.

   ![Подключение имеющегося управляемого диска Azure](./media/attach-disk-portal/select-existing-md.png)

3. Нажмите кнопку **Сохранить** существующие tooattach hello управляемого диска и обновление конфигурации виртуальной Машины hello:
   
   ![Сохранение обновлений управляемого диска Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. После Azure присоединяет hello диск toohello виртуальной машины, он будет отображен в параметры диска hello виртуальной машины в группе **диски с данными**.

## <a name="use-unmanaged-disks"></a>Использование неуправляемых дисков

### <a name="attach-a-new-disk"></a>Подключение нового диска

1. На hello **дисков** колонка, щелкните **+ добавить диск данных**.
2. Просмотрите параметры по умолчанию hello, обновление при необходимости и щелкните **ОК**.
   
   ![Просмотр параметров диска](./media/attach-disk-portal/attach-new.png)
3. Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**.

### <a name="attach-an-existing-disk"></a>Подключение существующего диска
1. На hello **дисков** колонка, щелкните **+ добавить диск данных**.
2. В разделе **Подключение существующего диска** щелкните **VHD-файл**.
   
   ![Подключение существующего диска](./media/attach-disk-portal/attach-existing.png)
3. В разделе **учетные записи хранения**, выберите учетную запись hello и контейнер, хранящий hello VHD-файл.
   
   ![Поиск расположения VHD](./media/attach-disk-portal/find-storage-container.png)
4. Выберите VHD-файл hello.
5. В разделе **подключить существующий диск**, файл hello, выбранной в списке под **VHD-файл**. Нажмите кнопку **ОК**.
6. После Azure присоединяет hello диск toohello виртуальной машины, он будет отображен в параметры диска hello виртуальной машины в группе **диски с данными**.


## <a name="next-steps"></a>Дальнейшие действия
После добавления hello диска необходимо tooprepare его для использования. Дополнительные сведения см. в разделе [Инициализация нового диска данных в Linux](add-disk.md).
