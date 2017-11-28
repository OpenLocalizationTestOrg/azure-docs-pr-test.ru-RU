---
title: "Потоковая трансляция с помощью локальных кодировщиков c использованием портала Azure | Документация Майкрософт"
description: "В этом руководстве рассматривается создание канала, настроенного для сквозной доставки."
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
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="f30d3-103">Потоковая трансляция с помощью локальных кодировщиков c использованием портала Azure</span><span class="sxs-lookup"><span data-stu-id="f30d3-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f30d3-104">Портал</span><span class="sxs-lookup"><span data-stu-id="f30d3-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="f30d3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f30d3-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="f30d3-106">REST</span><span class="sxs-lookup"><span data-stu-id="f30d3-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="f30d3-107">В этом руководстве рассматривается создание **канала** , настроенного для сквозной доставки, с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="f30d3-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f30d3-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f30d3-108">Prerequisites</span></span>
<span data-ttu-id="f30d3-109">Ниже перечислены необходимые условия для выполнения действий, описанных в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f30d3-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="f30d3-110">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f30d3-110">An Azure account.</span></span> <span data-ttu-id="f30d3-111">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f30d3-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="f30d3-112">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f30d3-112">A Media Services account.</span></span> <span data-ttu-id="f30d3-113">Инструкции по созданию учетной записи служб мультимедиа см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f30d3-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="f30d3-114">Веб-камера,</span><span class="sxs-lookup"><span data-stu-id="f30d3-114">A webcam.</span></span> <span data-ttu-id="f30d3-115">например [кодировщик Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="f30d3-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="f30d3-116">Настоятельно рекомендуется ознакомиться со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="f30d3-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="f30d3-117">Поддержка протокола RTMP службами мультимедиа Azure и динамические кодировщики</span><span class="sxs-lookup"><span data-stu-id="f30d3-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="f30d3-118">Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="f30d3-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="f30d3-119">Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями</span><span class="sxs-lookup"><span data-stu-id="f30d3-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="f30d3-120"><a id="scenario"></a>Стандартный сценарий потоковой передачи в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="f30d3-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="f30d3-121">Далее описаны задачи, связанные с созданием стандартных приложений для потоковой трансляции, которые используют каналы, настроенные для сквозной доставки.</span><span class="sxs-lookup"><span data-stu-id="f30d3-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="f30d3-122">В этом руководстве показано, как создавать сквозные каналы и интерактивные события, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="f30d3-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="f30d3-123">Убедитесь, что конечная точка потоковой передачи, из которой нужно передавать содержимое потоком, находится в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="f30d3-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="f30d3-124">Подключите видеокамеру к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="f30d3-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="f30d3-125">Запустите и настройте локальный динамический кодировщик, который выводит поток с разными скоростями RTMP или фрагментированный поток MP4.</span><span class="sxs-lookup"><span data-stu-id="f30d3-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="f30d3-126">Дополнительные сведения см. в статье о [поддержке протокола RTMP в службах мультимедиа Azure и о динамических кодировщиках](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="f30d3-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="f30d3-127">Это действие также можно выполнить после создания канала.</span><span class="sxs-lookup"><span data-stu-id="f30d3-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="f30d3-128">Создайте и запустите сквозной канал.</span><span class="sxs-lookup"><span data-stu-id="f30d3-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="f30d3-129">Получите URL-адрес приема канала.</span><span class="sxs-lookup"><span data-stu-id="f30d3-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="f30d3-130">URL-адрес приема используется динамическим кодировщиком для отправки потока в канал.</span><span class="sxs-lookup"><span data-stu-id="f30d3-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="f30d3-131">Получите URL-адрес предварительного просмотра канала.</span><span class="sxs-lookup"><span data-stu-id="f30d3-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="f30d3-132">С его помощью можно убедиться в том, что канал надлежащим образом получает поток.</span><span class="sxs-lookup"><span data-stu-id="f30d3-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="f30d3-133">Создайте интерактивное событие или программу.</span><span class="sxs-lookup"><span data-stu-id="f30d3-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="f30d3-134">Если вы используете портал Azure, при создании интерактивного события также создается ресурс.</span><span class="sxs-lookup"><span data-stu-id="f30d3-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="f30d3-135">Когда вы будете готовы начать потоковую передачу и архивацию, запустите событие или программу.</span><span class="sxs-lookup"><span data-stu-id="f30d3-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="f30d3-136">При необходимости динамическому кодировщику можно дать сигнал начать показ рекламы.</span><span class="sxs-lookup"><span data-stu-id="f30d3-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="f30d3-137">Реклама вставляется в выходной поток.</span><span class="sxs-lookup"><span data-stu-id="f30d3-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="f30d3-138">Чтобы остановить потоковую передачу и архивацию содержимого события, завершите работу события или программы.</span><span class="sxs-lookup"><span data-stu-id="f30d3-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="f30d3-139">Удалите событие или программу (и при необходимости ресурс).</span><span class="sxs-lookup"><span data-stu-id="f30d3-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="f30d3-140">Основные понятия и рекомендации, связанные с потоковой трансляцией с помощью локальных кодировщиков и сквозных каналов, см. в статье [Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="f30d3-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="f30d3-141">Просмотр уведомлений и сообщений об ошибках</span><span class="sxs-lookup"><span data-stu-id="f30d3-141">To view notifications and errors</span></span>
<span data-ttu-id="f30d3-142">Чтобы просмотреть уведомления и ошибки на портале Azure, щелкните значок уведомления.</span><span class="sxs-lookup"><span data-stu-id="f30d3-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Уведомления](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="f30d3-144">Создание и запуск сквозных каналов и событий</span><span class="sxs-lookup"><span data-stu-id="f30d3-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="f30d3-145">Канал связан с событиями и программами, с помощью которых вы можете управлять публикацией и хранением сегментов динамического потока.</span><span class="sxs-lookup"><span data-stu-id="f30d3-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="f30d3-146">Каналы управляют событиями.</span><span class="sxs-lookup"><span data-stu-id="f30d3-146">Channels manage events.</span></span> 

<span data-ttu-id="f30d3-147">Задать количество часов, в течение которых следует хранить записанное содержимое программы, можно с помощью параметра длины **окна архивирования** .</span><span class="sxs-lookup"><span data-stu-id="f30d3-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="f30d3-148">Для него можно задать значение от 5 минут до 25 часов.</span><span class="sxs-lookup"><span data-stu-id="f30d3-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="f30d3-149">Длина окна архивирования также определяет максимальный период, в пределах которого клиенты могут перемещаться назад во времени относительно текущей позиции в передаваемом потоке данных.</span><span class="sxs-lookup"><span data-stu-id="f30d3-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="f30d3-150">События могут происходить в течение определенного времени, однако содержимое, выходящее за пределы этого периода, теряется.</span><span class="sxs-lookup"><span data-stu-id="f30d3-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="f30d3-151">Значение этого свойства также определяет максимальный размер манифестов клиентов.</span><span class="sxs-lookup"><span data-stu-id="f30d3-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="f30d3-152">Каждое событие связано с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="f30d3-152">Each event is associated with an asset.</span></span> <span data-ttu-id="f30d3-153">Чтобы опубликовать событие, необходимо создать указатель OnDemand для соответствующего ресурса.</span><span class="sxs-lookup"><span data-stu-id="f30d3-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="f30d3-154">С помощью этого указателя можно сформировать URL-адрес потоковой передачи данных, который предоставляется клиентам.</span><span class="sxs-lookup"><span data-stu-id="f30d3-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="f30d3-155">Канал поддерживает одновременную потоковую трансляцию максимум трех событий, поэтому можно создавать по несколько архивов одного и того же входящего потока.</span><span class="sxs-lookup"><span data-stu-id="f30d3-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="f30d3-156">Благодаря этому можно публиковать и архивировать разные части транслируемого мероприятия.</span><span class="sxs-lookup"><span data-stu-id="f30d3-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="f30d3-157">Например ваш бизнес-требование — архивировать 6 часов программы, но для передачи только оставить последние 10 минут.</span><span class="sxs-lookup"><span data-stu-id="f30d3-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="f30d3-158">Для этого необходимо создать две одновременно работающие программы.</span><span class="sxs-lookup"><span data-stu-id="f30d3-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="f30d3-159">Для одной из них настроено архивирование 6 часов транслируемого мероприятия, но без публикации.</span><span class="sxs-lookup"><span data-stu-id="f30d3-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="f30d3-160">Для второй программы настроено архивирование 10 минут с публикацией.</span><span class="sxs-lookup"><span data-stu-id="f30d3-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="f30d3-161">Не следует использовать имеющиеся интерактивные события повторно.</span><span class="sxs-lookup"><span data-stu-id="f30d3-161">You should not reuse existing live events.</span></span> <span data-ttu-id="f30d3-162">Вместо этого создайте и запустите новое событие для каждого события.</span><span class="sxs-lookup"><span data-stu-id="f30d3-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="f30d3-163">Когда вы будете готовы начать потоковую передачу и архивацию, запустите событие.</span><span class="sxs-lookup"><span data-stu-id="f30d3-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="f30d3-164">Чтобы остановить потоковую передачу и архивацию содержимого мероприятия, завершите работу программы.</span><span class="sxs-lookup"><span data-stu-id="f30d3-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="f30d3-165">Чтобы удалить архивированное содержимое, остановите и удалите событие, а затем удалите связанный с ним ресурс.</span><span class="sxs-lookup"><span data-stu-id="f30d3-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="f30d3-166">Ресурс невозможно удалить, пока он используется каким-либо событием: сначала нужно удалить это событие.</span><span class="sxs-lookup"><span data-stu-id="f30d3-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="f30d3-167">Даже после остановки и удаления события пользователи смогут запрашивать потоковую передачу архивированного видеосодержимого, пока не удален соответствующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="f30d3-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="f30d3-168">Если вы хотите сохранить заархивированное содержимое, но при этом заблокировать возможность его потоковой передачи, удалите указатель.</span><span class="sxs-lookup"><span data-stu-id="f30d3-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="f30d3-169">Создание канала с помощью портала</span><span class="sxs-lookup"><span data-stu-id="f30d3-169">To use the portal to create a channel</span></span>
<span data-ttu-id="f30d3-170">В этом разделе показано, как использовать функцию **Быстрое создание** для создания сквозного канала.</span><span class="sxs-lookup"><span data-stu-id="f30d3-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="f30d3-171">Дополнительные сведения об этих каналах см. в статье [Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="f30d3-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="f30d3-172">Создание учетной записи служб мультимедиа Azure с помощью [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f30d3-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f30d3-173">В окне **Параметры** щелкните элемент **Потоковая трансляция**.</span><span class="sxs-lookup"><span data-stu-id="f30d3-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Приступая к работе](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="f30d3-175">Появится окно **Live streaming** (Потоковая трансляция).</span><span class="sxs-lookup"><span data-stu-id="f30d3-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="f30d3-176">Щелкните элемент **Быстрое создание** , чтобы создать сквозной канал с протоколом приема RTMP.</span><span class="sxs-lookup"><span data-stu-id="f30d3-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="f30d3-177">Появится окно **CREATE A NEW CHANNEL** (СОЗДАНИЕ КАНАЛА).</span><span class="sxs-lookup"><span data-stu-id="f30d3-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="f30d3-178">Присвойте имя новому каналу и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f30d3-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="f30d3-179">После этого будет создан сквозной канал с протоколом приема RTMP.</span><span class="sxs-lookup"><span data-stu-id="f30d3-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="f30d3-180">Создание событий</span><span class="sxs-lookup"><span data-stu-id="f30d3-180">Create events</span></span>
1. <span data-ttu-id="f30d3-181">Выберите канал, в который нужно добавить событие.</span><span class="sxs-lookup"><span data-stu-id="f30d3-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="f30d3-182">Нажмите кнопку **Интерактивное событие** .</span><span class="sxs-lookup"><span data-stu-id="f30d3-182">Press **Live Event** button.</span></span>

![Событие](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="f30d3-184">Получение URL-адресов приема</span><span class="sxs-lookup"><span data-stu-id="f30d3-184">Get ingest URLs</span></span>
<span data-ttu-id="f30d3-185">После создания канала можно получить URL-адреса приема, которые необходимо передать динамическому кодировщику.</span><span class="sxs-lookup"><span data-stu-id="f30d3-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="f30d3-186">Он использует эти адреса для передачи динамического потока на вход.</span><span class="sxs-lookup"><span data-stu-id="f30d3-186">The encoder uses these URLs to input a live stream.</span></span>

![Создано](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="f30d3-188">Просмотр события</span><span class="sxs-lookup"><span data-stu-id="f30d3-188">Watch the event</span></span>
<span data-ttu-id="f30d3-189">Чтобы просмотреть событие, щелкните **Посмотреть** на портале Azure или скопируйте URL-адрес потоковой передачи и используйте проигрыватель по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="f30d3-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Создано](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="f30d3-191">После остановки интерактивное событие автоматически преобразуется в содержимое по запросу.</span><span class="sxs-lookup"><span data-stu-id="f30d3-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="f30d3-192">Очистка</span><span class="sxs-lookup"><span data-stu-id="f30d3-192">Clean up</span></span>
<span data-ttu-id="f30d3-193">Дополнительные сведения об этих каналах см. в статье [Потоковая трансляция с помощью локальных кодировщиков, создающих потоки с разными скоростями](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="f30d3-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="f30d3-194">Канал можно остановить, только если все передаваемые по нему события и программы остановлены.</span><span class="sxs-lookup"><span data-stu-id="f30d3-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="f30d3-195">После остановки канала начисление платы прекращается.</span><span class="sxs-lookup"><span data-stu-id="f30d3-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="f30d3-196">Если вам понадобится снова запустить его, вы можете воспользоваться тем же URL-адресом приема (перенастраивать кодировщик не потребуется).</span><span class="sxs-lookup"><span data-stu-id="f30d3-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="f30d3-197">Канал можно удалить, только если все передаваемые по нему интерактивные события удалены.</span><span class="sxs-lookup"><span data-stu-id="f30d3-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="f30d3-198">Просмотр архивного содержимого</span><span class="sxs-lookup"><span data-stu-id="f30d3-198">View archived content</span></span>
<span data-ttu-id="f30d3-199">Даже после остановки и удаления события пользователи смогут запрашивать потоковую передачу архивированного видеосодержимого, пока не удален соответствующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="f30d3-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="f30d3-200">Ресурс невозможно удалить, пока он используется каким-либо событием: сначала нужно удалить это событие.</span><span class="sxs-lookup"><span data-stu-id="f30d3-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="f30d3-201">Для управления ресурсами последовательно выберите **Параметры** и **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="f30d3-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![ресурсы](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="f30d3-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f30d3-203">Next step</span></span>
<span data-ttu-id="f30d3-204">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f30d3-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f30d3-205">Отзывы</span><span class="sxs-lookup"><span data-stu-id="f30d3-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

