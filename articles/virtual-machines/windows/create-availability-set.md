---
title: "Создание группы доступности виртуальных машин в Azure | Документация Майкрософт"
description: "Узнайте, как создать управляемую или неуправляемую группу доступности для виртуальных машин посредством Azure PowerShell или портала в модели развертывания с помощью Resource Manager."
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="2353b-104">Повышение уровня доступности виртуальной машины с помощью группы доступности Azure</span><span class="sxs-lookup"><span data-stu-id="2353b-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="2353b-105">Группы доступности обеспечивают избыточность приложения.</span><span class="sxs-lookup"><span data-stu-id="2353b-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="2353b-106">Мы рекомендуем включить две или больше виртуальных машин в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="2353b-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="2353b-107">Эта конфигурация обеспечит доступность не менее одной виртуальной машины и достижение показателя 99,95 % уровня обслуживания (SLA) Azure как при событиях запланированного обслуживания, так и при незапланированного.</span><span class="sxs-lookup"><span data-stu-id="2353b-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="2353b-108">Дополнительные сведения см. в статье о [соглашении об уровне обслуживания для виртуальных машин](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="2353b-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2353b-109">Виртуальные машины должны быть созданы в той же группе ресурсов, что и группа доступности.</span><span class="sxs-lookup"><span data-stu-id="2353b-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="2353b-110">Если вы хотите, чтобы виртуальная машина входила в группу доступности, сначала нужно создать группу доступности, либо следует создать эту виртуальную машину в качестве первой виртуальной машины в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="2353b-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="2353b-111">Если виртуальная машина будет использовать управляемые диски, то должна быть создана управляемая группа доступности.</span><span class="sxs-lookup"><span data-stu-id="2353b-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="2353b-112">Дополнительную сведения о создании и использовании групп доступности см. в статье [Управление доступностью виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2353b-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="2353b-113">Создание группы доступности с помощью портала перед созданием виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2353b-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="2353b-114">В главном меню щелкните **Обзор** и выберите **Группы доступности**.</span><span class="sxs-lookup"><span data-stu-id="2353b-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="2353b-115">В **колонке "Группы доступности"** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2353b-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Снимок экрана, показывающий кнопку "Добавить" для создания новой группы доступности.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="2353b-117">В колонке **Создать группу доступности** заполните сведения для своей группы.</span><span class="sxs-lookup"><span data-stu-id="2353b-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Снимок экрана, показывающий, какие сведения необходимо ввести для создания группы доступности.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="2353b-119">**Имя** — имя должно содержать от 1 до 80 знаков, которыми могут быть цифры, буквы, точки, знаки подчеркивания и тире.</span><span class="sxs-lookup"><span data-stu-id="2353b-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="2353b-120">Первый знак должен быть буквой или цифрой.</span><span class="sxs-lookup"><span data-stu-id="2353b-120">The first character must be a letter or number.</span></span> <span data-ttu-id="2353b-121">Последний знак должен быть буквой, цифрой или знаком подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="2353b-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="2353b-122">**Домены сбоя** — домены сбоя определяют группу виртуальных машин, которые совместно используют общий источник питания и сетевой коммутатор.</span><span class="sxs-lookup"><span data-stu-id="2353b-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="2353b-123">По умолчанию виртуальные машины разделяются на несколько доменов сбоя, но не более трех. Их число можно менять от 1 до 3.</span><span class="sxs-lookup"><span data-stu-id="2353b-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="2353b-124">**Домены обновления** — пять доменов обновления назначаются по умолчанию, и их число можно изменить от 1 до 20.</span><span class="sxs-lookup"><span data-stu-id="2353b-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="2353b-125">Домены обновления — это группы виртуальных машин и базовое физическое оборудование, которое может быть перезагружено одновременно.</span><span class="sxs-lookup"><span data-stu-id="2353b-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="2353b-126">Например, если указать пять доменов обновления, то когда в одной группе доступности настраивается более пяти виртуальных машин, шестая виртуальная машина будет помещена в тот же домен обновления, что и первая виртуальная машина, седьмая — что и вторая, и т. д.</span><span class="sxs-lookup"><span data-stu-id="2353b-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="2353b-127">Порядок перезагрузки может не быть последовательным, но одновременно будет перезагружаться только один домен обновления.</span><span class="sxs-lookup"><span data-stu-id="2353b-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="2353b-128">**Подписка** — при наличии нескольких подписок выберите подписку, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="2353b-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="2353b-129">**Группа ресурсов** — выберите существующую группу ресурсов, щелкнув стрелку и выбрав группу ресурсов из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="2353b-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="2353b-130">Также можно создать новую группу ресурсов, введя имя.</span><span class="sxs-lookup"><span data-stu-id="2353b-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="2353b-131">Имя может содержать следующие знаки: буквы, цифры, точки, тире, знаки подчеркивания, а также открывающую и закрывающую скобки.</span><span class="sxs-lookup"><span data-stu-id="2353b-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="2353b-132">Имя не может заканчиваться точкой.</span><span class="sxs-lookup"><span data-stu-id="2353b-132">The name cannot end in a period.</span></span> <span data-ttu-id="2353b-133">Все виртуальные машины в группе доступности должны создаваться в той же группе ресурсов, что и группа доступности.</span><span class="sxs-lookup"><span data-stu-id="2353b-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="2353b-134">**Расположение** — выберите расположение из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="2353b-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="2353b-135">**Управляемая** — выберите *Да*, чтобы создать управляемую группу доступности для виртуальных машин, использующих Управляемые диски для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="2353b-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="2353b-136">Выберите **Нет**, если виртуальные машины в группе будут использовать неуправляемые диски, расположенные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2353b-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="2353b-137">После ввода необходимых сведений нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2353b-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="2353b-138">Одновременное создание виртуальной машины и группы доступности с помощью портала</span><span class="sxs-lookup"><span data-stu-id="2353b-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="2353b-139">При создании новой виртуальной машины с помощью портала можно также создать новую группу доступности для виртуальной машины в тот момент, когда создается первая виртуальная машина в группе.</span><span class="sxs-lookup"><span data-stu-id="2353b-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="2353b-140">Если вы решили использовать для виртуальной машины Управляемые диски, то будет создана управляемая группа доступности.</span><span class="sxs-lookup"><span data-stu-id="2353b-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Снимок экрана, показывающий процесс создания группы доступности одновременно с созданием виртуальной машины.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="2353b-142">Добавление новой виртуальной машины в существующую группу доступности на портале</span><span class="sxs-lookup"><span data-stu-id="2353b-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="2353b-143">При создании каждой дополнительной виртуальной машины, которая должна входить в группу, убедитесь, что она создается в той же **группе ресурсов** , а затем выберите существующую группу доступности из шага 3.</span><span class="sxs-lookup"><span data-stu-id="2353b-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![Снимок экрана, показывающий, как выбирать существующую группу доступности для виртуальной машины.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="2353b-145">Создание группы доступности с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2353b-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="2353b-146">В этом примере создается группа доступности **myAvailabilitySet** в группе ресурсов **myResourceGroup**, находящейся в расположении **Западная часть США**.</span><span class="sxs-lookup"><span data-stu-id="2353b-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="2353b-147">Это необходимо сделать до того, как в группе будет создана первая виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="2353b-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="2353b-148">Прежде чем начать, убедитесь, что у вас установлена последняя версия модуля PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="2353b-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="2353b-149">Выполните следующую команду, чтобы установить ее.</span><span class="sxs-lookup"><span data-stu-id="2353b-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="2353b-150">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2353b-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="2353b-151">Если для виртуальных машин вы используете управляемые диски, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2353b-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="2353b-152">Если вы используете для виртуальных машин собственные учетные записи хранения, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2353b-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="2353b-153">Дополнительные сведения см. в разделе [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="2353b-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2353b-154">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="2353b-154">Troubleshooting</span></span>
* <span data-ttu-id="2353b-155">Если при создании виртуальной машины необходимая вам группа доступности отсутствует в раскрывающемся списке на портале, возможно, она была создана в другой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2353b-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="2353b-156">Если вы не знаете, к какой группе ресурсов относится группа доступности, перейдите в главное меню и щелкните "Обзор" > "Группы доступности", чтобы просмотреть список групп доступности и соответствующие им группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2353b-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2353b-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2353b-157">Next steps</span></span>
<span data-ttu-id="2353b-158">Увеличьте емкость хранилища для виртуальной машины, добавив дополнительный [диск данных](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2353b-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

