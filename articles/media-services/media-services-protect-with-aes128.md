---
title: "AES-128 aaaUsing динамического шифрования и ключ службы доставки | Документы Microsoft"
description: "Службы мультимедиа Microsoft Azure позволяет вам toodeliver контент, зашифрованные с помощью ключей AES 128-разрядное шифрование. Службы мультимедиа также предоставляют службу доставки ключей hello, которая предоставляет пользователям tooauthorized ключи шифрования. В этом разделе показано, как toodynamically шифрования с помощью AES-128 и использовать службу доставки ключей hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: cb1b413ec2ba79f7437464099cf72236ab93f312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="6e86f-105">Использование динамического шифрования AES-128 и службы доставки ключей</span><span class="sxs-lookup"><span data-stu-id="6e86f-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e86f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="6e86f-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="6e86f-107">Java</span><span class="sxs-lookup"><span data-stu-id="6e86f-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="6e86f-108">PHP</span><span class="sxs-lookup"><span data-stu-id="6e86f-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="6e86f-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="6e86f-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="6e86f-110">В разделе [это](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) видео Общие сведения о том, как tooprotect мультимедиа контента с шифрованием AES.</span><span class="sxs-lookup"><span data-stu-id="6e86f-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how tooprotect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="6e86f-111">Службы мультимедиа Microsoft Azure позволяет toodeliver Http-Live-Streaming (HLS) и потоки Smooth Streams, зашифрованные с помощью Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования).</span><span class="sxs-lookup"><span data-stu-id="6e86f-111">Microsoft Azure Media Services enables you toodeliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="6e86f-112">Службы мультимедиа также предоставляют службу доставки ключей hello, которая предоставляет пользователям tooauthorized ключи шифрования.</span><span class="sxs-lookup"><span data-stu-id="6e86f-112">Media Services also provides hello Key Delivery service that delivers encryption keys tooauthorized users.</span></span> <span data-ttu-id="6e86f-113">Если требуется для служб мультимедиа tooencrypt актива, требуется tooassociate ключ шифрования с активом hello и также настроить политики авторизации для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-113">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key with hello asset and also configure authorization policies for hello key.</span></span> <span data-ttu-id="6e86f-114">Когда проигрыватель запрашивает поток, службы мультимедиа используют указанный hello toodynamically ключа шифрования контента с помощью шифрования AES.</span><span class="sxs-lookup"><span data-stu-id="6e86f-114">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="6e86f-115">поток toodecrypt hello, hello проигрыватель будет запрашивать ключ hello из службы доставки ключей hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-115">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="6e86f-116">toodecide ли он hello авторизованных tooget hello ключ, hello служба оценивает политики авторизации hello, заданные для ключа hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-116">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="6e86f-117">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="6e86f-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="6e86f-118">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: открыть или маркер ограниченного использования программ.</span><span class="sxs-lookup"><span data-stu-id="6e86f-118">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="6e86f-119">политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS).</span><span class="sxs-lookup"><span data-stu-id="6e86f-119">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="6e86f-120">Службы мультимедиа поддерживают только токены в hello [токенов SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) формат (SWT) и [веб-маркера JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) формате.</span><span class="sxs-lookup"><span data-stu-id="6e86f-120">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="6e86f-121">Дополнительные сведения см. в разделе [Настройка политики авторизации hello ключ содержимого](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="6e86f-121">For more information, see [Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="6e86f-122">преимущества tootake динамического шифрования требуется актив, содержащий набор MP4-файлов с разными скоростями или файлы источника Smooth Streaming с разными скоростями toohave.</span><span class="sxs-lookup"><span data-stu-id="6e86f-122">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="6e86f-123">Необходимо также tooconfigure политики доставки hello средства hello (описывается далее в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="6e86f-123">You also need tooconfigure hello delivery policy for hello asset (described later in this topic).</span></span> <span data-ttu-id="6e86f-124">Затем на основании hello формат, указанный в URL-адрес потоковой передачи hello, hello сервера потоковой передачи по требованию проверит доставку потока hello в протоколе hello, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="6e86f-124">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="6e86f-125">В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="6e86f-125">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="6e86f-126">В этом разделе будет полезно toodevelopers, работать с приложениями, осуществляющими доставку защищенных файлов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="6e86f-126">This topic would be useful toodevelopers that work on applications that deliver protected media.</span></span> <span data-ttu-id="6e86f-127">Hello разделе показано, как tooconfigure hello службы доставки ключей с политиками авторизации, чтобы только авторизованные клиенты могли получать hello ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="6e86f-127">hello topic shows you how tooconfigure hello key delivery service with authorization policies so that only authorized clients could receive hello encryption keys.</span></span> <span data-ttu-id="6e86f-128">Здесь также показано, как toouse динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="6e86f-128">It also shows how toouse dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="6e86f-129">Рабочий процесс динамического шифрования AES-128 и службы доставки ключей</span><span class="sxs-lookup"><span data-stu-id="6e86f-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="6e86f-130">Hello ниже приведены общие шаги, что tooperform понадобятся вам при шифровании активов с помощью AES, использовании службы доставки ключей Media Services hello и использовании динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="6e86f-130">hello following are general steps that you would need tooperform when encrypting your assets with AES, using hello Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="6e86f-131">[Создание актива и отправка файлов в актив hello](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="6e86f-131">[Create an asset and upload files into hello asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="6e86f-132">[Кодирование активов hello, содержащий hello файл toohello адаптивных битрейтов MP4](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="6e86f-132">[Encode hello asset containing hello file toohello adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="6e86f-133">[Создание ключа контента и связать его с активом hello кодировке](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="6e86f-133">[Create a content key and associate it with hello encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="6e86f-134">В службах мультимедиа ключ контента hello содержит ключ шифрования актива hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-134">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="6e86f-135">[Настройка политики авторизации hello ключ содержимого](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="6e86f-135">[Configure hello content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="6e86f-136">Политика авторизации ключей содержимого Hello должно быть настроена вами и клиент hello, чтобы клиент доставленный toohello содержимого ключа toobe hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-136">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>
5. <span data-ttu-id="6e86f-137">[Настроить политику hello доставки для актива](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="6e86f-137">[Configure hello delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="6e86f-138">Hello конфигурация политики доставки включает: ключевые URL-адрес получения и вектор инициализации (IV) (AES 128 требуется hello, предоставленный toobe же IV при шифровании и расшифровке), протокол доставки (например, MPEG DASH, HLS, Smooth Streaming или все), hello типа динамического шифрования (например конверт или без динамического шифрования).</span><span class="sxs-lookup"><span data-stu-id="6e86f-138">hello delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires hello same IV toobe supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="6e86f-139">Можно применить другой политике tooeach протокола на hello одного средства.</span><span class="sxs-lookup"><span data-stu-id="6e86f-139">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="6e86f-140">Например можно применить шифрование PlayReady tooSmooth/DASH и AES Envelope tooHLS.</span><span class="sxs-lookup"><span data-stu-id="6e86f-140">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="6e86f-141">Все протоколы, которые не определены в политике доставки (например, добавить отдельную политику, которая указывает в качестве протокола hello только HLS) будут заблокированы для потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="6e86f-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="6e86f-142">Hello toothis исключение — когда нет определенных политик доставки активов.</span><span class="sxs-lookup"><span data-stu-id="6e86f-142">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="6e86f-143">Затем все протоколы будут разрешены в hello снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="6e86f-143">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="6e86f-144">[Создание указателя OnDemand](media-services-protect-with-aes128.md#create_locator) чтобы tooget URL-адрес потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="6e86f-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order tooget a streaming URL.</span></span>

<span data-ttu-id="6e86f-145">Hello разделе также показано [как клиентское приложение можно запросить ключ от службы доставки ключей hello](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="6e86f-145">hello topic also shows [how a client application can request a key from hello key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="6e86f-146">Вы найдете полный .NET [пример](media-services-protect-with-aes128.md#example) конце hello hello раздела.</span><span class="sxs-lookup"><span data-stu-id="6e86f-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at hello end of hello topic.</span></span>

<span data-ttu-id="6e86f-147">Следующие изображения Hello демонстрирует hello рабочего процесса, описанного выше.</span><span class="sxs-lookup"><span data-stu-id="6e86f-147">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="6e86f-148">Здесь hello маркер используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6e86f-148">Here hello token is used for authentication.</span></span>

![Защита с помощью AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="6e86f-150">Hello остальной части этого раздела содержатся подробные объяснения, примеры кода и tootopics ссылки, которые показывают, как tooachieve hello задач, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="6e86f-150">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="6e86f-151">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="6e86f-151">Current limitations</span></span>
<span data-ttu-id="6e86f-152">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="6e86f-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="6e86f-153"><a id="create_asset"></a>Создание актива и отправка файлов в актив hello</span><span class="sxs-lookup"><span data-stu-id="6e86f-153"><a id="create_asset"></a>Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="6e86f-154">В порядке toomanage, кодирования и потоковой передачи видео необходимо сначала передать содержимое в службы мультимедиа Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6e86f-154">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="6e86f-155">После отправки контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="6e86f-155">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

<span data-ttu-id="6e86f-156">Дополнительные сведения см. в статье [Передача файлов в учетную запись служб мультимедиа с помощью .NET](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="6e86f-157"><a id="encode_asset"></a>Кодирование hello активов содержащего hello файл toohello с адаптивной скоростью набор MP4</span><span class="sxs-lookup"><span data-stu-id="6e86f-157"><a id="encode_asset"></a>Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="6e86f-158">При использовании динамического шифрования требуется всего лишь toocreate актив, содержащий набор MP4-файлов с разными скоростями или файлы источника Smooth Streaming с разными скоростями.</span><span class="sxs-lookup"><span data-stu-id="6e86f-158">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="6e86f-159">Затем на основе заданного формата hello в манифесте hello или фрагмента запроса, hello server проверит Получение потока hello в протоколе hello, которую вы выбрали потоковой передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="6e86f-159">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="6e86f-160">В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="6e86f-160">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="6e86f-161">Дополнительные сведения см. в разделе hello [Общие сведения о динамической упаковке](media-services-dynamic-packaging-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="6e86f-161">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="6e86f-162">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="6e86f-162">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="6e86f-163">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="6e86f-163">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="6e86f-164">Кроме того, toobe может toouse динамической упаковки и динамического шифрования ваш ресурс должен содержать набор MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="6e86f-164">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="6e86f-165">Инструкции о том, как tooencode, в разделе [как tooencode ресурс с помощью Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-165">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="6e86f-166"><a id="create_contentkey"></a>Создание ключа контента и связать его с активом hello кодировке</span><span class="sxs-lookup"><span data-stu-id="6e86f-166"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="6e86f-167">В службах мультимедиа ключ контента hello содержит ключ hello, что требуется tooencrypt актива с.</span><span class="sxs-lookup"><span data-stu-id="6e86f-167">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="6e86f-168">Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="6e86f-169"><a id="configure_key_auth_policy"></a>Настройка политики авторизации hello ключ содержимого</span><span class="sxs-lookup"><span data-stu-id="6e86f-169"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="6e86f-170">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="6e86f-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="6e86f-171">Политика авторизации ключей содержимого Hello должно быть настроена вами и hello клиент (проигрыватель) в порядке для ключа toobe hello доставить toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="6e86f-171">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="6e86f-172">Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: Откройте, token или ограничения IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6e86f-172">hello content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="6e86f-173">Дополнительные сведения см. в разделе [Настройка политики авторизации ключа содержимого](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="6e86f-174"><a id="configure_asset_delivery_policy"></a>Настройка политики доставки для ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="6e86f-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="6e86f-175">Настройте политику hello доставки для актива.</span><span class="sxs-lookup"><span data-stu-id="6e86f-175">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="6e86f-176">Некоторые элементы, которые hello конфигурация политики доставки актива включает в себя:</span><span class="sxs-lookup"><span data-stu-id="6e86f-176">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="6e86f-177">Hello ключ приобретения URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="6e86f-177">hello Key acquisition URL.</span></span> 
* <span data-ttu-id="6e86f-178">Hello toouse вектор инициализации (IV) для шифрования конвертов hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-178">hello Initialization Vector (IV) toouse for hello envelope encryption.</span></span> <span data-ttu-id="6e86f-179">AES-128 требуется hello, предоставленный toobe же IV при шифровании и расшифровке.</span><span class="sxs-lookup"><span data-stu-id="6e86f-179">AES 128 requires hello same IV toobe supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="6e86f-180">Hello протокол доставки актива (например, MPEG DASH, HLS, Smooth Streaming или все).</span><span class="sxs-lookup"><span data-stu-id="6e86f-180">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="6e86f-181">Hello тип динамического шифрования (например конверт AES) или отсутствие динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="6e86f-181">hello type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="6e86f-182">Дополнительные сведения см. в разделе [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="6e86f-183"><a id="create_locator"></a>Создание OnDemand потоковой передачи указателя в порядке tooget URL-адрес потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="6e86f-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="6e86f-184">Вам потребуется tooprovide пользователей с hello потоковой передачи URL-адрес для Smooth, DASH или HLS.</span><span class="sxs-lookup"><span data-stu-id="6e86f-184">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="6e86f-185">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="6e86f-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="6e86f-186">Инструкции по статье toopublish актива и построения URL-АДРЕСЕ потоковой передачи, [построения URL-адрес потоковой передачи](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-186">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="6e86f-187">Получение маркера тестирования</span><span class="sxs-lookup"><span data-stu-id="6e86f-187">Get a test token</span></span>
<span data-ttu-id="6e86f-188">Получение тестового токена, на основе ограничения токенов hello, которое использовалось для политики авторизации ключа hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-188">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="6e86f-189">Можно использовать hello [AMS проигрывателя](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest потока.</span><span class="sxs-lookup"><span data-stu-id="6e86f-189">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <span data-ttu-id="6e86f-190"><a id="client_request"></a>Как запрос клиентом ключа из службы доставки ключей hello?</span><span class="sxs-lookup"><span data-stu-id="6e86f-190"><a id="client_request"></a>How can your client request a key from hello key delivery service?</span></span>
<span data-ttu-id="6e86f-191">В предыдущем шаге hello созданный hello URL-адрес, который указывает файл манифеста tooa.</span><span class="sxs-lookup"><span data-stu-id="6e86f-191">In hello previous step, you constructed hello URL that points tooa manifest file.</span></span> <span data-ttu-id="6e86f-192">Клиент должен tooextract hello необходимые сведения из hello потоковой передачи файлов манифеста в порядке toomake службы доставки ключей toohello запроса.</span><span class="sxs-lookup"><span data-stu-id="6e86f-192">Your client needs tooextract hello necessary information from hello streaming manifest files in order toomake a request toohello key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="6e86f-193">Файлы манифестов</span><span class="sxs-lookup"><span data-stu-id="6e86f-193">Manifest files</span></span>
<span data-ttu-id="6e86f-194">Hello клиент должен tooextract hello URL-адрес (который также содержит идентификатор (kid) ключа контента) значение из файла манифеста hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-194">hello client needs tooextract hello URL (that also contains content key Id (kid)) value from hello manifest file.</span></span> <span data-ttu-id="6e86f-195">Затем клиент Hello пытается ключ шифрования hello tooget от службы доставки ключей hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-195">hello client will then try tooget hello encryption key from hello key delivery service.</span></span> <span data-ttu-id="6e86f-196">Hello клиент также должен tooextract значение hello IV и использовать его для расшифровки stream.hello hello, следующий фрагмент кода показывает hello <Protection> элемента манифеста Smooth Streaming hello.</span><span class="sxs-lookup"><span data-stu-id="6e86f-196">hello client also needs tooextract hello IV value and use it do decrypt hello stream.hello following snippet shows hello <Protection> element of hello Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="6e86f-197">В случае HLS hello hello корневой манифест разбивается на файлы сегментов.</span><span class="sxs-lookup"><span data-stu-id="6e86f-197">In hello case of HLS, hello root manifest is broken into segment files.</span></span> 

<span data-ttu-id="6e86f-198">Например, является hello корневой манифест: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) и она содержит список имен файлов сегмента.</span><span class="sxs-lookup"><span data-stu-id="6e86f-198">For example, hello root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="6e86f-199">Если один из файлов сегмента Привет открыть в текстовом редакторе (например, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should содержит #EXT-X-ключ, указывает, что этот файл hello шифруется.</span><span class="sxs-lookup"><span data-stu-id="6e86f-199">If you open one of hello segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that hello file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="6e86f-200">При планировании tooplay AES шифрования HLS в Safari см. в разделе [этот блог](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="6e86f-200">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-hello-key-from-hello-key-delivery-service"></a><span data-ttu-id="6e86f-201">Запросить hello ключ от службы доставки ключей hello</span><span class="sxs-lookup"><span data-stu-id="6e86f-201">Request hello key from hello key delivery service</span></span>

<span data-ttu-id="6e86f-202">Hello следующий код показывает, как toosend toohello запрос служб мультимедиа ключа службы доставки, с помощью Uri доставки ключей (полученного из манифеста hello) и токена (в этом разделе не касается как tooget простой Web токены из службы токенов безопасности).</span><span class="sxs-lookup"><span data-stu-id="6e86f-202">hello following code shows how toosend a request toohello Media Services key delivery service using a key delivery Uri (that was extracted from hello manifest) and a token (this topic does not talk about how tooget Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="6e86f-203">Защита содержимого с помощью AES-128 и .NET</span><span class="sxs-lookup"><span data-stu-id="6e86f-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6e86f-204">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e86f-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="6e86f-205">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6e86f-205">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="6e86f-206">Добавьте следующие элементы слишком hello**appSettings** определенной в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="6e86f-206">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="6e86f-207"><a id="example"></a>Пример</span><span class="sxs-lookup"><span data-stu-id="6e86f-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="6e86f-208">Перезаписать hello код в файле Program.cs кодом hello, приведенные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="6e86f-208">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="6e86f-209">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="6e86f-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="6e86f-210">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="6e86f-210">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="6e86f-211">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="6e86f-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="6e86f-212">Сделайте том tooupdate переменных toopoint toofolders где расположены входные файлы.</span><span class="sxs-lookup"><span data-stu-id="6e86f-212">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing hello issuer of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // hello Audience or Scope of hello token.  
        // Must match hello value in hello token for hello token toobe considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
            //so you have tooadd it in front of hello token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello bit.ly/aesplayer Flash player tootest hello URL 
            // (with open authorization policy). 
            // Paste hello URL and click hello Update button tooplay hello video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy tooContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key tooAsset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose tooassociate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in hello key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  hello URL does not contains a key ID

            // hello following policy configuration specifies: 
            // key url that will have KID=<Guid> appended toohello envelope and
            // hello Initialization Vector (IV) toouse for hello envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="6e86f-213">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="6e86f-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6e86f-214">Отзывы</span><span class="sxs-lookup"><span data-stu-id="6e86f-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

