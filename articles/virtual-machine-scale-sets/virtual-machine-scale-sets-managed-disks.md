---
title: "aaaUsing управляемых диски с Azure наборы масштабирования виртуальных машин | Документы Microsoft"
description: "Узнайте, почему и как toouse управляемых дисках с наборы масштабирования виртуальных машин"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Масштабируемые наборы виртуальных машин Azure и управляемые диски

[Масштабируемые наборы виртуальных машин](/azure/virtual-machine-scale-sets/) Azure теперь поддерживают виртуальные машины с управляемыми дисками. Использование управляемых дисков с масштабируемыми наборами имеет ряд преимуществ, в частности следующие:

* Больше не нужна toopre-Создание и управление ими диски hello ОС toostore учетных записей хранилища для виртуальных машин для набора масштабирования hello.

* Можно присоединить управляемых дисков toohello шкалы набора данных.

* благодаря управляемым дискам емкость масштабируемого набора может достигать 1000 виртуальных машин (на базе образа платформы) или 100 виртуальных машин (на базе пользовательского образа).

## <a name="get-started"></a>Начало работы

Простой способ tooget работы с наборами шкалы управляемого диска — toodeploy один из hello портал Azure. Дополнительные сведения см. в [этой статье](./virtual-machine-scale-sets-portal-create.md). Другой простой способ запуска tooget — toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy в наборе. Hello следующем примере показано, как набор масштабирования с 10 виртуальных машин, каждая из которых диск объемом 50 ГБ и 100 ГБ данных на основе toocreate Ubuntu:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Кроме того, может выглядеть в hello [в репозитории GitHub шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) для папок, содержащих `vmss` toosee готовые примеры шаблонов, развертываемые набора масштабирования. tootell, какие шаблоны, использующих управляемый диски, можно ссылаться слишком[этот список](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об управляемых дисках в целом см. в [этой статье](../virtual-machines/windows/managed-disks-overview.md).

toosee tooconvert задает масштаб tooprovision шаблона диспетчера ресурсов с управляемых дисках, разделе [в этой статье](./virtual-machine-scale-sets-convert-template-to-md.md). Hello шаблоны диспетчера ресурсов toohello же изменения применяются toohello Azure REST API.

в разделе toolearn Подробнее об использовании дисков данных, управляемых с помощью набора масштабирования [в этой статье](./virtual-machine-scale-sets-attached-disks.md).

Работа с наборами большого объема toobegin ссылаться слишком[в этой статье](./virtual-machine-scale-sets-placement-groups.md).


