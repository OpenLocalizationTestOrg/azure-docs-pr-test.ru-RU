---
title: "Перенос ExpressRoute связанные виртуальные сети из классической tooResource диспетчер: Azure: PowerShell | Документы Microsoft"
description: "На этой странице описаны как toomigrate связан tooResource виртуальных сетей Manager после перемещения ваш канал."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Миграция с tooResource классический диспетчер ExpressRoute связанные виртуальные сети

В этой статье объясняется, как Azure ExpressRoute toomigrate связан виртуальных сетей с hello классической модели toohello диспетчера ресурсов Azure развертывания модели развертывания после перемещения к каналу ExpressRoute. 


## <a name="before-you-begin"></a>Перед началом работы
* Проверьте наличие последней версии hello hello модули Azure PowerShell. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
* Проверьте сведения hello предоставляется на условиях [переход с классической tooResource диспетчера канал ExpressRoute](expressroute-move.md). Убедитесь, что полностью понимаете принципы hello ограничения и ограничения.
* Убедитесь, что цепь hello полностью в hello классической модели развертывания.
* Убедитесь, что группы ресурсов, который был создан в модели развертывания диспетчера ресурсов hello.
* Просмотрите hello Следующая документация по миграции ресурсов:

    * [Поддерживаемые платформы миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Вопросы и ответы: Поддерживаемые платформой миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Common errors during Classic to Azure Resource Manager migration](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Распространенные ошибки при переносе из классической модели на модель Azure Resource Manager)

## <a name="supported-and-unsupported-scenarios"></a>Поддерживаемые и неподдерживаемые сценарии

* Канал ExpressRoute можно перемещать из hello toohello классический диспетчер ресурсов среды без простоев. Любой канал ExpressRoute можно перемещать из классической toohello hello диспетчер ресурсов среды без простоев. Следуйте инструкциям в разделе hello [перемещение каналы ExpressRoute от hello классический toohello диспетчера ресурсов развертывания модели с помощью PowerShell](expressroute-howto-move-arm.md). Это подключенных toohello готовности к установке toomove ресурсы виртуальной сети.
* Виртуальные сети, шлюзы и связанные развертывания в виртуальной сети hello, вложенные tooan канал ExpressRoute, в которых может находиться в той же подписке hello миграции toohello диспетчер ресурсов среды без простоев. Вы можете использовать hello шаги описанных далее toomigrate ресурсы, такие как виртуальные сети, шлюзы и виртуальных машин, развернутых в виртуальной сети hello. Необходимо убедиться, что виртуальные сети hello настроены правильно прежде чем переносить их. 
* Виртуальные сети, шлюзы и связанных развертываний в виртуальной сети hello, которых нет в hello той же подписке, как hello канал ExpressRoute требуется некоторое время простоя toocomplete hello миграции. Последний раздел Hello hello документа описываются hello действия toobe за toomigrate ресурсы.
* Виртуальную сеть с обоими шлюзами (ExpressRoute и VPN-шлюз) нельзя переместить.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Переместить из классической tooResource диспетчера канал ExpressRoute
Необходимо переместить канал ExpressRoute из классической toohello hello диспетчер ресурсов среды, прежде чем пытаться toomigrate ресурсы, которые являются присоединен toohello канал ExpressRoute. tooaccomplish это задача, см. следующие статьи hello:

* Проверьте сведения hello предоставляется на условиях [переход с классической tooResource диспетчера канал ExpressRoute](expressroute-move.md).
* [Переместить канала из классической tooResource диспетчера с помощью Azure PowerShell](expressroute-howto-move-arm.md).
* С помощью портала управления службами Azure hello. Можно выполнить рабочий процесс hello слишком[создайте новый канал ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) и выберите вариант импорта hello. 

При этой операции прости не возникают. Вы можете продолжить tootransfer данных между вашей организацией и Microsoft hello миграции во время выполнения.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Перенос виртуальных сетей, шлюзов и связанных развертываний

Hello действия выполните toomigrate зависят ли ресурсы находятся в hello той же подписке и/или в разных подписках.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Перенос виртуальных сетей, шлюзы, и связанных развертываний в одной подписке hello, как hello канал ExpressRoute
В этом разделе описываются toomigrate toobe за действия hello виртуальной сети, шлюз и связанных развертываний в hello той же подписке, как hello канал ExpressRoute. При таком переносе простои не возникают. Вы можете продолжить toouse все ресурсы в процессе миграции hello. Hello плоскости управления блокируется во время миграции hello. 

1. Убедитесь, что канал ExpressRoute hello была перенесена в hello toohello классический диспетчер ресурсов среды.
2. Убедитесь, что hello виртуальной сети был подготовлен надлежащим образом для миграции hello.
3. Зарегистрируйте подписку для переноса ресурсов. tooregister подписки для миграции ресурсов, используйте hello, следующий фрагмент команды PowerShell:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Выполните проверку, подготовку и миграцию. toomove hello виртуальной сети, используйте hello, следующий фрагмент команды PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  Можно также прервать миграции, выполнив следующий командлет PowerShell hello:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Дальнейшие действия
* [Поддерживаемые платформы миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Технические близкое знакомство с платформа поддерживается перенос из классической tooAzure диспетчера ресурсов](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Вопросы и ответы: Поддерживаемые платформой миграции IaaS ресурсов от классических tooAzure диспетчера ресурсов](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Common errors during Classic to Azure Resource Manager migration](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Распространенные ошибки при переносе из классической модели на модель Azure Resource Manager)
