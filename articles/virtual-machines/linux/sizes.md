---
title: "изменяет размер aaaLinux ВМ в Azure | Документы Microsoft"
description: "Список hello различные размеры, доступные для виртуальных машин Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a>Размеры виртуальных машин Linux в Azure
В этой статье описываются доступные размеры hello и параметры для hello виртуальных машинах Azure можно использовать toorun Linux приложений и рабочих нагрузок. Он также предоставляет toobe вопросы развертывания учитывать при планировании toouse эти ресурсы. Также доступна версия этой статьи для [виртуальных машин Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


| Тип                     | Размеры           |    Описание       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Универсальные](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7  | Сбалансированное соотношение ресурсов ЦП и памяти. Идеально подходит для тестирования и разработки, toomedium небольших баз данных и низким toomedium трафик веб-серверов. |
| [Оптимизированные для вычислений](sizes-compute.md)        | Fs, F             | Высокое соотношение ресурсов ЦП и памяти. Подходят для веб-серверов со средним объемом трафика, сетевых устройств, пакетных процессов и серверов приложений.        |
| [Оптимизированные для памяти](sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Высокое соотношение ресурсов памяти и ядра. Идеально подходит для серверов реляционной базы данных, кэши средний toolarge и аналитики в памяти.                 |
| [Оптимизированные для хранилища](sizes-storage.md)        | Ls                | Высокая пропускная способность дисков и количество операций ввода-вывода. Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео. Доступны виртуальные машины одним или несколькими GPU.       |
| [Для высокопроизводительных вычислений](sizes-hpc.md) | H, A8–A11          | Виртуальные машины с самыми быстрыми и мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA). 

<br>

- Сведения о стоимости hello разного размера, в разделе [расценки на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux). 
- Доступность размеров виртуальных машин см. в статье [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).
- Общие ограничения toosee на виртуальных машинах Azure, в разделе [подписка Azure и ограничения служб, квоты и ограничения](../../azure-subscription-service-limits.md).
- Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](../windows/acu.md) сравнить производительность вычислений для различных номеров SKU Azure.


## <a name="rest-api"></a>Rest API

Сведения об использовании tooquery hello API-интерфейса REST для размеров виртуальных Машин см. в следующем hello:

- [List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Вывод доступных размеров виртуальных машин для изменения размеров)
- [List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Вывод доступных размеров виртуальных машин для подписки)
- [List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Вывод доступных размеров виртуальных машин в группе доступности)

## <a name="acu"></a>ACU

Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о размерах виртуальных Машин различных hello, которые доступны.
- [Универсальные](sizes-general.md)
- [Оптимизированные для вычислений](sizes-compute.md)
- [Оптимизированные для памяти](sizes-memory.md)
- [Оптимизированные для хранилища](sizes-storage.md)
- [GPU](sizes-gpu.md)
- [Для высокопроизводительных вычислений](sizes-hpc.md)



