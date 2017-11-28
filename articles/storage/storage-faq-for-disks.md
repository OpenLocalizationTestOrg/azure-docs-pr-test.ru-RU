---
title: "Часто задаваемые вопросы о дисках виртуальных машин Azure IaaS | Документация Майкрософт"
description: "Часто задаваемые вопросы о дисках виртуальных машин Azure IaaS и дисках класса \"Премиум\" (управляемых и неуправляемых)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="093c9-103">Часто задаваемые вопросы о дисках виртуальных машин Azure IaaS, а также об управляемых и неуправляемых дисках уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="093c9-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="093c9-104">В этой статье представлены ответы на некоторые часто задаваемые вопросы о службе "Управляемые диски" Azure и хранилище уровня "Премиум" Azure.</span><span class="sxs-lookup"><span data-stu-id="093c9-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="093c9-105">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="093c9-105">Managed Disks</span></span>

<span data-ttu-id="093c9-106">**Что такое управляемые диски Azure?**</span><span class="sxs-lookup"><span data-stu-id="093c9-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="093c9-107">Управляемые диски — это функция автоматического управления учетными записями хранения, которая упрощает управление дисками виртуальных машин Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="093c9-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="093c9-108">Дополнительные сведения см. в разделе hello [Общие сведения о дисках управляемых](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="093c9-108">For more information, see hello [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="093c9-109">**Сколько будет стоить создание управляемого диска уровня "Стандартный" из существующего VHD объемом 80 ГБ?**</span><span class="sxs-lookup"><span data-stu-id="093c9-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="093c9-110">Стандартного управляемого диска, созданные на основе на виртуальный жесткий ДИСК 80 ГБ считается hello Далее свободного стандартный размер, — S10 диск.</span><span class="sxs-lookup"><span data-stu-id="093c9-110">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="093c9-111">Будет взиматься плата соответствующим toohello — S10 диска цены.</span><span class="sxs-lookup"><span data-stu-id="093c9-111">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="093c9-112">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="093c9-112">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="093c9-113">**Взимается ли плата за транзакции для управляемых дисков класса "Стандартный"?**</span><span class="sxs-lookup"><span data-stu-id="093c9-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="093c9-114">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-114">Yes.</span></span> <span data-ttu-id="093c9-115">Плата взимается за каждую транзакцию.</span><span class="sxs-lookup"><span data-stu-id="093c9-115">You're charged for each transaction.</span></span> <span data-ttu-id="093c9-116">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="093c9-116">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="093c9-117">**Для стандартного управляемого диска будет ли взиматься плата для hello фактический размер данных hello на диске hello или подготовить hello емкости диска hello?**</span><span class="sxs-lookup"><span data-stu-id="093c9-117">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="093c9-118">Выставляются в зависимости от hello подготовки емкости диска hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-118">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="093c9-119">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="093c9-119">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="093c9-120">**Насколько отличается цена управляемых дисков уровня "Премиум" от цены неуправляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="093c9-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="093c9-121">Hello цены premium управляемых дисков hello то же, что диски неуправляемые premium.</span><span class="sxs-lookup"><span data-stu-id="093c9-121">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="093c9-122">**Можно изменить hello тип учетной записи хранения (Standard или Premium) my управляемых дисков**</span><span class="sxs-lookup"><span data-stu-id="093c9-122">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="093c9-123">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-123">Yes.</span></span> <span data-ttu-id="093c9-124">Тип учетной записи хранения hello управляемого диски можно изменить с помощью hello портал Azure, PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-124">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="093c9-125">**Есть ли способ, что я можно копировать или экспортировать управляемого диска tooa личная учетная запись хранения?**</span><span class="sxs-lookup"><span data-stu-id="093c9-125">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="093c9-126">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-126">Yes.</span></span> <span data-ttu-id="093c9-127">Можно экспортировать управляемый дисков с помощью hello портал Azure, PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-127">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="093c9-128">**Можно использовать файл виртуального жесткого диска в toocreate учетной записи хранилища Azure управляемого диска с помощью другой подписки**</span><span class="sxs-lookup"><span data-stu-id="093c9-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="093c9-129">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-129">No.</span></span>

<span data-ttu-id="093c9-130">**Можно использовать в toocreate учетной записи хранилища Azure управляемого диска VHD-файл в другом регионе?**</span><span class="sxs-lookup"><span data-stu-id="093c9-130">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="093c9-131">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-131">No.</span></span>

<span data-ttu-id="093c9-132">**Существуют ли какие-либо ограничения масштабирования для клиентов, использующих управляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="093c9-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="093c9-133">Управляемый диски устраняет hello ограничения, связанные с учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="093c9-133">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="093c9-134">Тем не менее hello число управляемых дисков для каждой подписки: ограниченный too2, 000 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="093c9-134">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="093c9-135">Это число может вызывать tooincrease поддержки.</span><span class="sxs-lookup"><span data-stu-id="093c9-135">You can call support tooincrease this number.</span></span>

<span data-ttu-id="093c9-136">**Могу ли я создать добавочный моментальный снимок управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="093c9-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="093c9-137">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-137">No.</span></span> <span data-ttu-id="093c9-138">текущий моментальный снимок возможность Hello обеспечивает поддержку полную копию управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="093c9-138">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="093c9-139">Тем не менее, мы планируем toosupport добавочных моментальных снимков в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-139">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="093c9-140">**Можно ли использовать для виртуальных машин в группе доступности сочетание управляемых и неуправляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="093c9-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="093c9-141">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-141">No.</span></span> <span data-ttu-id="093c9-142">Hello виртуальные машины в группу доступности необходимо использовать диски все управляемые или неуправляемые на всех дисках.</span><span class="sxs-lookup"><span data-stu-id="093c9-142">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="093c9-143">При создании группы доступности, можно выбрать, какие типы дисков требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="093c9-143">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="093c9-144">**Параметр по умолчанию hello управляемых дисков находится в hello портал Azure?**</span><span class="sxs-lookup"><span data-stu-id="093c9-144">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="093c9-145">В настоящее время не но она становится по умолчанию hello в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-145">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="093c9-146">**Могу ли я создать пустой управляемый диск?**</span><span class="sxs-lookup"><span data-stu-id="093c9-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="093c9-147">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-147">Yes.</span></span> <span data-ttu-id="093c9-148">Пустой диск можно создать.</span><span class="sxs-lookup"><span data-stu-id="093c9-148">You can create an empty disk.</span></span> <span data-ttu-id="093c9-149">Управляемого диска могут создаваться независимо от виртуальной Машины, например, не присоединяя его tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="093c9-149">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="093c9-150">**Что такое hello поддерживается число доменов сбоя для группы доступности управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="093c9-150">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="093c9-151">В зависимости от региона hello, где находится группа доступности hello управляемого диска число доменов сбоя hello поддерживается — 2 или 3.</span><span class="sxs-lookup"><span data-stu-id="093c9-151">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="093c9-152">**Как обеспечивается hello Стандартная учетная запись хранения для настройки диагностики?**</span><span class="sxs-lookup"><span data-stu-id="093c9-152">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="093c9-153">Для диагностики виртуальной машины следует настроить частную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="093c9-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="093c9-154">В будущем hello, мы планируем диагностики tooswitch tooManaged дисков.</span><span class="sxs-lookup"><span data-stu-id="093c9-154">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="093c9-155">**Какого вида управление доступом на основе ролей поддерживается для службы "Управляемые диски"?**</span><span class="sxs-lookup"><span data-stu-id="093c9-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="093c9-156">Для управляемых дисков поддерживаются три основные роли по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="093c9-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="093c9-157">"Владелец" — может управлять всем, включая доступ.</span><span class="sxs-lookup"><span data-stu-id="093c9-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="093c9-158">"Участник" — может управлять всем, кроме доступа.</span><span class="sxs-lookup"><span data-stu-id="093c9-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="093c9-159">"Читатель" — может все просматривать, но не может вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="093c9-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="093c9-160">**Есть ли способ, что я можно копировать или экспортировать управляемого диска tooa личная учетная запись хранения?**</span><span class="sxs-lookup"><span data-stu-id="093c9-160">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="093c9-161">Подпись общего доступа только для чтения URI для управляемых hello диск и использовать его можно получить toocopy hello содержимое tooa закрытого хранения учетных данных локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="093c9-161">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="093c9-162">**Могу ли я создать копию управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="093c9-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="093c9-163">Клиентов можно сделать снимок их управляемых дисков и затем использовать toocreate моментального снимка hello другого управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="093c9-163">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="093c9-164">**Поддерживаются ли еще неуправляемые диски?**</span><span class="sxs-lookup"><span data-stu-id="093c9-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="093c9-165">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-165">Yes.</span></span> <span data-ttu-id="093c9-166">Сейчас мы поддерживаем и управляемые диски, и неуправляемые.</span><span class="sxs-lookup"><span data-stu-id="093c9-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="093c9-167">Рекомендуется использовать управляемый диски для новых рабочих нагрузок и миграции текущего дисков toomanaged рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="093c9-167">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="093c9-168">**Если создать диск размером 128 ГБ, а затем увеличьте hello размер too130 ГБ, будет ли взиматься плата за hello Далее места на диске (512 ГБ)?**</span><span class="sxs-lookup"><span data-stu-id="093c9-168">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="093c9-169">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-169">Yes.</span></span>

<span data-ttu-id="093c9-170">**Можно ли создать управляемые диски локально избыточного хранилища, геоизбыточного хранилища и хранилища, избыточного в пределах зоны?**</span><span class="sxs-lookup"><span data-stu-id="093c9-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="093c9-171">Служба "Управляемые диски" Azure сейчас поддерживает только управляемые диски локально избыточного хранилища.</span><span class="sxs-lookup"><span data-stu-id="093c9-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="093c9-172">**Можно ли сжимать управляемые диски или уменьшать их размер?**</span><span class="sxs-lookup"><span data-stu-id="093c9-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="093c9-173">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-173">No.</span></span> <span data-ttu-id="093c9-174">Сейчас такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="093c9-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="093c9-175">**Можно ли изменить свойство имени компьютера hello при специальных (не создан с помощью средства подготовки системы hello или обобщить) операционной системы диска используется tooprovision виртуальной Машины?**</span><span class="sxs-lookup"><span data-stu-id="093c9-175">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="093c9-176">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-176">No.</span></span> <span data-ttu-id="093c9-177">Не удается обновить свойство имени компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-177">You can't update hello computer name property.</span></span> <span data-ttu-id="093c9-178">Hello новой виртуальной Машины наследует его от родительского hello виртуальную Машину, которая была диск операционной системы используется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-178">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="093c9-179">**Где найти toocreate шаблоны Azure Resource Manager образец виртуальные машины с дисками управляемого**</span><span class="sxs-lookup"><span data-stu-id="093c9-179">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="093c9-180">Список шаблонов с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="093c9-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="093c9-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="093c9-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="093c9-182">Управляемые диски и шифрование службы хранилища</span><span class="sxs-lookup"><span data-stu-id="093c9-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="093c9-183">**Включено ли шифрование службы хранилища Azure по умолчанию при создании управляемого диска?**</span><span class="sxs-lookup"><span data-stu-id="093c9-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="093c9-184">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-184">Yes.</span></span>

<span data-ttu-id="093c9-185">**Управляющий hello ключи шифрования?**</span><span class="sxs-lookup"><span data-stu-id="093c9-185">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="093c9-186">Корпорация Майкрософт управляет hello ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="093c9-186">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="093c9-187">**Можно ли отключить шифрование службы хранилища для моих управляемых дисков?**</span><span class="sxs-lookup"><span data-stu-id="093c9-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="093c9-188">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-188">No.</span></span>

<span data-ttu-id="093c9-189">**Шифрование службы хранилища доступно только в определенных регионах?**</span><span class="sxs-lookup"><span data-stu-id="093c9-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="093c9-190">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-190">No.</span></span> <span data-ttu-id="093c9-191">Он доступен во всех регионах hello, где доступен управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="093c9-191">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="093c9-192">Служба "Управляемые диски" доступна во всех общедоступных регионах, а также в Германии.</span><span class="sxs-lookup"><span data-stu-id="093c9-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="093c9-193">**Как узнать, шифруется ли мой управляемый диск?**</span><span class="sxs-lookup"><span data-stu-id="093c9-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="093c9-194">Чтобы узнать время hello создания управляемого диска из hello портал Azure, hello Azure CLI и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="093c9-194">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="093c9-195">Если время hello после 9 июня 2017 г., на диске шифруется.</span><span class="sxs-lookup"><span data-stu-id="093c9-195">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="093c9-196">**Как зашифровать мои диски, созданные до 10 июня 2017 года?**</span><span class="sxs-lookup"><span data-stu-id="093c9-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="093c9-197">Начиная с 10 июня 2017 г. управляемых tooexisting диски записываются новые данные автоматически шифруются.</span><span class="sxs-lookup"><span data-stu-id="093c9-197">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="093c9-198">Кроме того, мы планируем tooencrypt существующих данных и шифрования hello произойдет асинхронно в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-198">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="093c9-199">Если вам нужно зашифровать существующие данные уже сейчас, создайте копию своего диска.</span><span class="sxs-lookup"><span data-stu-id="093c9-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="093c9-200">Новые диски будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="093c9-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="093c9-201">Копирование дисков, управляемых с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="093c9-201">Copy managed disks by using hello Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="093c9-202">Копирование управляемых дисков с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="093c9-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="093c9-203">**Шифруются ли управляемые моментальные снимки и образы?**</span><span class="sxs-lookup"><span data-stu-id="093c9-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="093c9-204">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-204">Yes.</span></span> <span data-ttu-id="093c9-205">Все управляемые моментальные снимки и образы, созданные после 9 июня 2017 года, автоматически шифруются.</span><span class="sxs-lookup"><span data-stu-id="093c9-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="093c9-206">**Можно преобразовать виртуальных машин с неуправляемой диски, расположенные на учетные записи хранения, которые были ранее зашифрованные toomanaged дисков или**</span><span class="sxs-lookup"><span data-stu-id="093c9-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="093c9-207">Да</span><span class="sxs-lookup"><span data-stu-id="093c9-207">Yes</span></span>

<span data-ttu-id="093c9-208">**Будет ли также зашифрован экспортированный VHD из управляемого диска или моментального снимка?**</span><span class="sxs-lookup"><span data-stu-id="093c9-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="093c9-209">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-209">No.</span></span> <span data-ttu-id="093c9-210">Но если экспортировать VHD tooan шифрование учетной записи хранилища из управляемого зашифрованного диска или моментальный снимок, а затем он зашифрован.</span><span class="sxs-lookup"><span data-stu-id="093c9-210">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="093c9-211">Управляемые и неуправляемые диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="093c9-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="093c9-212">**Если для виртуальной машины используется размер, который поддерживает хранилище уровня "Премиум" (например, DSv2), можно ли подключить к ней одновременно диски данных уровня "Стандартный" и "Премиум"?**</span><span class="sxs-lookup"><span data-stu-id="093c9-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="093c9-213">Да.</span><span class="sxs-lookup"><span data-stu-id="093c9-213">Yes.</span></span>

<span data-ttu-id="093c9-214">**Можно ли подключить premium и стандартного дисков tooa размер набора данных, не поддерживают хранилище класса Premium, серии D "," Dv2 "," G "или" F?**</span><span class="sxs-lookup"><span data-stu-id="093c9-214">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="093c9-215">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-215">No.</span></span> <span data-ttu-id="093c9-216">Можно присоединить только стандартные данные диски tooVMs, которые не используют размер ряда, которое поддерживает хранилище Premium.</span><span class="sxs-lookup"><span data-stu-id="093c9-216">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="093c9-217">**Сколько будет стоить создание диска данных уровня "Премиум" из существующего VHD, который имел размер 80 ГБ?**</span><span class="sxs-lookup"><span data-stu-id="093c9-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="093c9-218">Диск данных premium, созданные на основе на виртуальный жесткий ДИСК 80 ГБ рассматривается как hello Далее доступной расширенной диск размером, равным P10 диска.</span><span class="sxs-lookup"><span data-stu-id="093c9-218">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="093c9-219">Будет взиматься плата соответствующим toohello P10 диска цены.</span><span class="sxs-lookup"><span data-stu-id="093c9-219">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="093c9-220">**Существуют toouse затраты на транзакции хранилища Premium?**</span><span class="sxs-lookup"><span data-stu-id="093c9-220">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="093c9-221">Для каждого размера диска установлена фиксированная стоимость и определенные ограничения пропускной способности и операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="093c9-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="093c9-222">Hello других расходов, являются исходящей пропускной способности и емкость моментального снимка, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="093c9-222">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="093c9-223">Дополнительные сведения см. в разделе hello [странице цен](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="093c9-223">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="093c9-224">**Что такое hello ограничения для операций ввода-ВЫВОДА и пропускную способность, можно получить из кэша диска hello**</span><span class="sxs-lookup"><span data-stu-id="093c9-224">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="093c9-225">Здравствуйте, объединенный ограничений для кэша и локальный SSD серии DS 4 000 операций ввода-ВЫВОДА на ядро и 33 МБ в секунду на ядро.</span><span class="sxs-lookup"><span data-stu-id="093c9-225">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="093c9-226">Hello серии GS предлагает 5 000 операций ввода-ВЫВОДА на ядро и 50 МБ в секунду на ядро.</span><span class="sxs-lookup"><span data-stu-id="093c9-226">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="093c9-227">**— Hello локальный SSD поддерживается для управляемых дисков виртуальной Машины?**</span><span class="sxs-lookup"><span data-stu-id="093c9-227">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="093c9-228">Hello локальный SSD — временное хранилище, которое входит в состав управляемых дисков виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="093c9-228">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="093c9-229">Никакая дополнительная плата за него не взимается.</span><span class="sxs-lookup"><span data-stu-id="093c9-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="093c9-230">Рекомендуется не использовать этот локальный SSD toostore данные приложения, так как он не сохранен в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="093c9-230">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="093c9-231">**Существует все последствия для hello используйте из TRIM на диски premium?**</span><span class="sxs-lookup"><span data-stu-id="093c9-231">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="093c9-232">Нет не используется toohello недостаток TRIM на диски Azure в либо premium или стандартные диски.</span><span class="sxs-lookup"><span data-stu-id="093c9-232">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="093c9-233">Размеры новых управляемых и неуправляемых дисков</span><span class="sxs-lookup"><span data-stu-id="093c9-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="093c9-234">**Что такое hello поддерживается для операционной системы и дисков данных наибольший размер диска**</span><span class="sxs-lookup"><span data-stu-id="093c9-234">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="093c9-235">Тип раздела Hello, который поддерживает Azure для диска операционной системы — hello основная загрузочная запись (MBR).</span><span class="sxs-lookup"><span data-stu-id="093c9-235">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="093c9-236">формат MBR Hello поддерживает размер диска вверх too2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="093c9-236">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="093c9-237">Максимальный объем Hello, который поддерживает Azure для диска операционной системы составляет 2 ТБ.</span><span class="sxs-lookup"><span data-stu-id="093c9-237">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="093c9-238">Azure поддерживает до too4 ТБ для дисков данных.</span><span class="sxs-lookup"><span data-stu-id="093c9-238">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="093c9-239">**Что такое hello наибольшее страницы размер большого двоичного объекта, поддерживаемый?**</span><span class="sxs-lookup"><span data-stu-id="093c9-239">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="093c9-240">Hello наибольшее страницы размер большого двоичного объекта, поддерживающий Azure — 8 ТБ (8191 ГБ).</span><span class="sxs-lookup"><span data-stu-id="093c9-240">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="093c9-241">Мы не поддерживаем страничные большие двоичные объекты размером более 4 ТБ (4095 ГБ) присоединенного tooa виртуальной Машины, данные и дисков операционной системы.</span><span class="sxs-lookup"><span data-stu-id="093c9-241">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="093c9-242">**Требуется новая версия toouse toocreate средства Azure присоединения, изменение размера и отправка дисков размером более 1 ТБ?**</span><span class="sxs-lookup"><span data-stu-id="093c9-242">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="093c9-243">Не требуется tooupgrade вашей существующей toocreate инструменты Azure, присоединить или изменить размер дисков размером более 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="093c9-243">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="093c9-244">tooupload файл вашего виртуального жесткого диска из локальной непосредственно tooAzure как страничный BLOB-объект или неуправляемые диска, необходимо toouse hello последние наборы инструментов:</span><span class="sxs-lookup"><span data-stu-id="093c9-244">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="093c9-245">Инструменты Azure</span><span class="sxs-lookup"><span data-stu-id="093c9-245">Azure tools</span></span>      | <span data-ttu-id="093c9-246">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="093c9-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="093c9-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="093c9-247">Azure PowerShell</span></span> | <span data-ttu-id="093c9-248">Версия 4.1.0: выпуск за июнь 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="093c9-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="093c9-249">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="093c9-249">Azure CLI v1</span></span>     | <span data-ttu-id="093c9-250">Версия 0.10.13: выпуск за май 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="093c9-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="093c9-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="093c9-251">AzCopy</span></span>           | <span data-ttu-id="093c9-252">Версия 6.1.0: выпуск за июнь 2017 г. или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="093c9-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="093c9-253">Поддержка Hello Azure CLI v2 и обозреватель хранилищ Azure ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="093c9-253">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="093c9-254">**Поддерживаются ли размеры диска P4 и P6 для неуправляемых дисков или страничных BLOB-объектов?**</span><span class="sxs-lookup"><span data-stu-id="093c9-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="093c9-255">Нет.</span><span class="sxs-lookup"><span data-stu-id="093c9-255">No.</span></span> <span data-ttu-id="093c9-256">Размеры диска P4 (32 ГБ) и P6 (64 ГБ) поддерживаются только для управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="093c9-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="093c9-257">Поддержка этих размеров для неуправляемых дисков и страничных BLOB-объектов ожидается в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="093c9-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="093c9-258">**Если моей существующей premium управляемых на диске меньше, чем 64 ГБ был создан до включения небольшой диск hello (около 15 июня 2017 г.), как он оплачивается?**</span><span class="sxs-lookup"><span data-stu-id="093c9-258">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="093c9-259">Существующие диски premium небольшой меньше 64 ГБ по-прежнему toobe плата соответствующим toohello P10 ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="093c9-259">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="093c9-260">**Как переключаться hello диска уровня диски premium небольшой меньше 64 ГБ из P10 tooP4 или P6**</span><span class="sxs-lookup"><span data-stu-id="093c9-260">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="093c9-261">Можно сделать снимок небольшие диски и создайте hello коммутатора tooautomatically диска, цены tooP4 уровня или P6 в зависимости от размера подготовить hello.</span><span class="sxs-lookup"><span data-stu-id="093c9-261">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="093c9-262">Мне не удалось найти ответ на свой вопрос. Что делать?</span><span class="sxs-lookup"><span data-stu-id="093c9-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="093c9-263">Если вашего вопроса нет в списке, сообщите нам об этом, и мы поможем найти ответ.</span><span class="sxs-lookup"><span data-stu-id="093c9-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="093c9-264">В комментариях hello можно разместить вопрос в конце hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="093c9-264">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="093c9-265">tooengage с группой хранилища Azure hello и другими участниками сообщества о в этой статье используется hello MSDN [форум хранилища Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="093c9-265">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="093c9-266">функции toorequest отправить на запросы и идеи toohello [форуме обратной связи хранилища Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="093c9-266">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
