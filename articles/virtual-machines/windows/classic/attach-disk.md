---
title: "aaaAttach tooa диска классической виртуальной Машине Azure | Документы Microsoft"
description: "Присоединение данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания и инициализировать его."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Присоединение данных диска tooa Windows виртуальную машину, созданную с помощью hello классической модели развертывания
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

В этой статье показано, как новые и существующие диски tooattach созданы с hello классического развертывания модели tooa виртуальной машины Windows с помощью hello портал Azure.

Вы также можете [присоединения tooa диска данных виртуальной Машины с Linux в hello портал Azure](../../linux/attach-disk-portal.md).

Прежде чем подключить диск, ознакомьтесь со следующими советами.

* размер Hello hello виртуальной машины определяет число дисков, можно присоединить. Дополнительную информацию см. в статье [Размеры виртуальных машин](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* toouse хранилище Premium необходимо виртуальную машину серии DS или GS-series. Эти виртуальные машины позволяют использовать диски из учетных записей хранения Premium и Standard. Хранилище Premium доступно в определенных регионах. Дополнительные сведения см. в разделе [Хранилище класса Premium: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Для нового диска не требуется toocreate его первого, так как Azure создает при его подключении.

Вы также можете [присоединить диск данных с помощью Powershell](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Найти hello виртуальную машину
1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите hello виртуальную машину из ресурсов hello в списке на панели мониторинга hello.
3. В левой области hello в разделе **параметры**, нажмите кнопку **дисков**.

    ![Открытие параметров диска](./media/attach-disk/virtualmachinedisks.png)

Продолжайте, следуя указаниям по подключению [нового](#option-1-attach-a-new-disk) или [существующего диска](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Вариант 1. Подключение и инициализация нового диска

1. На hello **дисков** колонка, щелкните **присоединения новой**.
2. Просмотрите параметры по умолчанию hello, обновление при необходимости и щелкните **ОК**.

   ![Просмотр параметров диска](./media/attach-disk/attach-new.png)

3. Azure создает диск hello и присоединяет его toohello виртуальной машины, новый диск hello указана в параметры диска hello виртуальной машины в группе **диски с данными**.

### <a name="initialize-a-new-data-disk"></a>Инициализация нового диска данных

1. Подключение toohello виртуальной машины. Инструкции см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. После входа в систему виртуальной машины toohello откройте **диспетчера сервера**. Выберите в левой области hello **файловых служб и служб хранилища**.

    ![Откройте диспетчер сервера.](../media/attach-disk-portal/fileandstorageservices.png)

3. Выберите **Диски**.
4. Hello **дисков** разделе перечислены диски hello. Чаще всего виртуальная машина содержит диск 0, диск 1 и диск 2. На диске 0 — диск операционной системы hello и диск 1 является hello временный диск 2 — диск данных hello вновь подключен toohello виртуальной машины. Hello списки диска данных hello раздел как **Неизвестный**.

 Щелкните правой кнопкой мыши диск hello и выберите **инициализировать**.

5. В случае получения уведомления, что при инициализации hello диска будут удалены все данные. Нажмите кнопку **Да** tooacknowledge hello предупреждение и инициализируйте hello диска. После завершения hello секции будут указаны как **GPT**. Щелкните правой кнопкой мыши диск hello и выберите **новый том**.

6. Выполните мастер hello, используя значения по умолчанию hello. По завершении мастер hello hello **тома** разделе перечислены hello новый том. Hello диск больше не подключен и готов toostore данных.

    ![Том успешно инициализирован](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Вариант 2. Подключение существующего диска
1. На hello **дисков** колонка, щелкните **присоединения существующего**.
2. В разделе **Подключение существующего диска** щелкните **Расположение**.

   ![Подключение существующего диска](./media/attach-disk/attachexistingdisksettings.png)
3. В разделе **учетные записи хранения**, выберите учетную запись hello и контейнер, хранящий hello VHD-файл.

   ![Поиск расположения VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Выберите VHD-файл hello.
5. В разделе **подключить существующий диск**, файл hello, выбранной в списке под **VHD-файл**. Нажмите кнопку **ОК**.
6. После Azure присоединяет hello диск toohello виртуальной машины, он будет отображен в параметры диска hello виртуальной машины в группе **диски с данными**.

## <a name="use-trim-with-standard-storage"></a>Использование функции TRIM в хранилище уровня "Стандартный"

Если вы используете хранилище уровня "Стандартный" (HDD), то следует включить функцию TRIM. TRIM удаляет неиспользуемые блоки на диске hello, начисляется только для хранения данных, который фактически используется. Использование функции TRIM может уменьшить затраты, включая затраты на неиспользуемые блоки, возникающие в результате удаления больших файлов.

Можно запустить это команда toocheck TRIM приветствия. На виртуальной машине Windows откройте командную строку и введите:

```
fsutil behavior query DisableDeleteNotify
```

Команда hello возвращает 0, Функция TRIM включения правильно. Если он возвращает 1, выполните следующие команды tooenable TRIM hello:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Дальнейшие действия
Если приложению требуются данные toostore диска D: hello toouse, вы можете [изменить букву временного диска Windows hello hello](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Дополнительные ресурсы
[О дисках и виртуальных жестких дисках для виртуальных машин](../../virtual-machines-linux-about-disks-vhds.md)
