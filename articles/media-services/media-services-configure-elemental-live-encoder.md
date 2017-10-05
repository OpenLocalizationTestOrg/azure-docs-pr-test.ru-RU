---
title: "Настройка кодировщика Elemental Live для отправки односкоростного обновляющегося потока | Документация Майкрософт"
description: "В этой статье показано, как настроить кодировщик Elemental Live для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени."
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
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="91d99-103">Использование кодировщика Elemental Live для отправки односкоростного обновляющегося потока</span><span class="sxs-lookup"><span data-stu-id="91d99-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91d99-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="91d99-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="91d99-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="91d99-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="91d99-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="91d99-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="91d99-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="91d99-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="91d99-108">В этой статье показано, как настроить кодировщик [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) для отправки односкоростного потока в каналы AMS, которые выполняют кодирование в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="91d99-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="91d99-109">Дополнительные сведения можно найти в разделе [Работа с каналами, выполняющими кодирование в реальном времени с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="91d99-110">В этом учебнике показано, как управлять службами мультимедиа Azure (AMS) с помощью Обозревателя служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="91d99-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="91d99-111">Это средство запускается только на компьютерах с ОС Windows.</span><span class="sxs-lookup"><span data-stu-id="91d99-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="91d99-112">Если вы используете Mac или Linux, воспользуйтесь классическим порталом Azure для создания [каналов](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программ](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91d99-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="91d99-113">Prerequisites</span></span>
* <span data-ttu-id="91d99-114">Вы должны иметь практические знания по созданию событий в реальном времени с помощью веб-интерфейса Elemental Live.</span><span class="sxs-lookup"><span data-stu-id="91d99-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* <span data-ttu-id="91d99-115">[Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-115">[Create an Azure Media Services account](media-services-portal-create-account.md)</span></span>
* <span data-ttu-id="91d99-116">Убедитесь, что запущена конечная точка потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="91d99-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="91d99-117">Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="91d99-118">Установите последнюю версию средства [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) .</span><span class="sxs-lookup"><span data-stu-id="91d99-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="91d99-119">Запустите его и подключитесь к учетной записи AMS.</span><span class="sxs-lookup"><span data-stu-id="91d99-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="91d99-120">Советы</span><span class="sxs-lookup"><span data-stu-id="91d99-120">Tips</span></span>
* <span data-ttu-id="91d99-121">По возможности используйте проводное подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="91d99-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="91d99-122">Для получения необходимой пропускной способности рекомендуется удвоить скорость потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="91d99-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="91d99-123">Хотя это требование не является обязательным, оно поможет уменьшить влияние перегрузки сети на пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="91d99-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="91d99-124">При использовании программных кодировщиков закройте все ненужные программы.</span><span class="sxs-lookup"><span data-stu-id="91d99-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="91d99-125">Использование Elemental Live с протоколом RTP</span><span class="sxs-lookup"><span data-stu-id="91d99-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="91d99-126">В этом разделе показано, как настроить кодировщик Elemental Live, который отправляет односкоростной обновляющийся поток по протоколу RTP.</span><span class="sxs-lookup"><span data-stu-id="91d99-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="91d99-127">Дополнительные сведения см. в подразделе, посвященному [передаче потока MPEG-TS по протоколу RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="91d99-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="91d99-128">Создание канала</span><span class="sxs-lookup"><span data-stu-id="91d99-128">Create a channel</span></span>

1. <span data-ttu-id="91d99-129">В средстве AMSE перейдите на вкладку **Поток** и щелкните правой кнопкой мыши в области канала.</span><span class="sxs-lookup"><span data-stu-id="91d99-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="91d99-130">Выберите **Создать канал...**</span><span class="sxs-lookup"><span data-stu-id="91d99-130">Select **Create channel…**</span></span> <span data-ttu-id="91d99-131">в меню.</span><span class="sxs-lookup"><span data-stu-id="91d99-131">from the menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="91d99-133">Укажите имя канала, поле описания является необязательным.</span><span class="sxs-lookup"><span data-stu-id="91d99-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="91d99-134">В разделе Channel Settings ("Параметры каналов") для параметра Live Encoding ("Кодирование в реальном времени") установите значение **Standard** (Стандартное), а для параметра Input Protocol ("Входной протокол") — значение **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="91d99-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="91d99-135">Остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="91d99-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="91d99-136">Убедитесь, что флажок **Start the new channel now** (Сразу запустить новый канал) установлен.</span><span class="sxs-lookup"><span data-stu-id="91d99-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="91d99-137">Щелкните **Создать канал**.</span><span class="sxs-lookup"><span data-stu-id="91d99-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="91d99-139">На запуск канала может потребоваться до 20 минут.</span><span class="sxs-lookup"><span data-stu-id="91d99-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="91d99-140">Во время запуска канала можно [настроить кодировщик](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="91d99-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91d99-141">Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности.</span><span class="sxs-lookup"><span data-stu-id="91d99-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="91d99-142">Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="91d99-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="91d99-143"><a id=configure_elemental_rtp></a>Настройка кодировщика Elemental Live</span><span class="sxs-lookup"><span data-stu-id="91d99-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="91d99-144">В этом руководстве используются следующие параметры вывода.</span><span class="sxs-lookup"><span data-stu-id="91d99-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="91d99-145">В оставшейся части этого раздела этапы настройки описываются более подробно.</span><span class="sxs-lookup"><span data-stu-id="91d99-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="91d99-146">**Видео:**</span><span class="sxs-lookup"><span data-stu-id="91d99-146">**Video**:</span></span>

* <span data-ttu-id="91d99-147">Кодек: H.264</span><span class="sxs-lookup"><span data-stu-id="91d99-147">Codec: H.264</span></span>
* <span data-ttu-id="91d99-148">Профиль: High (уровень 4.0)</span><span class="sxs-lookup"><span data-stu-id="91d99-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="91d99-149">Скорость: 5000 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="91d99-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="91d99-150">Опорный кадр: 2 секунды (60 секунд)</span><span class="sxs-lookup"><span data-stu-id="91d99-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="91d99-151">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="91d99-151">Frame Rate: 30</span></span>

<span data-ttu-id="91d99-152">**Звук:**</span><span class="sxs-lookup"><span data-stu-id="91d99-152">**Audio**:</span></span>

* <span data-ttu-id="91d99-153">Кодек: AAC (LC)</span><span class="sxs-lookup"><span data-stu-id="91d99-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="91d99-154">Скорость: 192 Кбит/с</span><span class="sxs-lookup"><span data-stu-id="91d99-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="91d99-155">Частота выборки: 44,1 кГц</span><span class="sxs-lookup"><span data-stu-id="91d99-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="91d99-156">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="91d99-156">Configuration steps</span></span>
1. <span data-ttu-id="91d99-157">Перейдите в веб-интерфейс **Elemental Live** и настройте кодировщик для потоковой передачи **UDP/TS**.</span><span class="sxs-lookup"><span data-stu-id="91d99-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="91d99-158">После создания нового события прокрутите содержимое окна вниз к группам вывода и добавьте группу вывода **UDP/TS** .</span><span class="sxs-lookup"><span data-stu-id="91d99-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="91d99-159">Создайте выходные данные, щелкнув **New Stream** (Новый поток), а затем **Add Output** (Добавить выходные данные).</span><span class="sxs-lookup"><span data-stu-id="91d99-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="91d99-161">Для события Elemental рекомендуется установить код времени в значение «Системные часы». Это позволит кодировщику выполнить повторное подключение в случае сбоя потока.</span><span class="sxs-lookup"><span data-stu-id="91d99-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="91d99-162">После создания выхода щелкните **Добавить поток**.</span><span class="sxs-lookup"><span data-stu-id="91d99-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="91d99-163">Теперь можно настроить параметры выхода.</span><span class="sxs-lookup"><span data-stu-id="91d99-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="91d99-164">Прокрутите содержимое окна вниз до только что созданного потока Stream 1. Щелкните вкладку **Video** (Видео) слева и разверните раздел **Advanced** (Дополнительные параметры).</span><span class="sxs-lookup"><span data-stu-id="91d99-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="91d99-166">Хотя Elemental Live имеет широкий спектр доступных настроек, для потоковой передачи с AMS рекомендуются следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="91d99-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="91d99-167">Разрешение: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="91d99-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="91d99-168">Частота кадров: 30</span><span class="sxs-lookup"><span data-stu-id="91d99-168">Framerate: 30</span></span>
   * <span data-ttu-id="91d99-169">Размер GOP: 60 кадров</span><span class="sxs-lookup"><span data-stu-id="91d99-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="91d99-170">Режим развертки: прогрессивная</span><span class="sxs-lookup"><span data-stu-id="91d99-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="91d99-171">Скорость: 5000000 бит/сек (это значение можно изменить в зависимости от ограничений сети)</span><span class="sxs-lookup"><span data-stu-id="91d99-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="91d99-173">Получение входного URL-адреса канала</span><span class="sxs-lookup"><span data-stu-id="91d99-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="91d99-174">Перейдите обратно в средство AMSE и проверьте состояние запуска канала.</span><span class="sxs-lookup"><span data-stu-id="91d99-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="91d99-175">После изменения состояния **Starting** (Запуск) на **Running** (Выполняется) можно получить URL-адрес входных данных.</span><span class="sxs-lookup"><span data-stu-id="91d99-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="91d99-176">Когда канал запустится, щелкните правой кнопкой мыши его имя, перейдите вниз к элементу **Copy Input URL to clipboard** (Скопировать входной URL-адрес в буфер обмена) и выберите пункт **Primary Input URL** (Основной входной URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="91d99-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="91d99-178">Вставьте этот адрес в поле **Основное назначение** Elemental.</span><span class="sxs-lookup"><span data-stu-id="91d99-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="91d99-179">Все остальные параметры можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="91d99-179">All other settings can remain the default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="91d99-181">Для обеспечения дополнительной надежности повторите эти действия с полем «Дополнительный входной URL-адрес», создав отдельную вкладку «Выход» для потоковой передачи UDP/TS.</span><span class="sxs-lookup"><span data-stu-id="91d99-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="91d99-182">Щелкните **Create** (Создать) (если событие создано) или **Update** (Обновить) (при изменении имеющегося события), а затем запустите кодировщик.</span><span class="sxs-lookup"><span data-stu-id="91d99-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91d99-183">Прежде чем нажать кнопку **Start** (Запустить) в веб-интерфейсе Elemental Live, **необходимо** убедиться, что канал находится в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="91d99-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="91d99-184">Кроме того, не оставляйте канал в состоянии готовности более 15 минут.</span><span class="sxs-lookup"><span data-stu-id="91d99-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="91d99-185">После отправки потока в течение 30 секунд, вернитесь к средству AMSE и проверьте воспроизведение.</span><span class="sxs-lookup"><span data-stu-id="91d99-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="91d99-186">Проверка воспроизведения</span><span class="sxs-lookup"><span data-stu-id="91d99-186">Test playback</span></span>

<span data-ttu-id="91d99-187">Перейдите в средство AMSE и щелкните правой кнопкой мыши на канале, который необходимо проверить.</span><span class="sxs-lookup"><span data-stu-id="91d99-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="91d99-188">В меню наведите указатель мыши на пункт **Playback the Preview** (Воспроизведение для предварительного просмотра) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="91d99-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="91d99-189">Если поток отображается в проигрывателе, то кодировщик правильно настроен для подключения к AMS.</span><span class="sxs-lookup"><span data-stu-id="91d99-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="91d99-190">При получении ошибки необходимо сбросить канал и настроить параметры кодировщика.</span><span class="sxs-lookup"><span data-stu-id="91d99-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="91d99-191">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="91d99-192">Создание программы</span><span class="sxs-lookup"><span data-stu-id="91d99-192">Create a program</span></span>
1. <span data-ttu-id="91d99-193">После проверки воспроизведения канала создайте программу.</span><span class="sxs-lookup"><span data-stu-id="91d99-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="91d99-194">На вкладке **Live** (Передача) в инструменте AMSE щелкните правой кнопкой мыши в области программы и выберите команду **Create New Program** (Создать программу).</span><span class="sxs-lookup"><span data-stu-id="91d99-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="91d99-196">Укажите имя программы и при необходимости измените параметр **Archive Window Length** (Длительность окна архивации) (по умолчанию она составляет 4 часа).</span><span class="sxs-lookup"><span data-stu-id="91d99-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="91d99-197">Также можно указать расположение для хранения или оставить значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="91d99-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="91d99-198">Установите флажок **Start the Program now** (Запустить программу сейчас).</span><span class="sxs-lookup"><span data-stu-id="91d99-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="91d99-199">Щелкните **Create Program**(Создать программу).</span><span class="sxs-lookup"><span data-stu-id="91d99-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="91d99-200">Создание программы занимает меньше времени, чем создание канала.</span><span class="sxs-lookup"><span data-stu-id="91d99-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="91d99-201">После запуска программы проверьте воспроизведение. Для этого щелкните правой кнопкой мыши программу, перейдите к пункту **Playback the program(s)** (Воспроизвести программы) и выберите пункт **with Azure Media Player** (с помощью Проигрывателя мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="91d99-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="91d99-202">После проверки снова щелкните программу правой кнопкой мыши и выберите команду **Copy the Output URL to Clipboard** (Копировать выходной URL-адрес в буфер обмена) или получите соответствующий адрес, используя пункт меню **Program information and settings** (Сведения о программе и параметры).</span><span class="sxs-lookup"><span data-stu-id="91d99-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="91d99-203">Теперь поток можно внедрить в проигрыватель или транслировать аудитории для просмотра в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="91d99-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="91d99-204">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="91d99-204">Troubleshooting</span></span>
<span data-ttu-id="91d99-205">Рекомендации см. в статье, посвященной [устранению неполадок](media-services-troubleshooting-live-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="91d99-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="91d99-206">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="91d99-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91d99-207">Отзывы</span><span class="sxs-lookup"><span data-stu-id="91d99-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
