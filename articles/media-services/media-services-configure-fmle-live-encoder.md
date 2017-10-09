---
title: "aaaConfigure hello toosend кодировщика FMLE односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello toosend кодировщика Flash Media Live кодировщик (FMLE) каналы tooAMS односкоростной поток, которые включены для динамического кодирования."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="0b73c-103">Используйте hello FMLE кодировщика toosend односкоростного динамического потока</span><span class="sxs-lookup"><span data-stu-id="0b73c-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b73c-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="0b73c-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="0b73c-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="0b73c-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="0b73c-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="0b73c-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="0b73c-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="0b73c-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="0b73c-108">В этом разделе показано, как tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) toosend кодировщик (FMLE) односкоростной поток tooAMS каналы, которые включены для динамического кодирования.</span><span class="sxs-lookup"><span data-stu-id="0b73c-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="0b73c-109">Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="0b73c-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="0b73c-110">В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="0b73c-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="0b73c-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="0b73c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="0b73c-112">Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="0b73c-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="0b73c-113">Обратите внимание, что в этом руководстве мы используем кодек AAC.</span><span class="sxs-lookup"><span data-stu-id="0b73c-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="0b73c-114">Однако FMLE не поддерживает AAC по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0b73c-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="0b73c-115">Потребовалось бы toopurchase подключаемого модуля для кодирования AAC например из MainConcept: [AAC подключаемого модуля](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="0b73c-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b73c-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b73c-116">Prerequisites</span></span>
* <span data-ttu-id="0b73c-117">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0b73c-117">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="0b73c-118">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="0b73c-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="0b73c-119">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="0b73c-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="0b73c-120">Установите последнюю версию hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) средства.</span><span class="sxs-lookup"><span data-stu-id="0b73c-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="0b73c-121">Запустите средство hello и tooyour AMS учетной записи для подключения.</span><span class="sxs-lookup"><span data-stu-id="0b73c-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="0b73c-122">Советы</span><span class="sxs-lookup"><span data-stu-id="0b73c-122">Tips</span></span>
* <span data-ttu-id="0b73c-123">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="0b73c-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="0b73c-124">Хорошее проверенное правило при определении требований к пропускной способности — toodouble hello, потоковая передача битрейтов.</span><span class="sxs-lookup"><span data-stu-id="0b73c-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="0b73c-125">Хотя это не является обязательным, он будет позволяет снизить влияние hello перегрузки сети.</span><span class="sxs-lookup"><span data-stu-id="0b73c-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="0b73c-126">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="0b73c-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="0b73c-127">Создание канала</span><span class="sxs-lookup"><span data-stu-id="0b73c-127">Create a channel</span></span>
1. <span data-ttu-id="0b73c-128">В средстве AMSE hello, перейдите toohello **Live** вкладку и щелкните правой кнопкой мыши в пределах области канала hello.</span><span class="sxs-lookup"><span data-stu-id="0b73c-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="0b73c-129">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="0b73c-129">Select **Create channel…**</span></span> <span data-ttu-id="0b73c-130">меню "hello".</span><span class="sxs-lookup"><span data-stu-id="0b73c-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="0b73c-132">Укажите имя канала hello поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="0b73c-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="0b73c-133">Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="0b73c-134">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="0b73c-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="0b73c-135">Убедитесь, что hello **начала hello новый канал теперь** выбран.</span><span class="sxs-lookup"><span data-stu-id="0b73c-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="0b73c-136">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="0b73c-138">Hello канала может занять до toostart 20 минут.</span><span class="sxs-lookup"><span data-stu-id="0b73c-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="0b73c-139">Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="0b73c-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b73c-140">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="0b73c-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="0b73c-141">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="0b73c-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="0b73c-142"><a id=configure_fmle_rtmp></a>Настройка кодировщика FMLE hello</span><span class="sxs-lookup"><span data-stu-id="0b73c-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="0b73c-143">В этот учебник hello используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="0b73c-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="0b73c-144">Hello оставшейся части этого раздела описываются шаги настройки более подробно.</span><span class="sxs-lookup"><span data-stu-id="0b73c-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="0b73c-145">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="0b73c-145">**Video**:</span></span>

* <span data-ttu-id="0b73c-146">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="0b73c-146">Codec: H.264</span></span>
* <span data-ttu-id="0b73c-147">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="0b73c-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="0b73c-148">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="0b73c-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="0b73c-149">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="0b73c-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="0b73c-150">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="0b73c-150">Frame Rate: 30</span></span>

<span data-ttu-id="0b73c-151">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="0b73c-151">**Audio**:</span></span>

* <span data-ttu-id="0b73c-152">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="0b73c-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="0b73c-153">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="0b73c-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="0b73c-154">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="0b73c-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="0b73c-155">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="0b73c-155">Configuration steps</span></span>
1. <span data-ttu-id="0b73c-156">Перейдите toohello, Flash Media Live кодировщика (FMLE) интерфейс на используемом компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="0b73c-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="0b73c-157">интерфейс Hello — одну главную страницу параметров.</span><span class="sxs-lookup"><span data-stu-id="0b73c-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="0b73c-158">Проверьте запишите hello следующие рекомендуемые параметры tooget работы с потоковой передачи с помощью FMLE.</span><span class="sxs-lookup"><span data-stu-id="0b73c-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="0b73c-159">Формат: H.264 Частота кадров: 30.00</span><span class="sxs-lookup"><span data-stu-id="0b73c-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="0b73c-160">Размер входного потока: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="0b73c-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="0b73c-161">Скорость: 5000 кбит/сек (это значение можно изменить в зависимости от ограничений сети)</span><span class="sxs-lookup"><span data-stu-id="0b73c-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="0b73c-163">При использование чередующихся источников, пожалуйста, флажок hello параметр «Устранить чересстрочную развертку»</span><span class="sxs-lookup"><span data-stu-id="0b73c-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="0b73c-164">Выберите hello гаечного ключа значок Далее tooFormat, эти дополнительные параметры должны быть:</span><span class="sxs-lookup"><span data-stu-id="0b73c-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="0b73c-165">Профиль: основной</span><span class="sxs-lookup"><span data-stu-id="0b73c-165">Profile: Main</span></span>
   * <span data-ttu-id="0b73c-166">Уровень: 4.0</span><span class="sxs-lookup"><span data-stu-id="0b73c-166">Level: 4.0</span></span>
   * <span data-ttu-id="0b73c-167">Частота опорного кадра: 2 секунды</span><span class="sxs-lookup"><span data-stu-id="0b73c-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="0b73c-169">Задайте следующие важные параметр hello.</span><span class="sxs-lookup"><span data-stu-id="0b73c-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="0b73c-170">Формат: AAC</span><span class="sxs-lookup"><span data-stu-id="0b73c-170">Format: AAC</span></span>
   * <span data-ttu-id="0b73c-171">Частота выборки: 44100 Гц</span><span class="sxs-lookup"><span data-stu-id="0b73c-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="0b73c-172">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="0b73c-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="0b73c-174">Получение входной URL-адрес канала hello в порядке tooassign его toohello FMLE **конечной точки RTMP**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="0b73c-175">Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello.</span><span class="sxs-lookup"><span data-stu-id="0b73c-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="0b73c-176">После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0b73c-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="0b73c-177">При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="0b73c-179">Вставить данные в hello **URL-адрес FMS** поле из раздела вывода hello и назначьте имя потока.</span><span class="sxs-lookup"><span data-stu-id="0b73c-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="0b73c-181">Для дополнительных избыточности повторите эти действия в hello URL-адрес дополнительного ввода.</span><span class="sxs-lookup"><span data-stu-id="0b73c-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="0b73c-182">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b73c-183">Прежде чем нажимать кнопку **Connect**, вы **должен** гарантировать готовность канала hello.</span><span class="sxs-lookup"><span data-stu-id="0b73c-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="0b73c-184">Кроме того, убедитесь, что веб-канала не tooleave hello канала в состоянии готовности без ввода вклад более > 15 минут.</span><span class="sxs-lookup"><span data-stu-id="0b73c-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="0b73c-185">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="0b73c-185">Test playback</span></span>

<span data-ttu-id="0b73c-186">Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы.</span><span class="sxs-lookup"><span data-stu-id="0b73c-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="0b73c-187">Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="0b73c-188">Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="0b73c-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="0b73c-189">При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены.</span><span class="sxs-lookup"><span data-stu-id="0b73c-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="0b73c-190">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="0b73c-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="0b73c-191">Создание программы</span><span class="sxs-lookup"><span data-stu-id="0b73c-191">Create a program</span></span>
1. <span data-ttu-id="0b73c-192">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="0b73c-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="0b73c-193">В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="0b73c-195">Имя программы hello и, при необходимости, исправьте hello **размер окна архива** (часы too4 какие значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="0b73c-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="0b73c-196">Также можно указать место хранения или оставьте значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0b73c-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="0b73c-197">Проверьте hello **теперь hello запуска программы** поле.</span><span class="sxs-lookup"><span data-stu-id="0b73c-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="0b73c-198">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="0b73c-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="0b73c-199">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="0b73c-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="0b73c-200">После запуска программы hello, подтвердите воспроизведения, щелкнув правой кнопкой мыши hello программы, а затем перейдя слишком**программах hello воспроизведения** и выбрав **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="0b73c-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="0b73c-201">После подтверждения, щелкните правой кнопкой мыши hello программы снова и выберите **скопируйте hello выходной URL-адрес tooClipboard** (или извлечь эту информацию из hello **программы сведения и параметры** параметр меню "hello").</span><span class="sxs-lookup"><span data-stu-id="0b73c-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="0b73c-202">поток Hello теперь является готов toobe, внедренных в проигрывателе или распределенных tooan аудитория live Просмотр.</span><span class="sxs-lookup"><span data-stu-id="0b73c-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="0b73c-203">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0b73c-203">Troubleshooting</span></span>
<span data-ttu-id="0b73c-204">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="0b73c-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0b73c-205">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0b73c-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0b73c-206">Отзывы</span><span class="sxs-lookup"><span data-stu-id="0b73c-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
