---
title: "Устранение неполадок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков в классической модели развертывания | Документация Майкрософт"
description: "Устранение неполадок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков в классической модели развертывания"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="bf0bf-103">Устранение неполадок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков в классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="bf0bf-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="bf0bf-104">При попытке удалить учетную запись хранения Azure, контейнер или виртуальный жесткий диск на [портале Azure](https://portal.azure.com/) или на [классическом портале Azure](https://manage.windowsazure.com/) могут возникать ошибки.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="bf0bf-105">Ошибки могут возникать при следующих обстоятельствах:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="bf0bf-106">При удалении виртуальной машины диск и виртуальный жесткий диск не удаляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="bf0bf-107">Это может быть причиной сбоя удаления учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="bf0bf-108">Диск не удаляется, чтобы вы могли использовать его для подключения другой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="bf0bf-109">Диск или большой двоичный объект, связанный с диском, по-прежнему находится в аренде.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="bf0bf-110">Остался образ виртуальной машины, который использует большой двоичный объект, контейнер или учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="bf0bf-111">Если в этой статье нет решения вашей проблемы с Azure, посетите форумы по Azure [на сайтах MSDN и Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="bf0bf-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="bf0bf-112">Проблему можно разместить на этих форумах или отправить по адресу @AzureSupport в Twitter.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="bf0bf-113">Кроме того, можно отправить запрос в службу поддержки Azure, выбрав **Получить поддержку** на сайте [службы поддержки Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="bf0bf-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="bf0bf-114">Симптомы</span><span class="sxs-lookup"><span data-stu-id="bf0bf-114">Symptoms</span></span>
<span data-ttu-id="bf0bf-115">В следующем разделе приводится список наиболее распространенных ошибок, которые могут возникать при попытке удаления учетных записей хранения Azure, контейнеров или виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="bf0bf-116">Сценарий 1. Невозможно удалить учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="bf0bf-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="bf0bf-117">Когда вы переходите в классическую учетную запись хранения на [портале Azure](https://portal.azure.com/) и выбираете **Удалить**, может появиться список объектов, которые препятствуют удалению учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Изображения ошибки, возникшей при удалении учетной записи хранения](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="bf0bf-119">При переходе в учетную запись хранения на [классическом портале Azure](https://manage.windowsazure.com/) и выборе элемента **Удалить** может появиться одна из следующих ошибок:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="bf0bf-120">*Учетная запись хранения "имя_учетной_записи_хранения" содержит образы виртуальных машин. Убедитесь, что эти образы будут удалены перед удалением этой учетной записи хранения.*</span><span class="sxs-lookup"><span data-stu-id="bf0bf-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="bf0bf-121">*Не удалось удалить учетную запись хранения <учетная_запись_хранения_ВМ>. Не удалось удалить учетную запись хранения <учетная_запись_хранения_ВМ>: "В учетной записи хранения <учетная_запись_хранения_ВМ> есть несколько активных образов или дисков. Убедитесь, что эти образы или диски удалены, перед тем как удалять эту учетную запись хранения".*</span><span class="sxs-lookup"><span data-stu-id="bf0bf-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="bf0bf-122">*В учетной записи хранения <учетная_запись_хранения_ВМ> есть несколько активных образов или дисков, например xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Убедитесь, что эти образы или диски удалены, перед тем как удалять эту учетную запись хранения.*</span><span class="sxs-lookup"><span data-stu-id="bf0bf-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="bf0bf-123">*Учетная запись хранения <учетная_запись_хранения_ВМ> содержит 1 контейнер с активными артефактами образа или диска. Убедитесь, что эти артефакты удалены из репозитория образов, перед удалением этой учетной записи хранения*.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="bf0bf-124">*Не удалось выполнить отправку. Учетная запись хранения <учетная_запись_хранения_ВМ> содержит 1 контейнер с активными артефактами образа или диска. Убедитесь, что эти артефакты удалены из репозитория образов, перед удалением этой учетной записи хранения. Когда вы пытаетесь удалить учетную запись хранения, у которой есть связанные активные диски, появится сообщение о том, что существуют активные диски, которые нужно удалить*.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="bf0bf-125">Сценарий 2. Невозможно удалить контейнер</span><span class="sxs-lookup"><span data-stu-id="bf0bf-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="bf0bf-126">При попытке удалить контейнер хранилища может появиться следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="bf0bf-127">*Не удалось удалить контейнер хранилища <container name>. Ошибка: "В настоящий момент контейнер находится в аренде, и в запросе не указан идентификатор аренды*".</span><span class="sxs-lookup"><span data-stu-id="bf0bf-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="bf0bf-128">Или</span><span class="sxs-lookup"><span data-stu-id="bf0bf-128">Or</span></span>

<span data-ttu-id="bf0bf-129">*Следующие диски виртуальной машины сейчас используют большие двоичные объекты в этом контейнере. Поэтому данный контейнер не может быть удален: VirtualMachineDiskName1, VirtualMachineDiskName2…*</span><span class="sxs-lookup"><span data-stu-id="bf0bf-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="bf0bf-130">Сценарий 3. Невозможно удалить виртуальный жесткий диск</span><span class="sxs-lookup"><span data-stu-id="bf0bf-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="bf0bf-131">После удаления виртуальной машины при попытке удаления больших двоичных объектов для связанных виртуальных жестких дисков может появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="bf0bf-132">*Не удалось удалить BLOB-объект "<путь>/XXXXXX-XXXXXX-os-1447379084699.vhd". Ошибка: "В настоящий момент BLOB-объект находится в аренде, и в запросе не указан идентификатор аренды".*</span><span class="sxs-lookup"><span data-stu-id="bf0bf-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="bf0bf-133">Или</span><span class="sxs-lookup"><span data-stu-id="bf0bf-133">Or</span></span>

<span data-ttu-id="bf0bf-134">*Большой двоичный объект "BlobName.vhd" используется в качестве диска виртуальной машины "VirtualMachineDiskName", поэтому его невозможно удалить.*</span><span class="sxs-lookup"><span data-stu-id="bf0bf-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="bf0bf-135">Решение</span><span class="sxs-lookup"><span data-stu-id="bf0bf-135">Solution</span></span>
<span data-ttu-id="bf0bf-136">Для устранения наиболее распространенных проблем попробуйте следующий метод:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="bf0bf-137">Шаг 1. Удалите любые диски, которые препятствуют удалению учетной записи хранения, контейнера или виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="bf0bf-138">Переключитесь на [классический портал Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf0bf-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="bf0bf-139">Выберите **ВИРТУАЛЬНАЯ МАШИНА** > **ДИСКИ**.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Изображение дисков на виртуальных машинах на классическом портале Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="bf0bf-141">Найдите диски, связанные с учетной записью хранения, контейнером или виртуальным жестким диском, которые нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="bf0bf-142">Проверив расположение диска, вы найдете связанную учетную запись хранения, контейнер или виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Рисунок, демонстрирующий сведения о расположении для дисков на классическом портале Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="bf0bf-144">Удалить эти диски можно с помощью одного из указанных ниже способов.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="bf0bf-145">Если в поле диска **Подключен к** нет виртуальных машин, то его можно удалить напрямую.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="bf0bf-146">Если это диск данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="bf0bf-147">Проверьте имя виртуальной машины, к которой подключен диск.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="bf0bf-148">Выберите **Виртуальные машины** > **Экземпляры** и найдите эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="bf0bf-149">Убедитесь, что никакой процесс не использует диск активно.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="bf0bf-150">Щелкните **Отсоединить диск** в нижней части окна портала, чтобы отключить диск.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="bf0bf-151">Выберите **Виртуальные машины** > **Диски** и подождите, пока поле **Подключен к** не станет пустым.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="bf0bf-152">Это означает, что диск был успешно отключен от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="bf0bf-153">Щелкните **Удалить** в нижней части окна (**Виртуальные машины** > **Диски**), чтобы удалить диск.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="bf0bf-154">Если это диск ОС (поле **Содержит ОС** имеет значение Windows или подобное), который подключен к виртуальной машине, выполните приведенные ниже действия, чтобы удалить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="bf0bf-155">Диск операционной системы невозможно отключить, так что для освобождения аренды нужно удалить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="bf0bf-156">Проверьте имя виртуальной машины, к которой подключен диск данных.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="bf0bf-157">Выберите **Виртуальные машины** > **Экземпляры**, затем выберите виртуальную машину, к которой подключен диск.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="bf0bf-158">Убедитесь, что виртуальная машина больше не используется и в ней нет необходимости.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="bf0bf-159">Выберите виртуальную машину, к которой подключен диск, затем щелкните **Удалить** > **Удалить присоединенные диски**.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="bf0bf-160">Выберите **Виртуальные машины** > **Диски** и подождите, пока диск исчезнет.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="bf0bf-161">На это может потребоваться несколько минут. Может также потребоваться обновить страницу.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="bf0bf-162">Если диск не исчез, подождите, пока поле **Подключен к** не станет пустым.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="bf0bf-163">Это означает, что диск был полностью отключен от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="bf0bf-164">Выберите этот диск и щелкните **Удалить** в нижней части страницы, чтобы удалить его.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="bf0bf-165">Если диск подключен к виртуальной машине, вы не сможете его удалить.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="bf0bf-166">Диски отключаются от удаленной виртуальной машины асинхронно.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="bf0bf-167">После удаления виртуальной машины может пройти несколько минут, прежде чем это поле будет очищено.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="bf0bf-168">Шаг 2. Удалите любые образы виртуальных машин, которые препятствуют удалению учетной записи хранения или контейнера.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="bf0bf-169">Переключитесь на [классический портал Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf0bf-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="bf0bf-170">Выберите **ВИРТУАЛЬНАЯ МАШИНА** > **ОБРАЗЫ**, а затем удалите образы, которые связаны с учетной записью хранения, контейнером или виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="bf0bf-171">После этого попробуйте удалить учетную запись хранения, контейнер или виртуальный жесткий диск снова.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="bf0bf-172">Создайте резервные копии нужных данных, прежде чем удалять учетную запись.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="bf0bf-173">Восстановить удаленный виртуальный жесткий диск, большой двоичный объект, таблицу, очередь и файл невозможно.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="bf0bf-174">Убедитесь, что ресурс не используется.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="bf0bf-175">О состоянии "Остановлена (освобождена)"</span><span class="sxs-lookup"><span data-stu-id="bf0bf-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="bf0bf-176">Виртуальные машины, которые были созданы в классической модели развертывания и сохранены, будут находиться в состоянии **Остановлено (освобождено)** на [портале Azure](https://portal.azure.com/) или [классическом портале Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="bf0bf-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="bf0bf-177">**Классический портал Azure**:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-177">**Azure classic portal**:</span></span>

![Состояние "Остановлено (освобождено)" виртуальных машин на портале Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="bf0bf-179">**Портал Azure**:</span><span class="sxs-lookup"><span data-stu-id="bf0bf-179">**Azure portal**:</span></span>

![Состояние "Остановлено (освобождено)" виртуальных машин на классическом портале Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="bf0bf-181">Состояние "Остановлено (освобождено)" освобождает ресурсы компьютера, такие как ЦП, память и сеть.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="bf0bf-182">Однако диски по-прежнему сохраняются, чтобы при необходимости вы могли быстро повторно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="bf0bf-183">Эти диски создаются на основе виртуальных жестких дисков, поддерживаемых службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="bf0bf-184">Учетная запись хранения имеет эти виртуальные жесткие диски, а диски арендуют их.</span><span class="sxs-lookup"><span data-stu-id="bf0bf-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf0bf-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf0bf-185">Next steps</span></span>
* [<span data-ttu-id="bf0bf-186">Удаление учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="bf0bf-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
