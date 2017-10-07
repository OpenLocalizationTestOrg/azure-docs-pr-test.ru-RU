---
title: "средства aaaCommunity — перемещение tooAzure классические ресурсы диспетчера ресурсов | Документы Microsoft"
description: "Эти средства hello каталоги статьи, предоставляемые hello сообщества toohelp миграции ресурсов IaaS с toohello классической модели развертывания диспетчера ресурсов Azure."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>Ресурсы IaaS toomigrate из tooAzure классического Resource Manager tools сообщества
Это статье каталоги hello средства, которые были дополнены по tooassist сообщества hello миграции IaaS ресурсов от toohello классической модели развертывания диспетчера ресурсов Azure.

> [!NOTE]
> Эти инструменты официально не поддерживаются службой поддержки Майкрософт. Таким образом они открыты исходный код на GitHub, и мы довольны tooaccept PR для исправления или дополнительных сценариев. tooreport проблему, используйте GitHub проблемы функции hello.
> 
> Перенос с использованием этих инструментов вызовет простой классической виртуальной машины. Если вы хотите выполнить поддерживаемый платформой перенос, см. следующие статьи: 
> 
>   * [Поддерживаемые платформой миграции IaaS ресурсов из классической tooAzure диспетчера ресурсов стека](migration-classic-resource-manager-overview.md)
>   * [Технические близкое знакомство с платформой поддерживается миграция из tooAzure классический диспетчер ресурсов](migration-classic-resource-manager-deep-dive.md)
>   * [Перенос ресурсов IaaS из классической tooAzure диспетчера ресурсов с помощью Azure PowerShell](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
Это набор средств поддержки создана как часть enterprise для миграции из tooAzure управления службами Azure Resource Manager. Это средство позволяет tooreplicate инфраструктуры в другую подписку, который может использоваться для проверки миграции и положите проблемы, перед выполнением миграции hello на вашей производственной подписке.

[Документацию к инструменту toohello ссылку](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz является дополнительным параметром toomigrate полный набор классические ресурсы IaaS диспетчера ресурсов tooAzure ресурсов IaaS. Hello миграции могут встречаться в hello же подписки или между разными подписками и типы подписок (ex: подписок CSP).

[Документацию к инструменту toohello ссылку](https://github.com/Azure/migAz)

## <a name="next-steps"></a>Дальнейшие действия

* [Общие сведения о миграции поддерживаются платформы IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Планирование миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Использовать ресурсы IaaS PowerShell toomigrate из классической tooAzure диспетчера ресурсов](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Использовать ресурсы IaaS toomigrate CLI из классической tooAzure диспетчера ресурсов](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Распространенные ошибки миграции](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Просмотрите hello наиболее часто задаваемые вопросы о миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

