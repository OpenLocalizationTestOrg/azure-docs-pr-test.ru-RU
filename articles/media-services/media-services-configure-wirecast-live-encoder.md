---
title: "aaaConfigure hello toosend кодировщик Telestream Wirecast односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello Wirecast live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="43703-103">Используйте hello Wirecast encoder toosend односкоростного динамического потока</span><span class="sxs-lookup"><span data-stu-id="43703-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="43703-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="43703-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="43703-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="43703-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="43703-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="43703-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="43703-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="43703-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="43703-108">В этом разделе показано, как tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования.</span><span class="sxs-lookup"><span data-stu-id="43703-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="43703-109">Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="43703-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="43703-110">В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="43703-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="43703-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="43703-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="43703-112">Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="43703-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43703-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="43703-113">Prerequisites</span></span>
* <span data-ttu-id="43703-114">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="43703-114">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="43703-115">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="43703-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="43703-116">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="43703-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="43703-117">Установите последнюю версию hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) средства.</span><span class="sxs-lookup"><span data-stu-id="43703-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="43703-118">Запустите средство hello и tooyour AMS учетной записи для подключения.</span><span class="sxs-lookup"><span data-stu-id="43703-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="43703-119">Советы</span><span class="sxs-lookup"><span data-stu-id="43703-119">Tips</span></span>
* <span data-ttu-id="43703-120">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="43703-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="43703-121">Хорошее проверенное правило при определении требований к пропускной способности — toodouble hello, потоковая передача битрейтов.</span><span class="sxs-lookup"><span data-stu-id="43703-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="43703-122">Хотя это не является обязательным, он будет позволяет снизить влияние hello перегрузки сети.</span><span class="sxs-lookup"><span data-stu-id="43703-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="43703-123">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="43703-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="43703-124">Создание канала</span><span class="sxs-lookup"><span data-stu-id="43703-124">Create a channel</span></span>
1. <span data-ttu-id="43703-125">В средстве AMSE hello, перейдите toohello **Live** вкладку и щелкните правой кнопкой мыши в пределах области канала hello.</span><span class="sxs-lookup"><span data-stu-id="43703-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="43703-126">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="43703-126">Select **Create channel…**</span></span> <span data-ttu-id="43703-127">меню "hello".</span><span class="sxs-lookup"><span data-stu-id="43703-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="43703-129">Укажите имя канала hello поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="43703-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="43703-130">Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="43703-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="43703-131">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="43703-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="43703-132">Убедитесь, что hello **начала hello новый канал теперь** выбран.</span><span class="sxs-lookup"><span data-stu-id="43703-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="43703-133">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="43703-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="43703-135">Hello канала может занять до toostart 20 минут.</span><span class="sxs-lookup"><span data-stu-id="43703-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="43703-136">Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="43703-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43703-137">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="43703-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="43703-138">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="43703-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="43703-139"><a id=configure_wirecast_rtmp></a>Настройка hello кодировщик Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="43703-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="43703-140">В этот учебник hello используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="43703-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="43703-141">Hello оставшейся части этого раздела описываются шаги настройки более подробно.</span><span class="sxs-lookup"><span data-stu-id="43703-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="43703-142">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="43703-142">**Video**:</span></span>

* <span data-ttu-id="43703-143">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="43703-143">Codec: H.264</span></span>
* <span data-ttu-id="43703-144">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="43703-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="43703-145">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="43703-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="43703-146">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="43703-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="43703-147">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="43703-147">Frame Rate: 30</span></span>

<span data-ttu-id="43703-148">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="43703-148">**Audio**:</span></span>

* <span data-ttu-id="43703-149">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="43703-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="43703-150">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="43703-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="43703-151">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="43703-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="43703-152">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="43703-152">Configuration steps</span></span>
1. <span data-ttu-id="43703-153">Откройте приложение hello Telestream Wirecast на компьютер hello не используется и для потоковой передачи RTMP.</span><span class="sxs-lookup"><span data-stu-id="43703-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="43703-154">Настройка вывода hello, перейдя по toohello **вывода** и выбрать **параметры вывода...** .</span><span class="sxs-lookup"><span data-stu-id="43703-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="43703-155">Убедитесь, что hello **места назначения вывода** задано слишком**RTMP-сервер**.</span><span class="sxs-lookup"><span data-stu-id="43703-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="43703-156">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43703-156">Click **OK**.</span></span>
4. <span data-ttu-id="43703-157">На странице "Параметры" hello задайте hello **назначения** toobe поле **служб мультимедиа Azure**.</span><span class="sxs-lookup"><span data-stu-id="43703-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="43703-158">Hello кодировка профиль автоматически выбирается слишком**Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="43703-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="43703-159">toocustomize эти параметры, выберите hello toohello значок шестеренки справа от приветствия раскрывающийся список, а затем выберите **новый набор параметров**.</span><span class="sxs-lookup"><span data-stu-id="43703-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="43703-161">Настройка предустановок кодировщика.</span><span class="sxs-lookup"><span data-stu-id="43703-161">Configure encoder presets.</span></span>

    <span data-ttu-id="43703-162">Hello имя конфигурации и для проверки наличия hello следующие рекомендуемые параметры:</span><span class="sxs-lookup"><span data-stu-id="43703-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="43703-163">**Видео**</span><span class="sxs-lookup"><span data-stu-id="43703-163">**Video**</span></span>

   * <span data-ttu-id="43703-164">Кодировщик: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="43703-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="43703-165">Кадров в секунду: 30</span><span class="sxs-lookup"><span data-stu-id="43703-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="43703-166">Средняя скорость: 5000 кбит/сек (это значение можно изменить в зависимости от ограничений сети)</span><span class="sxs-lookup"><span data-stu-id="43703-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="43703-167">Профиль: основной</span><span class="sxs-lookup"><span data-stu-id="43703-167">Profile: Main</span></span>
   * <span data-ttu-id="43703-168">Ключевой кадр: каждые 60 кадров</span><span class="sxs-lookup"><span data-stu-id="43703-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="43703-169">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="43703-169">**Audio**</span></span>

   * <span data-ttu-id="43703-170">Конечная скорость: 192 Кбит/сек</span><span class="sxs-lookup"><span data-stu-id="43703-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="43703-171">Частота выборки: 44,100 кГц</span><span class="sxs-lookup"><span data-stu-id="43703-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="43703-173">Нажмите кнопку **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="43703-173">Press **Save**.</span></span>

    <span data-ttu-id="43703-174">поле Encoding Hello теперь имеет hello только что созданный профиль, доступные для выбора.</span><span class="sxs-lookup"><span data-stu-id="43703-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="43703-175">Убедитесь, что выбран новый профиль hello.</span><span class="sxs-lookup"><span data-stu-id="43703-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="43703-176">Получение входной URL-адрес канала hello в порядке tooassign его toohello Wirecast **конечной точки RTMP**.</span><span class="sxs-lookup"><span data-stu-id="43703-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="43703-177">Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello.</span><span class="sxs-lookup"><span data-stu-id="43703-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="43703-178">После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="43703-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="43703-179">При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="43703-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="43703-181">В hello Wirecast **параметры вывода** окна, вставьте эти сведения в hello **адрес** поле из раздела вывода hello и назначьте имя потока.</span><span class="sxs-lookup"><span data-stu-id="43703-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="43703-183">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="43703-183">Select **OK**.</span></span>
2. <span data-ttu-id="43703-184">На главном hello **Wirecast** Подтвердите источников входных данных для видео и аудио готовы и нажмите клавишу **поток** в верхний левый угол hello.</span><span class="sxs-lookup"><span data-stu-id="43703-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="43703-186">Прежде чем нажимать кнопку **поток**, вы **должен** гарантировать готовность канала hello.</span><span class="sxs-lookup"><span data-stu-id="43703-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="43703-187">Кроме того, убедитесь, что веб-канала не tooleave hello канала в состоянии готовности без ввода вклад более > 15 минут.</span><span class="sxs-lookup"><span data-stu-id="43703-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="43703-188">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="43703-188">Test playback</span></span>

<span data-ttu-id="43703-189">Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы.</span><span class="sxs-lookup"><span data-stu-id="43703-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="43703-190">Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="43703-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="43703-191">Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="43703-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="43703-192">При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены.</span><span class="sxs-lookup"><span data-stu-id="43703-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="43703-193">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="43703-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="43703-194">Создание программы</span><span class="sxs-lookup"><span data-stu-id="43703-194">Create a program</span></span>
1. <span data-ttu-id="43703-195">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="43703-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="43703-196">В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.</span><span class="sxs-lookup"><span data-stu-id="43703-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="43703-198">Имя программы hello и, при необходимости, исправьте hello **размер окна архива** (часы too4 какие значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="43703-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="43703-199">Также можно указать место хранения или оставьте значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="43703-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="43703-200">Проверьте hello **теперь hello запуска программы** поле.</span><span class="sxs-lookup"><span data-stu-id="43703-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="43703-201">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="43703-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="43703-202">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="43703-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="43703-203">После запуска программы hello, подтвердите воспроизведения, щелкнув правой кнопкой мыши hello программы, а затем перейдя слишком**программах hello воспроизведения** и выбрав **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="43703-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="43703-204">После подтверждения, щелкните правой кнопкой мыши hello программы снова и выберите **скопируйте hello выходной URL-адрес tooClipboard** (или извлечь эту информацию из hello **программы сведения и параметры** параметр меню "hello").</span><span class="sxs-lookup"><span data-stu-id="43703-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="43703-205">поток Hello теперь является готов toobe, внедренных в проигрывателе или распределенных tooan аудитория live Просмотр.</span><span class="sxs-lookup"><span data-stu-id="43703-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="43703-206">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="43703-206">Troubleshooting</span></span>
<span data-ttu-id="43703-207">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="43703-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="43703-208">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="43703-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="43703-209">Отзывы</span><span class="sxs-lookup"><span data-stu-id="43703-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
