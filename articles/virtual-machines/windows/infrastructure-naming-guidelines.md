---
title: "Рекомендации по именованию для инфраструктуры Azure для Windows | Документация Майкрософт"
description: "Изучите основные рекомендации по проектированию и реализации, касающиеся именования в службах инфраструктуры Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a595d5c2f0316b5214af7b8939f1af8da187ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="b8a0d-103">Рекомендации по именованию для инфраструктуры Azure для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="b8a0d-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="b8a0d-104">Это статья посвящена тому, как выбрать соглашения об именовании различных ресурсов Azure, чтобы создать логичный и легко идентифицируемый набор ресурсов в своей среде.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="b8a0d-105">Рекомендации по реализации соглашений об именовании</span><span class="sxs-lookup"><span data-stu-id="b8a0d-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="b8a0d-106">Решения</span><span class="sxs-lookup"><span data-stu-id="b8a0d-106">Decisions:</span></span>

* <span data-ttu-id="b8a0d-107">Каковы соглашения об именовании для ресурсов Azure?</span><span class="sxs-lookup"><span data-stu-id="b8a0d-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="b8a0d-108">Задачи</span><span class="sxs-lookup"><span data-stu-id="b8a0d-108">Tasks:</span></span>

* <span data-ttu-id="b8a0d-109">Определите аффиксы, которые будут использоваться для ресурсов, чтобы обеспечить их согласованность.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="b8a0d-110">Определите имена учетных записей хранения, учитывая, что они должны быть глобально уникальными.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="b8a0d-111">Задокументируйте используемое соглашение об именовании и распространите его всем участникам, чтобы обеспечить согласованность развертываний.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="b8a0d-112">Соглашения об именовании.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-112">Naming conventions</span></span>
<span data-ttu-id="b8a0d-113">Прежде чем создавать что-либо в Azure, следует задать надлежащее соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="b8a0d-114">Такое соглашение гарантирует предсказуемость имен всех ресурсов, позволяющую снизить административную нагрузку, связанную с управлением этими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="b8a0d-115">Вы можете следовать некоторому набору соглашений об именовании, определенному для всей вашей организации, конкретной подписки Azure или учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="b8a0d-116">Хотя сотрудники организации могут с легкостью устанавливать неявные правила при работе с ресурсами Azure, такая модель плохо масштабируется, если команде нужно работать над проектом в Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="b8a0d-117">Установите соглашения об именовании заранее.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="b8a0d-118">Ниже приведено несколько рекомендаций по соглашениям об именовании, которые противоречат данному набору правил.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="b8a0d-119">Аффиксы</span><span class="sxs-lookup"><span data-stu-id="b8a0d-119">Affixes</span></span>
<span data-ttu-id="b8a0d-120">При определении соглашения об именовании следует решить, где будет находиться аффикс:</span><span class="sxs-lookup"><span data-stu-id="b8a0d-120">As you look to define a naming convention, one decision comes whether the affix is at:</span></span>

* <span data-ttu-id="b8a0d-121">в начале имени (префикс);</span><span class="sxs-lookup"><span data-stu-id="b8a0d-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="b8a0d-122">в конце имени (суффикс).</span><span class="sxs-lookup"><span data-stu-id="b8a0d-122">The end of the name (suffix)</span></span>

<span data-ttu-id="b8a0d-123">Например, группа ресурсов, использующая `rg`, может иметь такие два аффикса:</span><span class="sxs-lookup"><span data-stu-id="b8a0d-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="b8a0d-124">Rg-WebApp (префикс);</span><span class="sxs-lookup"><span data-stu-id="b8a0d-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="b8a0d-125">WebApp-Rg (суффикс).</span><span class="sxs-lookup"><span data-stu-id="b8a0d-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="b8a0d-126">Аффиксы относятся к различным аспектам, описывающим конкретные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="b8a0d-127">В следующей таблице приведены примеры типичных случаев.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="b8a0d-128">Аспект</span><span class="sxs-lookup"><span data-stu-id="b8a0d-128">Aspect</span></span> | <span data-ttu-id="b8a0d-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="b8a0d-129">Examples</span></span> | <span data-ttu-id="b8a0d-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="b8a0d-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b8a0d-131">Среда</span><span class="sxs-lookup"><span data-stu-id="b8a0d-131">Environment</span></span> |<span data-ttu-id="b8a0d-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="b8a0d-132">dev, stg, prod</span></span> |<span data-ttu-id="b8a0d-133">Зависит от назначения и имени каждой среды.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="b8a0d-134">Расположение</span><span class="sxs-lookup"><span data-stu-id="b8a0d-134">Location</span></span> |<span data-ttu-id="b8a0d-135">usw (западная часть США), use (восточная часть США 2)</span><span class="sxs-lookup"><span data-stu-id="b8a0d-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="b8a0d-136">Зависит от региона, в котором располагается центр обработки данных или организация.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="b8a0d-137">Служба, продукт или компонент Azure</span><span class="sxs-lookup"><span data-stu-id="b8a0d-137">Azure component, service, or product</span></span> |<span data-ttu-id="b8a0d-138">Rg — группа ресурсов, VNet — виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="b8a0d-139">Зависит от продукта, для которого ресурс обеспечивает поддержку.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="b8a0d-140">Роль</span><span class="sxs-lookup"><span data-stu-id="b8a0d-140">Role</span></span> |<span data-ttu-id="b8a0d-141">sql, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="b8a0d-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="b8a0d-142">Зависит от роли виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="b8a0d-143">Экземпляр</span><span class="sxs-lookup"><span data-stu-id="b8a0d-143">Instance</span></span> |<span data-ttu-id="b8a0d-144">01, 02, 03 и т. д.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="b8a0d-145">Для ресурсов, которые имеют более одного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-145">For resources that have more than one instance.</span></span> <span data-ttu-id="b8a0d-146">Например, веб-серверы с балансировкой нагрузки, размещенные в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="b8a0d-147">При установке соглашений об именовании убедитесь, что они явно указывают, какие аффиксы используются для каждого типа ресурсов, и их расположение (префикс или суффикс).</span><span class="sxs-lookup"><span data-stu-id="b8a0d-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="b8a0d-148">Даты</span><span class="sxs-lookup"><span data-stu-id="b8a0d-148">Dates</span></span>
<span data-ttu-id="b8a0d-149">Часто крайне важно определять дату создания по имени ресурса.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="b8a0d-150">Мы рекомендуем использовать формат даты ГГГГММДД.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="b8a0d-151">Этот формат обеспечивает не только запись полной даты, но и то, что два ресурса, имена которых отличаются только датой, сортируются в алфавитном и хронологическом порядке одновременно.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="b8a0d-152">Именование ресурсов</span><span class="sxs-lookup"><span data-stu-id="b8a0d-152">Naming resources</span></span>
<span data-ttu-id="b8a0d-153">В соглашении об именовании определите каждый тип ресурсов и правила назначения имен каждому создаваемому ресурсу.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="b8a0d-154">Эти правила применяются ко всем типам ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="b8a0d-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="b8a0d-155">Подписки</span><span class="sxs-lookup"><span data-stu-id="b8a0d-155">Subscriptions</span></span>
* <span data-ttu-id="b8a0d-156">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="b8a0d-156">Accounts</span></span>
* <span data-ttu-id="b8a0d-157">учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="b8a0d-157">Storage accounts</span></span>
* <span data-ttu-id="b8a0d-158">виртуальные сети;</span><span class="sxs-lookup"><span data-stu-id="b8a0d-158">Virtual networks</span></span>
* <span data-ttu-id="b8a0d-159">Подсети</span><span class="sxs-lookup"><span data-stu-id="b8a0d-159">Subnets</span></span>
* <span data-ttu-id="b8a0d-160">Группы доступности</span><span class="sxs-lookup"><span data-stu-id="b8a0d-160">Availability sets</span></span>
* <span data-ttu-id="b8a0d-161">Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="b8a0d-161">Resource groups</span></span>
* <span data-ttu-id="b8a0d-162">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="b8a0d-162">Virtual machines</span></span>
* <span data-ttu-id="b8a0d-163">Endpoints</span><span class="sxs-lookup"><span data-stu-id="b8a0d-163">Endpoints</span></span>
* <span data-ttu-id="b8a0d-164">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="b8a0d-164">Network security groups</span></span>
* <span data-ttu-id="b8a0d-165">Роли</span><span class="sxs-lookup"><span data-stu-id="b8a0d-165">Roles</span></span>

<span data-ttu-id="b8a0d-166">Используйте содержательные имена, которые позволяют безошибочно определить ресурсы, к которым они относятся.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="b8a0d-167">Имена компьютеров </span><span class="sxs-lookup"><span data-stu-id="b8a0d-167">Computer names</span></span>
<span data-ttu-id="b8a0d-168">При создании виртуальной машины в Microsoft Azure требуется указать ее имя, содержащее не более 15 знаков, которое используется в качестве имени ресурса.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span></span> <span data-ttu-id="b8a0d-169">Это же имя Azure использует в качестве имени компьютера в операционной системе виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="b8a0d-170">Однако эти имена могут и не совпадать.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="b8a0d-171">Если виртуальная машина создается с помощью VHD-файла образа, в котором уже установлена операционная система, то имя виртуальной машины в Azure может отличаться от имени компьютера, заданного в ее операционной системе.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="b8a0d-172">В таком случае управление виртуальной машиной может усложниться, поэтому мы рекомендуем не допускать этого.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="b8a0d-173">Используйте имя ресурса виртуальной машины Azure, совпадающее с именем компьютера, заданным в операционной системе этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="b8a0d-174">Мы рекомендуем использовать имя виртуальной машины Azure, совпадающее с именем компьютера базовой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="b8a0d-175">Имена учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="b8a0d-175">Storage account names</span></span>
<span data-ttu-id="b8a0d-176">Этот раздел не относится к [Управляемым дискам Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), так как вы не создаете отдельную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="b8a0d-177">Для неуправляемых дисков имена учетных записей хранения создаются по особым правилам.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="b8a0d-178">Вы можете использовать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="b8a0d-179">Дополнительные сведения см. в разделе [Создание учетной записи хранения](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b8a0d-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="b8a0d-180">Кроме того, имя учетной записи хранения в сочетании с core.windows.net должно являться глобально допустимым уникальным именем DNS.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="b8a0d-181">Например, если учетная запись хранения называется mystorageaccount, уникальными должны быть следующие имена DNS:</span><span class="sxs-lookup"><span data-stu-id="b8a0d-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="b8a0d-182">mystorageaccount.blob.core.windows.net;</span><span class="sxs-lookup"><span data-stu-id="b8a0d-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="b8a0d-183">mystorageaccount.table.core.windows.net;</span><span class="sxs-lookup"><span data-stu-id="b8a0d-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="b8a0d-184">mystorageaccount.queue.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="b8a0d-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8a0d-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8a0d-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

