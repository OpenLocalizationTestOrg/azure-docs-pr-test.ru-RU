---
title: "Установка aaaCreate доступности ВМ в Azure | Документы Microsoft"
description: "Сведения, как задать toocreate управляемого доступности или неуправляемые доступности для виртуальных машин с помощью Azure PowerShell или hello портала в модели развертывания диспетчера ресурсов hello."
keywords: "группа доступности"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="277da-104">Повышение уровня доступности виртуальной машины с помощью группы доступности Azure</span><span class="sxs-lookup"><span data-stu-id="277da-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="277da-105">Группы доступности предоставляют избыточности tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="277da-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="277da-106">Мы рекомендуем включить две или больше виртуальных машин в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="277da-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="277da-107">Эта конфигурация гарантирует, что во время любого запланированного или незапланированного события обслуживания, по крайней мере одной виртуальной машины будут доступны и соответствуют hello 99,95% соглашение об уровне ОБСЛУЖИВАНИЯ Azure.</span><span class="sxs-lookup"><span data-stu-id="277da-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="277da-108">Дополнительные сведения см. в разделе hello [соглашения об уровне ОБСЛУЖИВАНИЯ для виртуальных машин](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="277da-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="277da-109">Виртуальные машины должны быть созданы в hello же группе ресурсов, что группа доступности hello.</span><span class="sxs-lookup"><span data-stu-id="277da-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="277da-110">Часть toobe вашей ВМ группы доступности, вы должны toocreate hello доступности задать или пока пользователь создается первый ВМ в набор hello.</span><span class="sxs-lookup"><span data-stu-id="277da-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="277da-111">Если ВМ будет использовать управляемые дисков, hello доступности необходимо создать как набор управляемых доступности.</span><span class="sxs-lookup"><span data-stu-id="277da-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="277da-112">Дополнительные сведения о создании и использовании групп доступности см. в разделе [Управление доступностью виртуальных машин hello](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="277da-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="277da-113">Использование портала toocreate hello доступности задан до создания виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="277da-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="277da-114">В главном меню hello, щелкните **Обзор** и выберите **задает доступности**.</span><span class="sxs-lookup"><span data-stu-id="277da-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="277da-115">На hello **доступности задает колонке**, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="277da-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![Снимок экрана, показывающий hello добавить кнопку для создания нового набора доступности.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="277da-117">На hello **создать набор доступности** колонки, hello полные сведения для вашего набора.</span><span class="sxs-lookup"><span data-stu-id="277da-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![Снимок экрана, что показывает hello информацию, необходимую tooenter toocreate hello доступности задать.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="277da-119">**Имя** -hello имя должно быть 1 80 символов, состоящую из цифры, буквы, точки, символы подчеркивания и тире.</span><span class="sxs-lookup"><span data-stu-id="277da-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="277da-120">Hello первым символом должна быть буква или цифра.</span><span class="sxs-lookup"><span data-stu-id="277da-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="277da-121">Hello последним символом должны быть буквы, числа или знака подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="277da-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="277da-122">**Домены отказоустойчивости** -доменов сбоя определения hello группы виртуальных машин, которые совместно используют общие выключателем источника и сети.</span><span class="sxs-lookup"><span data-stu-id="277da-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="277da-123">По умолчанию виртуальные машины hello разделены в домены сбоя toothree и может быть измененные toobetween 1 и 3.</span><span class="sxs-lookup"><span data-stu-id="277da-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="277da-124">**Обновление доменов** - 5 доменами обновления назначаются по умолчанию и может иметь значение toobetween 1 до 20.</span><span class="sxs-lookup"><span data-stu-id="277da-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="277da-125">Домены обновления указания групп виртуальных машин и физического оборудования, можно перезагрузить в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="277da-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="277da-126">Например если мы указываем пять обновления для доменов, при более пяти виртуальные машины настроены в одной группе доступности, hello шестой виртуальной машины будут помещены в hello одном домене обновления как первая виртуальная машина hello hello седьмой в hello же UD как hello второй виртуальной машины и т. д.</span><span class="sxs-lookup"><span data-stu-id="277da-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="277da-127">Hello порядок перезагрузки hello не может быть последовательно, но только одно обновление домена будет перезагружен одновременно.</span><span class="sxs-lookup"><span data-stu-id="277da-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="277da-128">**Подписки** -выберите hello toouse подписки при наличии более одного.</span><span class="sxs-lookup"><span data-stu-id="277da-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="277da-129">**Группа ресурсов** -выберите существующую группу ресурсов, щелкнув стрелку hello и выбора группы ресурсов из hello раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="277da-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="277da-130">Также можно создать новую группу ресурсов, введя имя.</span><span class="sxs-lookup"><span data-stu-id="277da-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="277da-131">Hello имя может содержать следующие символы hello: буквы, цифры, точки, тире, символы подчеркивания и открывающей и закрывающей скобкой.</span><span class="sxs-lookup"><span data-stu-id="277da-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="277da-132">Имя Hello не может заканчиваться точкой.</span><span class="sxs-lookup"><span data-stu-id="277da-132">hello name cannot end in a period.</span></span> <span data-ttu-id="277da-133">Все hello виртуальных машин в группе доступности hello требуется toobe, созданных в hello же группе ресурсов, что группа доступности hello.</span><span class="sxs-lookup"><span data-stu-id="277da-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="277da-134">**Расположение** -выберите расположение из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="277da-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="277da-135">**Управляемый код** — выберите *Да* toocreate управляемого доступности задать toouse с виртуальными машинами, использующие управляемые диски для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="277da-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="277da-136">Выберите **нет** Если hello виртуальных машин, которые будут включены в набор hello использовать неуправляемый диски в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="277da-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="277da-137">После завершения ввода данных hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="277da-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="277da-138">Использование портала toocreate hello виртуальной машины и доступности равным hello же времени</span><span class="sxs-lookup"><span data-stu-id="277da-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="277da-139">При создании новой виртуальной Машины с помощью портала hello, можно также создать новый набор доступности для hello виртуальной Машины при создании hello первая виртуальная машина в наборе hello.</span><span class="sxs-lookup"><span data-stu-id="277da-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="277da-140">При выборе toouse управляемых диски для виртуальной Машины, создается набор управляемых доступности.</span><span class="sxs-lookup"><span data-stu-id="277da-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![Снимок экрана, показывающий hello процесс создания нового доступности при создании виртуальной Машины hello.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="277da-142">Добавить новый ВМ tooan существующий набор доступности hello портала</span><span class="sxs-lookup"><span data-stu-id="277da-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="277da-143">Для каждой дополнительной Виртуальной машине, должен входить в наборе hello, убедитесь в том, создайте его в hello же **группы ресурсов** и затем выберите hello доступности, существующие на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="277da-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![Снимок экрана настроек toouse tooselect существующую группу для виртуальной Машины.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="277da-145">Используйте PowerShell toocreate доступности задать</span><span class="sxs-lookup"><span data-stu-id="277da-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="277da-146">В этом примере создается именованный набор доступности **myAvailabilitySet** в hello **myResourceGroup** группы ресурсов в hello **Запад США** расположение.</span><span class="sxs-lookup"><span data-stu-id="277da-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="277da-147">Это необходимо сделать перед созданием hello toobe первая виртуальная машина, будут включены в набор hello.</span><span class="sxs-lookup"><span data-stu-id="277da-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="277da-148">Прежде чем начать, убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="277da-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="277da-149">Запустите hello следующие tooinstall команды.</span><span class="sxs-lookup"><span data-stu-id="277da-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="277da-150">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="277da-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="277da-151">Если для виртуальных машин вы используете управляемые диски, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="277da-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="277da-152">Если вы используете для виртуальных машин собственные учетные записи хранения, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="277da-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="277da-153">Дополнительные сведения см. в разделе [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="277da-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="277da-154">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="277da-154">Troubleshooting</span></span>
* <span data-ttu-id="277da-155">При создании виртуальной Машины, если набор доступности hello, которому требуется отсутствует в раскрывающемся списке hello hello портала может создать его в другой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="277da-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="277da-156">Если вы не знаете hello группы ресурсов для доступности задать, перейдите в меню toohello концентратора и нажмите кнопку обзора > toosee задает список доступности и групп ресурсов, которые они принадлежат к группы доступности.</span><span class="sxs-lookup"><span data-stu-id="277da-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="277da-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="277da-157">Next steps</span></span>
<span data-ttu-id="277da-158">Добавьте tooyour дополнительное хранилище виртуальной Машины, добавив дополнительный [диск данных](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="277da-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

