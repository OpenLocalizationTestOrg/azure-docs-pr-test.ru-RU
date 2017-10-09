---
title: "aaaUsing castLabs toodeliver Widevine лицензий tooAzure Media Services | Документы Microsoft"
description: "В этой статье описывается, как можно использовать toodeliver служб мультимедиа Azure (AMS) поток, который зашифрован динамически AMS с помощью PlayReady и Widevine DRMs. лицензии PlayReady Hello поступают из сервера лицензий PlayReady служб мультимедиа и лицензии Widevine доставляется сервером лицензирования castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="d4835-104">С помощью castLabs toodeliver Widevine лицензий tooAzure служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d4835-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d4835-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="d4835-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="d4835-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="d4835-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d4835-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="d4835-107">Overview</span></span>
<span data-ttu-id="d4835-108">В этой статье описывается, как можно использовать toodeliver служб мультимедиа Azure (AMS) поток, который зашифрован динамически AMS с помощью PlayReady и Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="d4835-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="d4835-109">лицензии PlayReady Hello поступают из сервера лицензий PlayReady служб мультимедиа и лицензии Widevine доставляется по **castLabs** сервера лицензирования.</span><span class="sxs-lookup"><span data-stu-id="d4835-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="d4835-110">tooplayback потоковой передачи содержимого, защищенного с CENC (PlayReady или Widevine), можно использовать [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d4835-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="d4835-111">Подробные сведения см. в [документе по AMP](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="d4835-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="d4835-112">Здравствуй, следующая диаграмма демонстрирует высокоуровневая архитектура Azure Media Services и castLabs интеграции.</span><span class="sxs-lookup"><span data-stu-id="d4835-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![интеграция](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="d4835-114">Настройка типичной системы</span><span class="sxs-lookup"><span data-stu-id="d4835-114">Typical system set up</span></span>
* <span data-ttu-id="d4835-115">Мультимедийное содержимое хранится в AMS.</span><span class="sxs-lookup"><span data-stu-id="d4835-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="d4835-116">Идентификаторы ключей содержимого хранятся в castLabs и AMS.</span><span class="sxs-lookup"><span data-stu-id="d4835-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="d4835-117">CastLabs и AMS имеют встроенную проверку подлинности маркеров.</span><span class="sxs-lookup"><span data-stu-id="d4835-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="d4835-118">Привет, в следующих разделах рассматриваются токены проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d4835-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="d4835-119">Когда клиент запрашивает видео toostream hello, содержимое hello динамически шифруется с **общее шифрование** (CENC) и динамического упаковать с AMS tooSmooth, потоковая передача и ТИРЕ.</span><span class="sxs-lookup"><span data-stu-id="d4835-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="d4835-120">Для протокола потоковой передачи HLS предлагается также шифрование элементарного потока PlayReady M2TS.</span><span class="sxs-lookup"><span data-stu-id="d4835-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="d4835-121">Лицензию PlayReady выдает сервер лицензирования AMS, а лицензию Widevine — сервер лицензирования castLabs.</span><span class="sxs-lookup"><span data-stu-id="d4835-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="d4835-122">Проигрыватель автоматически определяет, какие toofetch лицензии основании возможностей платформы клиента hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="d4835-123">Создания маркеров проверки подлинности для получения лицензии</span><span class="sxs-lookup"><span data-stu-id="d4835-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="d4835-124">CastLabs и AMS поддерживает tooauthorize используется формат маркера JWT (веб-маркера JSON) лицензию.</span><span class="sxs-lookup"><span data-stu-id="d4835-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="d4835-125">Маркер JWT в AMS</span><span class="sxs-lookup"><span data-stu-id="d4835-125">JWT token in AMS</span></span>
<span data-ttu-id="d4835-126">Привет, в следующей таблице описываются маркера JWT в AMS.</span><span class="sxs-lookup"><span data-stu-id="d4835-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="d4835-127">Издатель</span><span class="sxs-lookup"><span data-stu-id="d4835-127">Issuer</span></span> | <span data-ttu-id="d4835-128">Строка поставщика из hello выбранной службы токенов безопасности (STS)</span><span class="sxs-lookup"><span data-stu-id="d4835-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="d4835-129">Аудитория</span><span class="sxs-lookup"><span data-stu-id="d4835-129">Audience</span></span> |<span data-ttu-id="d4835-130">Строка аудитории из hello используется служба маркеров безопасности</span><span class="sxs-lookup"><span data-stu-id="d4835-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="d4835-131">Claims</span><span class="sxs-lookup"><span data-stu-id="d4835-131">Claims</span></span> |<span data-ttu-id="d4835-132">Набор утверждений</span><span class="sxs-lookup"><span data-stu-id="d4835-132">A set of claims</span></span> |
| <span data-ttu-id="d4835-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="d4835-133">NotBefore</span></span> |<span data-ttu-id="d4835-134">Начало действия маркера hello</span><span class="sxs-lookup"><span data-stu-id="d4835-134">Start validity of hello token</span></span> |
| <span data-ttu-id="d4835-135">Expires</span><span class="sxs-lookup"><span data-stu-id="d4835-135">Expires</span></span> |<span data-ttu-id="d4835-136">Окончания действия маркера hello</span><span class="sxs-lookup"><span data-stu-id="d4835-136">End validity of hello token</span></span> |
| <span data-ttu-id="d4835-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="d4835-137">SigningCredentials</span></span> |<span data-ttu-id="d4835-138">Hello ключ, который является общим для сервера лицензирования PlayReady, castLabs сервером лицензирования и STS, он может быть либо симметричный или асимметричный ключ.</span><span class="sxs-lookup"><span data-stu-id="d4835-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="d4835-139">Маркер JWT в castLabs</span><span class="sxs-lookup"><span data-stu-id="d4835-139">JWT token in castLabs</span></span>
<span data-ttu-id="d4835-140">Привет, в следующей таблице описываются маркера JWT в castLabs.</span><span class="sxs-lookup"><span data-stu-id="d4835-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="d4835-141">Имя</span><span class="sxs-lookup"><span data-stu-id="d4835-141">Name</span></span> | <span data-ttu-id="d4835-142">Описание</span><span class="sxs-lookup"><span data-stu-id="d4835-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4835-143">optData</span><span class="sxs-lookup"><span data-stu-id="d4835-143">optData</span></span> |<span data-ttu-id="d4835-144">Строка JSON со сведениями о вас.</span><span class="sxs-lookup"><span data-stu-id="d4835-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="d4835-145">crt</span><span class="sxs-lookup"><span data-stu-id="d4835-145">crt</span></span> |<span data-ttu-id="d4835-146">Строка JSON, содержащий сведения о средстве hello, его лицензионных прав сведения и воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="d4835-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="d4835-147">iat</span><span class="sxs-lookup"><span data-stu-id="d4835-147">iat</span></span> |<span data-ttu-id="d4835-148">Hello текущую дату и время в начала эпохи.</span><span class="sxs-lookup"><span data-stu-id="d4835-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="d4835-149">jti</span><span class="sxs-lookup"><span data-stu-id="d4835-149">jti</span></span> |<span data-ttu-id="d4835-150">Уникальный идентификатор о этот токен (каждый маркер может использоваться только один раз в системе castLabs hello).</span><span class="sxs-lookup"><span data-stu-id="d4835-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="d4835-151">Настройка образца решения</span><span class="sxs-lookup"><span data-stu-id="d4835-151">Sample solution set up</span></span>
<span data-ttu-id="d4835-152">Hello [образец решения](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) состоит из двух проектов:</span><span class="sxs-lookup"><span data-stu-id="d4835-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="d4835-153">Консольное приложение, которое может быть используется tooset ограничения актива уже полученный DRM PlayReady и Widevine.</span><span class="sxs-lookup"><span data-stu-id="d4835-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="d4835-154">Веб-приложение, которое передает маркеры, которые можно рассматривать как ОЧЕНЬ УПРОЩЕННУЮ версию службы маркеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="d4835-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="d4835-155">Консольное приложение hello toouse:</span><span class="sxs-lookup"><span data-stu-id="d4835-155">toouse hello console application:</span></span>

1. <span data-ttu-id="d4835-156">Изменить учетные данные toosetup AMS app.config hello, castLabs учетные данные, конфигурации STS и общего ключа.</span><span class="sxs-lookup"><span data-stu-id="d4835-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="d4835-157">Отправьте файл в AMS.</span><span class="sxs-lookup"><span data-stu-id="d4835-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="d4835-158">Get hello UUID из hello отправлен активов и измените 32 строки в файл Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="d4835-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="d4835-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="d4835-160">Используйте AssetId для hello активов в системе castLabs hello (44 строки в файл Program.cs hello).</span><span class="sxs-lookup"><span data-stu-id="d4835-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="d4835-161">Необходимо задать AssetId для **castLabs**; он должен toobe уникальный буквенно-цифровую строку.</span><span class="sxs-lookup"><span data-stu-id="d4835-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="d4835-162">Запустите программу hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-162">Run hello program.</span></span>

<span data-ttu-id="d4835-163">hello toouse веб-приложения (STS):</span><span class="sxs-lookup"><span data-stu-id="d4835-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="d4835-164">Изменение hello web.config toosetup castlabs merchant ID, конфигурации STS hello и hello общего ключа.</span><span class="sxs-lookup"><span data-stu-id="d4835-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="d4835-165">Развертывание tooAzure веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="d4835-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="d4835-166">Перейдите toohello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="d4835-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="d4835-167">Воспроизведение видео</span><span class="sxs-lookup"><span data-stu-id="d4835-167">Playing back a video</span></span>
<span data-ttu-id="d4835-168">tooplayback видео зашифрован общее шифрование (PlayReady или Widevine), вы можете использовать hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d4835-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="d4835-169">При запуске консольного приложения hello, передаются hello идентификатор ключа содержимого и hello URL-адрес манифеста.</span><span class="sxs-lookup"><span data-stu-id="d4835-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="d4835-170">Откройте новую вкладку и запустите службу маркеров безопасности: http://[имя_службы_маркеров_безопасности].azurewebsites.net/api/token/assetid/[ваш_AssetId_в_CastLabs]/contentkeyid/[идентификатор_ключа_содержимого].</span><span class="sxs-lookup"><span data-stu-id="d4835-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="d4835-171">Go слишком[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d4835-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="d4835-172">Вставьте URL-адрес потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="d4835-173">Нажмите кнопку hello **Дополнительно** флажок.</span><span class="sxs-lookup"><span data-stu-id="d4835-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="d4835-174">В hello **защиты** раскрывающийся список, выберите PlayReady и/или Widevine.</span><span class="sxs-lookup"><span data-stu-id="d4835-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="d4835-175">Вставьте токен hello, полученного от STS в текстовом поле токен hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="d4835-176">сервер лицензирования castLab Hello не обязательно hello» носителя =» префикс перед маркером hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="d4835-177">Поэтому удалите, перед отправкой маркера hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="d4835-178">Обновление проигрывателя hello.</span><span class="sxs-lookup"><span data-stu-id="d4835-178">Update hello player.</span></span>
8. <span data-ttu-id="d4835-179">должны играть Hello видео.</span><span class="sxs-lookup"><span data-stu-id="d4835-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d4835-180">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d4835-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d4835-181">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d4835-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

