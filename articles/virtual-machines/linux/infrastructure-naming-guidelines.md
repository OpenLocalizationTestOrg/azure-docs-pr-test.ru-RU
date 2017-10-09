---
title: "правила - Linux именования инфраструктуры aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello ключа проектирования и реализации соглашения об именах в службах инфраструктуры Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="7ca51-103">Рекомендации по именованию для инфраструктуры Azure для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="7ca51-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="7ca51-104">Это статье рассматриваются основные сведения об установке tooapproach соглашения об именовании для всех на различные ресурсы Azure toobuild a логических и понятными ресурсов во всей среде.</span><span class="sxs-lookup"><span data-stu-id="7ca51-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="7ca51-105">Рекомендации по реализации соглашений об именовании</span><span class="sxs-lookup"><span data-stu-id="7ca51-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="7ca51-106">Решения</span><span class="sxs-lookup"><span data-stu-id="7ca51-106">Decisions:</span></span>

* <span data-ttu-id="7ca51-107">Каковы соглашения об именовании для ресурсов Azure?</span><span class="sxs-lookup"><span data-stu-id="7ca51-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="7ca51-108">Задачи</span><span class="sxs-lookup"><span data-stu-id="7ca51-108">Tasks:</span></span>

* <span data-ttu-id="7ca51-109">Определения toouse Аффиксы hello на ваш согласованности toomaintain ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ca51-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="7ca51-110">Определение учетной записи хранения, именах hello требование для них toobe глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="7ca51-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="7ca51-111">Документ hello toobe соглашение об именовании используется и распределяют согласованности tooensure участвующих сторон tooall развертываний.</span><span class="sxs-lookup"><span data-stu-id="7ca51-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="7ca51-112">Соглашения об именовании.</span><span class="sxs-lookup"><span data-stu-id="7ca51-112">Naming conventions</span></span>
<span data-ttu-id="7ca51-113">Прежде чем создавать что-либо в Azure, следует задать надлежащее соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="7ca51-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="7ca51-114">Соглашение об именовании обеспечивает все ресурсы hello прогнозируемого имя, которое помогает нижней административную нагрузку hello связанные с управлением эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7ca51-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="7ca51-115">Вы можете toofollow ряд соглашения об именовании, определенные для всей организации или для определенной подписки Azure или учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7ca51-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="7ca51-116">Несмотря на то, что удобно для частных лиц в организациях tooestablish неявные правила при работе с ресурсами Azure, необходимо будет tooscale toobe для команд, совместной работы в Azure.</span><span class="sxs-lookup"><span data-stu-id="7ca51-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="7ca51-117">Установите соглашения об именовании заранее.</span><span class="sxs-lookup"><span data-stu-id="7ca51-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="7ca51-118">Ниже приведено несколько рекомендаций по соглашениям об именовании, которые составляют данный набор правил.</span><span class="sxs-lookup"><span data-stu-id="7ca51-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="7ca51-119">Аффиксы</span><span class="sxs-lookup"><span data-stu-id="7ca51-119">Affixes</span></span>
<span data-ttu-id="7ca51-120">Если просмотреть toodefine соглашение об именовании решение, является ли Аффикс hello в:</span><span class="sxs-lookup"><span data-stu-id="7ca51-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="7ca51-121">Начало Hello hello имени (префикс)</span><span class="sxs-lookup"><span data-stu-id="7ca51-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="7ca51-122">Hello конец имени hello (суффикс)</span><span class="sxs-lookup"><span data-stu-id="7ca51-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="7ca51-123">Например, ниже приведены два возможных имен для группы ресурсов с помощью hello `rg` прикреплять:</span><span class="sxs-lookup"><span data-stu-id="7ca51-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="7ca51-124">Rg-WebApp (префикс);</span><span class="sxs-lookup"><span data-stu-id="7ca51-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="7ca51-125">WebApp-Rg (суффикс).</span><span class="sxs-lookup"><span data-stu-id="7ca51-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="7ca51-126">Аффиксы может ссылаться toodifferent аспекты, которые описывают hello конкретные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7ca51-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="7ca51-127">Hello следующей таблице показаны некоторые примеры, которые обычно используются.</span><span class="sxs-lookup"><span data-stu-id="7ca51-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="7ca51-128">Аспект</span><span class="sxs-lookup"><span data-stu-id="7ca51-128">Aspect</span></span> | <span data-ttu-id="7ca51-129">Примеры</span><span class="sxs-lookup"><span data-stu-id="7ca51-129">Examples</span></span> | <span data-ttu-id="7ca51-130">Примечания</span><span class="sxs-lookup"><span data-stu-id="7ca51-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ca51-131">Среда</span><span class="sxs-lookup"><span data-stu-id="7ca51-131">Environment</span></span> |<span data-ttu-id="7ca51-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="7ca51-132">dev, stg, prod</span></span> |<span data-ttu-id="7ca51-133">В зависимости от цели hello и имя каждой из сред.</span><span class="sxs-lookup"><span data-stu-id="7ca51-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="7ca51-134">Расположение</span><span class="sxs-lookup"><span data-stu-id="7ca51-134">Location</span></span> |<span data-ttu-id="7ca51-135">usw (западная часть США), use (восточная часть США 2)</span><span class="sxs-lookup"><span data-stu-id="7ca51-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="7ca51-136">В зависимости от региона hello hello центре обработки данных или область hello hello организации.</span><span class="sxs-lookup"><span data-stu-id="7ca51-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="7ca51-137">Служба, продукт или компонент Azure</span><span class="sxs-lookup"><span data-stu-id="7ca51-137">Azure component, service, or product</span></span> |<span data-ttu-id="7ca51-138">Rg — группа ресурсов, VNet — виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="7ca51-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="7ca51-139">В зависимости от того, для какой hello ресурсов обеспечивает поддержку продукта hello.</span><span class="sxs-lookup"><span data-stu-id="7ca51-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="7ca51-140">Роль</span><span class="sxs-lookup"><span data-stu-id="7ca51-140">Role</span></span> |<span data-ttu-id="7ca51-141">базы данных, приложения, веб</span><span class="sxs-lookup"><span data-stu-id="7ca51-141">db, app, web</span></span> |<span data-ttu-id="7ca51-142">В зависимости от роли hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7ca51-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="7ca51-143">Экземпляр</span><span class="sxs-lookup"><span data-stu-id="7ca51-143">Instance</span></span> |<span data-ttu-id="7ca51-144">01, 02, 03 и т. д.</span><span class="sxs-lookup"><span data-stu-id="7ca51-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="7ca51-145">Для ресурсов, которые имеют более одного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="7ca51-145">For resources that have more than one instance.</span></span> <span data-ttu-id="7ca51-146">Например, веб-серверы с балансировкой нагрузки, размещенные в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="7ca51-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="7ca51-147">При создании вашего соглашения об именовании, убедитесь, что они явно указано, что affixes toouse для каждого типа ресурса и расположение (префикс и суффикс).</span><span class="sxs-lookup"><span data-stu-id="7ca51-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="7ca51-148">Даты</span><span class="sxs-lookup"><span data-stu-id="7ca51-148">Dates</span></span>
<span data-ttu-id="7ca51-149">Часто бывает важным toodetermine hello Дата создания hello имени ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ca51-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="7ca51-150">Рекомендуется использовать формат даты ГГГГММДД hello.</span><span class="sxs-lookup"><span data-stu-id="7ca51-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="7ca51-151">Этот формат обеспечивает не только hello полный записано даты, а также что два ресурса, имена которых отличаются только на дату hello сортируются в алфавитном порядке и в хронологическом порядке.</span><span class="sxs-lookup"><span data-stu-id="7ca51-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="7ca51-152">Именование ресурсов</span><span class="sxs-lookup"><span data-stu-id="7ca51-152">Naming resources</span></span>
<span data-ttu-id="7ca51-153">Определение каждого типа ресурсов в соглашение об именовании hello, который должен иметь правила, определяющие, каким образом tooassign имена tooeach ресурсов, создается.</span><span class="sxs-lookup"><span data-stu-id="7ca51-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="7ca51-154">Эти правила применяются tooall типы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="7ca51-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="7ca51-155">Подписки</span><span class="sxs-lookup"><span data-stu-id="7ca51-155">Subscriptions</span></span>
* <span data-ttu-id="7ca51-156">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="7ca51-156">Accounts</span></span>
* <span data-ttu-id="7ca51-157">учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="7ca51-157">Storage accounts</span></span>
* <span data-ttu-id="7ca51-158">виртуальные сети;</span><span class="sxs-lookup"><span data-stu-id="7ca51-158">Virtual networks</span></span>
* <span data-ttu-id="7ca51-159">Подсети</span><span class="sxs-lookup"><span data-stu-id="7ca51-159">Subnets</span></span>
* <span data-ttu-id="7ca51-160">Группы доступности</span><span class="sxs-lookup"><span data-stu-id="7ca51-160">Availability sets</span></span>
* <span data-ttu-id="7ca51-161">Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7ca51-161">Resource groups</span></span>
* <span data-ttu-id="7ca51-162">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="7ca51-162">Virtual machines</span></span>
* <span data-ttu-id="7ca51-163">Endpoints</span><span class="sxs-lookup"><span data-stu-id="7ca51-163">Endpoints</span></span>
* <span data-ttu-id="7ca51-164">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7ca51-164">Network security groups</span></span>
* <span data-ttu-id="7ca51-165">Роли</span><span class="sxs-lookup"><span data-stu-id="7ca51-165">Roles</span></span>

<span data-ttu-id="7ca51-166">tooensure, hello имя содержит недостаточно ресурсов toowhich toodetermine сведения, которые он ссылается, следует использовать описательные имена.</span><span class="sxs-lookup"><span data-stu-id="7ca51-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="7ca51-167">Имена компьютеров </span><span class="sxs-lookup"><span data-stu-id="7ca51-167">Computer names</span></span>
<span data-ttu-id="7ca51-168">При создании виртуальной машины (VM) Azure требуется имя виртуальной Машины из копии too64 символов, используемый для hello имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="7ca51-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="7ca51-169">Azure использует hello одно имя для hello операционной системы, установленной в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7ca51-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="7ca51-170">Однако эти имена могут не всегда быть hello же.</span><span class="sxs-lookup"><span data-stu-id="7ca51-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="7ca51-171">Если виртуальная машина создается из файла образа VHD, который уже содержит операционную систему, hello имя виртуальной Машины в Azure может отличаться от hello имя компьютера операционной системы Виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7ca51-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="7ca51-172">Такой ситуации можно добавить степень сложности tooVM управления таким образом не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="7ca51-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="7ca51-173">Назначьте hello hello ресурсов виртуальной Машины Azure, точно такое же имя в качестве имени компьютера hello назначении toohello операционной системы этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7ca51-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="7ca51-174">Рекомендуется, это имя виртуальной Машины Azure hello hello аналогично hello базовый имя операционной системы компьютера.</span><span class="sxs-lookup"><span data-stu-id="7ca51-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="7ca51-175">Имена учетных записей хранения</span><span class="sxs-lookup"><span data-stu-id="7ca51-175">Storage account names</span></span>
<span data-ttu-id="7ca51-176">В этом разделе не применяется слишком[управляемых дисков Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), как не следует создавать отдельную учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="7ca51-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="7ca51-177">Для неуправляемых дисков имена учетных записей хранения создаются по особым правилам.</span><span class="sxs-lookup"><span data-stu-id="7ca51-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="7ca51-178">Вы можете использовать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="7ca51-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="7ca51-179">Дополнительные сведения см. в разделе [Создание учетной записи хранения](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7ca51-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="7ca51-180">Кроме того имя учетной записи хранения hello с core.windows.net, должно быть глобально допустимое уникальное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="7ca51-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="7ca51-181">Например если учетной записи хранилища hello вызывается mystorageaccount, hello следующие результирующие DNS-имена должно быть уникальным:</span><span class="sxs-lookup"><span data-stu-id="7ca51-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="7ca51-182">mystorageaccount.blob.core.windows.net;</span><span class="sxs-lookup"><span data-stu-id="7ca51-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="7ca51-183">mystorageaccount.table.core.windows.net;</span><span class="sxs-lookup"><span data-stu-id="7ca51-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="7ca51-184">mystorageaccount.queue.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="7ca51-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ca51-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ca51-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

