---
title: "Настройка кодировщика NewTek TriCaster для отправки односкоростного обновляющегося потока | Документация Майкрософт"
description: "В этой статье показано, как настроить кодировщик Tricaster для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени."
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
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="bbcd0-103">Использование кодировщика NewTek TriCaster для отправки односкоростного обновляющегося потока</span><span class="sxs-lookup"><span data-stu-id="bbcd0-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bbcd0-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="bbcd0-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="bbcd0-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="bbcd0-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="bbcd0-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="bbcd0-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="bbcd0-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="bbcd0-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="bbcd0-108">В этой статье показано, как настроить динамический кодировщик [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="bbcd0-109">Дополнительные сведения можно найти в разделе [Работа с каналами, выполняющими кодирование в реальном времени с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="bbcd0-110">В этом учебнике показано, как управлять службами мультимедиа Azure (AMS) с помощью Обозревателя служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="bbcd0-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="bbcd0-112">Если вы используете Mac или Linux, воспользуйтесь классическим порталом Azure для создания [каналов](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программ](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bbcd0-113">При использовании Tricaster для отправки веб-канала доставки в каналы AMS с поддержкой кодирования в реальном времени возможны временные сбои видео или звука интерактивного события, если используются некоторые возможности Tricaster, например быстрый монтаж разных веб-каналов или переключение на баннеры и обратно.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="bbcd0-114">Команда AMS работает над устранением этих проблем. На данный момент не рекомендуется использовать эти возможности.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="bbcd0-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bbcd0-115">Prerequisites</span></span>
* <span data-ttu-id="bbcd0-116">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-116">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="bbcd0-117">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="bbcd0-118">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="bbcd0-119">Установите последнюю версию средства [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="bbcd0-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="bbcd0-120">Запустите его и подключитесь к учетной записи AMS.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="bbcd0-121">Советы</span><span class="sxs-lookup"><span data-stu-id="bbcd0-121">Tips</span></span>
* <span data-ttu-id="bbcd0-122">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="bbcd0-123">Для получения необходимой пропускной способности рекомендуется удвоить скорость потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="bbcd0-124">Хотя это требование не является обязательным, оно поможет уменьшить влияние перегрузки сети на пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="bbcd0-125">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="bbcd0-126">Создание канала</span><span class="sxs-lookup"><span data-stu-id="bbcd0-126">Create a channel</span></span>
1. <span data-ttu-id="bbcd0-127">В средстве AMSE перейдите на вкладку **Поток** и щелкните правой кнопкой мыши в области канала.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="bbcd0-128">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="bbcd0-128">Select **Create channel…**</span></span> <span data-ttu-id="bbcd0-129">в меню.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="bbcd0-131">Укажите имя канала, поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="bbcd0-132">В разделе Channel Settings ("Параметры каналов") для параметра Live Encoding ("Кодирование в реальном времени") установите значение **Standard** ("Стандартное"), а для параметра Input Protocol ("Входной протокол") — значение **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="bbcd0-133">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="bbcd0-134">Убедитесь, что флажок **Start the new channel now** (Сразу запустить новый канал) установлен.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="bbcd0-135">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="bbcd0-137">На запуск канала может потребоваться до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="bbcd0-138">Во время запуска канала можно [настроить кодировщик](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbcd0-139">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="bbcd0-140">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="bbcd0-141"><a id=configure_tricaster_rtmp></a>Настройка кодировщика NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="bbcd0-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="bbcd0-142">В этом руководстве используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="bbcd0-143">В оставшейся части этого раздела этапы настройки описываются более подробно.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="bbcd0-144">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="bbcd0-144">**Video**:</span></span>

* <span data-ttu-id="bbcd0-145">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="bbcd0-145">Codec: H.264</span></span>
* <span data-ttu-id="bbcd0-146">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="bbcd0-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="bbcd0-147">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="bbcd0-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="bbcd0-148">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="bbcd0-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="bbcd0-149">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="bbcd0-149">Frame Rate: 30</span></span>

<span data-ttu-id="bbcd0-150">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="bbcd0-150">**Audio**:</span></span>

* <span data-ttu-id="bbcd0-151">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="bbcd0-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="bbcd0-152">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="bbcd0-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="bbcd0-153">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="bbcd0-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="bbcd0-154">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="bbcd0-154">Configuration steps</span></span>
1. <span data-ttu-id="bbcd0-155">Создайте новый проект **NewTek TriCaster** в зависимости от того, какой входной источник видео используется.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="bbcd0-156">Создав проект, найдите кнопку **Stream** (Потоковая передача) и щелкните значок шестеренки рядом с ним для доступа к меню настройки потока.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="bbcd0-158">Открыв меню, щелкните **New** (Создать) под заголовком «Connection» (Подключение).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="bbcd0-159">При появлении запроса для типа подключения выберите **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="bbcd0-161">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-161">Click **OK**.</span></span>
5. <span data-ttu-id="bbcd0-162">Профиль FMLE теперь можно импортировать, щелкнув стрелку в раскрывающемся списке **Streaming Profile** (Профиль потоковой передачи) и выбрав пункт **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="bbcd0-164">Перейдите в каталог, в котором был сохранен настроенный профиль FMLE.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="bbcd0-165">Выберите его и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="bbcd0-166">После загрузки профиля перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="bbcd0-167">Получите входной URL-адрес канала, чтобы назначить его **конечной точке RTMP**Tricaster.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="bbcd0-168">Перейдите обратно в средство AMSE и проверьте состояние запуска канала.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="bbcd0-169">После изменения состояния **Starting** (Запуск) на **Running** (Выполняется) можно получить URL-адрес входных данных.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="bbcd0-170">Когда канал запустится, щелкните правой кнопкой мыши его имя, перейдите вниз к элементу **Copy Input URL to clipboard** (Скопировать входной URL-адрес в буфер обмена) и выберите пункт **Primary Input URL** (Основной входной URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="bbcd0-172">Вставьте этот адрес в поле **Location** (Расположение) в разделе **Flash Server** (Сервер Flash Server) в проекте Tricaster.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="bbcd0-173">Также укажите имя потока в поле **Stream ID** (Идентификатор потока).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="bbcd0-174">Если в профиль FMLE добавлена информация о потоке, ее также можно импортировать в этот раздел. Для этого нажмите кнопку **Import Settings** (Импорт параметров), перейдите к сохраненному профилю FMLE и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="bbcd0-175">Соответствующие поля Flash Server должны заполниться информацией от FMLE.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="bbcd0-177">По завершении нажмите кнопку **ОК** в нижней части окна.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="bbcd0-178">Когда входные видео и звук для Tricaster будут готовы, начните потоковую передачу в AMS, нажав кнопку **Stream** (Потоковая передача).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="bbcd0-180">Прежде чем щелкнуть **Stream** (Потоковая передача), **необходимо** убедиться, что канал готов.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="bbcd0-181">Кроме того, не оставляйте канал в состоянии готовности без входного потока более 15 минут.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="bbcd0-182">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="bbcd0-182">Test playback</span></span>
<span data-ttu-id="bbcd0-183">Перейдите в средство AMSE и щелкните правой кнопкой мыши на канале, который необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="bbcd0-184">В меню наведите указатель мыши на пункт **Playback the Preview** (Воспроизведение для предварительного просмотра) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="bbcd0-185">Если поток отображается в проигрывателе, то кодировщик правильно настроен для подключения к AMS.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="bbcd0-186">При получении ошибки необходимо сбросить канал и настроить параметры кодировщика.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="bbcd0-187">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="bbcd0-188">Создание программы</span><span class="sxs-lookup"><span data-stu-id="bbcd0-188">Create a program</span></span>
1. <span data-ttu-id="bbcd0-189">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="bbcd0-190">На вкладке **Live** (Передача) в инструменте AMSE щелкните правой кнопкой мыши в области программы и выберите команду **Create New Program** (Создать программу).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="bbcd0-192">Укажите имя программы и при необходимости измените параметр **Archive Window Length** (Длительность окна архивации) (по умолчанию она составляет 4 часа).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="bbcd0-193">Также можно указать расположение для хранения или оставить значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="bbcd0-194">Установите флажок **Start the Program now** (Запустить программу сейчас).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="bbcd0-195">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="bbcd0-196">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="bbcd0-197">После запуска программы проверьте воспроизведение. Для этого щелкните правой кнопкой мыши программу, перейдите к пункту **Playback the program(s)** (Воспроизвести программы) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="bbcd0-198">После проверки снова щелкните программу правой кнопкой мыши и выберите команду **Copy the Output URL to Clipboard** (Копировать выходной URL-адрес в буфер обмена) или получите соответствующий адрес, используя пункт меню **Program information and settings** (Сведения о программе и параметры).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="bbcd0-199">Теперь поток можно внедрить в проигрыватель или транслировать аудитории для просмотра в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="bbcd0-200">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="bbcd0-200">Troubleshooting</span></span>
<span data-ttu-id="bbcd0-201">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="bbcd0-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="bbcd0-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bbcd0-202">Next step</span></span>
<span data-ttu-id="bbcd0-203">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="bbcd0-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bbcd0-204">Отзывы</span><span class="sxs-lookup"><span data-stu-id="bbcd0-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
