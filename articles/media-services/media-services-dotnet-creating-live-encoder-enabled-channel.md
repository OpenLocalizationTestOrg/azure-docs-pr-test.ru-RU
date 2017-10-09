---
title: "aaaHow tooperform потоковой трансляции с помощью служб мультимедиа Azure toocreate многоскоростной потоков в .NET Framework | Документы Microsoft"
description: "Этот учебник последовательно по hello этапы создания канала, получает один-динамический поток и кодирует его toomulti потока с помощью пакета SDK для .NET."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 4df5e690-ff63-47cc-879b-9c57cb8ec240
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 22088e6a78a49bd839575614a7c17a411ae8081c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-net"></a><span data-ttu-id="216c2-103">Как потоки tooperform потоковой трансляции с помощью служб мультимедиа Azure toocreate с несколькими скоростями в .NET Framework</span><span class="sxs-lookup"><span data-stu-id="216c2-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="216c2-104">Портал</span><span class="sxs-lookup"><span data-stu-id="216c2-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="216c2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="216c2-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="216c2-106">REST API</span><span class="sxs-lookup"><span data-stu-id="216c2-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> [!NOTE]
> <span data-ttu-id="216c2-107">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="216c2-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="216c2-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="216c2-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="216c2-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="216c2-109">Overview</span></span>
<span data-ttu-id="216c2-110">Этот учебник поможет выполнить этапы создания hello **канала** , получающее обновляющегося потока одним скоростью и кодирует его toomulti потока.</span><span class="sxs-lookup"><span data-stu-id="216c2-110">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

<span data-ttu-id="216c2-111">Для получения более подробных сведений см. связанные tooChannels, которые включены для динамического кодирования [потоковой трансляции с помощью служб мультимедиа Azure toocreate многоскоростной потоков](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="216c2-111">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="216c2-112">Стандартный сценарий потоковой передачи в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="216c2-112">Common Live Streaming Scenario</span></span>
<span data-ttu-id="216c2-113">Привет, следующие шаги описывают задачи, связанные с созданием общих приложений потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="216c2-113">hello following steps describe tasks involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="216c2-114">В настоящее время hello max рекомендуется длительность динамической события — 8 часов.</span><span class="sxs-lookup"><span data-stu-id="216c2-114">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="216c2-115">Если вам требуется toorun канала для более длительного времени, обратитесь в службу amslived сайте Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="216c2-115">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="216c2-116">Подключение компьютера tooa камеры.</span><span class="sxs-lookup"><span data-stu-id="216c2-116">Connect a video camera tooa computer.</span></span> <span data-ttu-id="216c2-117">Запустить и настроить на локальный динамический кодировщик, может выводить односкоростной поток в одном из следующих протоколов hello: RTMP, Smooth Streaming или RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="216c2-117">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="216c2-118">Дополнительные сведения см. в статье о [поддержке протокола RTMP в службах мультимедиа Azure и о динамических кодировщиках](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="216c2-118">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>

    <span data-ttu-id="216c2-119">Это действие также можно выполнить после создания канала.</span><span class="sxs-lookup"><span data-stu-id="216c2-119">This step could also be performed after you create your Channel.</span></span>

2. <span data-ttu-id="216c2-120">Создайте и запустите канал.</span><span class="sxs-lookup"><span data-stu-id="216c2-120">Create and start a Channel.</span></span>
3. <span data-ttu-id="216c2-121">Получение hello канал приема URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="216c2-121">Retrieve hello Channel ingest URL.</span></span>

    <span data-ttu-id="216c2-122">URL-адрес приема Hello используется toohello hello динамического кодировщика toosend hello потока канала.</span><span class="sxs-lookup"><span data-stu-id="216c2-122">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>

4. <span data-ttu-id="216c2-123">Получить URL-адрес предварительного просмотра канала hello.</span><span class="sxs-lookup"><span data-stu-id="216c2-123">Retrieve hello Channel preview URL.</span></span>

    <span data-ttu-id="216c2-124">Используйте этот URL-адрес tooverify, что ваш канал правильно получает hello обновляющегося потока.</span><span class="sxs-lookup"><span data-stu-id="216c2-124">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>

5. <span data-ttu-id="216c2-125">Создайте ресурс.</span><span class="sxs-lookup"><span data-stu-id="216c2-125">Create an asset.</span></span>
6. <span data-ttu-id="216c2-126">Если требуется для шифрования динамически во время воспроизведения toobe активов hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="216c2-126">If you want for hello asset toobe dynamically encrypted during playback, do hello following:</span></span>
7. <span data-ttu-id="216c2-127">Создайте ключ содержимого.</span><span class="sxs-lookup"><span data-stu-id="216c2-127">Create a content key.</span></span>
8. <span data-ttu-id="216c2-128">Настройка политики авторизации hello ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="216c2-128">Configure hello content key's authorization policy.</span></span>
9. <span data-ttu-id="216c2-129">Настройте политику передачи ресурсов (она используется средствами динамической упаковки и шифрования).</span><span class="sxs-lookup"><span data-stu-id="216c2-129">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
10. <span data-ttu-id="216c2-130">Создание программы и укажите toouse hello актива, который был создан.</span><span class="sxs-lookup"><span data-stu-id="216c2-130">Create a program and specify toouse hello asset that you created.</span></span>
11. <span data-ttu-id="216c2-131">Опубликуйте актив hello, связанный с программой hello путем создания указателя по запросу.</span><span class="sxs-lookup"><span data-stu-id="216c2-131">Publish hello asset associated with hello program by creating an OnDemand locator.</span></span>

    >[!NOTE]
    ><span data-ttu-id="216c2-132">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="216c2-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="216c2-133">Привет, из которого нужно toostream содержимое конечной точки потоковой передачи имеет toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="216c2-133">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

12. <span data-ttu-id="216c2-134">Запуск программы hello, при готовности toostart потоковой передачи и архивированию.</span><span class="sxs-lookup"><span data-stu-id="216c2-134">Start hello program when you are ready toostart streaming and archiving.</span></span>
13. <span data-ttu-id="216c2-135">При необходимости hello динамическому кодировщику можно сигнальное toostart объявления.</span><span class="sxs-lookup"><span data-stu-id="216c2-135">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="216c2-136">объявления Hello вставляется в выходной поток hello.</span><span class="sxs-lookup"><span data-stu-id="216c2-136">hello advertisement is inserted in hello output stream.</span></span>
14. <span data-ttu-id="216c2-137">Остановите программу hello, когда захотите toostop потоковую передачу и архивировать событие hello.</span><span class="sxs-lookup"><span data-stu-id="216c2-137">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span>
15. <span data-ttu-id="216c2-138">Удалите hello программы (и при необходимости удалить средство hello).</span><span class="sxs-lookup"><span data-stu-id="216c2-138">Delete hello Program (and optionally delete hello asset).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="216c2-139">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="216c2-139">What you'll learn</span></span>
<span data-ttu-id="216c2-140">В этом разделе показано, как tooexecute различные операции с каналами и программами, с помощью пакета SDK .NET служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="216c2-140">This topic shows you how tooexecute different operations on channels and programs using Media Services .NET SDK.</span></span> <span data-ttu-id="216c2-141">Поскольку многие операции являются длительными, используются API-интерфейсы .NET, предназначенные для управления длительными операциями.</span><span class="sxs-lookup"><span data-stu-id="216c2-141">Because many operations are long-running .NET APIs that manage long running operations are used.</span></span>

<span data-ttu-id="216c2-142">Здравствуйте разделе показано как toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="216c2-142">hello topic shows how toodo hello following:</span></span>

1. <span data-ttu-id="216c2-143">Создайте и запустите канал.</span><span class="sxs-lookup"><span data-stu-id="216c2-143">Create and start a channel.</span></span> <span data-ttu-id="216c2-144">Используются API для длительных операций.</span><span class="sxs-lookup"><span data-stu-id="216c2-144">Long-running APIs are used.</span></span>
2. <span data-ttu-id="216c2-145">Получение каналов hello приема (input) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="216c2-145">Get hello channels ingest (input) endpoint.</span></span> <span data-ttu-id="216c2-146">Эта конечная точка предоставляется toohello кодировщик, который можно отправить односкоростного динамического потока.</span><span class="sxs-lookup"><span data-stu-id="216c2-146">This endpoint should be provided toohello encoder that can send a single bitrate live stream.</span></span>
3. <span data-ttu-id="216c2-147">Получите конечную точку предварительного просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="216c2-147">Get hello preview endpoint.</span></span> <span data-ttu-id="216c2-148">Эта конечная точка является используется toopreview потока.</span><span class="sxs-lookup"><span data-stu-id="216c2-148">This endpoint is used toopreview your stream.</span></span>
4. <span data-ttu-id="216c2-149">Создайте актив, который будет использоваться toostore контента.</span><span class="sxs-lookup"><span data-stu-id="216c2-149">Create an asset that will be used toostore your content.</span></span> <span data-ttu-id="216c2-150">политики доставки активов Hello должны быть настроены так, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="216c2-150">hello asset delivery policies should be configured as well, as shown in this example.</span></span>
5. <span data-ttu-id="216c2-151">Создание программы и укажите toouse hello актива, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="216c2-151">Create a program and specify toouse hello asset that was created earlier.</span></span> <span data-ttu-id="216c2-152">Запуск программы hello.</span><span class="sxs-lookup"><span data-stu-id="216c2-152">Start hello program.</span></span> <span data-ttu-id="216c2-153">Используются API для длительных операций.</span><span class="sxs-lookup"><span data-stu-id="216c2-153">Long-running APIs are used.</span></span>
6. <span data-ttu-id="216c2-154">Создает указатель для средства hello, поэтому содержимое hello публикуемых и может передаваться tooyour клиентов.</span><span class="sxs-lookup"><span data-stu-id="216c2-154">Create a locator for hello asset, so hello content gets published and can be streamed tooyour clients.</span></span>
7. <span data-ttu-id="216c2-155">Показ и скрытие планшетов.</span><span class="sxs-lookup"><span data-stu-id="216c2-155">Show and hide slates.</span></span> <span data-ttu-id="216c2-156">Запуск и остановка объявления.</span><span class="sxs-lookup"><span data-stu-id="216c2-156">Start and stop advertisements.</span></span> <span data-ttu-id="216c2-157">Используются API для длительных операций.</span><span class="sxs-lookup"><span data-stu-id="216c2-157">Long-running APIs are used.</span></span>
8. <span data-ttu-id="216c2-158">Очистить канал и Здравствуйте, все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="216c2-158">Clean up your channel and all hello associated resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="216c2-159">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="216c2-159">Prerequisites</span></span>
<span data-ttu-id="216c2-160">Здесь представлены Hello учебника требуется toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="216c2-160">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="216c2-161">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="216c2-161">An Azure account.</span></span> <span data-ttu-id="216c2-162">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="216c2-162">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="216c2-163">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="216c2-163">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="216c2-164">Вы получаете кредиты, которые могут быть используется tootry out платных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="216c2-164">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="216c2-165">Даже после израсходования кредитов hello, можно защитить учетную запись hello и использования бесплатной службы Azure и функции, такие как функции hello веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="216c2-165">Even after hello credits are used up, you can keep hello account and use free Azure services and features, such as hello Web Apps feature in Azure App Service.</span></span>
* <span data-ttu-id="216c2-166">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="216c2-166">A Media Services account.</span></span> <span data-ttu-id="216c2-167">toocreate учетную запись служб носителей в разделе [Создание учетной записи](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="216c2-167">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="216c2-168">Visual Studio 2010 с пакетом обновления 1 (SP1) (Professional, Premium, Ultimate или Express) или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="216c2-168">Visual Studio 2010 SP1 (Professional, Premium, Ultimate, or Express) or later versions.</span></span>
* <span data-ttu-id="216c2-169">Вам нужно использовать пакет SDK служб мультимедиа для .NET 3.2.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="216c2-169">You must use Media Services .NET SDK version 3.2.0.0 or newer.</span></span>
* <span data-ttu-id="216c2-170">Веб-камера и кодировщик, который передает динамический односкоростной поток данных.</span><span class="sxs-lookup"><span data-stu-id="216c2-170">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="considerations"></a><span data-ttu-id="216c2-171">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="216c2-171">Considerations</span></span>
* <span data-ttu-id="216c2-172">В настоящее время hello max рекомендуется длительность динамической события — 8 часов.</span><span class="sxs-lookup"><span data-stu-id="216c2-172">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="216c2-173">Если вам требуется toorun канала для более длительного времени, обратитесь в службу amslived сайте Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="216c2-173">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="216c2-174">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="216c2-174">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="216c2-175">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="216c2-175">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="216c2-176">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="216c2-176">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="download-sample"></a><span data-ttu-id="216c2-177">Скачивание образца</span><span class="sxs-lookup"><span data-stu-id="216c2-177">Download sample</span></span>

<span data-ttu-id="216c2-178">Вы можете загрузить пример hello, описанное в этом разделе из [здесь](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span><span class="sxs-lookup"><span data-stu-id="216c2-178">You can download hello sample that is described in this topic from [here](https://azure.microsoft.com/documentation/samples/media-services-dotnet-encode-live-stream-with-ams-clear/).</span></span>

## <a name="set-up-for-development-with-media-services-sdk-for-net"></a><span data-ttu-id="216c2-179">Подготовка к работе с использованием пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="216c2-179">Set up for development with Media Services SDK for .NET</span></span>

<span data-ttu-id="216c2-180">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="216c2-180">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="code-example"></a><span data-ttu-id="216c2-181">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="216c2-181">Code example</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Net;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace EncodeLiveStreamWithAmsClear
    {
        class Program
        {
        private const string ChannelName = "channel001";
        private const string AssetlName = "asset001";
        private const string ProgramlName = "program001";

        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            IChannel channel = CreateAndStartChannel();

            // hello channel's input endpoint:
            string ingestUrl = channel.Input.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Intest URL: {0}", ingestUrl);


            // Use hello previewEndpoint toopreview and verify 
            // that hello input from hello encoder is actually reaching hello Channel. 
            string previewEndpoint = channel.Preview.Endpoints.FirstOrDefault().Url.ToString();

            Console.WriteLine("Preview URL: {0}", previewEndpoint);

            // When Live Encoding is enabled, you can now get a preview of hello live feed as it reaches hello Channel. 
            // This can be a valuable tool toocheck whether your live feed is actually reaching hello Channel. 
            // hello thumbnail is exposed via hello same end-point as hello Channel Preview URL.
            string thumbnailUri = new UriBuilder
            {
            Scheme = Uri.UriSchemeHttps,
            Host = channel.Preview.Endpoints.FirstOrDefault().Url.Host,
            Path = "thumbnails/input.jpg"
            }.Uri.ToString();

            Console.WriteLine("Thumbain URL: {0}", thumbnailUri);

            // Once you previewed your stream and verified that it is flowing into your Channel, 
            // you can create an event by creating an Asset, Program, and Streaming Locator. 
            IAsset asset = CreateAndConfigureAsset();

            IProgram program = CreateAndStartProgram(channel, asset);

            ILocator locator = CreateLocatorForAsset(program.Asset, program.ArchiveWindowLength);

            // You can use slates and ads only if hello channel type is Standard.  
            StartStopAdsSlates(channel);

            // Once you are done streaming, clean up your resources.
            Cleanup(channel);
        }

        public static IChannel CreateAndStartChannel()
        {
            var channelInput = CreateChannelInput();
            var channePreview = CreateChannelPreview();
            var channelEncoding = CreateChannelEncoding();

            ChannelCreationOptions options = new ChannelCreationOptions
            {
            EncodingType = ChannelEncodingType.Standard,
            Name = ChannelName,
            Input = channelInput,
            Preview = channePreview,
            Encoding = channelEncoding
            };

            Log("Creating channel");
            IOperation channelCreateOperation = _context.Channels.SendCreateOperation(options);
            string channelId = TrackOperation(channelCreateOperation, "Channel create");

            IChannel channel = _context.Channels.Where(c => c.Id == channelId).FirstOrDefault();

            Log("Starting channel");
            var channelStartOperation = channel.SendStartOperation();
            TrackOperation(channelStartOperation, "Channel start");

            return channel;
        }

        /// <summary>
        /// Create channel input, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
            StreamingProtocol = StreamingProtocol.RTPMPEG2TS,
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelInput001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel preview, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
            AccessControl = new ChannelAccessControl
            {
                IPAllowList = new List<IPRange>
                {
                    new IPRange
                    {
                    Name = "TestChannelPreview001",
                    Address = IPAddress.Parse("0.0.0.0"),
                    SubnetPrefixLength = 0
                    }
                }
            }
            };
        }

        /// <summary>
        /// Create channel encoding, used in channel creation options. 
        /// </summary>
        /// <returns></returns>
        private static ChannelEncoding CreateChannelEncoding()
        {
            return new ChannelEncoding
            {
            SystemPreset = "Default720p",
            IgnoreCea708ClosedCaptions = false,
            AdMarkerSource = AdMarkerSource.Api,
            // You can only set audio if streaming protocol is set tooStreamingProtocol.RTPMPEG2TS.
            AudioStreams = new List<AudioStream> { new AudioStream { Index = 103, Language = "eng" } }.AsReadOnly()
            };
        }

        /// <summary>
        /// Create an asset and configure asset delivery policies.
        /// </summary>
        /// <returns></returns>
        public static IAsset CreateAndConfigureAsset()
        {
            IAsset asset = _context.Assets.Create(AssetlName, AssetCreationOptions.None);

            IAssetDeliveryPolicy policy =
            _context.AssetDeliveryPolicies.Create("Clear Policy",
            AssetDeliveryPolicyType.NoDynamicEncryption,
            AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);

            asset.DeliveryPolicies.Add(policy);

            return asset;
        }

        /// <summary>
        /// Create a Program on hello Channel. You can have multiple Programs that overlap or are sequential;
        /// however each Program must have a unique name within your Media Services account.
        /// </summary>
        /// <param name="channel"></param>
        /// <param name="asset"></param>
        /// <returns></returns>
        public static IProgram CreateAndStartProgram(IChannel channel, IAsset asset)
        {
            IProgram program = channel.Programs.Create(ProgramlName, TimeSpan.FromHours(3), asset.Id);
            Log("Program created", program.Id);

            Log("Starting program");
            var programStartOperation = program.SendStartOperation();
            TrackOperation(programStartOperation, "Program start");

            return program;
        }

        /// <summary>
        /// Create locators in order toobe able toopublish and stream hello video.
        /// </summary>
        /// <param name="asset"></param>
        /// <param name="ArchiveWindowLength"></param>
        /// <returns></returns>
        public static ILocator CreateLocatorForAsset(IAsset asset, TimeSpan ArchiveWindowLength)
        {
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            var locator = _context.Locators.CreateLocator
            (
                LocatorType.OnDemandOrigin,
                asset,
                _context.AccessPolicies.Create
                (
                    "Live Stream Policy",
                    ArchiveWindowLength,
                    AccessPermissions.Read
                )
            );

            return locator;
        }

        /// <summary>
        /// Perform operations on slates.
        /// </summary>
        /// <param name="channel"></param>
        public static void StartStopAdsSlates(IChannel channel)
        {
            int cueId = new Random().Next(int.MaxValue);
            var path = Path.GetFullPath(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\\..\\SlateJPG\\DefaultAzurePortalSlate.jpg"));

            Log("Creating asset");
            var slateAsset = _context.Assets.Create("Slate test asset " + DateTime.Now.ToString("yyyy-MM-dd HH-mm"), AssetCreationOptions.None);
            Log("Slate asset created", slateAsset.Id);

            Log("Uploading file");
            var assetFile = slateAsset.AssetFiles.Create("DefaultAzurePortalSlate.jpg");
            assetFile.Upload(path);
            assetFile.IsPrimary = true;
            assetFile.Update();

            Log("Showing slate");
            var showSlateOpeartion = channel.SendShowSlateOperation(TimeSpan.FromMinutes(1), slateAsset.Id);
            TrackOperation(showSlateOpeartion, "Show slate");

            Log("Hiding slate");
            var hideSlateOperation = channel.SendHideSlateOperation();
            TrackOperation(hideSlateOperation, "Hide slate");

            Log("Starting ad");
            var startAdOperation = channel.SendStartAdvertisementOperation(TimeSpan.FromMinutes(1), cueId, false);
            TrackOperation(startAdOperation, "Start ad");

            Log("Ending ad");
            var endAdOperation = channel.SendEndAdvertisementOperation(cueId);
            TrackOperation(endAdOperation, "End ad");

            Log("Deleting slate asset");
            slateAsset.Delete();
        }

        /// <summary>
        /// Clean up resources associated with hello channel.
        /// </summary>
        /// <param name="channel"></param>
        public static void Cleanup(IChannel channel)
        {
            IAsset asset;
            if (channel != null)
            {
            foreach (var program in channel.Programs)
            {
                asset = _context.Assets.Where(se => se.Id == program.AssetId)
                            .FirstOrDefault();

                Log("Stopping program");
                var programStopOperation = program.SendStopOperation();
                TrackOperation(programStopOperation, "Program stop");

                program.Delete();

                if (asset != null)
                {
                Log("Deleting locators");
                foreach (var l in asset.Locators)
                    l.Delete();

                Log("Deleting asset");
                asset.Delete();
                }
            }

            Log("Stopping channel");
            var channelStopOperation = channel.SendStopOperation();
            TrackOperation(channelStopOperation, "Channel stop");

            Log("Deleting channel");
            var channelDeleteOperation = channel.SendDeleteOperation();
            TrackOperation(channelDeleteOperation, "Channel delete");
            }
        }

        /// <summary>
        /// Track long running operations.
        /// </summary>
        /// <param name="operation"></param>
        /// <param name="description"></param>
        /// <returns></returns>
        public static string TrackOperation(IOperation operation, string description)
        {
            string entityId = null;
            bool isCompleted = false;

            Log("starting tootrack ", null, operation.Id);
            while (isCompleted == false)
            {
            operation = _context.Operations.GetOperation(operation.Id);
            isCompleted = IsCompleted(operation, out entityId);
            System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
            }
            // If we got here, hello operation succeeded.
            Log(description + " in completed", operation.TargetEntityId, operation.Id);

            return entityId;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created entity Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello entity Id associated with hello sucessful operation is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        private static bool IsCompleted(IOperation operation, out string entityId)
        {
            bool completed = false;

            entityId = null;

            switch (operation.State)
            {
            case OperationState.Failed:
                // Handle hello failure. 
                // For example, throw an exception. 
                // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                Log("operation failed", operation.TargetEntityId, operation.Id);
                break;
            case OperationState.Succeeded:
                completed = true;
                entityId = operation.TargetEntityId;
                break;
            case OperationState.InProgress:
                completed = false;
                Log("operation in progress", operation.TargetEntityId, operation.Id);
                break;
            }
            return completed;
        }

        private static void Log(string action, string entityId = null, string operationId = null)
        {
            Console.WriteLine(
            "{0,-21}{1,-51}{2,-51}{3,-51}",
            DateTime.Now.ToString("yyyy'-'MM'-'dd HH':'mm':'ss"),
            action,
            entityId ?? string.Empty,
            operationId ?? string.Empty);
        }
        }
    }

## <a name="next-step"></a><span data-ttu-id="216c2-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="216c2-182">Next step</span></span>
<span data-ttu-id="216c2-183">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="216c2-183">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="216c2-184">Отзывы</span><span class="sxs-lookup"><span data-stu-id="216c2-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


