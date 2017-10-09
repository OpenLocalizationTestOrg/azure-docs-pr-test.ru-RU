---
title: "Обновление 0,5 StorSimple Virtual Array aaaInstall | Документы Microsoft"
description: "Описывает, как tooapply toouse hello StorSimple Virtual Array веб пользовательского интерфейса обновлений с помощью hello Azure portal и исправление метода"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="30931-103">Установка обновления 0.5 на виртуальный массив StorSimple</span><span class="sxs-lookup"><span data-stu-id="30931-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="30931-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="30931-104">Overview</span></span>

<span data-ttu-id="30931-105">В этой статье описывает tooinstall необходимые шаги hello обновления 0,5 виртуального массива StorSimple через hello локального пользовательского веб-интерфейса, а также через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30931-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="30931-106">Необходимо tookeep обновлений или исправлений программного обеспечения tooapply виртуального массива StorSimple актуальной.</span><span class="sxs-lookup"><span data-stu-id="30931-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="30931-107">Перед установкой обновления рекомендуется воспользоваться hello тома или папок в автономном режиме на hello сначала размещения и затем hello устройства.</span><span class="sxs-lookup"><span data-stu-id="30931-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="30931-108">Это уменьшает возможность повреждения данных.</span><span class="sxs-lookup"><span data-stu-id="30931-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="30931-109">После папки или тома hello находятся в автономном режиме, также следует вручную hello устройства резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="30931-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="30931-110">Обновление 0,5 соответствует слишком**10.0.10290.0** версии программного обеспечения на устройстве.</span><span class="sxs-lookup"><span data-stu-id="30931-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="30931-111">Сведения о новых возможностях этого обновления перейдите слишком[заметки о выпуске для обновления 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="30931-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="30931-112">Если вы используете обновления 0,2 или более поздней версии, рекомендуется установки hello обновлений через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30931-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="30931-113">При выполнении обновления 0,1 или Общедоступной версии программного обеспечения, необходимо использовать метод исправление hello через tooinstall пользовательского интерфейса локального web hello обновления 0,5.</span><span class="sxs-lookup"><span data-stu-id="30931-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="30931-114">Помните, что при установке обновления или исправления происходит перезагрузка устройства.</span><span class="sxs-lookup"><span data-stu-id="30931-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="30931-115">При заданном hello StorSimple Virtual Array является устройством с одним узлом, прерваны все операции ввода-вывода выполняется и устройство испытывает время простоя.</span><span class="sxs-lookup"><span data-stu-id="30931-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="30931-116">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="30931-116">Use hello Azure portal</span></span>

<span data-ttu-id="30931-117">Если выполняется обновление, 0.2 и более поздней версии, рекомендуется установить обновления через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30931-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="30931-118">Hello портала процедура требует tooscan пользователя hello, загрузите и установите обновления hello.</span><span class="sxs-lookup"><span data-stu-id="30931-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="30931-119">Эта процедура принимает toocomplete около 7 минут.</span><span class="sxs-lookup"><span data-stu-id="30931-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="30931-120">Hello следующих шагов tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="30931-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="30931-121">Hello установки после завершения, выберите tooyour службы диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="30931-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="30931-122">Выберите **устройств** выберите и щелкните только что обновлено устройства hello.</span><span class="sxs-lookup"><span data-stu-id="30931-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="30931-123">Go слишком**параметры > Управление > обновления устройства**.</span><span class="sxs-lookup"><span data-stu-id="30931-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="30931-124">Hello отображается версия программного обеспечения должна быть **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="30931-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="30931-125">Используйте hello локальный веб-Интерфейс</span><span class="sxs-lookup"><span data-stu-id="30931-125">Use hello local web UI</span></span>

<span data-ttu-id="30931-126">Состоит из двух шагов при использовании hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="30931-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="30931-127">Загрузите hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="30931-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="30931-128">Установка hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="30931-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="30931-129">Загрузите hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="30931-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="30931-130">Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.</span><span class="sxs-lookup"><span data-stu-id="30931-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="30931-131">исправление обновлений или hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="30931-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="30931-132">Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="30931-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="30931-133">Если вы впервые используете hello каталога Центра обновления Майкрософт на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="30931-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="30931-134">В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload.</span><span class="sxs-lookup"><span data-stu-id="30931-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="30931-135">Введите **4021576** для обновления 0.5 и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="30931-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="30931-136">Hello исправление вхождение отображаться, например, **StorSimple Virtual Array обновления 0,5**.</span><span class="sxs-lookup"><span data-stu-id="30931-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="30931-138">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="30931-138">Click **Download**.</span></span> 

5. <span data-ttu-id="30931-139">Вы увидите два toodownload файлы, *файлы MSU* и *.cab* файла.</span><span class="sxs-lookup"><span data-stu-id="30931-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="30931-140">Скачайте все папки tooa этих файлов.</span><span class="sxs-lookup"><span data-stu-id="30931-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="30931-141">Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.</span><span class="sxs-lookup"><span data-stu-id="30931-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="30931-142">Откройте папку hello, где находятся файлы hello.</span><span class="sxs-lookup"><span data-stu-id="30931-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="30931-143">![Файлы в пакете hello](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="30931-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="30931-144">Вот что вы увидите:</span><span class="sxs-lookup"><span data-stu-id="30931-144">You see:</span></span>
    -  <span data-ttu-id="30931-145">Файл автономного пакета Центра обновления Майкрософт `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="30931-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="30931-146">Этот файл является программное обеспечение устройства используется tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="30931-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="30931-147">Файл Geneva Monitoring Agent Package `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="30931-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="30931-148">Этот файл является используется tooupdate hello наблюдения и диагностики службы (MDS) агента.</span><span class="sxs-lookup"><span data-stu-id="30931-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="30931-149">Дважды щелкните hello CAB-файл.</span><span class="sxs-lookup"><span data-stu-id="30931-149">Double-click hello cab file.</span></span> <span data-ttu-id="30931-150">Отобразится MSI-файл.</span><span class="sxs-lookup"><span data-stu-id="30931-150">A .msi is displayed.</span></span> <span data-ttu-id="30931-151">Выберите hello файл, щелкните правой кнопкой мыши и затем **извлечь** файл hello.</span><span class="sxs-lookup"><span data-stu-id="30931-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="30931-152">Вы воспользуетесь hello _.msi_ файл tooupdate hello агента.</span><span class="sxs-lookup"><span data-stu-id="30931-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Извлечение файла обновления агента MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="30931-154">Установка hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="30931-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="30931-155">Предыдущий toohello обновления или исправления установки, убедитесь, что у вас есть обновления hello или исправление hello загружены либо локально на узле или через общий сетевой ресурс.</span><span class="sxs-lookup"><span data-stu-id="30931-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="30931-156">Используйте этот метод обновляет tooinstall на устройствах под управлением общедоступной версии или обновить 0,1 версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="30931-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="30931-157">Эта процедура занимает меньше, чем toocomplete 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="30931-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="30931-158">Hello следующих шагов tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="30931-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="30931-159">исправление обновлений или hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="30931-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="30931-160">В hello локального веб-интерфейса, перейдите слишком**обслуживания** > **обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="30931-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="30931-162">В **путь к файлу обновления**, введите имя файла hello hello обновления или исправления hello.</span><span class="sxs-lookup"><span data-stu-id="30931-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="30931-163">Также можно открыть файл установки обновления или исправления toohello, если размещены на общем сетевом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="30931-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="30931-164">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="30931-164">Click **Apply**.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="30931-166">Отобразится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="30931-166">A warning is displayed.</span></span> <span data-ttu-id="30931-167">Учитывая это является устройство с одним узлом, после применения обновления hello, перезапуска устройства hello и происходит простой.</span><span class="sxs-lookup"><span data-stu-id="30931-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="30931-168">Щелкните значок галочки hello.</span><span class="sxs-lookup"><span data-stu-id="30931-168">Click hello check icon.</span></span>
   
   ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="30931-170">начинается обновление Hello.</span><span class="sxs-lookup"><span data-stu-id="30931-170">hello update starts.</span></span> <span data-ttu-id="30931-171">После успешного обновления hello устройство перезапускается.</span><span class="sxs-lookup"><span data-stu-id="30931-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="30931-172">Hello пользовательского интерфейса локального недоступен в это время.</span><span class="sxs-lookup"><span data-stu-id="30931-172">hello local UI is not accessible in this duration.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="30931-174">После завершения перезагрузки hello берутся toohello **входа** страницы.</span><span class="sxs-lookup"><span data-stu-id="30931-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="30931-175">tooverify обновления программного обеспечения для устройств hello, в hello локального пользовательского веб-интерфейса, перейдите в слишком**обслуживания** > **обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="30931-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="30931-176">Hello отображается версия программного обеспечения должна быть **10.0.0.0.0.10290.0** для обновления 0,5.</span><span class="sxs-lookup"><span data-stu-id="30931-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="30931-177">Мы отчетов версий программного обеспечения hello немного иначе в hello локального пользовательского веб-интерфейса и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="30931-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="30931-178">Например, hello пользовательского интерфейса локального веб-отчеты **10.0.0.0.0.10290** и hello Azure портала отчетов **10.0.10290.0** для hello одинаковую версию.</span><span class="sxs-lookup"><span data-stu-id="30931-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="30931-180">Hello следующим шагом является tooupdate hello MDS агента.</span><span class="sxs-lookup"><span data-stu-id="30931-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="30931-181">В hello **обновление программного обеспечения** страницы, перейдите toohello **путь к файлу обновления** и обзор toohello `GenevaMonitoringAgentPackageInstaller.msi` файл.</span><span class="sxs-lookup"><span data-stu-id="30931-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="30931-182">Повторите шаги 2–4.</span><span class="sxs-lookup"><span data-stu-id="30931-182">Repeat steps 2-4.</span></span> <span data-ttu-id="30931-183">После перезапуска виртуального массива hello, войдите с hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="30931-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="30931-184">Обновление Hello завершена.</span><span class="sxs-lookup"><span data-stu-id="30931-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30931-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30931-185">Next steps</span></span>

<span data-ttu-id="30931-186">Дополнительные сведения см. в статье [Использование пользовательского веб-интерфейса для администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="30931-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

