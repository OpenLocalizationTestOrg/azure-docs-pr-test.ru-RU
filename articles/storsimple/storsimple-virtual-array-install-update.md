---
title: "Установка обновлений на виртуальный массив Microsoft Azure StorSimple | Документация Майкрософт"
description: "В этой статье объясняется, как установить обновления на виртуальный массив StorSimple с помощью локального пользовательского веб-интерфейса и портала."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c2d081604c0ca01f47c3ff2aab7477859d280963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="4844b-103">Установка обновлений на виртуальный массив StorSimple с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4844b-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="4844b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4844b-104">Overview</span></span>

<span data-ttu-id="4844b-105">В этой статье описываются шаги, необходимые для установки обновлений на виртуальный массив StorSimple с помощью локального пользовательского веб-интерфейса и портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4844b-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="4844b-106">Применение обновлений или исправлений программного обеспечения необходима, чтобы виртуальный массив StorSimple был актуальным.</span><span class="sxs-lookup"><span data-stu-id="4844b-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="4844b-107">Помните, что при установке обновления или исправления происходит перезагрузка устройства.</span><span class="sxs-lookup"><span data-stu-id="4844b-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="4844b-108">Если виртуальный массив StorSimple — это устройство с одним узлом, то любые выполняемые операции ввода-вывода будут прерваны, а само устройство будет простаивать в течение некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="4844b-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="4844b-109">Перед применением обновления рекомендуется перевести в автономный режим тома или общие папки на узле, а затем перевести в автономный режим само устройство.</span><span class="sxs-lookup"><span data-stu-id="4844b-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="4844b-110">Это уменьшает возможность повреждения данных.</span><span class="sxs-lookup"><span data-stu-id="4844b-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4844b-111">Если у вас установлено обновление 0.1 или общедоступные версии программного обеспечения, то необходимо воспользоваться методом исправления через локальный пользовательский веб-интерфейс и установить обновление 0.3.</span><span class="sxs-lookup"><span data-stu-id="4844b-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="4844b-112">Если у вас установлено обновление 0.2, то рекомендуется устанавливать обновления с помощью классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4844b-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="4844b-113">Использование локального веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="4844b-113">Use the local web UI</span></span>

<span data-ttu-id="4844b-114">При использовании локального веб-интерфейса установка обновлений включает два этапа:</span><span class="sxs-lookup"><span data-stu-id="4844b-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="4844b-115">Загрузка обновления или исправления</span><span class="sxs-lookup"><span data-stu-id="4844b-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="4844b-116">Установка обновления или исправления</span><span class="sxs-lookup"><span data-stu-id="4844b-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="4844b-117">Загрузка обновления или исправления</span><span class="sxs-lookup"><span data-stu-id="4844b-117">Download the update or the hotfix</span></span>

<span data-ttu-id="4844b-118">Для загрузки обновления программного обеспечения из каталога обновления Майкрософт выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4844b-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="4844b-119">Загрузка обновления или исправления</span><span class="sxs-lookup"><span data-stu-id="4844b-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="4844b-120">Запустите Internet Explorer и откройте страницу [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4844b-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="4844b-121">Если вы впервые используете каталог Центра обновления Майкрософт на этом компьютере, нажмите кнопку **Установить** , когда будет предложено установить надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="4844b-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="4844b-122">В поле поиска каталога Центра обновления Майкрософт введите номер необходимого исправления в базе знаний, которое нужно скачать.</span><span class="sxs-lookup"><span data-stu-id="4844b-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="4844b-123">Введите **3182061** для обновления 0.3 и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="4844b-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="4844b-124">Появится список исправлений, например **Обновление 0.3 для виртуального массива StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="4844b-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="4844b-126">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4844b-126">Click **Add**.</span></span> <span data-ttu-id="4844b-127">Обновление будет добавлено в корзину.</span><span class="sxs-lookup"><span data-stu-id="4844b-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="4844b-128">Щелкните **Просмотреть корзину**.</span><span class="sxs-lookup"><span data-stu-id="4844b-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="4844b-129">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="4844b-129">Click **Download**.</span></span> <span data-ttu-id="4844b-130">Укажите или **выберите** локальное расположение, в которое хотите скачать файлы.</span><span class="sxs-lookup"><span data-stu-id="4844b-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="4844b-131">Обновления скачиваются в указанное расположение и помещаются во вложенную папку с тем же именем, что и имя обновления.</span><span class="sxs-lookup"><span data-stu-id="4844b-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="4844b-132">Этот каталог также можно скопировать в сетевую папку, которая доступна с вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="4844b-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="4844b-133">Откройте папку, в которую выполнено копирование. Вы увидите файл изолированного пакета Центра обновления Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="4844b-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="4844b-134">Этот файл используется для установки обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="4844b-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="4844b-135">Установка обновления или исправления</span><span class="sxs-lookup"><span data-stu-id="4844b-135">Install the update or the hotfix</span></span>

<span data-ttu-id="4844b-136">Перед установкой обновления или исправления убедитесь, что обновление или исправление загружено локально на вашем узле или доступно в сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="4844b-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="4844b-137">Воспользуйтесь этим методом для установки обновлений на устройствах, на которых установлены общедоступные версии программного обеспечения или обновление 0.1.</span><span class="sxs-lookup"><span data-stu-id="4844b-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="4844b-138">Эта процедура занимает менее двух минут.</span><span class="sxs-lookup"><span data-stu-id="4844b-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="4844b-139">Для установки обновления или исправления выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4844b-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="4844b-140">Установка обновления или исправления</span><span class="sxs-lookup"><span data-stu-id="4844b-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="4844b-141">В локальном пользовательском веб-интерфейсе перейдите в раздел **Обслуживание** > **Обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="4844b-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="4844b-143">В поле **Путь к файлу обновления**введите имя файла обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="4844b-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="4844b-144">Также вы можете найти файл установки обновления или исправления, если он расположен в сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="4844b-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="4844b-145">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="4844b-145">Click **Apply**.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="4844b-147">Отобразится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="4844b-147">A warning is displayed.</span></span> <span data-ttu-id="4844b-148">Если это устройство с одним узлом, то после применения обновления оно перезагружается, а также возникает время простоя.</span><span class="sxs-lookup"><span data-stu-id="4844b-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="4844b-149">Щелкните значок галочки.</span><span class="sxs-lookup"><span data-stu-id="4844b-149">Click the check icon.</span></span>
   
   ![обновление устройства](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="4844b-151">Начинается обновление.</span><span class="sxs-lookup"><span data-stu-id="4844b-151">The update starts.</span></span> <span data-ttu-id="4844b-152">После успешного обновления устройство перезапускается.</span><span class="sxs-lookup"><span data-stu-id="4844b-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="4844b-153">В течение этого времени локальный пользовательский интерфейс недоступен.</span><span class="sxs-lookup"><span data-stu-id="4844b-153">The local UI is not accessible in this duration.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="4844b-155">После перезапуска открывается страница **входа** .</span><span class="sxs-lookup"><span data-stu-id="4844b-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="4844b-156">Чтобы убедиться, что программное обеспечение устройства обновлено, в локальном пользовательском веб-интерфейсе перейдите в раздел **Обслуживание** > **Обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="4844b-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="4844b-157">Для обновления 0.3 должна отображаться версия программного обеспечения **10.0.0.0.0.10288.0** .</span><span class="sxs-lookup"><span data-stu-id="4844b-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4844b-158">Версии программного обеспечения в локальном веб-интерфейсе и на портале Azure отображаются немного по-разному.</span><span class="sxs-lookup"><span data-stu-id="4844b-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="4844b-159">Например, для одной и той же версии в локальном пользовательском веб-интерфейсе отображается номер **10.0.0.0.0.10288**, а на портале Azure — **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="4844b-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure portal reports **10.0.10288.0** for the same version.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="4844b-161">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="4844b-161">Use the Azure portal</span></span>

<span data-ttu-id="4844b-162">Если используется обновление 0.2, то рекомендуется устанавливать обновления с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4844b-162">If running Update 0.2, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="4844b-163">При использовании портала пользователю нужно проверить наличие обновлений, а затем скачать и установить обновления.</span><span class="sxs-lookup"><span data-stu-id="4844b-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="4844b-164">Эта процедура занимает около 7 минут.</span><span class="sxs-lookup"><span data-stu-id="4844b-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="4844b-165">Для установки обновления или исправления выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4844b-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="4844b-166">После окончания установки (об этом свидетельствует состояние задания "100 %") перейдите к службе диспетчера устройств StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4844b-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="4844b-167">Перейдите к **устройствам** и в списке устройств, подключенных к службе, выберите то, которое требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="4844b-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="4844b-168">В колонке **Параметры** щелкните **Управление** и выберите **Обновления устройства**.</span><span class="sxs-lookup"><span data-stu-id="4844b-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="4844b-169">Отображаемая версия программного обеспечения должна быть следующей: **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="4844b-169">The displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4844b-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4844b-170">Next steps</span></span>

<span data-ttu-id="4844b-171">Дополнительные сведения см. в статье [Использование пользовательского веб-интерфейса для администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="4844b-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

