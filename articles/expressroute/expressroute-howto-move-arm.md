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
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="324d1-103">Перемещение каналов ExpressRoute с hello классический toohello диспетчера ресурсов развертывания модели с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="324d1-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="324d1-104">toouse канал ExpressRoute для классического hello и модели развертывания диспетчера ресурсов, необходимо переместить модель развертывания диспетчера ресурсов toohello цепи hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="324d1-105">Hello следующие разделы помогут перемещение ваш канал с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="324d1-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="324d1-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="324d1-106">Before you begin</span></span>

* <span data-ttu-id="324d1-107">Убедитесь, что последняя версия hello модули Azure PowerShell hello (по крайней мере версии 1.0).</span><span class="sxs-lookup"><span data-stu-id="324d1-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="324d1-108">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="324d1-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="324d1-109">Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.</span><span class="sxs-lookup"><span data-stu-id="324d1-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="324d1-110">Проверьте сведения hello предоставляется на условиях [переход с классической tooResource диспетчера канал ExpressRoute](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="324d1-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="324d1-111">Убедитесь, что полностью понимаете принципы hello ограничения и ограничения.</span><span class="sxs-lookup"><span data-stu-id="324d1-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="324d1-112">Убедитесь, что цепь hello полностью в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="324d1-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="324d1-113">Убедитесь, что группы ресурсов, который был создан в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="324d1-114">Перемещение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="324d1-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="324d1-115">Шаг 1: Сведения о канале сбор hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="324d1-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="324d1-116">Войдите в toohello Azure классическую среду и собирать hello ключа службы.</span><span class="sxs-lookup"><span data-stu-id="324d1-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="324d1-117">Войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="324d1-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="324d1-118">Выберите соответствующую подписку Azure hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="324d1-119">Импортируйте модули hello PowerShell для Azure и ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="324d1-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="324d1-120">Воспользуйтесь командлетом hello tooget hello службы ключей для всех схем ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="324d1-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="324d1-121">После получения ключей hello, скопируйте hello **ключ службы** hello канала, что требуется модели развертывания диспетчера ресурсов toohello toomove.</span><span class="sxs-lookup"><span data-stu-id="324d1-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="324d1-122">Шаг 2. Вход и создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="324d1-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="324d1-123">Войдите в диспетчер ресурсов среды toohello и создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="324d1-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="324d1-124">Войдите в среду tooyour диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="324d1-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="324d1-125">Выберите соответствующую подписку Azure hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="324d1-126">Если у вас еще нет группы ресурсов, измените фрагмент кода hello ниже toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="324d1-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="324d1-127">Шаг 3: Перемещение модели развертывания диспетчера ресурсов toohello цепь ExpressRoute hello</span><span class="sxs-lookup"><span data-stu-id="324d1-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="324d1-128">Вы являются toomove теперь готовы к каналу ExpressRoute от hello классической модели toohello диспетчера ресурсов развертывания модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="324d1-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="324d1-129">Прежде чем продолжить, просмотрите сведения hello в [перемещение канал ExpressRoute от модели развертывания диспетчера ресурсов hello классический toohello](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="324d1-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="324d1-130">toomove ваш канал, изменение и выполните следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="324d1-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="324d1-131">После завершения перемещения hello hello новое имя, указанное в предыдущий командлет hello будет используется tooaddress hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="324d1-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="324d1-132">по существу Hello канала будет переименован.</span><span class="sxs-lookup"><span data-stu-id="324d1-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="324d1-133">Изменение доступа к каналу</span><span class="sxs-lookup"><span data-stu-id="324d1-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="324d1-134">tooenable доступа цепь ExpressRoute для обеих моделей развертывания</span><span class="sxs-lookup"><span data-stu-id="324d1-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="324d1-135">После перемещения классический используемой модели развертывания toohello цепь ExpressRoute диспетчера ресурсов, можно включить доступ tooboth развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="324d1-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="324d1-136">Выполните следующие командлеты tooenable доступа tooboth развертывания моделей hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="324d1-137">Получите сведения о канале hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="324d1-138">Задать tooTRUE «Разрешить классический операции».</span><span class="sxs-lookup"><span data-stu-id="324d1-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="324d1-139">Обновление схемы hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-139">Update hello circuit.</span></span> <span data-ttu-id="324d1-140">После успешного завершения этой операции можно канала может tooview hello в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="324d1-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="324d1-141">Выполните приведенные ниже сведения hello tooget командлета из hello канал ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="324d1-142">Должен быть ключ службы может toosee hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="324d1-143">Теперь вы можете управлять ссылки toohello каналом expressroute команды hello классическое развертывание модели для классических виртуальных сетей, а также команд hello диспетчера ресурсов для виртуальных сетей диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="324d1-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="324d1-144">Hello ниже статьях помогают управлять ссылки toohello канал ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="324d1-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="324d1-145">Связать вашей виртуальной сети tooyour канал ExpressRoute в модели развертывания диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="324d1-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="324d1-146">Связать вашей виртуальной сети tooyour канал ExpressRoute в hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="324d1-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="324d1-147">toodisable ExpressRoute канала доступа toohello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="324d1-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="324d1-148">Запустите следующие командлеты toodisable доступа toohello классической модели развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="324d1-149">Возвращает подробные сведения о hello канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="324d1-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="324d1-150">Задать tooFALSE «Разрешить классический операции».</span><span class="sxs-lookup"><span data-stu-id="324d1-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="324d1-151">Обновление схемы hello.</span><span class="sxs-lookup"><span data-stu-id="324d1-151">Update hello circuit.</span></span> <span data-ttu-id="324d1-152">После успешного завершения этой операции, не будет возможности tooview цепи hello в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="324d1-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="324d1-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="324d1-153">Next steps</span></span>

* [<span data-ttu-id="324d1-154">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="324d1-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="324d1-155">Связать вашей виртуальной сети tooyour канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="324d1-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
