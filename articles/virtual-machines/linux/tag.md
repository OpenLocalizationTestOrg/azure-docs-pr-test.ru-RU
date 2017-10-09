---
title: "aaaHow tootag виртуальной машине Azure Linux | Документы Microsoft"
description: "Дополнительные сведения о виртуальной машине Azure Linux, созданные в Azure с помощью модели развертывания диспетчера ресурсов hello тегов."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Как tootag виртуальной машины Linux в Azure
Этой статье описываются различные способы tootag виртуальной машины Linux в Azure через hello модели развертывания диспетчера ресурсов. Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов. В настоящее время Azure поддерживает теги too15 каждого ресурса и группы ресурсов. Теги можно поместить в ресурс во время создания hello или добавлены tooan существующий ресурс. Обратите внимание, теги поддерживаются для ресурсов, созданные с помощью модели развертывания диспетчера ресурсов hello только.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Отметка тегами с помощью интерфейса командной строки Azure
toobegin, требуется hello последней [Azure CLI 2.0 (Предварительная версия)](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Можно также выполнить следующие действия с hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Можно просмотреть все свойства для данной виртуальной машине, в том числе теги hello, с помощью этой команды:

        az vm show --resource-group MyResourceGroup --name MyTestVM

tooadd новый тег виртуальной Машины через hello Azure CLI можно использовать hello `azure vm update` команды и параметра тег hello **--задать**:

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

теги tooremove можно использовать hello **--удаление** параметр в hello `azure vm update` команды.

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


Теперь, когда мы применили теги tooour ресурсы Azure CLI и hello портала, давайте рассмотрим toosee сведения об использовании hello hello теги в портале выставления счетов hello.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о тегов ресурсам Azure в разделе [Обзор диспетчера ресурсов Azure] [ Azure Resource Manager Overview] и [tooorganize с помощью тегов ресурсов Azure] [ Using Tags tooorganize your Azure Resources].
* toosee теги помогают управлять использование ресурсов Azure разделе [основные сведения о счете Azure] [ Understanding your Azure Bill] и [анализировать потребления ресурсов Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
