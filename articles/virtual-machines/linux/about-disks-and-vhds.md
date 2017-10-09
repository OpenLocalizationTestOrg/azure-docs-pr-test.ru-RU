---
title: "aaaAbout дисков и виртуальных жестких дисков виртуальных машин Microsoft Azure Linux | Документы Microsoft"
description: "Дополнительные сведения об основах hello дисков и виртуальных жестких дисков для виртуальных машин Linux в Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 862217e4f15ff8fd2e08de71386c4f367d0c39db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Сведения о дисках и виртуальных жестких дисках для виртуальных машин Azure под управлением Linux
Так же, как и любой другой компьютер виртуальные машины в Azure используют дисков, когда toostore месте операционной системы, приложений и данных. Все виртуальные машины Azure имеют по крайней мере два диска — диск операционной системы Linux и временный диск. Hello диск операционной системы создается из образа, а hello диска операционной системы и образа hello, фактически виртуальные жесткие диски (VHD) хранятся в учетной записи хранилища Azure. Кроме того, виртуальные машины могут иметь один или несколько дисков данных, которые также хранятся на виртуальных жестких дисках. 

В этой статье мы поговорим о различных вариантах hello для дисков hello и затем рассматриваются различные типы дисков можно создавать и использовать hello. Также доступна версия этой статьи для [виртуальных машин Windows](../windows/about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Диски, используемые виртуальными машинами

Давайте рассмотрим, как используются диски hello в hello виртуальных машин.

## <a name="operating-system-disk"></a>Диск операционной системы
У каждой виртуальной машины есть один подключенный диск операционной системы. Он зарегистрирован как диск SATA и обозначается как /dev/sda по умолчанию. Максимальная емкость этого диска составляет 2048 ГБ. 

## <a name="temporary-disk"></a>Временный диск
У каждой виртуальной машины есть временный диск. временный диск Hello предоставляет краткосрочного хранения приложениями и процессами и предполагаемого tooonly хранения данных, таких как страница или файлы подкачки. Данные на временном диске hello могут быть потеряны во время [события обслуживания](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) или если вы [повторного развертывания виртуальной Машины](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Во время стандартной перезагрузки hello ВМ должен сохранять hello данные на временном диске hello.

На виртуальных машинах Linux диск hello обычно является **/dev/sdb** и форматируются и подключено слишком**/mnt** по hello агент Azure Linux. размер Hello hello временного диска зависит от размера hello hello виртуальной машины. Чтобы узнать больше, ознакомьтесь с [размерами виртуальных машин Linux](../windows/sizes.md).

Дополнительные сведения об использовании hello временный диск Azure см. в разделе [основные сведения о временном диске hello на виртуальных машинах Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Диск данных
Диск с данными — данные приложения toostore вложенного tooa виртуальной машины или другие данные, необходимые tookeep виртуального жесткого диска. Диски данных регистрируются как диски SCSI и обозначаются любой указанной буквой. Максимальная емкость каждого диска составляет 4095 ГБ. Hello размер hello виртуальной машины определяет число дисков, можно присоединить tooit и hello тип хранилища, можно использовать toohost hello дисков.

> [!NOTE]
> Чтобы узнать больше о емкости виртуальных машин, ознакомьтесь с [размерами виртуальных машин Linux](../windows/sizes.md).
> 

Azure создает диск операционной системы при создании виртуальной машины из образа. При использовании образа, включающее диски данных Azure также создает hello диски с данными при создании виртуальной машины hello. В противном случае диски с данными добавляются после создания виртуальной машины hello.

Виртуальная машина tooa диски данных в любое время можно добавить путем **присоединение** hello диск toohello виртуальной машины. Можно использовать VHD, который вы загруженный или скопированный tooyour учетной записи хранилища или один, Azure создает для вас. При подключении диска данных связывает hello VHD-файл с hello виртуальной Машины, размещая аренды на hello виртуального жесткого диска, поэтому его нельзя удалить из хранилища, когда он присоединен по-прежнему.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Устранение неполадок
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Дальнейшие действия
* [Присоединить диск](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd дополнительное хранилище для виртуальной Машины.
* [Настройте программный RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), чтобы обеспечить избыточность.
* [Запишите образ виртуальной машины Linux](./classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json), чтобы иметь возможность быстро развернуть дополнительные виртуальные машины.

