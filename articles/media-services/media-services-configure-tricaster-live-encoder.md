---
title: "aaaConfigure hello кодировщика toosend NewTek TriCaster односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello Tricaster live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="320c2-103">Использовать hello кодировщика NewTek TriCaster toosend односкоростного динамического потока</span><span class="sxs-lookup"><span data-stu-id="320c2-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="320c2-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="320c2-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="320c2-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="320c2-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="320c2-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="320c2-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="320c2-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="320c2-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="320c2-108">В этом разделе показано, как tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования.</span><span class="sxs-lookup"><span data-stu-id="320c2-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="320c2-109">Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="320c2-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="320c2-110">В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE).</span><span class="sxs-lookup"><span data-stu-id="320c2-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="320c2-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="320c2-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="320c2-112">Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="320c2-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="320c2-113">При использовании Tricaster для отправки в публикацию веб-канала tooAMS каналы, которые включены для динамического кодирования, может существовать сбоев аудио/видео в передачи интерактивного события при использовании некоторых возможностей Tricaster, такие как быстрая вырезания между потоками или переключения от портативные ПК .</span><span class="sxs-lookup"><span data-stu-id="320c2-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="320c2-114">работа команды Hello AMS о решении этих проблем, до тех пор, рекомендуется не toouse эти функции.</span><span class="sxs-lookup"><span data-stu-id="320c2-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="320c2-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="320c2-115">Prerequisites</span></span>
* <span data-ttu-id="320c2-116">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="320c2-116">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="320c2-117">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="320c2-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="320c2-118">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="320c2-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="320c2-119">Установите последнюю версию hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) средства.</span><span class="sxs-lookup"><span data-stu-id="320c2-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="320c2-120">Запустите средство hello и tooyour AMS учетной записи для подключения.</span><span class="sxs-lookup"><span data-stu-id="320c2-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="320c2-121">Советы</span><span class="sxs-lookup"><span data-stu-id="320c2-121">Tips</span></span>
* <span data-ttu-id="320c2-122">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="320c2-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="320c2-123">Хорошее проверенное правило при определении требований к пропускной способности — toodouble hello, потоковая передача битрейтов.</span><span class="sxs-lookup"><span data-stu-id="320c2-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="320c2-124">Хотя это не является обязательным, он будет позволяет снизить влияние hello перегрузки сети.</span><span class="sxs-lookup"><span data-stu-id="320c2-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="320c2-125">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="320c2-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="320c2-126">Создание канала</span><span class="sxs-lookup"><span data-stu-id="320c2-126">Create a channel</span></span>
1. <span data-ttu-id="320c2-127">В средстве AMSE hello, перейдите toohello **Live** вкладку и щелкните правой кнопкой мыши в пределах области канала hello.</span><span class="sxs-lookup"><span data-stu-id="320c2-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="320c2-128">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="320c2-128">Select **Create channel…**</span></span> <span data-ttu-id="320c2-129">меню "hello".</span><span class="sxs-lookup"><span data-stu-id="320c2-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="320c2-131">Укажите имя канала hello поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="320c2-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="320c2-132">Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="320c2-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="320c2-133">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="320c2-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="320c2-134">Убедитесь, что hello **начала hello новый канал теперь** выбран.</span><span class="sxs-lookup"><span data-stu-id="320c2-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="320c2-135">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="320c2-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="320c2-137">Hello канала может занять до toostart 20 минут.</span><span class="sxs-lookup"><span data-stu-id="320c2-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="320c2-138">Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="320c2-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="320c2-139">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="320c2-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="320c2-140">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="320c2-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="320c2-141"><a id=configure_tricaster_rtmp></a>Настройка hello NewTek TriCaster кодировщика</span><span class="sxs-lookup"><span data-stu-id="320c2-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="320c2-142">В этот учебник hello используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="320c2-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="320c2-143">Hello оставшейся части этого раздела описываются шаги настройки более подробно.</span><span class="sxs-lookup"><span data-stu-id="320c2-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="320c2-144">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="320c2-144">**Video**:</span></span>

* <span data-ttu-id="320c2-145">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="320c2-145">Codec: H.264</span></span>
* <span data-ttu-id="320c2-146">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="320c2-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="320c2-147">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="320c2-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="320c2-148">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="320c2-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="320c2-149">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="320c2-149">Frame Rate: 30</span></span>

<span data-ttu-id="320c2-150">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="320c2-150">**Audio**:</span></span>

* <span data-ttu-id="320c2-151">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="320c2-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="320c2-152">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="320c2-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="320c2-153">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="320c2-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="320c2-154">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="320c2-154">Configuration steps</span></span>
1. <span data-ttu-id="320c2-155">Создайте новый проект **NewTek TriCaster** в зависимости от того, какой входной источник видео используется.</span><span class="sxs-lookup"><span data-stu-id="320c2-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="320c2-156">Один раз в рамках проекта, найти hello **поток** кнопки и меню hello шестеренки значок Далее tooit tooaccess hello потока конфигурации.</span><span class="sxs-lookup"><span data-stu-id="320c2-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="320c2-158">Когда открытых hello меню, щелкните **New** под заголовком hello соединения.</span><span class="sxs-lookup"><span data-stu-id="320c2-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="320c2-159">При появлении запроса для типа соединения hello выберите **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="320c2-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="320c2-161">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="320c2-161">Click **OK**.</span></span>
5. <span data-ttu-id="320c2-162">Профиль FMLE теперь может быть импортирован, щелкнув hello стрелку раскрывающегося списка под **профиль Streaming** и переход слишком**Обзор**.</span><span class="sxs-lookup"><span data-stu-id="320c2-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="320c2-164">Перейдите toowhere hello настроен FMLE профиль был сохранен.</span><span class="sxs-lookup"><span data-stu-id="320c2-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="320c2-165">Выберите его и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="320c2-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="320c2-166">После загрузки профиля hello продолжить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="320c2-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="320c2-167">Получение входной URL-адрес канала hello в порядке tooassign его toohello Tricaster **конечной точки RTMP**.</span><span class="sxs-lookup"><span data-stu-id="320c2-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="320c2-168">Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello.</span><span class="sxs-lookup"><span data-stu-id="320c2-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="320c2-169">После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="320c2-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="320c2-170">При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.</span><span class="sxs-lookup"><span data-stu-id="320c2-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="320c2-172">Вставить данные в hello **расположение** под **Flash Server** в рамках проекта Tricaster hello.</span><span class="sxs-lookup"><span data-stu-id="320c2-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="320c2-173">Также назначить имя потока в hello **идентификатор потока** поля.</span><span class="sxs-lookup"><span data-stu-id="320c2-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="320c2-174">Если профиль FMLE toohello был добавлен поток информации, его можно также импортировать toothis статьи, щелкнув **Импорт параметров**, навигация по toohello сохранить FMLE профиль и щелкнув **ОК**.</span><span class="sxs-lookup"><span data-stu-id="320c2-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="320c2-175">Hello соответствующие поля Flash Server необходимо заполнить данными hello из FMLE.</span><span class="sxs-lookup"><span data-stu-id="320c2-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="320c2-177">По завершении нажмите кнопку **ОК** hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="320c2-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="320c2-178">По мере готовности видео- и аудиопотоки входными данными для hello Tricaster начать потоковую передачу tooAMS, щелкнув hello **поток** кнопки.</span><span class="sxs-lookup"><span data-stu-id="320c2-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="320c2-180">Прежде чем нажимать кнопку **поток**, вы **должен** гарантировать готовность канала hello.</span><span class="sxs-lookup"><span data-stu-id="320c2-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="320c2-181">Кроме того, убедитесь, что веб-канала не tooleave hello канала в состоянии готовности без ввода вклад более > 15 минут.</span><span class="sxs-lookup"><span data-stu-id="320c2-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="320c2-182">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="320c2-182">Test playback</span></span>
<span data-ttu-id="320c2-183">Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы.</span><span class="sxs-lookup"><span data-stu-id="320c2-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="320c2-184">Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="320c2-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="320c2-185">Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.</span><span class="sxs-lookup"><span data-stu-id="320c2-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="320c2-186">При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены.</span><span class="sxs-lookup"><span data-stu-id="320c2-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="320c2-187">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="320c2-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="320c2-188">Создание программы</span><span class="sxs-lookup"><span data-stu-id="320c2-188">Create a program</span></span>
1. <span data-ttu-id="320c2-189">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="320c2-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="320c2-190">В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.</span><span class="sxs-lookup"><span data-stu-id="320c2-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="320c2-192">Имя программы hello и, при необходимости, исправьте hello **размер окна архива** (часы too4 какие значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="320c2-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="320c2-193">Также можно указать место хранения или оставьте значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="320c2-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="320c2-194">Проверьте hello **теперь hello запуска программы** поле.</span><span class="sxs-lookup"><span data-stu-id="320c2-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="320c2-195">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="320c2-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="320c2-196">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="320c2-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="320c2-197">После запуска программы hello, подтвердите воспроизведения, щелкнув правой кнопкой мыши hello программы, а затем перейдя слишком**программах hello воспроизведения** и выбрав **с помощью Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="320c2-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="320c2-198">После подтверждения, щелкните правой кнопкой мыши hello программы снова и выберите **скопируйте hello выходной URL-адрес tooClipboard** (или извлечь эту информацию из hello **программы сведения и параметры** параметр меню "hello").</span><span class="sxs-lookup"><span data-stu-id="320c2-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="320c2-199">поток Hello теперь является готов toobe, внедренных в проигрывателе или распределенных tooan аудитория live Просмотр.</span><span class="sxs-lookup"><span data-stu-id="320c2-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="320c2-200">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="320c2-200">Troubleshooting</span></span>
<span data-ttu-id="320c2-201">См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.</span><span class="sxs-lookup"><span data-stu-id="320c2-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="320c2-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="320c2-202">Next step</span></span>
<span data-ttu-id="320c2-203">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="320c2-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="320c2-204">Отзывы</span><span class="sxs-lookup"><span data-stu-id="320c2-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
