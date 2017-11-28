---
title: "Виртуальный массив aaaStorSimple web пользовательского интерфейса администрирования | Документы Microsoft"
description: "Описывает выполнение задач администрирования tooperform базовые устройств через hello StorSimple Virtual Array пользовательского веб-интерфейса."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="58248-103">Использовать tooadminister hello веб-интерфейса виртуального массива StorSimple</span><span class="sxs-lookup"><span data-stu-id="58248-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![последовательность операций процесса настройки](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="58248-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="58248-105">Overview</span></span>
<span data-ttu-id="58248-106">учебники Hello в данной статье применимы выпуска общедоступной (версии GA) выполняющегося марта 2016 г. toohello Microsoft Azure StorSimple Virtual Array (также известный как hello локального виртуального устройства StorSimple).</span><span class="sxs-lookup"><span data-stu-id="58248-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="58248-107">В этой статье описываются некоторые hello сложных рабочих процессов и задач управления, которые могут быть выполнены на hello StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="58248-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="58248-108">Вы можете управлять hello StorSimple Virtual Array, с помощью пользовательского интерфейса (который ссылается tooas hello пользовательском Интерфейсе портала) в службе StorSimple Manager hello и hello локальный веб-Интерфейс для hello устройства.</span><span class="sxs-lookup"><span data-stu-id="58248-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="58248-109">Эта статья посвящена hello задачи, которые можно выполнять с помощью hello веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58248-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="58248-110">Эта статья содержит следующие учебники hello:</span><span class="sxs-lookup"><span data-stu-id="58248-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="58248-111">Получение ключа шифрования данных службы hello</span><span class="sxs-lookup"><span data-stu-id="58248-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="58248-112">устранение ошибок настройки пользовательского веб-интерфейса;</span><span class="sxs-lookup"><span data-stu-id="58248-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="58248-113">создание пакета журналов;</span><span class="sxs-lookup"><span data-stu-id="58248-113">Generate a log package</span></span>
* <span data-ttu-id="58248-114">завершение работы или перезапуск устройства.</span><span class="sxs-lookup"><span data-stu-id="58248-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="58248-115">Получение ключа шифрования данных службы hello</span><span class="sxs-lookup"><span data-stu-id="58248-115">Get hello service data encryption key</span></span>
<span data-ttu-id="58248-116">Ключ шифрования данных службы создается при регистрации первого устройства с hello в службе StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="58248-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="58248-117">Этот параметр, выберите необходимые в связи с hello службы регистрации ключа tooregister дополнительных устройств с hello в службе StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="58248-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="58248-118">Если перемещено ключ шифрования данных службы и должны tooretrieve, hello следующих действия, описанные в hello локального пользовательского веб-интерфейса hello устройства, зарегистрированные в службе.</span><span class="sxs-lookup"><span data-stu-id="58248-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="58248-119">ключ шифрования данных службы tooget hello</span><span class="sxs-lookup"><span data-stu-id="58248-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="58248-120">Подключите toohello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58248-120">Connect toohello local web UI.</span></span> <span data-ttu-id="58248-121">Go слишком**конфигурации** > **параметры облака**.</span><span class="sxs-lookup"><span data-stu-id="58248-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="58248-122">Внизу hello страницы приветствия щелкните **ключ шифрования данных службы Get**.</span><span class="sxs-lookup"><span data-stu-id="58248-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="58248-123">После этого отобразится ключ.</span><span class="sxs-lookup"><span data-stu-id="58248-123">A key will appear.</span></span> <span data-ttu-id="58248-124">Скопируйте и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="58248-124">Copy and save this key.</span></span>
   
    ![получение ключа шифрования данных службы 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="58248-126">устранение ошибок настройки пользовательского веб-интерфейса;</span><span class="sxs-lookup"><span data-stu-id="58248-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="58248-127">В некоторых случаях при настройке устройства hello через hello локального пользовательского веб-интерфейса, возможны ошибки.</span><span class="sxs-lookup"><span data-stu-id="58248-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="58248-128">toodiagnose и устранения таких ошибок, можно выполнять тесты диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="58248-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="58248-129">диагностические тесты toorun hello</span><span class="sxs-lookup"><span data-stu-id="58248-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="58248-130">В hello локального веб-интерфейса, перейдите слишком**Устранение неполадок** > **диагностические тесты**.</span><span class="sxs-lookup"><span data-stu-id="58248-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![запуск диагностики 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="58248-132">Внизу hello страницы приветствия щелкните **запустите диагностические тесты**.</span><span class="sxs-lookup"><span data-stu-id="58248-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="58248-133">Это инициирует toodiagnose тестов все возможные проблемы с сетью, устройства, веб-прокси, времени или параметры облака.</span><span class="sxs-lookup"><span data-stu-id="58248-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="58248-134">Вы получите уведомление, что это устройство hello выполняет тесты.</span><span class="sxs-lookup"><span data-stu-id="58248-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="58248-135">После завершения тестов hello, отображаются результаты hello.</span><span class="sxs-lookup"><span data-stu-id="58248-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="58248-136">Hello пример hello результаты диагностические тесты.</span><span class="sxs-lookup"><span data-stu-id="58248-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="58248-137">Обратите внимание, что параметры веб-прокси hello не были настроены на этом устройстве таким образом, прокси-сервера веб-hello тест не был выполнен.</span><span class="sxs-lookup"><span data-stu-id="58248-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="58248-138">Здравствуйте, все другие тесты для параметров сети, DNS-сервер, и параметры времени выполнены успешно.</span><span class="sxs-lookup"><span data-stu-id="58248-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![запуск диагностики 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="58248-140">создание пакета журналов;</span><span class="sxs-lookup"><span data-stu-id="58248-140">Generate a log package</span></span>
<span data-ttu-id="58248-141">Пакет журналов состоит из всех hello журналы, которые могут помочь технической поддержки Майкрософт при устранении неполадок любого устройства.</span><span class="sxs-lookup"><span data-stu-id="58248-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="58248-142">В этом выпуске пакета журналов может быть создан при помощи hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58248-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="58248-143">пакет журналов toogenerate hello</span><span class="sxs-lookup"><span data-stu-id="58248-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="58248-144">В hello локального веб-интерфейса, перейдите слишком**Устранение неполадок** > **системные журналы**.</span><span class="sxs-lookup"><span data-stu-id="58248-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![создание пакета журналов 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="58248-146">Внизу hello страницы приветствия щелкните **Создание журнала пакета**.</span><span class="sxs-lookup"><span data-stu-id="58248-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="58248-147">Создается пакет hello системные журналы.</span><span class="sxs-lookup"><span data-stu-id="58248-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="58248-148">Это займет несколько минут.</span><span class="sxs-lookup"><span data-stu-id="58248-148">This will take a couple of minutes.</span></span>
   
    ![создание пакета журналов 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="58248-150">Вы получите уведомление после успешного создания пакета hello и hello страница будет обновляться tooindicate hello время и дату создания пакета hello.</span><span class="sxs-lookup"><span data-stu-id="58248-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![создание пакета журналов 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="58248-152">Щелкните **Скачать пакет журналов**.</span><span class="sxs-lookup"><span data-stu-id="58248-152">Click **Download log package**.</span></span> <span data-ttu-id="58248-153">В систему будет скачан сжатый ZIP-пакет.</span><span class="sxs-lookup"><span data-stu-id="58248-153">A zipped package will be downloaded on your system.</span></span>
   
    ![создание пакета журналов 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="58248-155">Можно распаковать hello журнала загруженного пакета и просмотр файлов журнала системы hello.</span><span class="sxs-lookup"><span data-stu-id="58248-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="58248-156">Завершение работы и перезапуск устройства</span><span class="sxs-lookup"><span data-stu-id="58248-156">Shut down and restart your device</span></span>
<span data-ttu-id="58248-157">Можно завершить работу или перезапустить виртуальное устройство с помощью hello локального пользовательского веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58248-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="58248-158">Рекомендуется перед перезапустить, принимают hello папки или тома автономный режим на узле hello и затем hello устройства.</span><span class="sxs-lookup"><span data-stu-id="58248-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="58248-159">Это уменьшит возможность повреждения данных.</span><span class="sxs-lookup"><span data-stu-id="58248-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="58248-160">tooshut вниз виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="58248-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="58248-161">В hello локального веб-интерфейса, перейдите слишком**обслуживания** > **параметры питания**.</span><span class="sxs-lookup"><span data-stu-id="58248-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="58248-162">Внизу hello страницы приветствия щелкните **завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="58248-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![завершение работы устройства 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="58248-164">Появится предупреждение о том, что отключение hello устройства приведет к прерыванию все операции ввода-ВЫВОДА, которые были в состоянии выполнения, что приведет к простоям.</span><span class="sxs-lookup"><span data-stu-id="58248-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="58248-165">Щелкните значок галочки hello</span><span class="sxs-lookup"><span data-stu-id="58248-165">Click hello check icon</span></span> ![значок галочки](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="58248-167">.</span><span class="sxs-lookup"><span data-stu-id="58248-167">.</span></span>
   
    ![предупреждение о завершении работы устройства](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="58248-169">Вы получите уведомление, инициированные этого отключение hello.</span><span class="sxs-lookup"><span data-stu-id="58248-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![завершение работы устройства запущено](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="58248-171">Теперь устройство Hello завершит работу.</span><span class="sxs-lookup"><span data-stu-id="58248-171">hello device will now shut down.</span></span> <span data-ttu-id="58248-172">Если вы хотите toostart устройство, необходимо будет toodo, через hello диспетчера Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="58248-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="58248-173">toorestart виртуального устройства</span><span class="sxs-lookup"><span data-stu-id="58248-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="58248-174">В hello локального веб-интерфейса, перейдите слишком**обслуживания** > **параметры питания**.</span><span class="sxs-lookup"><span data-stu-id="58248-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="58248-175">Внизу hello страницы приветствия щелкните **перезапустите**.</span><span class="sxs-lookup"><span data-stu-id="58248-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![перезапуск устройства](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="58248-177">Появится предупреждение о том, что перезапускать hello устройства приведет к прерыванию любой IOs, которые были в состоянии выполнения, что приведет к простоям.</span><span class="sxs-lookup"><span data-stu-id="58248-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="58248-178">Щелкните значок галочки hello</span><span class="sxs-lookup"><span data-stu-id="58248-178">Click hello check icon</span></span> ![значок галочки](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="58248-180">.</span><span class="sxs-lookup"><span data-stu-id="58248-180">.</span></span>
   
    ![предупреждение о перезапуске](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="58248-182">Вы получите уведомление было инициировано что перезапуск hello.</span><span class="sxs-lookup"><span data-stu-id="58248-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![перезапуск инициирован](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="58248-184">Во время перезапуска hello будут потеряны toohello подключения hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58248-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="58248-185">Вы можете отслеживать перезапуска hello, обновив периодически hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="58248-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="58248-186">Кроме того можно отслеживать состояние перезагрузки устройства hello через hello диспетчера Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="58248-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58248-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58248-187">Next steps</span></span>
<span data-ttu-id="58248-188">Узнайте, каким образом слишком[используйте hello toomanage службы диспетчера StorSimple устройство](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="58248-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

