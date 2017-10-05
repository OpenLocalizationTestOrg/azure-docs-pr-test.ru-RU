---
title: "Перемещение каналов ExpressRoute из классической модели развертывания в модель Resource Manager с помощью PowerShell и Azure | Документация Майкрософт"
description: "В этой статье описывается перемещение классического канала в модель развертывания Resource Manager с помощью PowerShell."
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
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="930a5-103">Перемещение каналов ExpressRoute из классической модели развертывания в модель Resource Manager с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="930a5-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="930a5-104">Чтобы канал ExpressRoute можно было использовать в классической модели развертывания и в модели Resource Manager, необходимо переместить его в модель развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="930a5-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="930a5-105">Сведения о перемещении канала с помощью PowerShell содержатся в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="930a5-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="930a5-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="930a5-106">Before you begin</span></span>

* <span data-ttu-id="930a5-107">Убедитесь в наличии последней версии модулей Azure PowerShell (не ниже версии 1.0).</span><span class="sxs-lookup"><span data-stu-id="930a5-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="930a5-108">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="930a5-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="930a5-109">Не забудьте изучить [предварительные требования](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md) и [рабочие процессы](expressroute-workflows.md), прежде чем приступать к настройке.</span><span class="sxs-lookup"><span data-stu-id="930a5-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="930a5-110">Просмотрите сведения в статье [Перемещение каналов ExpressRoute из классической модели развертывания в модель развертывания с помощью Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="930a5-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="930a5-111">Убедитесь, что вам полностью понятны пределы и ограничения.</span><span class="sxs-lookup"><span data-stu-id="930a5-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="930a5-112">Убедитесь, что канал полноценно работает в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="930a5-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="930a5-113">Убедитесь в наличии группы ресурсов, созданной в модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="930a5-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="930a5-114">Перемещение канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="930a5-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="930a5-115">Шаг 1. Соберите сведения о канале из классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="930a5-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="930a5-116">Войдите в классическую среду Azure и получите ключ службы.</span><span class="sxs-lookup"><span data-stu-id="930a5-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="930a5-117">Войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="930a5-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="930a5-118">Выберите соответствующую подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="930a5-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="930a5-119">Импортируйте модули PowerShell для Azure и ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="930a5-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="930a5-120">Используйте указанный ниже командлет, чтобы получить ключи службы для всех каналов ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="930a5-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="930a5-121">После получения ключей скопируйте **ключ службы** канала, который требуется переместить в модель развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="930a5-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="930a5-122">Шаг 2. Вход и создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="930a5-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="930a5-123">Войдите в среду Resource Manager и создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="930a5-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="930a5-124">Войдите в среду Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="930a5-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="930a5-125">Выберите соответствующую подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="930a5-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="930a5-126">Измените следующий фрагмент, чтобы создать группу ресурсов, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="930a5-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="930a5-127">Шаг 3. Перемещение канала ExpressRoute в модель развертывания Resource Manager</span><span class="sxs-lookup"><span data-stu-id="930a5-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="930a5-128">Теперь все готово для перемещения канала ExpressRoute из классической модели развертывания в модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="930a5-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="930a5-129">Прежде чем продолжить, просмотрите сведения в статье [Перемещение каналов ExpressRoute из классической модели развертывания в модель развертывания с помощью Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="930a5-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="930a5-130">Чтобы переместить канал, измените и выполните следующий фрагмент:</span><span class="sxs-lookup"><span data-stu-id="930a5-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="930a5-131">После завершения перемещения новое имя, указанное в предыдущем командлете, будет использоваться для адресации ресурсов.</span><span class="sxs-lookup"><span data-stu-id="930a5-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="930a5-132">По существу канал будет переименован.</span><span class="sxs-lookup"><span data-stu-id="930a5-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="930a5-133">Изменение доступа к каналу</span><span class="sxs-lookup"><span data-stu-id="930a5-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="930a5-134">Включение доступа к каналу ExpressRoute для обеих моделей развертывания</span><span class="sxs-lookup"><span data-stu-id="930a5-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="930a5-135">После перемещения классического канала ExpressRoute в модель развертывания Resource Manager его можно сделать доступным для обеих моделей развертывания.</span><span class="sxs-lookup"><span data-stu-id="930a5-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="930a5-136">Выполните следующие командлеты, чтобы разрешить доступ для обеих моделей развертывания:</span><span class="sxs-lookup"><span data-stu-id="930a5-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="930a5-137">Получите сведения о канале.</span><span class="sxs-lookup"><span data-stu-id="930a5-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="930a5-138">Задайте параметру "Allow Classic Operations" (Разрешить классические операции) значение TRUE.</span><span class="sxs-lookup"><span data-stu-id="930a5-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="930a5-139">Обновите канал.</span><span class="sxs-lookup"><span data-stu-id="930a5-139">Update the circuit.</span></span> <span data-ttu-id="930a5-140">После успешного завершения этой операции канал будет отображаться в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="930a5-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="930a5-141">Выполните следующий командлет, чтобы получить сведения о канале ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="930a5-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="930a5-142">Выходные данные должны содержать ключ службы.</span><span class="sxs-lookup"><span data-stu-id="930a5-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="930a5-143">Теперь вы можете управлять связями с каналом ExpressRoute с помощью команд классической модели развертывания для классических виртуальных сетей, а с помощью команд Resource Manager — для виртуальных сетей Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="930a5-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="930a5-144">Следующие статьи содержат сведения об управлении ссылками на канал ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="930a5-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="930a5-145">Связывание виртуальных сетей с каналами ExpressRoute в модели развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="930a5-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="930a5-146">Связывание виртуальных сетей с каналами ExpressRoute в классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="930a5-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="930a5-147">Отключение доступа к каналу ExpressRoute для классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="930a5-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="930a5-148">Выполните следующий командлет, чтобы отключить доступ для классической модели развертывания:</span><span class="sxs-lookup"><span data-stu-id="930a5-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="930a5-149">Получите сведения о канале ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="930a5-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="930a5-150">Задайте параметру "Allow Classic Operations" (Разрешить классические операции) значение FALSE.</span><span class="sxs-lookup"><span data-stu-id="930a5-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="930a5-151">Обновите канал.</span><span class="sxs-lookup"><span data-stu-id="930a5-151">Update the circuit.</span></span> <span data-ttu-id="930a5-152">После успешного завершения этой операции канал не будет отображаться в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="930a5-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="930a5-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="930a5-153">Next steps</span></span>

* [<span data-ttu-id="930a5-154">Создание и изменение маршрутизации для канала ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="930a5-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="930a5-155">Связывание виртуальной сети с каналом ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="930a5-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)