---
title: "службе диспетчера StorSimple устройство aaaDeploy | Документы Microsoft"
description: "Объясняет, как toocreate и delete hello службы диспетчера StorSimple устройство в hello портал Azure и описывает, как toomanage hello ключ регистрации службы."
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
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="759c8-103">Развертывание службы диспетчера StorSimple устройство hello для StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="759c8-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="759c8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="759c8-104">Overview</span></span>

<span data-ttu-id="759c8-105">службе диспетчера StorSimple устройство Hello выполняется в Microsoft Azure и подключается toomultiple устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="759c8-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="759c8-106">После создания службы hello, его можно использовать устройства hello toomanage hello Microsoft Azure портала запуск в браузере.</span><span class="sxs-lookup"><span data-stu-id="759c8-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="759c8-107">Это позволяет toomonitor всех hello устройствах, подключенных toohello устройства StorSimple службы из централизованного расположения, что сокращает административную нагрузку.</span><span class="sxs-lookup"><span data-stu-id="759c8-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="759c8-108">Hello распространенные задачи связанные tooa службы диспетчера StorSimple устройств являются:</span><span class="sxs-lookup"><span data-stu-id="759c8-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="759c8-109">создание службы;</span><span class="sxs-lookup"><span data-stu-id="759c8-109">Create a service</span></span>
* <span data-ttu-id="759c8-110">удаление службы;</span><span class="sxs-lookup"><span data-stu-id="759c8-110">Delete a service</span></span>
* <span data-ttu-id="759c8-111">Получить ключ регистрации службы hello</span><span class="sxs-lookup"><span data-stu-id="759c8-111">Get hello service registration key</span></span>
* <span data-ttu-id="759c8-112">Повторное создание ключа регистрации службы hello</span><span class="sxs-lookup"><span data-stu-id="759c8-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="759c8-113">В данном учебнике как tooperform каждого из hello выше задач.</span><span class="sxs-lookup"><span data-stu-id="759c8-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="759c8-114">Hello сведения, содержащиеся в этой статье — применимо только tooStorSimple виртуальных массивов.</span><span class="sxs-lookup"><span data-stu-id="759c8-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="759c8-115">Дополнительные сведения о StorSimple серии 8000 go слишком[развертывание службы диспетчера StorSimple](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="759c8-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="759c8-116">создание службы;</span><span class="sxs-lookup"><span data-stu-id="759c8-116">Create a service</span></span>

<span data-ttu-id="759c8-117">toocreate службы требуется toohave:</span><span class="sxs-lookup"><span data-stu-id="759c8-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="759c8-118">подписка с соглашением Enterprise;</span><span class="sxs-lookup"><span data-stu-id="759c8-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="759c8-119">активная учетная запись хранения Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="759c8-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="759c8-120">Здравствуйте, сведений о выставлении счетов, который используется для управления доступом</span><span class="sxs-lookup"><span data-stu-id="759c8-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="759c8-121">Можно также выбрать toogenerate учетной записи хранилища при создании службы hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="759c8-122">Одна служба может управлять несколькими устройствами.</span><span class="sxs-lookup"><span data-stu-id="759c8-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="759c8-123">Однако устройство не может охватить несколько служб.</span><span class="sxs-lookup"><span data-stu-id="759c8-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="759c8-124">Крупные организации могут иметь несколько toowork экземпляров службы с разными подписками, организациями или даже местоположениями развертывания.</span><span class="sxs-lookup"><span data-stu-id="759c8-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="759c8-125">Необходимо, чтобы отдельные экземпляры устройствам серии StorSimple 8000 toomanage службы диспетчера StorSimple устройство и StorSimple виртуальных массивов.</span><span class="sxs-lookup"><span data-stu-id="759c8-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="759c8-126">Выполните следующие шаги toocreate службы hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="759c8-127">удаление службы;</span><span class="sxs-lookup"><span data-stu-id="759c8-127">Delete a service</span></span>

<span data-ttu-id="759c8-128">Перед удалением службы убедитесь в отсутствии подключенных устройств, которые используют ее.</span><span class="sxs-lookup"><span data-stu-id="759c8-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="759c8-129">Если используется служба hello деактивируйте hello подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="759c8-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="759c8-130">Операция отключения Hello sever hello соединения между устройством hello и hello службы, но сохранить данные устройства hello в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="759c8-131">После удаления службы hello операцию невозможно отменить.</span><span class="sxs-lookup"><span data-stu-id="759c8-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="759c8-132">Любое устройство, использовавшей hello службы потребуется toobe сброса к заводским настройкам прежде, чем он может использоваться с другой службой.</span><span class="sxs-lookup"><span data-stu-id="759c8-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="759c8-133">В этом случае локальные данные hello на hello устройства, а также конфигурации hello, будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="759c8-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="759c8-134">Выполните следующие шаги toodelete службы hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="759c8-135">toodelete службы</span><span class="sxs-lookup"><span data-stu-id="759c8-135">toodelete a service</span></span>

1. <span data-ttu-id="759c8-136">Go слишком**все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="759c8-136">Go too**All resources**.</span></span> <span data-ttu-id="759c8-137">Найдите службу диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="759c8-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="759c8-138">Выберите службу hello, что вы хотите toodelete.</span><span class="sxs-lookup"><span data-stu-id="759c8-138">Select hello service that you wish toodelete.</span></span>
   
    ![Выберите службы toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="759c8-140">Go tooyour службы мониторинга tooensure существует нет устройств, подключенных toohello служб.</span><span class="sxs-lookup"><span data-stu-id="759c8-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="759c8-141">Нет устройств, зарегистрированных с помощью этой службы, также увидите эффект toohello заголовка сообщения.</span><span class="sxs-lookup"><span data-stu-id="759c8-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="759c8-142">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="759c8-142">Click **Delete**.</span></span>
   
    ![Удаление службы](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="759c8-144">При появлении запроса на подтверждение нажмите кнопку **Да** в уведомлении подтверждения hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Подтверждение удаления службы](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="759c8-146">Он может занять несколько минут, чтобы удалить toobe службы hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="759c8-147">После hello служба успешно удалена, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="759c8-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Успешное удаление службы](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="759c8-149">Список Hello служб будет обновлен.</span><span class="sxs-lookup"><span data-stu-id="759c8-149">hello list of services will be refreshed.</span></span>

 ![Обновленный список служб](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="759c8-151">Получить ключ регистрации службы hello</span><span class="sxs-lookup"><span data-stu-id="759c8-151">Get hello service registration key</span></span>
<span data-ttu-id="759c8-152">После успешного создания службы необходимо будет tooregister устройства StorSimple со службой hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="759c8-153">tooregister первого устройства StorSimple будет необходимо hello ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="759c8-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="759c8-154">tooregister дополнительных устройств с существующей службой StorSimple, необходимо будет hello регистрационный ключ и ключ шифрования данных службы hello (который создается на первом устройстве hello во время регистрации).</span><span class="sxs-lookup"><span data-stu-id="759c8-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="759c8-155">Дополнительные сведения о ключе шифрования данных службы hello см. в разделе [безопасность StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="759c8-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="759c8-156">Hello регистрационный ключ можно получить, обратившись к hello **ключей** колонку для службы.</span><span class="sxs-lookup"><span data-stu-id="759c8-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="759c8-157">Выполните следующие шаги tooget hello регистрационный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="759c8-158">Ключ регистрации службы tooget hello</span><span class="sxs-lookup"><span data-stu-id="759c8-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="759c8-159">В hello **устройства StorSimple** колонке go слишком**управления &gt;**  **ключей**.</span><span class="sxs-lookup"><span data-stu-id="759c8-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Колонка "Ключи"](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="759c8-161">В hello **ключей** колонки, отображается ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="759c8-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="759c8-162">Скопируйте ключ регистрации hello, используя значок копирования hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="759c8-163">Ключ регистрации службы hello храните в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="759c8-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="759c8-164">Вам потребуется этот ключ, а также ключ шифрования данных службы hello tooregister дополнительных устройств с этой службой.</span><span class="sxs-lookup"><span data-stu-id="759c8-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="759c8-165">После получения ключа регистрации службы hello, необходимо будет tooconfigure устройством через hello Windows PowerShell для StorSimple интерфейса.</span><span class="sxs-lookup"><span data-stu-id="759c8-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="759c8-166">Повторное создание ключа регистрации службы hello</span><span class="sxs-lookup"><span data-stu-id="759c8-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="759c8-167">Tooregenerate ключ регистрации службы потребуется tooperform требуется смена ключей или если hello список администраторов службы изменился.</span><span class="sxs-lookup"><span data-stu-id="759c8-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="759c8-168">При повторном создании ключа hello, hello новый ключ используется только для регистрации последующих устройств.</span><span class="sxs-lookup"><span data-stu-id="759c8-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="759c8-169">Hello устройств, которые уже были зарегистрированы, не затрагиваются этим процессом.</span><span class="sxs-lookup"><span data-stu-id="759c8-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="759c8-170">Выполните следующие tooregenerate действия ключа регистрации службы hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="759c8-171">Ключ регистрации службы tooregenerate hello</span><span class="sxs-lookup"><span data-stu-id="759c8-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="759c8-172">В hello **устройства StorSimple** колонке go слишком**управления &gt;**  **ключей**.</span><span class="sxs-lookup"><span data-stu-id="759c8-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Колонка "Ключи"](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="759c8-174">В hello **ключей** колонка, щелкните **повторно создать**.</span><span class="sxs-lookup"><span data-stu-id="759c8-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Кнопка повторного создания](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="759c8-176">В hello **регистрационный ключ службы заново** колонке действие hello проверка требуется, если hello повторно создаются ключи.</span><span class="sxs-lookup"><span data-stu-id="759c8-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="759c8-177">Все устройства последующие hello, которые зарегистрированы с помощью этой службы будет использовать новый ключ hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="759c8-178">Нажмите кнопку **повторно создать** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="759c8-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="759c8-179">Вы получите уведомление после завершения регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="759c8-179">You will be notified after hello registration is complete.</span></span>
   
   ![Подтверждение повторного создания ключа](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="759c8-181">Появится новый ключ регистрации службы.</span><span class="sxs-lookup"><span data-stu-id="759c8-181">A new service registration key will appear.</span></span>
   
    ![Подтверждение повторного создания ключа](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="759c8-183">Скопируйте этот ключ и сохраните его для регистрации новых устройств в службе.</span><span class="sxs-lookup"><span data-stu-id="759c8-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="759c8-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="759c8-184">Next steps</span></span>
* <span data-ttu-id="759c8-185">Узнайте, каким образом слишком[начать](storsimple-virtual-array-deploy1-portal-prep.md) с StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="759c8-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="759c8-186">Узнайте, каким образом слишком[Администрирование устройства StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="759c8-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

