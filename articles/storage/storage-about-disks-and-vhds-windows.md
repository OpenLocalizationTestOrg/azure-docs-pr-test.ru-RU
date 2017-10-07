---
title: "aaaAbout дисков и виртуальных жестких дисков для виртуальных машин Windows Azure Майкрософт | Документы Microsoft"
description: "Дополнительные сведения об основах hello дисков и виртуальных жестких дисков для виртуальных машинах в Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Сведения о дисках и VHD для виртуальных машин Azure под управлением Windows
Так же, как и любой другой компьютер виртуальные машины в Azure используют дисков, когда toostore месте операционной системы, приложений и данных. Все виртуальные машины Azure имеют как минимум два диска — диск операционной системы Windows и временный диск. Hello диск операционной системы создается из образа, а hello диска операционной системы и образа hello, виртуальные жесткие диски (VHD) хранятся в учетной записи хранилища Azure. Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках. 

В этой статье мы поговорим о различных вариантах hello для дисков hello и затем рассматриваются различные типы дисков можно создавать и использовать hello. Также доступна версия этой статьи для [виртуальных машин Linux](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Диски, используемые виртуальными машинами

Давайте рассмотрим, как используются диски hello в hello виртуальных машин.

### <a name="operating-system-disk"></a>Диск операционной системы
У каждой виртуальной машины есть один подключенный диск операционной системы. Зарегистрирован как диск SATA и помечены как диск C: hello по умолчанию. Максимальная емкость этого диска составляет 2048 гигабайта (ГБ). 

### <a name="temporary-disk"></a>Временный диск
У каждой виртуальной машины есть временный диск. временный диск Hello предоставляет краткосрочного хранения приложениями и процессами и предполагаемого tooonly хранения данных, таких как страница или файлы подкачки. Данные на временном диске hello могут быть потеряны во время [события обслуживания](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) или если вы [повторного развертывания виртуальной Машины](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Во время стандартной перезагрузки hello ВМ должен сохранять hello данные на временном диске hello.

временный диск Hello обозначается как диск D: hello по умолчанию и он используется для хранения pagefile.sys. tooremap этот диск tooa другой буквой диска, в разделе [изменений hello букву временного диска Windows hello](../virtual-machines/windows/change-drive-letter.md). размер Hello hello временного диска зависит от размера hello hello виртуальной машины. Чтобы узнать больше, ознакомьтесь с [размерами виртуальных машин Windows](../virtual-machines/windows/sizes.md).

Дополнительные сведения об использовании hello временный диск Azure см. в разделе [основные сведения о временном диске hello на виртуальных машинах Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Диск данных
Диск с данными — данные приложения toostore вложенного tooa виртуальной машины или другие данные, необходимые tookeep виртуального жесткого диска. Диски данных регистрируются как диски SCSI и обозначаются любой указанной буквой. Максимальная емкость каждого диска составляет 4095 ГБ. Hello размер hello виртуальной машины определяет число дисков, можно присоединить tooit и hello тип хранилища, можно использовать toohost hello дисков.

> [!NOTE]
> Дополнительные сведения о емкости виртуальных машин см. в статье [Размеры виртуальных машин Windows](../virtual-machines/windows/sizes.md).
> 

Azure создает диск операционной системы при создании виртуальной машины из образа. При использовании образа, включающее диски данных Azure также создает hello диски с данными при создании виртуальной машины hello. В противном случае диски с данными добавляются после создания виртуальной машины hello.

Виртуальная машина tooa диски данных в любое время можно добавить путем **присоединение** hello диск toohello виртуальной машины. Можно использовать VHD, который вы загруженный или скопированный tooyour учетной записи хранилища или один, Azure создает для вас. При подключении диска данных связывает hello VHD-файл с hello виртуальной Машины, размещая аренды в hello виртуального жесткого диска, поэтому его нельзя удалить из хранилища, когда он присоединен по-прежнему.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Последняя рекомендация. Использование TRIM с неуправляемыми дисками уровня "Стандартный" 

Если вы используете неуправляемые диски уровня "Стандартный", то следует включить функцию TRIM. TRIM удаляет неиспользуемые блоки на диске hello, начисляется только для хранения данных, который фактически используется. Это позволяет сократить затраты, если вы создаете большие файлы, а затем удаляете их. 

Можно запустить это команда toocheck TRIM приветствия. На виртуальной машине Windows откройте командную строку и введите:


```
fsutil behavior query DisableDeleteNotify
```

Команда hello возвращает 0, Функция TRIM включения правильно. Если он возвращает 1, выполните следующие команды tooenable TRIM hello:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Примечание: Поддержка функции Trim начинается с Windows Server 2012 или Windows 8 и более поздних версий, см. в разделе [новый интерфейс API позволяет приложениям toosend «ОБРЕЗАТЬ и отменить сопоставление» подсказки toostorage мультимедиа](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Дальнейшие действия
* [Присоединить диск](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd дополнительное хранилище для виртуальной Машины.
* [Изменение буквы диска hello временного диска Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) , приложение может использовать диск D: hello для данных.

