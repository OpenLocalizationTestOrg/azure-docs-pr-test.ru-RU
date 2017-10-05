---
title: "Развертывание службы диспетчера устройств StorSimple | Документация Майкрософт"
description: "Сведения о создании и удалении службы диспетчера устройств StorSimple на портале Azure, а также об управлении ключом регистрации службы."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="36ad3-103">Развертывание службы диспетчера устройств StorSimple для виртуального массива StorSimple</span><span class="sxs-lookup"><span data-stu-id="36ad3-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="36ad3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="36ad3-104">Overview</span></span>

<span data-ttu-id="36ad3-105">Служба диспетчера устройств StorSimple выполняется в Microsoft Azure и подключается к нескольким устройствам StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36ad3-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="36ad3-106">После создания службы вы можете использовать ее для управления этими устройствами на портале Microsoft Azure, запущенном в браузере.</span><span class="sxs-lookup"><span data-stu-id="36ad3-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="36ad3-107">Это позволит отследить все устройства, которые подключены к службе диспетчера устройств StorSimple из одного центрального расположения, таким образом, снизив административную нагрузку.</span><span class="sxs-lookup"><span data-stu-id="36ad3-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="36ad3-108">Стандартные задачи, связанные со службой диспетчера устройств StorSimple:</span><span class="sxs-lookup"><span data-stu-id="36ad3-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="36ad3-109">Создание службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-109">Create a service</span></span>
* <span data-ttu-id="36ad3-110">удаление службы;</span><span class="sxs-lookup"><span data-stu-id="36ad3-110">Delete a service</span></span>
* <span data-ttu-id="36ad3-111">Получение регистрационного ключа службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-111">Get the service registration key</span></span>
* <span data-ttu-id="36ad3-112">повторное создание ключа регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-112">Regenerate the service registration key</span></span>

<span data-ttu-id="36ad3-113">В этом руководстве описано, как выполнить каждую из этих задач.</span><span class="sxs-lookup"><span data-stu-id="36ad3-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="36ad3-114">Сведения в этой статье применимы только к виртуальным массивам StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36ad3-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="36ad3-115">Дополнительные сведения о серии StorSimple 8000 см. в разделе о [развертывании службы диспетчера StorSimple](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="36ad3-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="36ad3-116">Создание службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-116">Create a service</span></span>

<span data-ttu-id="36ad3-117">Для создания службы требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="36ad3-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="36ad3-118">подписка с соглашением Enterprise;</span><span class="sxs-lookup"><span data-stu-id="36ad3-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="36ad3-119">активная учетная запись хранения Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="36ad3-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="36ad3-120">сведения о выставлении счетов, которые используются для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="36ad3-120">The billing information that is used for access management</span></span>

<span data-ttu-id="36ad3-121">Вы также можете создать учетную запись хранения во время создания службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="36ad3-122">Одна служба может управлять несколькими устройствами.</span><span class="sxs-lookup"><span data-stu-id="36ad3-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="36ad3-123">Однако устройство не может охватить несколько служб.</span><span class="sxs-lookup"><span data-stu-id="36ad3-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="36ad3-124">В большую организацию может входить несколько экземпляров служб для работы с разными подписками, организациями или даже местоположениями развернутых служб.</span><span class="sxs-lookup"><span data-stu-id="36ad3-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="36ad3-125">Для управления виртуальными массивами StorSimple и устройствами StorSimple серии 8000 необходимо создать отдельные экземпляры службы диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36ad3-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="36ad3-126">Выполните следующие действия, чтобы создать службу.</span><span class="sxs-lookup"><span data-stu-id="36ad3-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="36ad3-127">удаление службы;</span><span class="sxs-lookup"><span data-stu-id="36ad3-127">Delete a service</span></span>

<span data-ttu-id="36ad3-128">Перед удалением службы убедитесь в отсутствии подключенных устройств, которые используют ее.</span><span class="sxs-lookup"><span data-stu-id="36ad3-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="36ad3-129">Если служба используется, деактивируйте подключенные устройства.</span><span class="sxs-lookup"><span data-stu-id="36ad3-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="36ad3-130">Операция деактивации разорвет подключение между устройством и службой, но сохранит данные устройства в облаке.</span><span class="sxs-lookup"><span data-stu-id="36ad3-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36ad3-131">Операцию удаления службы невозможно обратить.</span><span class="sxs-lookup"><span data-stu-id="36ad3-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="36ad3-132">На всех устройствах, где использовалась служба, потребуется сброс до заводских настроек перед тем, как на них можно будет использовать другие службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="36ad3-133">В этом случае локальные данные на устройстве, а также конфигурация, будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="36ad3-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="36ad3-134">Чтобы удалить службу, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="36ad3-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="36ad3-135">Удаление службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-135">To delete a service</span></span>

1. <span data-ttu-id="36ad3-136">Щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="36ad3-136">Go to **All resources**.</span></span> <span data-ttu-id="36ad3-137">Найдите службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36ad3-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="36ad3-138">Выберите службу, которую требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="36ad3-138">Select the service that you wish to delete.</span></span>
   
    ![Выбор службы, которую необходимо удалить](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="36ad3-140">Перейдите к панели мониторинга службы, чтобы убедиться в отсутствии устройств, подключенных к службе.</span><span class="sxs-lookup"><span data-stu-id="36ad3-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="36ad3-141">Если в этой службе не зарегистрированы устройства, вы также увидите заглавное сообщение, указывающее, что они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="36ad3-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="36ad3-142">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="36ad3-142">Click **Delete**.</span></span>
   
    ![Удаление службы](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="36ad3-144">При появлении запроса на подтверждение щелкните **Да** в уведомлении о подтверждении.</span><span class="sxs-lookup"><span data-stu-id="36ad3-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Подтверждение удаления службы](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="36ad3-146">Удаление службы может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="36ad3-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="36ad3-147">Как только служба будет удалена, вы получите соответствующее уведомление.</span><span class="sxs-lookup"><span data-stu-id="36ad3-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Успешное удаление службы](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="36ad3-149">Список служб будет обновлен.</span><span class="sxs-lookup"><span data-stu-id="36ad3-149">The list of services will be refreshed.</span></span>

 ![Обновленный список служб](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="36ad3-151">Получение регистрационного ключа службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-151">Get the service registration key</span></span>
<span data-ttu-id="36ad3-152">После успешного создания службы потребуется зарегистрировать устройство StorSimple в службе.</span><span class="sxs-lookup"><span data-stu-id="36ad3-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="36ad3-153">Для регистрации первого устройства StorSimple необходим ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="36ad3-154">Для регистрации дополнительных устройств в существующей службе StorSimple потребуется ключ регистрации и ключ шифрования данных службы (который создается на первом устройстве во время регистрации).</span><span class="sxs-lookup"><span data-stu-id="36ad3-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="36ad3-155">Дополнительные сведения о ключе шифрования данных службы см. в разделе [Безопасность StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="36ad3-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="36ad3-156">Ключ регистрации службы можно получить в колонке **Ключи** соответствующей службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="36ad3-157">Выполните следующие действия, чтобы получить ключ регистрации.</span><span class="sxs-lookup"><span data-stu-id="36ad3-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="36ad3-158">Получение ключа регистрации службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-158">To get the service registration key</span></span>
1. <span data-ttu-id="36ad3-159">В колонке **Диспетчер устройств StorSimple** выберите **Управление &gt;** **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="36ad3-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Колонка "Ключи"](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="36ad3-161">В колонке **Ключи** вы увидите ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="36ad3-162">Скопируйте ключ регистрации, используя значок копирования.</span><span class="sxs-lookup"><span data-stu-id="36ad3-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="36ad3-163">Сохраните ключ регистрации в безопасном расположении.</span><span class="sxs-lookup"><span data-stu-id="36ad3-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="36ad3-164">Этот ключ, а также ключ шифрования данных службы потребуется для регистрации дополнительных устройств в службе.</span><span class="sxs-lookup"><span data-stu-id="36ad3-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="36ad3-165">После получения ключа регистрации службы вам потребуется настроить устройство в интерфейсе Windows PowerShell для StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36ad3-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="36ad3-166">повторное создание ключа регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-166">Regenerate the service registration key</span></span>
<span data-ttu-id="36ad3-167">Если вам необходимо сменить ключ или при изменении списка администраторов службы потребуется повторно создать ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="36ad3-168">При повторном создании ключа новый ключ используется только для регистрации последующих устройств.</span><span class="sxs-lookup"><span data-stu-id="36ad3-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="36ad3-169">Этот процесс не затронет уже зарегистрированные устройства.</span><span class="sxs-lookup"><span data-stu-id="36ad3-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="36ad3-170">Выполните следующие действия, чтобы повторно создать ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="36ad3-171">Повторное создание ключа регистрации службы</span><span class="sxs-lookup"><span data-stu-id="36ad3-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="36ad3-172">В колонке **Диспетчер устройств StorSimple** выберите **Управление &gt;** **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="36ad3-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Колонка "Ключи"](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="36ad3-174">В колонке **Ключи** нажмите кнопку **Повторно создать**.</span><span class="sxs-lookup"><span data-stu-id="36ad3-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Кнопка повторного создания](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="36ad3-176">В колонке **Повторное создание ключа регистрации службы** просмотрите действие, необходимое при повторном создании ключей.</span><span class="sxs-lookup"><span data-stu-id="36ad3-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="36ad3-177">Все последующие устройства, зарегистрированные в этой службе, будут использовать новый ключ регистрации.</span><span class="sxs-lookup"><span data-stu-id="36ad3-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="36ad3-178">Для подтверждения нажмите кнопку **Повторно создать**.</span><span class="sxs-lookup"><span data-stu-id="36ad3-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="36ad3-179">После завершения регистрации вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="36ad3-179">You will be notified after the registration is complete.</span></span>
   
   ![Подтверждение повторного создания ключа](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="36ad3-181">Появится новый ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="36ad3-181">A new service registration key will appear.</span></span>
   
    ![Подтверждение повторного создания ключа](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="36ad3-183">Скопируйте этот ключ и сохраните его для регистрации новых устройств в службе.</span><span class="sxs-lookup"><span data-stu-id="36ad3-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36ad3-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36ad3-184">Next steps</span></span>
* <span data-ttu-id="36ad3-185">Узнайте, как [приступить к работе](storsimple-virtual-array-deploy1-portal-prep.md) с виртуальным массивом StorSimple.</span><span class="sxs-lookup"><span data-stu-id="36ad3-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="36ad3-186">Узнайте, как [администрировать устройство StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="36ad3-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

