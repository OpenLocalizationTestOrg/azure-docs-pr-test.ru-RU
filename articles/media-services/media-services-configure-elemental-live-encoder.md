---
title: "aaaConfigure hello toosend кодировщика Live элементарных односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello toosend кодировщика Live элементарных каналы tooAMS односкоростной поток, которые включены для динамического кодирования."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="bd84b-103">Использовать toosend кодировщика Live элементарных hello односкоростного динамического потока</span><span class="sxs-lookup"><span data-stu-id="bd84b-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd84b-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="bd84b-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="bd84b-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="bd84b-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="bd84b-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="bd84b-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="bd84b-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="bd84b-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="bd84b-108">В этом разделе показано, как tooconfigure hello [элементарных Live](http://www.elementaltechnologies.com/products/elemental-live) toosend кодировщика односкоростной поток tooAMS каналы, которые включены для динамического кодирования.</span><span class="sxs-lookup"><span data-stu-id="bd84b-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="bd84b-109">Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="bd84b-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="bd84b-110">В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="bd84b-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="bd84b-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="bd84b-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="bd84b-112">Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="bd84b-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd84b-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bd84b-113">Prerequisites</span></span>
* <span data-ttu-id="bd84b-114">Необходимо иметь опыт работы с помощью элементарных Live веб-интерфейс toocreate динамической события.</span><span class="sxs-lookup"><span data-stu-id="bd84b-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* <span data-ttu-id="bd84b-115">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bd84b-115">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="bd84b-116">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="bd84b-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="bd84b-117">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="bd84b-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="bd84b-118">Установите последнюю версию hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) средства.</span><span class="sxs-lookup"><span data-stu-id="bd84b-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="bd84b-119">Запустите средство hello и tooyour AMS учетной записи для подключения.</span><span class="sxs-lookup"><span data-stu-id="bd84b-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="bd84b-120">Советы</span><span class="sxs-lookup"><span data-stu-id="bd84b-120">Tips</span></span>
* <span data-ttu-id="bd84b-121">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="bd84b-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="bd84b-122">Хорошее проверенное правило при определении требований к пропускной способности — toodouble hello, потоковая передача битрейтов.</span><span class="sxs-lookup"><span data-stu-id="bd84b-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="bd84b-123">Хотя это не является обязательным, он будет позволяет снизить влияние hello перегрузки сети.</span><span class="sxs-lookup"><span data-stu-id="bd84b-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="bd84b-124">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="bd84b-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="bd84b-125">Использование Elemental Live с протоколом RTP</span><span class="sxs-lookup"><span data-stu-id="bd84b-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="bd84b-126">В этом разделе показано, как tooconfigure hello элементарных Live кодировщик, который отправляет односкоростной динамический поток через RTP.</span><span class="sxs-lookup"><span data-stu-id="bd84b-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="bd84b-127">Дополнительные сведения см. в подразделе, посвященному [передаче потока MPEG-TS по протоколу RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="bd84b-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="bd84b-128">Создание канала</span><span class="sxs-lookup"><span data-stu-id="bd84b-128">Create a channel</span></span>

1. <span data-ttu-id="bd84b-129">В средстве AMSE hello, перейдите toohello **Live** вкладку и щелкните правой кнопкой мыши в пределах области канала hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="bd84b-130">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="bd84b-130">Select **Create channel…**</span></span> <span data-ttu-id="bd84b-131">меню "hello".</span><span class="sxs-lookup"><span data-stu-id="bd84b-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="bd84b-133">Укажите имя канала hello поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="bd84b-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="bd84b-134">Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="bd84b-135">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="bd84b-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="bd84b-136">Убедитесь, что hello **начала hello новый канал теперь** выбран.</span><span class="sxs-lookup"><span data-stu-id="bd84b-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="bd84b-137">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="bd84b-139">Hello канала может занять до toostart 20 минут.</span><span class="sxs-lookup"><span data-stu-id="bd84b-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="bd84b-140">Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="bd84b-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd84b-141">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="bd84b-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="bd84b-142">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="bd84b-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="bd84b-143"><a id=configure_elemental_rtp></a>Настройка hello элементарных динамического кодировщика</span><span class="sxs-lookup"><span data-stu-id="bd84b-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="bd84b-144">В этот учебник hello используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="bd84b-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="bd84b-145">Hello оставшейся части этого раздела описываются шаги настройки более подробно.</span><span class="sxs-lookup"><span data-stu-id="bd84b-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="bd84b-146">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="bd84b-146">**Video**:</span></span>

* <span data-ttu-id="bd84b-147">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="bd84b-147">Codec: H.264</span></span>
* <span data-ttu-id="bd84b-148">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="bd84b-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="bd84b-149">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="bd84b-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="bd84b-150">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="bd84b-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="bd84b-151">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="bd84b-151">Frame Rate: 30</span></span>

<span data-ttu-id="bd84b-152">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="bd84b-152">**Audio**:</span></span>

* <span data-ttu-id="bd84b-153">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="bd84b-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="bd84b-154">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="bd84b-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="bd84b-155">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="bd84b-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="bd84b-156">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="bd84b-156">Configuration steps</span></span>
1. <span data-ttu-id="bd84b-157">Перейдите toohello **элементарных Live** веб-интерфейса и настройка hello кодировщика для **UDP/служб Терминалов** потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="bd84b-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="bd84b-158">После создания нового события прокрутите toohello выходные группы и добавить hello **UDP/служб Терминалов** выходной группы.</span><span class="sxs-lookup"><span data-stu-id="bd84b-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="bd84b-159">Создайте выходные данные, щелкнув **New Stream** (Новый поток), а затем **Add Output** (Добавить выходные данные).</span><span class="sxs-lookup"><span data-stu-id="bd84b-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="bd84b-161">Рекомендуется элементарных события hello имеет слишком задать код времени hello повторного подключения кодировщика hello toohelp «Системные часы» в случае сбоя потока hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="bd84b-162">Hello выходных данных будет создан, щелкните кнопку **добавить поток**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="bd84b-163">Теперь можно настроить параметры вывода Hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="bd84b-164">Прокрутите вниз toohello «Stream 1», созданную ранее, щелкните hello **видео** слева hello и разверните hello **Дополнительно** разделе "Параметры".</span><span class="sxs-lookup"><span data-stu-id="bd84b-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="bd84b-166">Хотя элементарных Live имеет широкий спектр доступных Настройка, hello рекомендуются следующие настройки для начала работы с потоковой передачи tooAMS.</span><span class="sxs-lookup"><span data-stu-id="bd84b-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="bd84b-167">Разрешение: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="bd84b-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="bd84b-168">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="bd84b-168">Framerate: 30</span></span>
   * <span data-ttu-id="bd84b-169">Размер GOP: 60 кадров</span><span class="sxs-lookup"><span data-stu-id="bd84b-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="bd84b-170">Режим развертки: прогрессивная</span><span class="sxs-lookup"><span data-stu-id="bd84b-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="bd84b-171">Скорость: 5000000 бит/сек (это значение можно изменить в зависимости от ограничений сети)</span><span class="sxs-lookup"><span data-stu-id="bd84b-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="bd84b-173">Получение входной URL-адрес канала hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="bd84b-174">Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="bd84b-175">После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bd84b-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="bd84b-176">При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="bd84b-178">Вставить данные в hello **основной целевой** поле hello кодировщики Elemental.</span><span class="sxs-lookup"><span data-stu-id="bd84b-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="bd84b-179">Другие параметры могут оставаться по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="bd84b-181">Для дополнительных избыточности повторите эти действия в hello URL-адрес получателя входные данные путем создания отдельной вкладке «Выход» для потоковой передачи UDP/служб Терминалов.</span><span class="sxs-lookup"><span data-stu-id="bd84b-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="bd84b-182">Нажмите кнопку **создать** (если он был создан новое событие) или **обновление** (если изменяете существующие события) и затем продолжить toostart hello кодировщика.</span><span class="sxs-lookup"><span data-stu-id="bd84b-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd84b-183">Прежде чем нажимать кнопку **запустить** на hello элементарных Live веб-интерфейса вы **должен** гарантировать готовность канала hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="bd84b-184">Кроме того, убедитесь, что не tooleave hello канала в состоянии готовности без событие более > 15 минут.</span><span class="sxs-lookup"><span data-stu-id="bd84b-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="bd84b-185">После выполнения потока hello в течение 30 секунд, перейдите назад toohello AMSE средство и тестирования воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="bd84b-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="bd84b-186">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="bd84b-186">Test playback</span></span>

<span data-ttu-id="bd84b-187">Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы.</span><span class="sxs-lookup"><span data-stu-id="bd84b-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="bd84b-188">Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="bd84b-189">Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="bd84b-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="bd84b-190">При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены.</span><span class="sxs-lookup"><span data-stu-id="bd84b-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="bd84b-191">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="bd84b-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="bd84b-192">Создание программы</span><span class="sxs-lookup"><span data-stu-id="bd84b-192">Create a program</span></span>
1. <span data-ttu-id="bd84b-193">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="bd84b-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="bd84b-194">В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="bd84b-196">Имя программы hello и, при необходимости, исправьте hello **размер окна архива** (часы too4 какие значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="bd84b-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="bd84b-197">Также можно указать место хранения или оставьте значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="bd84b-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="bd84b-198">Проверьте hello **теперь hello запуска программы** поле.</span><span class="sxs-lookup"><span data-stu-id="bd84b-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="bd84b-199">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="bd84b-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="bd84b-200">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="bd84b-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="bd84b-201">После запуска программы hello, подтвердите воспроизведения, щелкнув правой кнопкой мыши hello программы, а затем перейдя слишком**программах hello воспроизведения** и выбрав **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="bd84b-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="bd84b-202">После подтверждения, щелкните правой кнопкой мыши hello программы снова и выберите **скопируйте hello выходной URL-адрес tooClipboard** (или извлечь эту информацию из hello **программы сведения и параметры** параметр меню "hello").</span><span class="sxs-lookup"><span data-stu-id="bd84b-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="bd84b-203">поток Hello теперь является готов toobe, внедренных в проигрывателе или распределенных tooan аудитория live Просмотр.</span><span class="sxs-lookup"><span data-stu-id="bd84b-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="bd84b-204">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="bd84b-204">Troubleshooting</span></span>
<span data-ttu-id="bd84b-205">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="bd84b-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="bd84b-206">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="bd84b-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bd84b-207">Отзывы</span><span class="sxs-lookup"><span data-stu-id="bd84b-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
