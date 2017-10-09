---
title: "поток aaaLive с локальных кодировщиков, с помощью hello портал Azure | Документы Microsoft"
description: "Этот учебник поможет выполнить этапы создания канала, который настроен для сквозной доставки hello."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="55cd1-103">Как tooperform потоковой трансляции с помощью локальных кодировщиков, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="55cd1-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55cd1-104">Портал</span><span class="sxs-lookup"><span data-stu-id="55cd1-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="55cd1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="55cd1-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="55cd1-106">REST</span><span class="sxs-lookup"><span data-stu-id="55cd1-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="55cd1-107">Этот учебник поможет вам выполнить этапы hello использования hello Azure портала toocreate **канала** , настроенного для сквозной доставки.</span><span class="sxs-lookup"><span data-stu-id="55cd1-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="55cd1-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55cd1-108">Prerequisites</span></span>
<span data-ttu-id="55cd1-109">Здесь представлены Hello необходимые toocomplete hello учебника:</span><span class="sxs-lookup"><span data-stu-id="55cd1-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="55cd1-110">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="55cd1-110">An Azure account.</span></span> <span data-ttu-id="55cd1-111">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55cd1-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="55cd1-112">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="55cd1-112">A Media Services account.</span></span> <span data-ttu-id="55cd1-113">toocreate учетную запись служб носителей в разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="55cd1-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="55cd1-114">Веб-камера,</span><span class="sxs-lookup"><span data-stu-id="55cd1-114">A webcam.</span></span> <span data-ttu-id="55cd1-115">например [кодировщик Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="55cd1-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="55cd1-116">Настоятельно рекомендуется hello tooreview следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="55cd1-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="55cd1-117">Поддержка протокола RTMP службами мультимедиа Azure и динамические кодировщики</span><span class="sxs-lookup"><span data-stu-id="55cd1-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="55cd1-118">Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="55cd1-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="55cd1-119">Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями</span><span class="sxs-lookup"><span data-stu-id="55cd1-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="55cd1-120"><a id="scenario"></a>Стандартный сценарий потоковой передачи в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="55cd1-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="55cd1-121">Hello следующие шаги описывают задачи, связанные с созданием общих динамической потоковой передачи приложений, использующих каналы, которые настроены для сквозной доставки.</span><span class="sxs-lookup"><span data-stu-id="55cd1-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="55cd1-122">В этом учебнике показано как toocreate к серверу каналов и событий в реальном времени и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="55cd1-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="55cd1-123">Убедитесь, что hello, из которого нужно toostream содержимое конечной точки потоковой передачи в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="55cd1-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="55cd1-124">Подключение компьютера tooa камеры.</span><span class="sxs-lookup"><span data-stu-id="55cd1-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="55cd1-125">Запустите и настройте локальный динамический кодировщик, который выводит поток с разными скоростями RTMP или фрагментированный поток MP4.</span><span class="sxs-lookup"><span data-stu-id="55cd1-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="55cd1-126">Дополнительные сведения см. в статье о [поддержке протокола RTMP в службах мультимедиа Azure и о динамических кодировщиках](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="55cd1-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="55cd1-127">Это действие также можно выполнить после создания канала.</span><span class="sxs-lookup"><span data-stu-id="55cd1-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="55cd1-128">Создайте и запустите сквозной канал.</span><span class="sxs-lookup"><span data-stu-id="55cd1-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="55cd1-129">Получение hello канал приема URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="55cd1-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="55cd1-130">URL-адрес приема Hello используется toohello hello динамического кодировщика toosend hello потока канала.</span><span class="sxs-lookup"><span data-stu-id="55cd1-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="55cd1-131">Получить URL-адрес предварительного просмотра канала hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="55cd1-132">Используйте этот URL-адрес tooverify, что ваш канал правильно получает hello обновляющегося потока.</span><span class="sxs-lookup"><span data-stu-id="55cd1-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="55cd1-133">Создайте интерактивное событие или программу.</span><span class="sxs-lookup"><span data-stu-id="55cd1-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="55cd1-134">Когда с помощью hello портал Azure, при создании интерактивное событие также создается актива.</span><span class="sxs-lookup"><span data-stu-id="55cd1-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="55cd1-135">Запустите hello событий или программы при готовности toostart потоковой передачи и архивированию.</span><span class="sxs-lookup"><span data-stu-id="55cd1-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="55cd1-136">При необходимости hello динамическому кодировщику можно сигнальное toostart объявления.</span><span class="sxs-lookup"><span data-stu-id="55cd1-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="55cd1-137">объявления Hello вставляется в выходной поток hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="55cd1-138">Остановите hello событий или программа всякий раз, когда требуется toostop потоковую передачу и архивировать событие hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="55cd1-139">Удалить событие hello или программа (и при необходимости удалить средство hello).</span><span class="sxs-lookup"><span data-stu-id="55cd1-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="55cd1-140">См. в статье [потоковой трансляции с помощью локальных кодировщиков, которые создают потоки с разными скоростями](media-services-live-streaming-with-onprem-encoders.md) toolearn о основные понятия и рекомендации, связанные с toolive потоковой передачи с локальных кодировщиков и к серверу каналов.</span><span class="sxs-lookup"><span data-stu-id="55cd1-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="55cd1-141">уведомления о tooview и ошибок</span><span class="sxs-lookup"><span data-stu-id="55cd1-141">tooview notifications and errors</span></span>
<span data-ttu-id="55cd1-142">Если tooview уведомлений и ошибок, создаваемыми hello портал Azure, щелкните значок уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Уведомления](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="55cd1-144">Создание и запуск сквозных каналов и событий</span><span class="sxs-lookup"><span data-stu-id="55cd1-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="55cd1-145">Канал не сопоставлено события или программы, позволяющие toocontrol hello публикацией и хранением сегментов в потоковой трансляции.</span><span class="sxs-lookup"><span data-stu-id="55cd1-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="55cd1-146">Каналы управляют событиями.</span><span class="sxs-lookup"><span data-stu-id="55cd1-146">Channels manage events.</span></span> 

<span data-ttu-id="55cd1-147">Можно указать hello количество часов, должна tooretain hello записанного содержимого для программы hello, установка hello **размер окна архива** длины.</span><span class="sxs-lookup"><span data-stu-id="55cd1-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="55cd1-148">Это значение может быть задано в диапазоне от 5 минут до tooa 25 часов.</span><span class="sxs-lookup"><span data-stu-id="55cd1-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="55cd1-149">Размер окна архива также указывает максимальное количество раз, когда клиенты могут вернуться назад от текущей позиции трансляции hello hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="55cd1-150">События могут быть запущены по hello определенный промежуток времени, но контент за пределами hello длину промежутка постоянно удаляется.</span><span class="sxs-lookup"><span data-stu-id="55cd1-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="55cd1-151">Это значение этого свойства также определяет, как долго клиента hello манифестов может увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="55cd1-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="55cd1-152">Каждое событие связано с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="55cd1-152">Each event is associated with an asset.</span></span> <span data-ttu-id="55cd1-153">событие toopublish hello, необходимо создать указатель OnDemand для связанного hello активов.</span><span class="sxs-lookup"><span data-stu-id="55cd1-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="55cd1-154">Наличие указателя позволяет toobuild URL-адрес потоковой передачи, могут предоставить клиентам tooyour.</span><span class="sxs-lookup"><span data-stu-id="55cd1-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="55cd1-155">Канал поддерживает до toothree, одновременно выполняемых события, поэтому можно создавать несколько архивов hello того же входящего потока.</span><span class="sxs-lookup"><span data-stu-id="55cd1-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="55cd1-156">Это позволяет toopublish и архивировать разные части события при необходимости.</span><span class="sxs-lookup"><span data-stu-id="55cd1-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="55cd1-157">Например ваших бизнес-требований — tooarchive 6-часовой программы, но toobroadcast только последние 10 минут.</span><span class="sxs-lookup"><span data-stu-id="55cd1-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="55cd1-158">tooaccomplish это, необходимо toocreate две параллельно выполняющиеся программы.</span><span class="sxs-lookup"><span data-stu-id="55cd1-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="55cd1-159">Одна программа установлено tooarchive 6 часов hello события, но программа hello не публикуется.</span><span class="sxs-lookup"><span data-stu-id="55cd1-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="55cd1-160">Hello программа не tooarchive набор на 10 минут и публикации этой программы.</span><span class="sxs-lookup"><span data-stu-id="55cd1-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="55cd1-161">Не следует использовать имеющиеся интерактивные события повторно.</span><span class="sxs-lookup"><span data-stu-id="55cd1-161">You should not reuse existing live events.</span></span> <span data-ttu-id="55cd1-162">Вместо этого создайте и запустите новое событие для каждого события.</span><span class="sxs-lookup"><span data-stu-id="55cd1-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="55cd1-163">Начальное событие hello при готовности toostart потоковой передачи и архивированию.</span><span class="sxs-lookup"><span data-stu-id="55cd1-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="55cd1-164">Остановите программу hello, когда захотите toostop потоковую передачу и архивировать событие hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="55cd1-165">toodelete архивировать содержимое, остановить и удалить событие hello и затем удалите связанный ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="55cd1-166">Актив нельзя удалить, если он используется в событии; Сначала необходимо удалить событие Hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="55cd1-167">Даже после остановки и удаления событий hello, hello пользователей будет доступ toostream заархивированный контент как видео по запросу, до тех пор, пока вы не удалите hello активов.</span><span class="sxs-lookup"><span data-stu-id="55cd1-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="55cd1-168">Если вы хотите архивировать hello tooretain содержимого, но не было доступно для потоковой передачи, удалите hello потоковой передачи указателя.</span><span class="sxs-lookup"><span data-stu-id="55cd1-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="55cd1-169">toouse hello портала toocreate канала</span><span class="sxs-lookup"><span data-stu-id="55cd1-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="55cd1-170">В этом разделе показано, как toouse hello **быстрое создание** параметр toocreate к серверу каналов.</span><span class="sxs-lookup"><span data-stu-id="55cd1-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="55cd1-171">Дополнительные сведения об этих каналах см. в статье [Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="55cd1-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="55cd1-172">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="55cd1-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="55cd1-173">В hello **параметры** окно, нажмите кнопку **Live streaming**.</span><span class="sxs-lookup"><span data-stu-id="55cd1-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Приступая к работе](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="55cd1-175">Hello **потоковой трансляции** появится окно.</span><span class="sxs-lookup"><span data-stu-id="55cd1-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="55cd1-176">Нажмите кнопку **быстрое создание** toocreate сквозной канал с hello RTMP приема протокола.</span><span class="sxs-lookup"><span data-stu-id="55cd1-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="55cd1-177">Hello **создать новый канал** появится окно.</span><span class="sxs-lookup"><span data-stu-id="55cd1-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="55cd1-178">Присвойте имя новому каналу hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="55cd1-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="55cd1-179">Это создает канал к серверу с hello RTMP приема протокола.</span><span class="sxs-lookup"><span data-stu-id="55cd1-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="55cd1-180">Создание событий</span><span class="sxs-lookup"><span data-stu-id="55cd1-180">Create events</span></span>
1. <span data-ttu-id="55cd1-181">Выберите канал toowhich, требуется tooadd события.</span><span class="sxs-lookup"><span data-stu-id="55cd1-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="55cd1-182">Нажмите кнопку **Интерактивное событие** .</span><span class="sxs-lookup"><span data-stu-id="55cd1-182">Press **Live Event** button.</span></span>

![Событие](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="55cd1-184">Получение URL-адресов приема</span><span class="sxs-lookup"><span data-stu-id="55cd1-184">Get ingest URLs</span></span>
<span data-ttu-id="55cd1-185">После создания канала hello, вы можете получить URL-адреса, которые предоставят toohello динамического кодировщика приема.</span><span class="sxs-lookup"><span data-stu-id="55cd1-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="55cd1-186">кодировщик Hello использует эти URL-адреса tooinput обновляющегося потока.</span><span class="sxs-lookup"><span data-stu-id="55cd1-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Создано](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="55cd1-188">Событие hello Контрольное значение</span><span class="sxs-lookup"><span data-stu-id="55cd1-188">Watch hello event</span></span>
<span data-ttu-id="55cd1-189">событие toowatch hello, нажмите кнопку **Контрольные значения** в hello Azure hello портала или Копировать URL-адрес потоковой передачи и использовать проигрыватель, по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="55cd1-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Создано](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="55cd1-191">Трансляция автоматически получают tooon запросу преобразованное содержимое при остановке.</span><span class="sxs-lookup"><span data-stu-id="55cd1-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="55cd1-192">Очистка</span><span class="sxs-lookup"><span data-stu-id="55cd1-192">Clean up</span></span>
<span data-ttu-id="55cd1-193">Дополнительные сведения об этих каналах см. в статье [Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="55cd1-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="55cd1-194">Канал может быть остановлен только в том случае, если были остановлены все события или программы на канале hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="55cd1-195">После остановки канала hello, она не создает все расходы.</span><span class="sxs-lookup"><span data-stu-id="55cd1-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="55cd1-196">При необходимости toostart его снова, она будет иметь hello же приема URL-адрес, устраняя необходимость tooreconfigure кодировщика.</span><span class="sxs-lookup"><span data-stu-id="55cd1-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="55cd1-197">Канал можно удалить только в том случае, если были удалены все динамической события в канале hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="55cd1-198">Просмотр архивного содержимого</span><span class="sxs-lookup"><span data-stu-id="55cd1-198">View archived content</span></span>
<span data-ttu-id="55cd1-199">Даже после остановки и удаления событий hello, hello пользователей будет доступ toostream заархивированный контент как видео по запросу, до тех пор, пока вы не удалите hello активов.</span><span class="sxs-lookup"><span data-stu-id="55cd1-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="55cd1-200">Актив нельзя удалить, если он используется в событии; Сначала необходимо удалить событие Hello.</span><span class="sxs-lookup"><span data-stu-id="55cd1-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="55cd1-201">Выберите Ваши активы toomanage **параметр** и нажмите кнопку **активы**.</span><span class="sxs-lookup"><span data-stu-id="55cd1-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Активы](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="55cd1-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55cd1-203">Next step</span></span>
<span data-ttu-id="55cd1-204">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="55cd1-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="55cd1-205">Отзывы</span><span class="sxs-lookup"><span data-stu-id="55cd1-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

