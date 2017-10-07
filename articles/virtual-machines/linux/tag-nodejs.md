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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Как tootag виртуальной машины Linux в Azure
Этой статье описываются различные способы tootag виртуальной машины Linux в Azure через hello модели развертывания диспетчера ресурсов. Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов. В настоящее время Azure поддерживает теги too15 каждого ресурса и группы ресурсов. Теги можно поместить в ресурс во время создания hello или добавлены tooan существующий ресурс. Обратите внимание, теги поддерживаются для ресурсов, созданные с помощью модели развертывания диспетчера ресурсов hello только.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Отметка тегами с помощью интерфейса командной строки Azure
toobegin, [Установка и настройка hello Azure CLI](../../xplat-cli-azure-resource-manager.md) и убедитесь, что вы находитесь в режим диспетчера ресурсов (`azure config mode arm`).

Можно просмотреть все свойства для данной виртуальной машине, в том числе теги hello, с помощью этой команды:

        azure vm show -g MyResourceGroup -n MyTestVM

tooadd новый тег виртуальной Машины через hello Azure CLI можно использовать hello `azure vm set` команды и параметра тег hello **-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

tooremove все теги, можно использовать hello **– T** параметр в hello `azure vm set` команды.

        azure vm set – g MyResourceGroup –n MyTestVM -T


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
