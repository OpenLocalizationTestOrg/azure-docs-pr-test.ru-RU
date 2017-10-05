---
title: "Устранение ошибок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков | Документация Майкрософт"
description: "Устранение ошибок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="468da-103">Устранение ошибок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков</span><span class="sxs-lookup"><span data-stu-id="468da-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="468da-104">При попытке удалить учетную запись хранения Azure, контейнер или виртуальный жесткий диск (VHD) на [портале Azure](https://portal.azure.com) могут возникать ошибки.</span><span class="sxs-lookup"><span data-stu-id="468da-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="468da-105">В этой статье содержатся рекомендации по устранению ошибок в модели развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="468da-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="468da-106">Если эта статья не помогла устранить проблему с Azure, посетите форумы по Azure на сайтах [MSDN и Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="468da-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="468da-107">Проблему можно разместить на этих форумах или отправить по адресу @AzureSupport в Twitter.</span><span class="sxs-lookup"><span data-stu-id="468da-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="468da-108">Кроме того, можно отправить запрос в службу поддержки Azure, выбрав **Получить поддержку** на сайте [службы поддержки Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="468da-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="468da-109">Проблемы</span><span class="sxs-lookup"><span data-stu-id="468da-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="468da-110">Сценарий 1</span><span class="sxs-lookup"><span data-stu-id="468da-110">Scenario 1</span></span>
<span data-ttu-id="468da-111">При попытке удалить виртуальный жесткий диск в учетной записи хранения в модели развертывания с помощью Resource Manager пользователь получил следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="468da-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="468da-112">**Не удалось удалить большой двоичный объект vhds/BlobName.vhd. Ошибка: There is currently a lease on the blob and no lease ID was specified in the request (В настоящий момент большой двоичный объект находится в аренде, и в запросе не указан идентификатор аренды).**</span><span class="sxs-lookup"><span data-stu-id="468da-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="468da-113">Эта проблема может возникнуть, если виртуальный жесткий диск, который вы пытаетесь удалить, по-прежнему находится в аренде на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="468da-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="468da-114">Сценарий 2</span><span class="sxs-lookup"><span data-stu-id="468da-114">Scenario 2</span></span>
<span data-ttu-id="468da-115">При попытке удалить контейнер в учетной записи хранения в модели развертывания с помощью Resource Manager пользователь получил следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="468da-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="468da-116">**Не удалось удалить контейнер хранилища vhds. Ошибка: There is currently a lease on the container and no lease ID was specified in the request (В настоящий момент контейнер находится в аренде, и в запросе не указан идентификатор аренды).**</span><span class="sxs-lookup"><span data-stu-id="468da-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="468da-117">Эта проблема может возникнуть, если контейнер содержит виртуальный жесткий диск, заблокированный в состоянии аренды.</span><span class="sxs-lookup"><span data-stu-id="468da-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="468da-118">Сценарий 3</span><span class="sxs-lookup"><span data-stu-id="468da-118">Scenario 3</span></span>
<span data-ttu-id="468da-119">При попытке удалить учетную запись хранения в модели развертывания с помощью Resource Manager пользователь получил следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="468da-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="468da-120">**Не удалось удалить учетную запись хранения "имя_учетной_записи_хранения". Ошибка: "Не удается удалить учетную запись хранения, так как ее артефакты используются".**</span><span class="sxs-lookup"><span data-stu-id="468da-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="468da-121">Эта проблема может возникнуть, если учетная запись хранения содержит виртуальный жесткий диск, который находится в состоянии аренды.</span><span class="sxs-lookup"><span data-stu-id="468da-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="468da-122">Решение</span><span class="sxs-lookup"><span data-stu-id="468da-122">Solution</span></span> 
<span data-ttu-id="468da-123">Чтобы устранить эти проблемы, необходимо определить виртуальный жесткий диск, который вызывает ошибку, и связанную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="468da-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="468da-124">Затем отсоедините виртуальный жесткий диск от виртуальной машины (для дисков данных) или удалите виртуальную машину, на которой используется виртуальный жесткий диск (для дисков ОС).</span><span class="sxs-lookup"><span data-stu-id="468da-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="468da-125">Это позволит вывести виртуальный жесткий диск из состояния аренды и удалить его.</span><span class="sxs-lookup"><span data-stu-id="468da-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="468da-126">Для этого используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="468da-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="468da-127">Метод 1. Использование обозревателя хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="468da-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="468da-128">Шаг 1. Определение виртуального жесткого диска, который препятствует удалению учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="468da-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="468da-129">При удалении учетной записи хранения появится следующее диалоговое окно сообщения:</span><span class="sxs-lookup"><span data-stu-id="468da-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![сообщение об удалении учетной записи хранения](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="468da-131">Проверьте **URL-адрес диска**, чтобы определить учетную запись хранения и виртуальный жесткий диск, который не позволяет удалить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="468da-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="468da-132">В следующем примере имя учетной записи хранения указано перед строкой .blob.core.windows.net, а имя виртуального жесткого диска — SCCM2012-2015-08-28.vhd.</span><span class="sxs-lookup"><span data-stu-id="468da-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="468da-133">Шаг 2. Удаление виртуального жесткого диска с помощью обозревателя хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="468da-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="468da-134">Скачайте и установите последнюю версию [обозревателя хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="468da-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="468da-135">Это средство является автономным приложением от корпорации Майкрософт, позволяющим работать с данными из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="468da-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="468da-136">Откройте обозреватель хранилищ Azure, щелкните</span><span class="sxs-lookup"><span data-stu-id="468da-136">Open Azure Storage Explorer, select</span></span> ![значок учетной записи](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="468da-138">на левой панели, выберите среду Azure и войдите в нее.</span><span class="sxs-lookup"><span data-stu-id="468da-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="468da-139">Выберите все подписки или подписку, содержащую учетную запись хранения, которую вы хотите удалить.</span><span class="sxs-lookup"><span data-stu-id="468da-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![Добавление подписки](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="468da-141">Перейдите в учетную запись хранения, которая была получена из URL-адреса диска ранее, выберите **Контейнеры BLOB-объектов** > **vhds** и найдите виртуальный жесткий диск, который не позволяет удалить учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="468da-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="468da-142">Если виртуальный жесткий диск найден, определите виртуальную машину, которая использует этот виртуальный жесткий диск, в столбце **Имя виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="468da-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Поиск виртуальной машины](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="468da-144">Удалите аренду виртуального жесткого диска с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="468da-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="468da-145">Дополнительные сведения см. в статье [Устранение ошибок при удалении учетных записей хранения Azure, контейнеров или виртуальных жестких дисков в модели развертывания с помощью Resource Manager](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="468da-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="468da-146">В обозревателе хранилищ Azure щелкните правой кнопкой мыши виртуальный жесткий диск и выберите "Удалить".</span><span class="sxs-lookup"><span data-stu-id="468da-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="468da-147">Удаляет учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="468da-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="468da-148">Метод 2. Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="468da-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="468da-149">Шаг 1. Определение виртуального жесткого диска, который препятствует удалению учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="468da-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="468da-150">При удалении учетной записи хранения появится следующее диалоговое окно сообщения:</span><span class="sxs-lookup"><span data-stu-id="468da-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![сообщение об удалении учетной записи хранения](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="468da-152">Проверьте **URL-адрес диска**, чтобы определить учетную запись хранения и виртуальный жесткий диск, который не позволяет удалить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="468da-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="468da-153">В следующем примере имя учетной записи хранения указано перед строкой .blob.core.windows.net, а имя виртуального жесткого диска — SCCM2012-2015-08-28.vhd.</span><span class="sxs-lookup"><span data-stu-id="468da-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="468da-154">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="468da-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="468da-155">В главном меню выберите **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="468da-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="468da-156">Перейдите к учетной записи хранения и выберите **BLOB-объекты** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="468da-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Снимок экрана: учетная запись хранения с выделенным контейнером vhds на портале](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="468da-158">Найдите виртуальный жесткий диск, полученный с помощью URL-адреса диска ранее.</span><span class="sxs-lookup"><span data-stu-id="468da-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="468da-159">Затем определите виртуальную машину, использующую этот виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="468da-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="468da-160">Как правило, это можно сделать по имени виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="468da-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="468da-161">Виртуальная машина в модели разработки Resource Manager</span><span class="sxs-lookup"><span data-stu-id="468da-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="468da-162">Диски ОС используют следующее соглашение об именовании: "Имя_ВМ-YYYY-MM-DD-HHMMSS.vhd".</span><span class="sxs-lookup"><span data-stu-id="468da-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="468da-163">Диски данных используют следующее соглашение об именовании: "Имя_ВМ-YYYY-MM-DD-HHMMSS.vhd".</span><span class="sxs-lookup"><span data-stu-id="468da-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="468da-164">Виртуальная машина в классической модели разработки</span><span class="sxs-lookup"><span data-stu-id="468da-164">VM in Classic development model</span></span>

   * <span data-ttu-id="468da-165">Диски ОС используют следующее соглашение об именовании: "имя_облачной_службы-имя_ВМ-YYYY-MM-DD-HHMMSS.vhd".</span><span class="sxs-lookup"><span data-stu-id="468da-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="468da-166">Диски данных используют следующее соглашение об именовании: "имя_облачной_службы-имя_ВМ-YYYY-MM-DD-HHMMSS.vhd".</span><span class="sxs-lookup"><span data-stu-id="468da-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="468da-167">Шаг 2. Удаление аренды виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="468da-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="468da-168">[Удалите аренду виртуального жесткого диска](#remove-the-lease-from-the-vhd), а затем удалите учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="468da-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="468da-169">Общие сведения об аренде</span><span class="sxs-lookup"><span data-stu-id="468da-169">What is a lease?</span></span>
<span data-ttu-id="468da-170">Аренда — это блокировка, используемая для контроля доступа к большому двоичному объекту (например, к виртуальному жесткому диску).</span><span class="sxs-lookup"><span data-stu-id="468da-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="468da-171">Если большой двоичный объект находится в состоянии аренды, к нему могут получить доступ только владельцы аренды.</span><span class="sxs-lookup"><span data-stu-id="468da-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="468da-172">Аренда предоставляет следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="468da-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="468da-173">предотвращает повреждение данных при одновременной записи несколькими владельцами данных в ту же самую часть большого двоичного объекта;</span><span class="sxs-lookup"><span data-stu-id="468da-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="468da-174">предотвращает удаление большого двоичного объекта в случае его активного использования (например, виртуальной машиной);</span><span class="sxs-lookup"><span data-stu-id="468da-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="468da-175">предотвращает удаление учетной записи хранения в случае ее активного использования (например, виртуальной машиной).</span><span class="sxs-lookup"><span data-stu-id="468da-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="468da-176">Удаление аренды виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="468da-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="468da-177">Если виртуальный жесткий диск является диском ОС, чтобы удалить аренду, необходимо удалить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="468da-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="468da-178">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="468da-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="468da-179">В **главном** меню выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="468da-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="468da-180">Выберите виртуальную машину, арендующую виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="468da-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="468da-181">Убедитесь, что виртуальная машина больше не используется и в ней нет необходимости.</span><span class="sxs-lookup"><span data-stu-id="468da-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="468da-182">В верхней части колонки **сведений о виртуальной машине** выберите **Удалить**, а затем нажмите кнопку **Да**, чтобы подтвердить.</span><span class="sxs-lookup"><span data-stu-id="468da-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="468da-183">После этого виртуальная машина будет удалена, но виртуальный жесткий диск останется.</span><span class="sxs-lookup"><span data-stu-id="468da-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="468da-184">Однако он выйдет из состояния аренды.</span><span class="sxs-lookup"><span data-stu-id="468da-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="468da-185">Освобождение от аренды может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="468da-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="468da-186">Чтобы убедиться, что аренда удалена, выберите **Все ресурсы** > **Имя учетной записи хранения** > **BLOB-объекты** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="468da-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="468da-187">В области **Свойства BLOB-объекта** для параметра **Состояние аренды** должно быть задано значение **Разблокировано**.</span><span class="sxs-lookup"><span data-stu-id="468da-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="468da-188">Если виртуальный жесткий диск является диском данных, чтобы удалить аренду, отсоедините его от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="468da-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="468da-189">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="468da-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="468da-190">В **главном** меню выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="468da-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="468da-191">Выберите виртуальную машину, арендующую виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="468da-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="468da-192">В колонке **сведений о виртуальной машине** выберите **Диски**.</span><span class="sxs-lookup"><span data-stu-id="468da-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="468da-193">Выберите диск данных, арендующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="468da-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="468da-194">Виртуальный жесткий диск, присоединенный к диску данных, можно определить, просмотрев его URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="468da-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="468da-195">Убедитесь, что диск данных больше не используется.</span><span class="sxs-lookup"><span data-stu-id="468da-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="468da-196">В колонке **Сведения о диске** щелкните **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="468da-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="468da-197">После этого диск будет отсоединен от виртуальной машины, а виртуальный жесткий диск освобожден от аренды.</span><span class="sxs-lookup"><span data-stu-id="468da-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="468da-198">Освобождение от аренды может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="468da-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="468da-199">Чтобы убедиться, что аренда удалена, выберите **Все ресурсы** > **Имя учетной записи хранения** > **BLOB-объекты** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="468da-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="468da-200">В области **Свойства BLOB-объекта** для параметра **Состояние аренды** должно быть задано значение **Разблокировано**.</span><span class="sxs-lookup"><span data-stu-id="468da-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="468da-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="468da-201">Next steps</span></span>
* [<span data-ttu-id="468da-202">Удаление учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="468da-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="468da-203">Приостановка заблокированной аренды хранилища BLOB-объектов в Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="468da-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
