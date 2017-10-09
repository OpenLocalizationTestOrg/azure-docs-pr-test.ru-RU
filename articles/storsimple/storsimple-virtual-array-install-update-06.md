---
title: "Обновление 0,6 StorSimple Virtual Array aaaInstall | Документы Microsoft"
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="69425-103">Установка обновления 0.6 для виртуального массива StorSimple</span><span class="sxs-lookup"><span data-stu-id="69425-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="69425-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="69425-104">Overview</span></span>

<span data-ttu-id="69425-105">В этой статье описывает tooinstall необходимые шаги hello обновления 0,6 виртуального массива StorSimple через hello локального пользовательского веб-интерфейса, а также через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="69425-105">This article describes hello steps required tooinstall Update 0.6 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="69425-106">Применить tookeep обновлений или исправлений программного обеспечения hello вашей StorSimple Virtual Array актуальной.</span><span class="sxs-lookup"><span data-stu-id="69425-106">You apply hello software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="69425-107">Перед установкой обновления рекомендуется воспользоваться hello тома или папок в автономном режиме на hello сначала размещения и затем hello устройства.</span><span class="sxs-lookup"><span data-stu-id="69425-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="69425-108">Это уменьшает возможность повреждения данных.</span><span class="sxs-lookup"><span data-stu-id="69425-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="69425-109">После папки или тома hello находятся в автономном режиме, также следует вручную hello устройства резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="69425-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="69425-110">Обновление 0,6 соответствует слишком**10.0.10293.0** версии программного обеспечения на устройстве.</span><span class="sxs-lookup"><span data-stu-id="69425-110">Update 0.6 corresponds too**10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="69425-111">Сведения о новых возможностях этого обновления перейдите слишком[заметки о выпуске для обновления 0,6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="69425-111">For information on what is new in this update, go too[Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="69425-112">Если вы используете обновления 0,2 или более поздней версии, рекомендуется установки hello обновлений через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="69425-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="69425-113">При выполнении обновления 0,1 или Общедоступной версии программного обеспечения, необходимо использовать метод исправление hello через tooinstall пользовательского интерфейса локального web hello обновления 0,6.</span><span class="sxs-lookup"><span data-stu-id="69425-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.6.</span></span>
>
> - <span data-ttu-id="69425-114">Помните, что при установке обновления или исправления происходит перезагрузка устройства.</span><span class="sxs-lookup"><span data-stu-id="69425-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="69425-115">При заданном hello StorSimple Virtual Array является устройством с одним узлом, прерваны все операции ввода-вывода выполняется и устройство испытывает время простоя.</span><span class="sxs-lookup"><span data-stu-id="69425-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="69425-116">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="69425-116">Use hello Azure portal</span></span>

<span data-ttu-id="69425-117">Если выполняется обновление, 0.2 и более поздней версии, рекомендуется установить обновления через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="69425-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="69425-118">Hello портала процедура требует tooscan пользователя hello, загрузите и установите обновления hello.</span><span class="sxs-lookup"><span data-stu-id="69425-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="69425-119">Эта процедура принимает toocomplete около 7 минут.</span><span class="sxs-lookup"><span data-stu-id="69425-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="69425-120">Hello следующих шагов tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="69425-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="69425-121">Hello установки после завершения, выберите tooyour службы диспетчера StorSimple устройство.</span><span class="sxs-lookup"><span data-stu-id="69425-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="69425-122">Выберите **устройств** выберите и щелкните только что обновлено устройства hello.</span><span class="sxs-lookup"><span data-stu-id="69425-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="69425-123">Go слишком**параметры > Управление > обновления устройства**.</span><span class="sxs-lookup"><span data-stu-id="69425-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="69425-124">Hello отображается версия программного обеспечения должна быть **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="69425-124">hello displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="69425-125">Используйте hello локальный веб-Интерфейс</span><span class="sxs-lookup"><span data-stu-id="69425-125">Use hello local web UI</span></span>

<span data-ttu-id="69425-126">Состоит из двух шагов при использовании hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="69425-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="69425-127">Загрузите hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="69425-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="69425-128">Установка hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="69425-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="69425-129">Загрузите hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="69425-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="69425-130">Выполните следующие действия toodownload hello обновления из каталога Центра обновления Майкрософт hello hello.</span><span class="sxs-lookup"><span data-stu-id="69425-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="69425-131">исправление обновлений или hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="69425-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="69425-132">Запустите Internet Explorer и перейдите слишком[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="69425-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="69425-133">Если вы используете hello каталога Центра обновления Майкрософт для hello первый раз на этом компьютере, нажмите кнопку **установить** при запрашиваемые tooinstall hello надстройку каталога Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="69425-133">If you are using hello Microsoft Update Catalog for hello first time on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="69425-134">В поле поиска hello hello каталога Центра обновления Майкрософт, введите номер базы знаний (KB) hello hello исправления требуется toodownload.</span><span class="sxs-lookup"><span data-stu-id="69425-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="69425-135">Введите **4023268** для обновления 0.6 и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="69425-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="69425-136">Hello исправление вхождение отображаться, например, **StorSimple Virtual Array обновления 0,6**.</span><span class="sxs-lookup"><span data-stu-id="69425-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Поиск в каталоге](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="69425-138">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="69425-138">Click **Download**.</span></span>

5. <span data-ttu-id="69425-139">Вы увидите toodownload пять файлов.</span><span class="sxs-lookup"><span data-stu-id="69425-139">You should see five files toodownload.</span></span> <span data-ttu-id="69425-140">Скачайте все папки tooa этих файлов.</span><span class="sxs-lookup"><span data-stu-id="69425-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="69425-141">Папка Hello также может быть скопированный tooa сетевая папка, которая доступна из устройства hello.</span><span class="sxs-lookup"><span data-stu-id="69425-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="69425-142">Откройте папку hello, где находятся файлы hello.</span><span class="sxs-lookup"><span data-stu-id="69425-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="69425-143">![Файлы в пакете hello](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="69425-143">![Files in hello package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="69425-144">Вот что вы увидите:</span><span class="sxs-lookup"><span data-stu-id="69425-144">You see:</span></span>
    -  <span data-ttu-id="69425-145">Файл автономного пакета Центра обновления Майкрософт `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="69425-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="69425-146">Этот файл является программное обеспечение устройства используется tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="69425-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="69425-147">Файл Geneva Monitoring Agent Package `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="69425-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="69425-148">Этот файл является используется tooupdate hello наблюдения и диагностики службы (MDS) агента.</span><span class="sxs-lookup"><span data-stu-id="69425-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="69425-149">Дважды щелкните hello CAB-файл.</span><span class="sxs-lookup"><span data-stu-id="69425-149">Double-click hello cab file.</span></span> <span data-ttu-id="69425-150">Отобразится _MSI_-файл.</span><span class="sxs-lookup"><span data-stu-id="69425-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="69425-151">Выберите hello файл, щелкните правой кнопкой мыши и затем **извлечь** файл hello.</span><span class="sxs-lookup"><span data-stu-id="69425-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="69425-152">Использовать hello _.msi_ файл tooupdate hello агента.</span><span class="sxs-lookup"><span data-stu-id="69425-152">You use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Извлечение файла обновления агента MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="69425-154">Агент MDS tooupdate hello не обязательно при выполнении обновления StorSimple 0,5 (0.0.10293.0).</span><span class="sxs-lookup"><span data-stu-id="69425-154">You do not need tooupdate hello MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="69425-155">Три файла, которые содержат важные обновления системы безопасности Windows, `windows8.1-kb4012213-x64`, `windows8.1-kb3205400-x64` и `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="69425-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="69425-156">Установка hello обновления или исправления hello</span><span class="sxs-lookup"><span data-stu-id="69425-156">Install hello update or hello hotfix</span></span>

<span data-ttu-id="69425-157">Предыдущий toohello обновления или исправления установки, убедитесь, что у вас есть обновления hello или исправление hello загружены либо локально на узле или через общий сетевой ресурс.</span><span class="sxs-lookup"><span data-stu-id="69425-157">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="69425-158">Используйте этот метод обновляет tooinstall на устройствах под управлением общедоступной версии или обновить 0,1 версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="69425-158">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="69425-159">Эта процедура занимает приблизительно toocomplete 12 минут.</span><span class="sxs-lookup"><span data-stu-id="69425-159">This procedure takes approximately 12 minutes toocomplete.</span></span> <span data-ttu-id="69425-160">Hello следующих шагов tooinstall hello обновления или исправления.</span><span class="sxs-lookup"><span data-stu-id="69425-160">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="69425-161">исправление обновлений или hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="69425-161">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="69425-162">В hello локального веб-интерфейса, перейдите слишком**обслуживания** > **обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="69425-162">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="69425-163">Запишите hello версия программного обеспечения, которое выполняется.</span><span class="sxs-lookup"><span data-stu-id="69425-163">Make a note of hello software version that you are running.</span></span> <span data-ttu-id="69425-164">Если вы используете **10.0.10290.0**, нет необходимости tooupdate hello MDS агент на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="69425-164">If you are running **10.0.10290.0**, you do not need tooupdate hello MDS agent in step 6.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="69425-166">В **путь к файлу обновления**, введите имя файла hello hello обновления или исправления hello.</span><span class="sxs-lookup"><span data-stu-id="69425-166">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="69425-167">Также можно открыть файл установки обновления или исправления toohello, если размещены на общем сетевом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="69425-167">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="69425-168">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="69425-168">Click **Apply**.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="69425-170">Отобразится предупреждение.</span><span class="sxs-lookup"><span data-stu-id="69425-170">A warning is displayed.</span></span> <span data-ttu-id="69425-171">Данный hello виртуального массива находится устройство с одним узлом, после применения обновления hello, перезапуска устройства hello и происходит простой.</span><span class="sxs-lookup"><span data-stu-id="69425-171">Given hello virtual array is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="69425-172">Щелкните значок галочки hello.</span><span class="sxs-lookup"><span data-stu-id="69425-172">Click hello check icon.</span></span>
   
   ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="69425-174">начинается обновление Hello.</span><span class="sxs-lookup"><span data-stu-id="69425-174">hello update starts.</span></span> <span data-ttu-id="69425-175">После успешного обновления hello устройство перезапускается.</span><span class="sxs-lookup"><span data-stu-id="69425-175">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="69425-176">Hello пользовательского интерфейса локального недоступен в это время.</span><span class="sxs-lookup"><span data-stu-id="69425-176">hello local UI is not accessible in this duration.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="69425-178">После завершения перезагрузки hello берутся toohello **входа** страницы.</span><span class="sxs-lookup"><span data-stu-id="69425-178">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="69425-179">tooverify обновления программного обеспечения для устройств hello, в hello локального пользовательского веб-интерфейса, перейдите в слишком**обслуживания** > **обновление программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="69425-179">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="69425-180">Hello отображается версия программного обеспечения должна быть **10.0.0.0.0.10293** для обновления 0,6.</span><span class="sxs-lookup"><span data-stu-id="69425-180">hello displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="69425-181">Мы отчетов версий программного обеспечения hello немного иначе в hello локального пользовательского веб-интерфейса и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="69425-181">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="69425-182">Например, hello пользовательского интерфейса локального веб-отчеты **10.0.0.0.0.10293** и hello Azure портала отчетов **10.0.10293.0** для hello одинаковую версию.</span><span class="sxs-lookup"><span data-stu-id="69425-182">For example, hello local web UI reports **10.0.0.0.0.10293** and hello Azure portal reports **10.0.10293.0** for hello same version.</span></span>
   
    ![обновление устройства](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="69425-184">Пропустите этот шаг, если на компьютере выполнялось обновление виртуального массива StorSimple 0.5 (**10.0.10290.0**) до применения этого обновления.</span><span class="sxs-lookup"><span data-stu-id="69425-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="69425-185">Примечание версии программного обеспечения hello установленные на шаге 1, до начала tooupdate.</span><span class="sxs-lookup"><span data-stu-id="69425-185">You made a note of hello software version in step 1 before you began tooupdate.</span></span> <span data-ttu-id="69425-186">Если выполнялась версия обновления 0.5, агент MDS уже обновлен.</span><span class="sxs-lookup"><span data-stu-id="69425-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="69425-187">При выполнении предыдущего tooUpdate каталога версии программного обеспечения 0,5 hello следующим шагом для вас является tooupdate hello MDS агента.</span><span class="sxs-lookup"><span data-stu-id="69425-187">If you are running a software version prior tooUpdate 0.5, hello next step for you is tooupdate hello MDS agent.</span></span> <span data-ttu-id="69425-188">В hello **обновление программного обеспечения** страницы, перейдите toohello **путь к файлу обновления** и обзор toohello `GenevaMonitoringAgentPackageInstaller.msi` файл.</span><span class="sxs-lookup"><span data-stu-id="69425-188">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="69425-189">Повторите шаги 2–4.</span><span class="sxs-lookup"><span data-stu-id="69425-189">Repeat steps 2-4.</span></span> <span data-ttu-id="69425-190">После перезапуска виртуального массива hello, войдите с hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="69425-190">After hello virtual array restarts, sign into hello local web UI.</span></span>

7. <span data-ttu-id="69425-191">Повторите шаг 2 – 4 tooinstall hello Windows исправления безопасности с помощью файлов `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, и `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="69425-191">Repeat step 2-4 tooinstall hello Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="69425-192">виртуальный массив Hello перезапускается после установки каждого и потребуется toosign в hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="69425-192">hello virtual array restarts after each install and you need toosign into hello local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69425-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69425-193">Next steps</span></span>

<span data-ttu-id="69425-194">Дополнительные сведения см. в статье [Использование пользовательского веб-интерфейса для администрирования виртуального массива StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="69425-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

