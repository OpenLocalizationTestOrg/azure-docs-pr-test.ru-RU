---
title: "Перемещение каналов ExpressRoute с классической tooResource диспетчера: PowerShell: Azure | Документы Microsoft"
description: "На этой странице описаны как toomove toohello классический канала диспетчера ресурсов развертывания модели с помощью PowerShell."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Перемещение каналов ExpressRoute с hello классический toohello диспетчера ресурсов развертывания модели с помощью PowerShell

toouse канал ExpressRoute для классического hello и модели развертывания диспетчера ресурсов, необходимо переместить модель развертывания диспетчера ресурсов toohello цепи hello. Hello следующие разделы помогут перемещение ваш канал с помощью PowerShell.

## <a name="before-you-begin"></a>Перед началом работы

* Убедитесь, что последняя версия hello модули Azure PowerShell hello (по крайней мере версии 1.0). Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
* Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
* Проверьте сведения hello предоставляется на условиях [переход с классической tooResource диспетчера канал ExpressRoute](expressroute-move.md). Убедитесь, что полностью понимаете принципы hello ограничения и ограничения.
* Убедитесь, что цепь hello полностью в hello классической модели развертывания.
* Убедитесь, что группы ресурсов, который был создан в модели развертывания диспетчера ресурсов hello.

## <a name="move-an-expressroute-circuit"></a>Перемещение канала ExpressRoute

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Шаг 1: Сведения о канале сбор hello классической модели развертывания

Войдите в toohello Azure классическую среду и собирать hello ключа службы.

1. Войдите в tooyour учетная запись Azure.

  ```powershell
  Add-AzureAccount
  ```

2. Выберите соответствующую подписку Azure hello.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Импортируйте модули hello PowerShell для Azure и ExpressRoute.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Воспользуйтесь командлетом hello tooget hello службы ключей для всех схем ExpressRoute. После получения ключей hello, скопируйте hello **ключ службы** hello канала, что требуется модели развертывания диспетчера ресурсов toohello toomove.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Шаг 2. Вход и создание группы ресурсов

Войдите в диспетчер ресурсов среды toohello и создать новую группу ресурсов.

1. Войдите в среду tooyour диспетчера ресурсов Azure.

  ```powershell
  Login-AzureRmAccount
  ```

2. Выберите соответствующую подписку Azure hello.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Если у вас еще нет группы ресурсов, измените фрагмент кода hello ниже toocreate новую группу ресурсов.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Шаг 3: Перемещение модели развертывания диспетчера ресурсов toohello цепь ExpressRoute hello

Вы являются toomove теперь готовы к каналу ExpressRoute от hello классической модели toohello диспетчера ресурсов развертывания модели развертывания. Прежде чем продолжить, просмотрите сведения hello в [перемещение канал ExpressRoute от модели развертывания диспетчера ресурсов hello классический toohello](expressroute-move.md).

toomove ваш канал, изменение и выполните следующий фрагмент кода hello:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> После завершения перемещения hello hello новое имя, указанное в предыдущий командлет hello будет используется tooaddress hello ресурсов. по существу Hello канала будет переименован.
> 

## <a name="modify-circuit-access"></a>Изменение доступа к каналу

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable доступа цепь ExpressRoute для обеих моделей развертывания

После перемещения классический используемой модели развертывания toohello цепь ExpressRoute диспетчера ресурсов, можно включить доступ tooboth развертывания моделей. Выполните следующие командлеты tooenable доступа tooboth развертывания моделей hello.

1. Получите сведения о канале hello.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Задать tooTRUE «Разрешить классический операции».

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Обновление схемы hello. После успешного завершения этой операции можно канала может tooview hello в hello классической модели развертывания.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Выполните приведенные ниже сведения hello tooget командлета из hello канал ExpressRoute hello. Должен быть ключ службы может toosee hello.

  ```powershell
  get-azurededicatedcircuit
  ```

5. Теперь вы можете управлять ссылки toohello каналом expressroute команды hello классическое развертывание модели для классических виртуальных сетей, а также команд hello диспетчера ресурсов для виртуальных сетей диспетчера ресурсов. Hello ниже статьях помогают управлять ссылки toohello канал ExpressRoute:

    * [Связать вашей виртуальной сети tooyour канал ExpressRoute в модели развертывания диспетчера ресурсов hello](expressroute-howto-linkvnet-arm.md)
    * [Связать вашей виртуальной сети tooyour канал ExpressRoute в hello классической модели развертывания](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>toodisable ExpressRoute канала доступа toohello классической модели развертывания

Запустите следующие командлеты toodisable доступа toohello классической модели развертывания hello.

1. Возвращает подробные сведения о hello канал ExpressRoute.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Задать tooFALSE «Разрешить классический операции».

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Обновление схемы hello. После успешного завершения этой операции, не будет возможности tooview цепи hello в hello классической модели развертывания.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Дальнейшие действия

* [Создание и изменение маршрутизации для канала ExpressRoute](expressroute-howto-routing-arm.md)
* [Связать вашей виртуальной сети tooyour канал ExpressRoute](expressroute-howto-linkvnet-arm.md)
