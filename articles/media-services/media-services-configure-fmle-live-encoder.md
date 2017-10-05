---
title: "Настройка кодировщика FMLE для отправки односкоростного обновляющегося потока | Документация Майкрософт"
description: "В этой статье показано, как настроить кодировщик Flash Media Live Encoder (FMLE) для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени."
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
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="27a24-103">Использование кодировщика FMLE для отправки односкоростного обновляющегося потока</span><span class="sxs-lookup"><span data-stu-id="27a24-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="27a24-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="27a24-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="27a24-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="27a24-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="27a24-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="27a24-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="27a24-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="27a24-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="27a24-108">В этой статье показано, как настроить кодировщик [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="27a24-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="27a24-109">Дополнительные сведения можно найти в разделе [Работа с каналами, выполняющими кодирование в реальном времени с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="27a24-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="27a24-110">В этом учебнике показано, как управлять службами мультимедиа Azure (AMS) с помощью Обозревателя служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="27a24-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="27a24-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="27a24-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="27a24-112">Если вы используете Mac или Linux, воспользуйтесь классическим порталом Azure для создания [каналов](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программ](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="27a24-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="27a24-113">Обратите внимание, что в этом руководстве мы используем кодек AAC.</span><span class="sxs-lookup"><span data-stu-id="27a24-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="27a24-114">Однако FMLE не поддерживает AAC по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27a24-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="27a24-115">Для использования AAC необходимо приобрести подключаемый модуль, например, от MainConcept: [подключаемый модуль AAC](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="27a24-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27a24-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="27a24-116">Prerequisites</span></span>
* <span data-ttu-id="27a24-117">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="27a24-117">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="27a24-118">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="27a24-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="27a24-119">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="27a24-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="27a24-120">Установите последнюю версию средства [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="27a24-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="27a24-121">Запустите его и подключитесь к учетной записи AMS.</span><span class="sxs-lookup"><span data-stu-id="27a24-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="27a24-122">Советы</span><span class="sxs-lookup"><span data-stu-id="27a24-122">Tips</span></span>
* <span data-ttu-id="27a24-123">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="27a24-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="27a24-124">Для получения необходимой пропускной способности рекомендуется удвоить скорость потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="27a24-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="27a24-125">Хотя это требование не является обязательным, оно поможет уменьшить влияние перегрузки сети на пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="27a24-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="27a24-126">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="27a24-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="27a24-127">Создание канала</span><span class="sxs-lookup"><span data-stu-id="27a24-127">Create a channel</span></span>
1. <span data-ttu-id="27a24-128">В средстве AMSE перейдите на вкладку **Поток** и щелкните правой кнопкой мыши в области канала.</span><span class="sxs-lookup"><span data-stu-id="27a24-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="27a24-129">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="27a24-129">Select **Create channel…**</span></span> <span data-ttu-id="27a24-130">в меню.</span><span class="sxs-lookup"><span data-stu-id="27a24-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="27a24-132">Укажите имя канала, поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="27a24-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="27a24-133">В разделе Channel Settings ("Параметры каналов") для параметра Live Encoding ("Кодирование в реальном времени") установите значение **Standard** ("Стандартное"), а для параметра Input Protocol ("Входной протокол") — значение **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="27a24-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="27a24-134">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="27a24-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="27a24-135">Убедитесь, что флажок **Start the new channel now** (Сразу запустить новый канал) установлен.</span><span class="sxs-lookup"><span data-stu-id="27a24-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="27a24-136">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="27a24-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="27a24-138">На запуск канала может потребоваться до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="27a24-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="27a24-139">Во время запуска канала можно [настроить кодировщик](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="27a24-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27a24-140">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="27a24-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="27a24-141">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="27a24-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="27a24-142"><a id=configure_fmle_rtmp></a>Настройка кодировщика FMLE</span><span class="sxs-lookup"><span data-stu-id="27a24-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="27a24-143">В этом руководстве используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="27a24-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="27a24-144">В оставшейся части этого раздела этапы настройки описываются более подробно.</span><span class="sxs-lookup"><span data-stu-id="27a24-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="27a24-145">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="27a24-145">**Video**:</span></span>

* <span data-ttu-id="27a24-146">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="27a24-146">Codec: H.264</span></span>
* <span data-ttu-id="27a24-147">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="27a24-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="27a24-148">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="27a24-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="27a24-149">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="27a24-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="27a24-150">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="27a24-150">Frame Rate: 30</span></span>

<span data-ttu-id="27a24-151">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="27a24-151">**Audio**:</span></span>

* <span data-ttu-id="27a24-152">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="27a24-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="27a24-153">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="27a24-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="27a24-154">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="27a24-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="27a24-155">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="27a24-155">Configuration steps</span></span>
1. <span data-ttu-id="27a24-156">Перейдите к интерфейсу Flash Media Live Encoder (FMLE) на используемом компьютере.</span><span class="sxs-lookup"><span data-stu-id="27a24-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="27a24-157">Интерфейс представляет собой одну главную страницу с параметрами.</span><span class="sxs-lookup"><span data-stu-id="27a24-157">The interface is one main page of settings.</span></span> <span data-ttu-id="27a24-158">Пожалуйста, обратите внимание на следующие рекомендуемые параметры для потоковой передачи с FMLE.</span><span class="sxs-lookup"><span data-stu-id="27a24-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="27a24-159">Формат: H.264 Частота кадров: 30.00</span><span class="sxs-lookup"><span data-stu-id="27a24-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="27a24-160">Размер входного потока: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="27a24-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="27a24-161">Скорость: 5000 кбит/сек (это значение можно изменить в зависимости от ограничений сети)</span><span class="sxs-lookup"><span data-stu-id="27a24-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="27a24-163">При использовании источников с чересстрочной разверткой установите флажок «Устранить чересстрочную развертку».</span><span class="sxs-lookup"><span data-stu-id="27a24-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="27a24-164">Выберите значок гаечного ключа рядом с полем «Формат», там должны быть установлены следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="27a24-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="27a24-165">Профиль: основной</span><span class="sxs-lookup"><span data-stu-id="27a24-165">Profile: Main</span></span>
   * <span data-ttu-id="27a24-166">Уровень: 4.0</span><span class="sxs-lookup"><span data-stu-id="27a24-166">Level: 4.0</span></span>
   * <span data-ttu-id="27a24-167">Частота опорного кадра: 2 секунды</span><span class="sxs-lookup"><span data-stu-id="27a24-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="27a24-169">Установите следующие важные параметры звука:</span><span class="sxs-lookup"><span data-stu-id="27a24-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="27a24-170">Формат: AAC</span><span class="sxs-lookup"><span data-stu-id="27a24-170">Format: AAC</span></span>
   * <span data-ttu-id="27a24-171">Частота выборки: 44100 Гц</span><span class="sxs-lookup"><span data-stu-id="27a24-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="27a24-172">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="27a24-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="27a24-174">Получите входной URL-адрес канала, чтобы назначить его **конечной точке RTMP**FMLE.</span><span class="sxs-lookup"><span data-stu-id="27a24-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="27a24-175">Перейдите обратно в средство AMSE и проверьте состояние запуска канала.</span><span class="sxs-lookup"><span data-stu-id="27a24-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="27a24-176">После изменения состояния **Starting** (Запуск) на **Running** (Выполняется) можно получить URL-адрес входных данных.</span><span class="sxs-lookup"><span data-stu-id="27a24-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="27a24-177">Когда канал запустится, щелкните правой кнопкой мыши его имя, перейдите вниз к элементу **Copy Input URL to clipboard** (Скопировать входной URL-адрес в буфер обмена) и выберите пункт **Primary Input URL** (Основной входной URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="27a24-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="27a24-179">Вставьте этот адрес в поле **URL-адрес FMS** раздела выхода и укажите имя потока.</span><span class="sxs-lookup"><span data-stu-id="27a24-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="27a24-181">Для обеспечения дополнительной надежности повторите эти действия с полем «Дополнительный входной URL-адрес».</span><span class="sxs-lookup"><span data-stu-id="27a24-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="27a24-182">Нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="27a24-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27a24-183">Прежде чем нажать кнопку **Connect** ("Подключиться"), **необходимо** убедиться, что канал находится в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="27a24-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="27a24-184">Кроме того, не оставляйте канал в состоянии готовности без входного потока более 15 минут.</span><span class="sxs-lookup"><span data-stu-id="27a24-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="27a24-185">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="27a24-185">Test playback</span></span>

<span data-ttu-id="27a24-186">Перейдите в средство AMSE и щелкните правой кнопкой мыши на канале, который необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="27a24-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="27a24-187">В меню наведите указатель мыши на пункт **Playback the Preview** (Воспроизведение для предварительного просмотра) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="27a24-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="27a24-188">Если поток отображается в проигрывателе, то кодировщик правильно настроен для подключения к AMS.</span><span class="sxs-lookup"><span data-stu-id="27a24-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="27a24-189">При получении ошибки необходимо сбросить канал и настроить параметры кодировщика.</span><span class="sxs-lookup"><span data-stu-id="27a24-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="27a24-190">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="27a24-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="27a24-191">Создание программы</span><span class="sxs-lookup"><span data-stu-id="27a24-191">Create a program</span></span>
1. <span data-ttu-id="27a24-192">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="27a24-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="27a24-193">На вкладке **Live** (Передача) в инструменте AMSE щелкните правой кнопкой мыши в области программы и выберите команду **Create New Program** (Создать программу).</span><span class="sxs-lookup"><span data-stu-id="27a24-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="27a24-195">Укажите имя программы и при необходимости измените параметр **Archive Window Length** (Длительность окна архивации) (по умолчанию она составляет 4 часа).</span><span class="sxs-lookup"><span data-stu-id="27a24-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="27a24-196">Также можно указать расположение для хранения или оставить значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="27a24-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="27a24-197">Установите флажок **Start the Program now** (Запустить программу сейчас).</span><span class="sxs-lookup"><span data-stu-id="27a24-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="27a24-198">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="27a24-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="27a24-199">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="27a24-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="27a24-200">После запуска программы проверьте воспроизведение. Для этого щелкните правой кнопкой мыши программу, перейдите к пункту **Playback the program(s)** (Воспроизвести программы) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="27a24-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="27a24-201">После проверки снова щелкните программу правой кнопкой мыши и выберите команду **Copy the Output URL to Clipboard** (Копировать выходной URL-адрес в буфер обмена) или получите соответствующий адрес, используя пункт меню **Program information and settings** (Сведения о программе и параметры).</span><span class="sxs-lookup"><span data-stu-id="27a24-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="27a24-202">Теперь поток можно внедрить в проигрыватель или транслировать аудитории для просмотра в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="27a24-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="27a24-203">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="27a24-203">Troubleshooting</span></span>
<span data-ttu-id="27a24-204">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="27a24-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="27a24-205">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="27a24-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="27a24-206">Отзывы</span><span class="sxs-lookup"><span data-stu-id="27a24-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
