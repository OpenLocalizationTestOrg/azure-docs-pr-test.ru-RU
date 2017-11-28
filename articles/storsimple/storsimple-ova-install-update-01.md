---
title: "Обновления StorSimple Virtual Array aaaInstall | Документы Microsoft"
description: "Описывается, как hello StorSimple Virtual Array toouse веб-tooapply пользовательский Интерфейс обновления с помощью метода портала, а также исправление hello"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="fa458-103">Установка обновлений на виртуальный массив StorSimple</span><span class="sxs-lookup"><span data-stu-id="fa458-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="fa458-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="fa458-104">Overview</span></span>
<span data-ttu-id="fa458-105">В этой статье описывает hello действия требуется tooinstall обновления виртуального массива StorSimple через hello локального пользовательского веб-интерфейса, а также через hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fa458-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure classic portal.</span></span> <span data-ttu-id="fa458-106">Необходимо tookeep обновлений или исправлений программного обеспечения tooapply виртуального массива StorSimple актуальной.</span><span class="sxs-lookup"><span data-stu-id="fa458-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="fa458-107">Помните, что при установке обновления или исправления происходит перезагрузка устройства.</span><span class="sxs-lookup"><span data-stu-id="fa458-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="fa458-108">При заданном hello StorSimple Virtual Array является устройством с одним узлом, прерваны все операции ввода-вывода выполняется и устройство испытывает время простоя.</span><span class="sxs-lookup"><span data-stu-id="fa458-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="fa458-109">Перед установкой обновления рекомендуется воспользоваться hello тома или папок в автономном режиме на hello сначала размещения и затем hello устройства.</span><span class="sxs-lookup"><span data-stu-id="fa458-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="fa458-110">Это уменьшает возможность повреждения данных.</span><span class="sxs-lookup"><span data-stu-id="fa458-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa458-111">При выполнении обновления 0,1 или Общедоступной версии программного обеспечения, необходимо использовать метод исправление hello через Центр tooinstall обновления 0,3 hello локального web пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="fa458-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="fa458-112">При выполнении обновления 0,2 рекомендуется установить обновления hello через hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fa458-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
> 
> 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="fa458-113">Используйте hello локальный веб-Интерфейс</span><span class="sxs-lookup"><span data-stu-id="fa458-113">Use hello local web UI</span></span>
<span data-ttu-id="fa458-114">Состоит из двух шагов при использовании hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="fa458-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="fa458-115">Загрузите hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="fa458-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="fa458-116">Установка hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="fa458-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="fa458-117">Загрузите hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="fa458-117">Download hello update or hello hotfix</span></span>
<span data-ttu-id="fa458-118">Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="fa458-119">исправление обновлений или hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="fa458-119">toodownload hello update or hello hotfix</span></span>
1. <span data-ttu-id="fa458-120">Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="fa458-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="fa458-121">Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fa458-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="fa458-122">В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload.</span><span class="sxs-lookup"><span data-stu-id="fa458-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="fa458-123">Введите **3182061** для обновления 0.3 и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="fa458-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="fa458-124">Hello исправление вхождение отображаться, например, **обновление массива StorSimple Virtual 0,3**.</span><span class="sxs-lookup"><span data-stu-id="fa458-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="fa458-126">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fa458-126">Click **Add**.</span></span> <span data-ttu-id="fa458-127">Обновление Hello добавляется toohello корзины.</span><span class="sxs-lookup"><span data-stu-id="fa458-127">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="fa458-128">Щелкните **Просмотреть корзину**.</span><span class="sxs-lookup"><span data-stu-id="fa458-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="fa458-129">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="fa458-129">Click **Download**.</span></span> <span data-ttu-id="fa458-130">Укажите или **Обзор** tooa локального место tooappear загружает hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="fa458-131">Hello обновления загружаются toohello определенное место и помещается во вложенную папку с точно такое же имя, как и при обновлении hello hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="fa458-132">Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
7. <span data-ttu-id="fa458-133">Откройте hello скопирована папка, должен находиться файл автономного пакета Центра обновления Майкрософт `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="fa458-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="fa458-134">Этот файл является используется tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="fa458-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="fa458-135">Установка hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="fa458-135">Install hello update or hello hotfix</span></span>
<span data-ttu-id="fa458-136">Предыдущий toohello обновления или исправления установки, убедитесь, что у вас есть обновления hello или исправление hello загружены либо локально на узле или через общий сетевой ресурс.</span><span class="sxs-lookup"><span data-stu-id="fa458-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="fa458-137">Используйте этот метод обновляет tooinstall на устройствах под управлением общедоступной версии или обновить 0,1 версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="fa458-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="fa458-138">Эта процедура занимает меньше, чем toocomplete 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="fa458-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="fa458-139">Hello следующих шагов tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="fa458-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="fa458-140">исправление обновлений или hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="fa458-140">tooinstall hello update or hello hotfix</span></span>
1. <span data-ttu-id="fa458-141">В hello локального веб-интерфейса, перейдите слишком**обслуживания** > **обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="fa458-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![обновление устройства](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="fa458-143">В **путь к файлу обновления**, введите имя файла hello hello обновления или исправления hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="fa458-144">Также можно открыть файл установки обновления или исправления toohello, если размещены на общем сетевом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="fa458-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="fa458-145">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="fa458-145">Click **Apply**.</span></span>
   
    ![обновление устройства](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="fa458-147">Отобразится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="fa458-147">A warning is displayed.</span></span> <span data-ttu-id="fa458-148">Учитывая это является устройство с одним узлом, после применения обновления hello, перезапуска устройства hello и происходит простой.</span><span class="sxs-lookup"><span data-stu-id="fa458-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="fa458-149">Щелкните значок галочки hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-149">Click hello check icon.</span></span>
   
   ![обновление устройства](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="fa458-151">начинается обновление Hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-151">hello update starts.</span></span> <span data-ttu-id="fa458-152">После успешного обновления hello устройство перезапускается.</span><span class="sxs-lookup"><span data-stu-id="fa458-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="fa458-153">Hello пользовательского интерфейса локального недоступен в это время.</span><span class="sxs-lookup"><span data-stu-id="fa458-153">hello local UI is not accessible in this duration.</span></span>
   
    ![обновление устройства](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="fa458-155">После завершения перезагрузки hello берутся toohello **входа** страницы.</span><span class="sxs-lookup"><span data-stu-id="fa458-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="fa458-156">tooverify обновления программного обеспечения для устройств hello, в hello локального пользовательского веб-интерфейса, перейдите в слишком**обслуживания** > **обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="fa458-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="fa458-157">Hello отображается версия программного обеспечения должна быть **10.0.0.0.0.10288.0** для обновления 0,3.</span><span class="sxs-lookup"><span data-stu-id="fa458-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fa458-158">Мы отчетов версий программного обеспечения hello немного иначе в hello локального пользовательского веб-интерфейса и hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fa458-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure classic portal.</span></span> <span data-ttu-id="fa458-159">Например, hello пользовательского интерфейса локального веб-отчеты **10.0.0.0.0.10288** и hello Azure классические отчеты портала **10.0.10288.0** для hello одинаковую версию.</span><span class="sxs-lookup"><span data-stu-id="fa458-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure classic portal reports **10.0.10288.0** for hello same version.</span></span> 
   > 
   > 
   
    ![обновление устройства](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="fa458-161">Hello используйте классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="fa458-161">Use hello Azure classic portal</span></span>
<span data-ttu-id="fa458-162">Если выполняется обновление 0,2, рекомендуется установить обновления с помощью hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fa458-162">If running Update 0.2, we recommend that you install updates through hello Azure classic portal.</span></span> <span data-ttu-id="fa458-163">Hello портала процедура требует tooscan пользователя hello, загрузите и установите обновления hello.</span><span class="sxs-lookup"><span data-stu-id="fa458-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="fa458-164">Эта процедура принимает toocomplete около 7 минут.</span><span class="sxs-lookup"><span data-stu-id="fa458-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="fa458-165">Hello следующих шагов tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="fa458-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="fa458-166">После hello Установка завершена (как указано в состояние задания в масштабе 100%), перейдите в слишком**устройства > обслуживание > обновлений программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="fa458-166">After hello installation is complete (as indicated by job status at 100 %), go too**Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="fa458-167">Hello отображается версия программного обеспечения, должна быть 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="fa458-167">hello displayed software version should be 10.0.10288.0.</span></span>

![обновление устройства](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="fa458-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa458-169">Next steps</span></span>
<span data-ttu-id="fa458-170">Дополнительные сведения см. в статье [Использование пользовательского веб-интерфейса для администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="fa458-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

