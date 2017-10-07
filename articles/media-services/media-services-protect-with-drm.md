---
title: "aaaUsing PlayReady и/или Widevine динамического общее шифрование | Документы Microsoft"
description: "Службы мультимедиа Microsoft Azure позволяет вам toodeliver MPEG-DASH, Smooth Streaming и Http-Live-Streaming (HLS) потоки защищены с помощью Microsoft PlayReady DRM. Он также позволяет toodelivery зашифрован Widevine DRM ТИРЕ. В этом разделе показано, как зашифровать toodynamically с помощью PlayReady и Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="2833d-105">Использование общего динамического шифрования PlayReady и (или) Widevine DRM</span><span class="sxs-lookup"><span data-stu-id="2833d-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2833d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2833d-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="2833d-107">Java</span><span class="sxs-lookup"><span data-stu-id="2833d-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2833d-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2833d-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="2833d-109">Службы мультимедиа Microsoft Azure позволяет toodeliver MPEG-DASH, Smooth Streaming и HTTP-Live-Streaming (HLS) потоки, защищенные с помощью [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="2833d-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="2833d-110">Он также позволяет потоки ТИРЕ toodeliver зашифрованы с лицензии Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="2833d-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="2833d-111">PlayReady и Widevine шифруются на hello спецификации общее шифрование (CENC ISO/IEC 23001-7).</span><span class="sxs-lookup"><span data-stu-id="2833d-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="2833d-112">Можно использовать [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (начиная с версии hello 3.5.1) или REST API tooconfigure вашей AssetDeliveryConfiguration toouse Widevine.</span><span class="sxs-lookup"><span data-stu-id="2833d-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="2833d-113">Службы мультимедиа обеспечивают доставку лицензий PlayReady и DRM Widevine.</span><span class="sxs-lookup"><span data-stu-id="2833d-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="2833d-114">Службы мультимедиа также предоставляют интерфейсы API, позволяющие настроить hello права и ограничения, которые hello PlayReady или Widevine DRM среды выполнения tooenforce, в когда пользователь воспроизводит защищенное содержимое.</span><span class="sxs-lookup"><span data-stu-id="2833d-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="2833d-115">Когда пользователь запрашивает содержимое защищенного DRM, приложение hello-проигрыватель будет запрашивать лицензию из службы лицензий hello AMS.</span><span class="sxs-lookup"><span data-stu-id="2833d-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="2833d-116">Служба лицензий AMS Hello будет выдавать лицензии проигрыватель toohello ли он авторизован.</span><span class="sxs-lookup"><span data-stu-id="2833d-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="2833d-117">Лицензии PlayReady или Widevine содержит ключ расшифровки hello, который может использоваться hello клиента toodecrypt и поток hello содержимое проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="2833d-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="2833d-118">Можно также использовать следующие toohelp партнеров AMS доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="2833d-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="2833d-119">Дополнительные сведения см. в статьях, посвященных интеграции с [Axinom](media-services-axinom-integration.md) и [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="2833d-120">Службы мультимедиа поддерживают несколько способов авторизации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="2833d-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="2833d-121">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: открыть или маркер ограниченного использования программ.</span><span class="sxs-lookup"><span data-stu-id="2833d-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="2833d-122">политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS).</span><span class="sxs-lookup"><span data-stu-id="2833d-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="2833d-123">Службы мультимедиа поддерживают только токены в hello [токенов SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) формат (SWT) и [веб-маркера JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) формате.</span><span class="sxs-lookup"><span data-stu-id="2833d-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="2833d-124">Дополнительные сведения см. в разделе Настройка hello содержимого политики авторизации ключа.</span><span class="sxs-lookup"><span data-stu-id="2833d-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="2833d-125">преимущества tootake динамического шифрования требуется актив, содержащий набор MP4-файлов с разными скоростями или файлы источника Smooth Streaming с разными скоростями toohave.</span><span class="sxs-lookup"><span data-stu-id="2833d-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="2833d-126">Необходимо также tooconfigure hello доставки политик для средства hello (описывается далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="2833d-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="2833d-127">Затем на основании hello формат, указанный в URL-адрес потоковой передачи hello, hello сервера потоковой передачи по требованию проверит доставку потока hello в протоколе hello, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="2833d-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="2833d-128">В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать hello соответствующие HTTP-ответа на основе каждого запроса от клиента.</span><span class="sxs-lookup"><span data-stu-id="2833d-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="2833d-129">В этом разделе будет полезно toodevelopers, работы с приложениями, доставки мультимедиа, защищенные с помощью нескольких DRMs, например, PlayReady и Widevine.</span><span class="sxs-lookup"><span data-stu-id="2833d-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="2833d-130">Hello разделе показано, как tooconfigure hello службы доставки лицензий PlayReady с политиками авторизации, чтобы только авторизованные клиенты могли получать лицензии PlayReady или Widevine.</span><span class="sxs-lookup"><span data-stu-id="2833d-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="2833d-131">Здесь также показано, как шифрование toouse динамического шифрования с помощью PlayReady или DRM Widevine через дефис.</span><span class="sxs-lookup"><span data-stu-id="2833d-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="2833d-132">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="2833d-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="2833d-133">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="2833d-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="2833d-134">Скачивание образца</span><span class="sxs-lookup"><span data-stu-id="2833d-134">Download sample</span></span>
<span data-ttu-id="2833d-135">Вы можете загрузить пример hello, описанных в этой статье из [здесь](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="2833d-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="2833d-136">Настройка общего динамического шифрования и службы доставки лицензий DRM</span><span class="sxs-lookup"><span data-stu-id="2833d-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="2833d-137">Hello ниже приведены общие шаги, что tooperform понадобятся вам при защите ресурсов с помощью PlayReady, использовании службы доставки лицензий Media Services hello и использовании динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="2833d-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="2833d-138">Создание актива и отправка файлов в актив hello.</span><span class="sxs-lookup"><span data-stu-id="2833d-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="2833d-139">Кодирование hello активов содержащего hello файл toohello с адаптивной скоростью набор MP4.</span><span class="sxs-lookup"><span data-stu-id="2833d-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="2833d-140">Создание ключа контента и связать его с активом hello кодировке.</span><span class="sxs-lookup"><span data-stu-id="2833d-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="2833d-141">В службах мультимедиа ключ контента hello содержит ключ шифрования актива hello.</span><span class="sxs-lookup"><span data-stu-id="2833d-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="2833d-142">Настройка политики авторизации hello ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="2833d-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="2833d-143">Политика авторизации ключей содержимого Hello должно быть настроена вами и клиент hello, чтобы клиент доставленный toohello содержимого ключа toobe hello.</span><span class="sxs-lookup"><span data-stu-id="2833d-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="2833d-144">При создании политики авторизации ключа контента hello, необходимо следующее hello toospecify: метод (PlayReady или Widevine) ограничения доставки (open или маркер) и сведения о конкретных toohello доставки ключей тип, который определяет способ доставки ключа hello Клиент toohello ([PlayReady](media-services-playready-license-template-overview.md) или [Widevine](media-services-widevine-license-template-overview.md) шаблон лицензии).</span><span class="sxs-lookup"><span data-stu-id="2833d-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="2833d-145">Настройте политику hello доставки для актива.</span><span class="sxs-lookup"><span data-stu-id="2833d-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="2833d-146">Hello конфигурация политики доставки включает: тип динамического шифрования (например, общее шифрование), PlayReady или URL-адрес приобретения лицензии Widevine hello протокол доставки (например, MPEG DASH, HLS, Smooth Streaming или все).</span><span class="sxs-lookup"><span data-stu-id="2833d-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="2833d-147">Можно применить другой политике tooeach протокола на hello одного средства.</span><span class="sxs-lookup"><span data-stu-id="2833d-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="2833d-148">Например можно применить шифрование PlayReady tooSmooth/DASH и AES Envelope tooHLS.</span><span class="sxs-lookup"><span data-stu-id="2833d-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="2833d-149">Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="2833d-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="2833d-150">Hello toothis исключение — когда нет определенных политик доставки активов.</span><span class="sxs-lookup"><span data-stu-id="2833d-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="2833d-151">Затем все протоколы будут разрешены в hello снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="2833d-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="2833d-152">Создание указателя OnDemand в порядке tooget URL-адрес потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="2833d-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="2833d-153">Можно найти полный пример, в конце hello раздела hello .NET.</span><span class="sxs-lookup"><span data-stu-id="2833d-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="2833d-154">Следующие изображения Hello демонстрирует hello рабочего процесса, описанного выше.</span><span class="sxs-lookup"><span data-stu-id="2833d-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="2833d-155">Здесь hello маркер используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2833d-155">Here hello token is used for authentication.</span></span>

![Защита с помощью PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="2833d-157">Hello остальной части этого раздела содержатся подробные объяснения, примеры кода и tootopics ссылки, которые показывают, как tooachieve hello задач, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="2833d-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="2833d-158">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="2833d-158">Current limitations</span></span>
<span data-ttu-id="2833d-159">При добавлении или обновлении политики доставки активов необходимо удалить hello связанные указатель (если есть) и создать новый указатель.</span><span class="sxs-lookup"><span data-stu-id="2833d-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="2833d-160">Ограничение при шифровании с помощью Widevine в службах мультимедиа Azure: в настоящее время использование нескольких ключей содержимого не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2833d-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="2833d-161">Создание актива и отправка файлов в актив hello</span><span class="sxs-lookup"><span data-stu-id="2833d-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="2833d-162">В порядке toomanage, кодирования и потоковой передачи видео необходимо сначала передать содержимое в службы мультимедиа Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2833d-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="2833d-163">После отправки контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="2833d-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="2833d-164">Дополнительные сведения см. в статье [Передача файлов в учетную запись служб мультимедиа с помощью .NET](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="2833d-165">Кодирование hello активов содержащего hello файл toohello с адаптивной скоростью набор MP4</span><span class="sxs-lookup"><span data-stu-id="2833d-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="2833d-166">При использовании динамического шифрования требуется всего лишь toocreate актив, содержащий набор MP4-файлов с разными скоростями или файлы источника Smooth Streaming с разными скоростями.</span><span class="sxs-lookup"><span data-stu-id="2833d-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="2833d-167">Затем на основе заданного формата hello в манифесте hello и фрагмент запроса, hello server проверит Получение потока hello в протоколе hello, которую вы выбрали потоковой передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="2833d-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="2833d-168">В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="2833d-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="2833d-169">Дополнительные сведения см. в разделе hello [Общие сведения о динамической упаковке](media-services-dynamic-packaging-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="2833d-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="2833d-170">Инструкции о том, как tooencode, в разделе [как tooencode ресурс с помощью Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="2833d-171"><a id="create_contentkey"></a>Создание ключа контента и связать его с активом hello кодировке</span><span class="sxs-lookup"><span data-stu-id="2833d-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="2833d-172">В службах мультимедиа ключ контента hello содержит ключ hello, что требуется tooencrypt актива с.</span><span class="sxs-lookup"><span data-stu-id="2833d-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="2833d-173">Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="2833d-174"><a id="configure_key_auth_policy"></a>Настройка политики авторизации hello ключ содержимого</span><span class="sxs-lookup"><span data-stu-id="2833d-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="2833d-175">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="2833d-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="2833d-176">Политика авторизации ключей содержимого Hello должно быть настроена вами и hello клиент (проигрыватель) в порядке для ключа toobe hello доставить toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="2833d-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="2833d-177">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: открыть или маркер ограниченного использования программ.</span><span class="sxs-lookup"><span data-stu-id="2833d-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="2833d-178">Дополнительные сведения см. в разделе [Настройка политики авторизации ключа содержимого](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="2833d-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="2833d-179"><a id="configure_asset_delivery_policy"></a>Настройка политики доставки для ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="2833d-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="2833d-180">Настройте политику hello доставки для актива.</span><span class="sxs-lookup"><span data-stu-id="2833d-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="2833d-181">Некоторые элементы, которые hello конфигурация политики доставки актива включает в себя:</span><span class="sxs-lookup"><span data-stu-id="2833d-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="2833d-182">Hello DRM приобретения URL-адрес лицензии.</span><span class="sxs-lookup"><span data-stu-id="2833d-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="2833d-183">Hello протокол доставки актива (например, MPEG DASH, HLS, Smooth Streaming или все).</span><span class="sxs-lookup"><span data-stu-id="2833d-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="2833d-184">Hello тип динамического шифрования (в данном случае общее шифрование).</span><span class="sxs-lookup"><span data-stu-id="2833d-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="2833d-185">Дополнительные сведения см. в разделе [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="2833d-186"><a id="create_locator"></a>Создание OnDemand потоковой передачи указателя в порядке tooget URL-адрес потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="2833d-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="2833d-187">Вам потребуется tooprovide пользователей с hello потоковой передачи URL-адрес для Smooth, DASH или HLS.</span><span class="sxs-lookup"><span data-stu-id="2833d-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="2833d-188">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="2833d-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="2833d-189">Инструкции по статье toopublish актива и построения URL-АДРЕСЕ потоковой передачи, [построения URL-адрес потоковой передачи](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="2833d-190">Получение маркера тестирования</span><span class="sxs-lookup"><span data-stu-id="2833d-190">Get a test token</span></span>
<span data-ttu-id="2833d-191">Получение тестового токена, на основе ограничения токенов hello, которое использовалось для политики авторизации ключа hello.</span><span class="sxs-lookup"><span data-stu-id="2833d-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="2833d-192">Можно использовать hello [AMS проигрывателя](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest потока.</span><span class="sxs-lookup"><span data-stu-id="2833d-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2833d-193">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2833d-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="2833d-194">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2833d-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="2833d-195">Добавьте следующие элементы слишком hello**appSettings** определенной в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="2833d-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="2833d-196">Пример</span><span class="sxs-lookup"><span data-stu-id="2833d-196">Example</span></span>

<span data-ttu-id="2833d-197">Hello следующий пример демонстрирует функциональных возможностей, появившихся в Azure Media Services SDK для .net-версии 3.5.2 (в частности, toodefine возможность hello Widevine лицензии шаблона и запрос лицензии Widevine из службы мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="2833d-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="2833d-198">Перезаписать hello код в файле Program.cs кодом hello, приведенные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="2833d-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="2833d-199">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="2833d-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="2833d-200">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="2833d-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="2833d-201">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="2833d-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="2833d-202">Сделайте том tooupdate переменных toopoint toofolders где расположены входные файлы.</span><span class="sxs-lookup"><span data-stu-id="2833d-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a><span data-ttu-id="2833d-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2833d-203">Next step</span></span>
<span data-ttu-id="2833d-204">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="2833d-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2833d-205">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2833d-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2833d-206">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="2833d-206">See also</span></span>
[<span data-ttu-id="2833d-207">CENC with Multi-DRM and Access Control (CENC с несколькими подсистемами DRM и контролем доступа)</span><span class="sxs-lookup"><span data-stu-id="2833d-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="2833d-208">Настройка упаковки Widevine с использованием AMS</span><span class="sxs-lookup"><span data-stu-id="2833d-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="2833d-209">Анонс служб доставки лицензий Google Widevine в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="2833d-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
