---
title: "Использование динамического шифрования AES-128 и службы доставки ключей | Документация Майкрософт"
description: "Службы мультимедиа Microsoft Azure позволяют доставлять содержимое, зашифрованное с помощью 128-битных ключей шифрования AES. Они также включают в себя службу доставки ключей, которая доставляет ключи шифрования авторизованным пользователям. В этой статье показано, как динамически шифровать содержимое с помощью алгоритма AES-128 и службы доставки ключей."
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
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="7b7fa-105">Использование динамического шифрования AES-128 и службы доставки ключей</span><span class="sxs-lookup"><span data-stu-id="7b7fa-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b7fa-106">.NET</span><span class="sxs-lookup"><span data-stu-id="7b7fa-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="7b7fa-107">Java</span><span class="sxs-lookup"><span data-stu-id="7b7fa-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="7b7fa-108">PHP</span><span class="sxs-lookup"><span data-stu-id="7b7fa-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="7b7fa-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="7b7fa-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="7b7fa-110">Обзор способов защиты содержимого мультимедиа с помощью шифрования AES представлен в [этом](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) видео.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="7b7fa-111">Службы мультимедиа Microsoft Azure позволяют доставлять по каналам HLS и Smooth Streaming содержимое, зашифрованное с помощью AES (с использованием 128-битных ключей шифрования).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="7b7fa-112">Они также включают в себя службу доставки ключей, которая доставляет ключи шифрования авторизованным пользователям.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="7b7fa-113">Если вам нужно, чтобы службы мультимедиа зашифровали ресурс-контейнер, свяжите с ним ключ шифрования и настройте политики авторизации для ключа.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="7b7fa-114">Когда поток запрашивается проигрывателем, службы мультимедиа используют указанный ключ для динамического шифрования содержимого с помощью AES.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="7b7fa-115">Чтобы расшифровать поток, проигрыватель запросит ключ у службы доставки ключей.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="7b7fa-116">Чтобы определить, есть ли у пользователя право на получение ключа, служба оценивает политики авторизации, заданные для ключа.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="7b7fa-117">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="7b7fa-118">Для политики авторизации ключа содержимого можно задать одно или несколько из ограничений авторизации: открытая авторизация или с ограничением по маркеру.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="7b7fa-119">При ограничении по маркеру к политике должен прилагаться маркер, выданный службой маркеров безопасности (STS).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="7b7fa-120">Службы мультимедиа поддерживают [простые веб-маркеры](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) и маркеры в формате [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="7b7fa-121">Дополнительную информацию см. в разделе [Настройка политики авторизации для ключа содержимого](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="7b7fa-122">Чтобы воспользоваться преимуществами динамического шифрования, необходимо иметь ресурс-контейнер, содержащий набор многоскоростных MP4-файлов или многоскоростных исходных файлов Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="7b7fa-123">Вам также потребуется настроить политику доставки для ресурса-контейнера (описывается далее в этой статье).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="7b7fa-124">В зависимости от формата, указанного в URL-адресе потоковой передачи, сервер потокового воспроизведения по запросу обеспечивает доставку содержимого по выбранному протоколу.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="7b7fa-125">В результате вы сможете хранить и оплачивать файлы только в одном формате, а службы мультимедиа выполнят сборку и будут обслуживать соответствующий ответ на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="7b7fa-126">Эта статья будет полезна разработчикам приложений, которые доставляют защищенные файлы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="7b7fa-127">В ней показано, как настроить политики авторизации для службы доставки ключей, чтобы только авторизованные клиенты могли получать ключи шифрования,</span><span class="sxs-lookup"><span data-stu-id="7b7fa-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="7b7fa-128">а также рассматривается использование динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="7b7fa-129">Рабочий процесс динамического шифрования AES-128 и службы доставки ключей</span><span class="sxs-lookup"><span data-stu-id="7b7fa-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="7b7fa-130">Ниже описаны общие действия, которые необходимо выполнить для шифрования ресурсов-контейнеров с помощью AES, используя службу доставки ключей служб мультимедиа и динамическое шифрование.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="7b7fa-131">[Создание ресурса-контейнера и отправка в него файлов](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="7b7fa-132">[Кодирование ресурса-контейнера с файлами в набор MP4-файлов с переменной скоростью](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="7b7fa-133">[Создание ключа содержимого и связывание его с закодированным ресурсом-контейнером](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="7b7fa-134">В службах мультимедиа ключ содержимого содержит ключ шифрования ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="7b7fa-135">[Настройка политики авторизации для ключа содержимого](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="7b7fa-136">Чтобы получить ключ содержимого, клиент должен соответствовать заданной для этого ключа политике авторизации.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="7b7fa-137">[Настройте политику доставки для ресурса-контейнера](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="7b7fa-138">Конфигурация политики доставки включает: URL-адрес для получения ключа и вектор инициализации (IV) (при использовании AES 128 необходимо указывать один и тот же вектор инициализации для шифрования и расшифровки), протокол доставки (например, MPEG-DASH, HLS, Smooth Streaming или все перечисленные) и тип динамического шифрования (например, конвертное или без динамического шифрования).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="7b7fa-139">К разным протоколам можно применять разные политики в отношении одного и того же ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="7b7fa-140">Например, вы можете применить шифрование PlayReady при использовании Smooth или DASH и конвертное шифрование AES при использовании HLS.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="7b7fa-141">Потоковая передача по тем протоколам, которые не определены в политике доставки (например, если вы добавили одну политику, которая предусматривает использование только протокола HLS), будет блокироваться.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="7b7fa-142">Исключением являются те случаи, когда политика доставки ресурсов совсем не определена.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="7b7fa-143">Тогда все протоколы могут использоваться в незашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="7b7fa-144">[Создайте указатель OnDemand](media-services-protect-with-aes128.md#create_locator) , чтобы получить URL-адрес для потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="7b7fa-145">В этой статье также показано, [как клиентское приложение может запрашивать ключ у службы доставки ключей](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="7b7fa-146">В конце раздела вы найдете полный [пример](media-services-protect-with-aes128.md#example) для .NET.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="7b7fa-147">На следующем изображении показан описанный выше рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="7b7fa-148">В данном случае для проверки подлинности используется маркер.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-148">Here the token is used for authentication.</span></span>

![Защита с помощью AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="7b7fa-150">Далее приводятся подробные объяснения, примеры кода и ссылки на статьи с инструкциями для выполнения описанных выше задач.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="7b7fa-151">Текущие ограничения</span><span class="sxs-lookup"><span data-stu-id="7b7fa-151">Current limitations</span></span>
<span data-ttu-id="7b7fa-152">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="7b7fa-153"><a id="create_asset"></a>Создание ресурса-контейнера и отправка в него файлов</span><span class="sxs-lookup"><span data-stu-id="7b7fa-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="7b7fa-154">Для кодирования и потоковой передачи видео, а также управления ими необходимо сначала отправить содержимое в службы мультимедиа Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="7b7fa-155">Оно будет сохранено в безопасном облачном хранилище для последующей обработки и потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="7b7fa-156">Дополнительные сведения см. в статье [Передача файлов в учетную запись служб мультимедиа с помощью .NET](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="7b7fa-157"><a id="encode_asset"></a>Закодируйте ресурс-контейнер с файлами в набор MP4-файлов с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="7b7fa-158">При использовании динамического шифрования вам достаточно создать ресурс-контейнер, содержащий набор многоскоростных MP4-файлов или многоскоростных исходных файлов Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="7b7fa-159">Затем с учетом формата, указанного в манифесте или запросе фрагмента, сервер потоковой передачи по запросу организует передачу содержимого по выбранному протоколу.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="7b7fa-160">В результате вы сможете хранить и оплачивать файлы только в одном формате, а службы мультимедиа выполнят сборку и будут обслуживать соответствующий ответ на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="7b7fa-161">Дополнительные сведения см. в статье [Динамическая упаковка](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="7b7fa-162">При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="7b7fa-163">Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи, из которой необходимо выполнять потоковую передачу содержимого, должна находиться в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="7b7fa-164">Кроме того, чтобы использовать динамическую упаковку и динамическое шифрование, ресурс должен содержать набор файлов формата MP4 или потоковой передачи Smooth Streaming с переменной скоростью.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="7b7fa-165">Инструкции по выполнению шифрования см. в статье [Порядок кодирования ресурса с использованием стандартного кодировщика мультимедиа](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="7b7fa-166"><a id="create_contentkey"></a>Создание ключа содержимого и связывание его с закодированным ресурсом-контейнером</span><span class="sxs-lookup"><span data-stu-id="7b7fa-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="7b7fa-167">В службах мультимедиа ключ содержимого содержит ключ, который используется для шифрования ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="7b7fa-168">Дополнительные сведения см. в статье [Создание ContentKey с использованием .NET](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="7b7fa-169"><a id="configure_key_auth_policy"></a>Настройка политики авторизации ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="7b7fa-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="7b7fa-170">Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="7b7fa-171">Чтобы получить ключ содержимого, клиент (проигрыватель) должен соответствовать заданной для этого ключа политике авторизации.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="7b7fa-172">Для политики авторизации ключа содержимого можно задать одно или несколько из ограничений авторизации: открытая авторизация, с ограничением по маркеру или с ограничением по IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="7b7fa-173">Дополнительные сведения см. в разделе [Настройка политики авторизации ключа содержимого](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="7b7fa-174"><a id="configure_asset_delivery_policy"></a>Настройка политики доставки для ресурса-контейнера</span><span class="sxs-lookup"><span data-stu-id="7b7fa-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="7b7fa-175">Настройте политику доставки для ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="7b7fa-176">Вот некоторые элементы, входящие в конфигурацию политики доставки:</span><span class="sxs-lookup"><span data-stu-id="7b7fa-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="7b7fa-177">URL-адрес для получения ключа.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="7b7fa-178">Вектор инициализации, используемый для конвертного шифрования.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="7b7fa-179">При использовании AES 128 для шифрования и расшифровки необходимо указывать один и тот же вектор инициализации.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="7b7fa-180">Протокол доставки ресурсов-контейнеров (например, MPEG-DASH, HLS, Smooth Streaming или все перечисленные).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="7b7fa-181">Тип динамического шифрования (например, конвертное шифрование с помощью AES), если оно используется.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="7b7fa-182">Дополнительные сведения см. в разделе [Настройка политик доставки ресурсов](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="7b7fa-183"><a id="create_locator"></a>Создание указателя потоковой передачи по запросу для получения URL-адреса для потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="7b7fa-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="7b7fa-184">При использовании протоколов Smooth, DASH или HLS вам потребуется предоставить пользователю URL-адрес для потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="7b7fa-185">При добавлении или обновлении политики доставки ресурсов необходимо удалить существующий указатель (если он есть) и создать новый.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="7b7fa-186">Указания по публикации ресурса и созданию URL-адреса потоковой передачи см. в статье [Создание URL-адреса потоковой передачи](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="7b7fa-187">Получение маркера тестирования</span><span class="sxs-lookup"><span data-stu-id="7b7fa-187">Get a test token</span></span>
<span data-ttu-id="7b7fa-188">Получите маркер тестирования в зависимости от ограничения по маркеру, заданного в политике авторизации ключа.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="7b7fa-189">Для проверки потока можно использовать [проигрыватель AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) .</span><span class="sxs-lookup"><span data-stu-id="7b7fa-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="7b7fa-190"><a id="client_request"></a>Отправка запроса клиента на получение ключа в службе доставки ключей</span><span class="sxs-lookup"><span data-stu-id="7b7fa-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="7b7fa-191">На предыдущем этапе вы создали URL-адрес, указывающий на файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="7b7fa-192">Клиент должен извлечь необходимые сведения из файлов манифеста потоковой передачи и отправить запрос в службу доставки ключей.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="7b7fa-193">Файлы манифестов</span><span class="sxs-lookup"><span data-stu-id="7b7fa-193">Manifest files</span></span>
<span data-ttu-id="7b7fa-194">Клиенту необходимо извлечь из файла манифеста значение URL-адреса (который также содержит идентификатор ключа содержимого (KID)).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="7b7fa-195">Затем клиент попытается получить ключ шифрования в службе доставки ключей.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="7b7fa-196">Клиенту также потребуется извлечь значение вектора инициализации и использовать его для расшифровки потока. В следующем фрагменте кода показан элемент <Protection> манифеста Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

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

<span data-ttu-id="7b7fa-197">При использовании протокола HLS корневой манифест разбивается на файлы сегментов.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="7b7fa-198">Например, корневой манифест http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) содержит список имен файлов сегментов.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="7b7fa-199">Если открыть один из файлов сегментов в текстовом редакторе (например, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels (514369)/Manifest(video,format=m3u8-aapl), можно увидеть строку #EXT-X-KEY, которая означает, что файл зашифрован.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

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
><span data-ttu-id="7b7fa-200">Если вы планируете воспроизводить HLS с шифрованием AES в Safari, см. [этот блог](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="7b7fa-201">Запрос ключа в службе доставки ключей</span><span class="sxs-lookup"><span data-stu-id="7b7fa-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="7b7fa-202">В следующем коде показано, как отправить запрос в службу доставки ключей служб мультимедиа, используя код URI доставки ключа (извлеченный из манифеста) и маркер (получение простых веб-маркеров из службы маркеров безопасности в этой статье не рассматривается).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

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

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="7b7fa-203">Защита содержимого с помощью AES-128 и .NET</span><span class="sxs-lookup"><span data-stu-id="7b7fa-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="7b7fa-204">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b7fa-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="7b7fa-205">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="7b7fa-206">Добавьте следующие элементы в **appSettings**, определенные в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="7b7fa-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="7b7fa-207"><a id="example"></a>Пример</span><span class="sxs-lookup"><span data-stu-id="7b7fa-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="7b7fa-208">Замените код в файле Program.cs кодом, приведенным в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="7b7fa-209">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="7b7fa-210">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="7b7fa-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="7b7fa-211">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="7b7fa-212">Обязательно обновите переменные, чтобы они указывали на папки, в которых находятся входные файлы.</span><span class="sxs-lookup"><span data-stu-id="7b7fa-212">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
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
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
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

            // Associate the key with the asset.
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

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
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

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin. 
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file. 
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="7b7fa-213">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="7b7fa-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7b7fa-214">Отзывы</span><span class="sxs-lookup"><span data-stu-id="7b7fa-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

