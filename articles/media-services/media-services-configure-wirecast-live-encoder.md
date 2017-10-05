---
title: "Настройка кодировщика Telestream Wirecast для отправки односкоростного обновляющегося потока | Документация Майкрософт"
description: "В этой статье показано, как настроить динамический кодировщик Wirecast для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени. "
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
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="6e72d-103">Использование кодировщика Wirecast для отправки односкоростного обновляющегося потока</span><span class="sxs-lookup"><span data-stu-id="6e72d-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e72d-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="6e72d-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="6e72d-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="6e72d-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="6e72d-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="6e72d-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="6e72d-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="6e72d-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="6e72d-108">В этой статье показано, как настроить динамический кодировщик [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="6e72d-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="6e72d-109">Дополнительные сведения можно найти в разделе [Работа с каналами, выполняющими кодирование в реальном времени с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="6e72d-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="6e72d-110">В этом учебнике показано, как управлять службами мультимедиа Azure (AMS) с помощью Обозревателя служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="6e72d-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="6e72d-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="6e72d-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="6e72d-112">Если вы используете Mac или Linux, воспользуйтесь классическим порталом Azure для создания [каналов](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программ](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="6e72d-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e72d-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6e72d-113">Prerequisites</span></span>
* <span data-ttu-id="6e72d-114">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6e72d-114">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="6e72d-115">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="6e72d-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="6e72d-116">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="6e72d-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="6e72d-117">Установите последнюю версию средства [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="6e72d-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="6e72d-118">Запустите его и подключитесь к учетной записи AMS.</span><span class="sxs-lookup"><span data-stu-id="6e72d-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="6e72d-119">Советы</span><span class="sxs-lookup"><span data-stu-id="6e72d-119">Tips</span></span>
* <span data-ttu-id="6e72d-120">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="6e72d-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="6e72d-121">Для получения необходимой пропускной способности рекомендуется удвоить скорость потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="6e72d-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="6e72d-122">Хотя это требование не является обязательным, оно поможет уменьшить влияние перегрузки сети на пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="6e72d-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="6e72d-123">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="6e72d-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="6e72d-124">Создание канала</span><span class="sxs-lookup"><span data-stu-id="6e72d-124">Create a channel</span></span>
1. <span data-ttu-id="6e72d-125">В средстве AMSE перейдите на вкладку **Поток** и щелкните правой кнопкой мыши в области канала.</span><span class="sxs-lookup"><span data-stu-id="6e72d-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="6e72d-126">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="6e72d-126">Select **Create channel…**</span></span> <span data-ttu-id="6e72d-127">в меню.</span><span class="sxs-lookup"><span data-stu-id="6e72d-127">from the menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="6e72d-129">Укажите имя канала, поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="6e72d-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="6e72d-130">В разделе Channel Settings ("Параметры каналов") для параметра Live Encoding ("Кодирование в реальном времени") установите значение **Standard** ("Стандартное"), а для параметра Input Protocol ("Входной протокол") — значение **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="6e72d-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="6e72d-131">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="6e72d-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="6e72d-132">Убедитесь, что флажок **Start the new channel now** (Сразу запустить новый канал) установлен.</span><span class="sxs-lookup"><span data-stu-id="6e72d-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="6e72d-133">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="6e72d-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="6e72d-135">На запуск канала может потребоваться до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="6e72d-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="6e72d-136">Во время запуска канала можно [настроить кодировщик](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="6e72d-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e72d-137">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="6e72d-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="6e72d-138">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="6e72d-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="6e72d-139"><a id=configure_wirecast_rtmp></a>Настройка кодировщика Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="6e72d-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="6e72d-140">В этом руководстве используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="6e72d-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="6e72d-141">В оставшейся части этого раздела этапы настройки описываются более подробно.</span><span class="sxs-lookup"><span data-stu-id="6e72d-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="6e72d-142">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="6e72d-142">**Video**:</span></span>

* <span data-ttu-id="6e72d-143">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="6e72d-143">Codec: H.264</span></span>
* <span data-ttu-id="6e72d-144">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="6e72d-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="6e72d-145">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="6e72d-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="6e72d-146">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="6e72d-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="6e72d-147">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="6e72d-147">Frame Rate: 30</span></span>

<span data-ttu-id="6e72d-148">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="6e72d-148">**Audio**:</span></span>

* <span data-ttu-id="6e72d-149">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="6e72d-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="6e72d-150">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="6e72d-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="6e72d-151">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="6e72d-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="6e72d-152">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="6e72d-152">Configuration steps</span></span>
1. <span data-ttu-id="6e72d-153">Откройте приложение Telestream Wirecast на используемом компьютере и настройте его для потоковой передачи RTMP.</span><span class="sxs-lookup"><span data-stu-id="6e72d-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="6e72d-154">Настройте выходные данные, перейдя на вкладку **Output** (Вывод) и выбрав **Output Settings…** (Параметры вывода…).</span><span class="sxs-lookup"><span data-stu-id="6e72d-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="6e72d-155">В поле **Output Destination** (Назначение вывода) выберите значение **RTMP Server** (Сервер RTMP).</span><span class="sxs-lookup"><span data-stu-id="6e72d-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="6e72d-156">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6e72d-156">Click **OK**.</span></span>
4. <span data-ttu-id="6e72d-157">На странице параметров в поле **Destination** (Назначение) задайте значение **Azure Media Services** (Службы мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="6e72d-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="6e72d-158">В поле «Профиль кодировки» будет выбран профиль **Azure H.264 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="6e72d-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="6e72d-159">Чтобы настроить эти параметры, выберите значок шестеренки справа от раскрывающегося списка и затем выберите **New Preset**(Новая предустановка).</span><span class="sxs-lookup"><span data-stu-id="6e72d-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="6e72d-161">Настройка предустановок кодировщика.</span><span class="sxs-lookup"><span data-stu-id="6e72d-161">Configure encoder presets.</span></span>

    <span data-ttu-id="6e72d-162">Задайте имя набора параметров и проверьте следующие рекомендуемые параметры:</span><span class="sxs-lookup"><span data-stu-id="6e72d-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="6e72d-163">**Видео**</span><span class="sxs-lookup"><span data-stu-id="6e72d-163">**Video**</span></span>

   * <span data-ttu-id="6e72d-164">Кодировщик: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="6e72d-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="6e72d-165">Кадров в секунду: 30</span><span class="sxs-lookup"><span data-stu-id="6e72d-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="6e72d-166">Средняя скорость: 5000 кбит/сек (это значение можно изменить в зависимости от ограничений сети)</span><span class="sxs-lookup"><span data-stu-id="6e72d-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="6e72d-167">Профиль: основной</span><span class="sxs-lookup"><span data-stu-id="6e72d-167">Profile: Main</span></span>
   * <span data-ttu-id="6e72d-168">Ключевой кадр: каждые 60 кадров</span><span class="sxs-lookup"><span data-stu-id="6e72d-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="6e72d-169">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="6e72d-169">**Audio**</span></span>

   * <span data-ttu-id="6e72d-170">Конечная скорость: 192 Кбит/сек</span><span class="sxs-lookup"><span data-stu-id="6e72d-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="6e72d-171">Частота выборки: 44,100 кГц</span><span class="sxs-lookup"><span data-stu-id="6e72d-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="6e72d-173">Нажмите кнопку **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="6e72d-173">Press **Save**.</span></span>

    <span data-ttu-id="6e72d-174">Созданный профиль теперь доступен для выбора в поле «Профиль кодировки».</span><span class="sxs-lookup"><span data-stu-id="6e72d-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="6e72d-175">Убедитесь, что выбран новый профиль.</span><span class="sxs-lookup"><span data-stu-id="6e72d-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="6e72d-176">Получите входной URL-адрес канала, чтобы назначить его **конечной точке RTMP**Wirecast.</span><span class="sxs-lookup"><span data-stu-id="6e72d-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="6e72d-177">Перейдите обратно в средство AMSE и проверьте состояние запуска канала.</span><span class="sxs-lookup"><span data-stu-id="6e72d-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="6e72d-178">После изменения состояния **Starting** (Запуск) на **Running** (Выполняется) можно получить URL-адрес входных данных.</span><span class="sxs-lookup"><span data-stu-id="6e72d-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="6e72d-179">Когда канал запустится, щелкните правой кнопкой мыши его имя, перейдите вниз к элементу **Copy Input URL to clipboard** (Скопировать входной URL-адрес в буфер обмена) и выберите пункт **Primary Input URL** (Основной входной URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="6e72d-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="6e72d-181">В окне Wirecast **Output Settings** (Параметры вывода) вставьте этот адрес в поле **Address** (Адрес) раздела параметров вывода и укажите имя потока.</span><span class="sxs-lookup"><span data-stu-id="6e72d-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="6e72d-183">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6e72d-183">Select **OK**.</span></span>
2. <span data-ttu-id="6e72d-184">На главном экране **Wirecast** подтвердите готовность источников ввода для видео и звука, а затем щелкните **Stream** (Потоковая передача) в верхнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="6e72d-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="6e72d-186">Прежде чем щелкнуть **Stream** (Потоковая передача), **необходимо** убедиться, что канал готов.</span><span class="sxs-lookup"><span data-stu-id="6e72d-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="6e72d-187">Кроме того, не оставляйте канал в состоянии готовности без входного потока более 15 минут.</span><span class="sxs-lookup"><span data-stu-id="6e72d-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="6e72d-188">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="6e72d-188">Test playback</span></span>

<span data-ttu-id="6e72d-189">Перейдите в средство AMSE и щелкните правой кнопкой мыши на канале, который необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="6e72d-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="6e72d-190">В меню наведите указатель мыши на пункт **Playback the Preview** (Воспроизведение для предварительного просмотра) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="6e72d-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="6e72d-191">Если поток отображается в проигрывателе, то кодировщик правильно настроен для подключения к AMS.</span><span class="sxs-lookup"><span data-stu-id="6e72d-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="6e72d-192">При получении ошибки необходимо сбросить канал и настроить параметры кодировщика.</span><span class="sxs-lookup"><span data-stu-id="6e72d-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="6e72d-193">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="6e72d-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="6e72d-194">Создание программы</span><span class="sxs-lookup"><span data-stu-id="6e72d-194">Create a program</span></span>
1. <span data-ttu-id="6e72d-195">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="6e72d-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="6e72d-196">На вкладке **Live** (Передача) в инструменте AMSE щелкните правой кнопкой мыши в области программы и выберите команду **Create New Program** (Создать программу).</span><span class="sxs-lookup"><span data-stu-id="6e72d-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="6e72d-198">Укажите имя программы и при необходимости измените параметр **Archive Window Length** (Длительность окна архивации) (по умолчанию она составляет 4 часа).</span><span class="sxs-lookup"><span data-stu-id="6e72d-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="6e72d-199">Также можно указать расположение для хранения или оставить значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6e72d-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="6e72d-200">Установите флажок **Start the Program now** (Запустить программу сейчас).</span><span class="sxs-lookup"><span data-stu-id="6e72d-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="6e72d-201">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="6e72d-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="6e72d-202">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="6e72d-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="6e72d-203">После запуска программы проверьте воспроизведение. Для этого щелкните правой кнопкой мыши программу, перейдите к пункту **Playback the program(s)** (Воспроизвести программы) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="6e72d-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="6e72d-204">После проверки снова щелкните программу правой кнопкой мыши и выберите команду **Copy the Output URL to Clipboard** (Копировать выходной URL-адрес в буфер обмена) или получите соответствующий адрес, используя пункт меню **Program information and settings** (Сведения о программе и параметры).</span><span class="sxs-lookup"><span data-stu-id="6e72d-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="6e72d-205">Теперь поток можно внедрить в проигрыватель или транслировать аудитории для просмотра в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="6e72d-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="6e72d-206">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="6e72d-206">Troubleshooting</span></span>
<span data-ttu-id="6e72d-207">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="6e72d-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6e72d-208">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="6e72d-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6e72d-209">Отзывы</span><span class="sxs-lookup"><span data-stu-id="6e72d-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
