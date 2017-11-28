---
title: "aaaProtect HLS содержимого с помощью Microsoft PlayReady или Apple FairPlay - Azure | Документы Microsoft"
description: "В этом разделе приводится обзор и показано, как службы мультимедиа Azure toodynamically toouse шифрования контента с Apple FairPlay HTTP Live Streaming (HLS). Здесь также показано, как toouse hello Media Services лицензии toodeliver службы доставки лицензий tooclients FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="12f94-104">Защита содержимого HLS с помощью Apple FairPlay или Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="12f94-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="12f94-105">Службы мультимедиа позволяют Azure, вы toodynamically шифрования контента HTTP Live Streaming (HLS) с помощью hello следующие форматы:</span><span class="sxs-lookup"><span data-stu-id="12f94-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="12f94-106">**Незащищенный ключ конверта AES-128**</span><span class="sxs-lookup"><span data-stu-id="12f94-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="12f94-107">Hello весь блок шифруется с помощью hello **CBC AES-128** режим.</span><span class="sxs-lookup"><span data-stu-id="12f94-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="12f94-108">Расшифровка Hello hello потока имеет собственной поддержки iOS и OS X проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="12f94-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="12f94-109">Дополнительные сведения см. в статье [Использование динамического шифрования AES-128 и службы доставки ключей](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="12f94-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="12f94-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="12f94-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="12f94-111">Здравствуйте, отдельные видео и аудио образцы, шифруются с помощью hello **CBC AES-128** режим.</span><span class="sxs-lookup"><span data-stu-id="12f94-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="12f94-112">**Потоковая передача FairPlay** интегрируется в hello операционных систем устройств со встроенной поддержкой в iOS и Apple TV (кадров/с).</span><span class="sxs-lookup"><span data-stu-id="12f94-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="12f94-113">Safari в OS X позволяет кадров в Секунду, используя поддержку интерфейса hello зашифрованные мультимедиа расширения (EME).</span><span class="sxs-lookup"><span data-stu-id="12f94-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="12f94-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="12f94-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="12f94-115">Hello на рисунке показаны hello **HLS + FairPlay или PlayReady динамического шифрования** рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="12f94-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Схема рабочего процесса динамического шифрования](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="12f94-117">В этом разделе показано, как toodynamically toouse Media Services зашифровать содержимое HLS с Apple FairPlay.</span><span class="sxs-lookup"><span data-stu-id="12f94-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="12f94-118">Здесь также показано, как toouse hello Media Services лицензии toodeliver службы доставки лицензий tooclients FairPlay.</span><span class="sxs-lookup"><span data-stu-id="12f94-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="12f94-119">Если также требуется tooencrypt контента HLS содержимого с помощью PlayReady, требуется toocreate общим ключом содержимого и связать его с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="12f94-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="12f94-120">Необходимо также tooconfigure hello содержимого политики авторизации ключа, как описано в [динамического общее шифрование с помощью PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="12f94-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="12f94-121">Требования и рекомендации</span><span class="sxs-lookup"><span data-stu-id="12f94-121">Requirements and considerations</span></span>

<span data-ttu-id="12f94-122">При использовании служб мультимедиа toodeliver шифрования HLS с FairPlay и лицензии FairPlay toodeliver, не требуется Hello следующие:</span><span class="sxs-lookup"><span data-stu-id="12f94-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="12f94-123">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="12f94-123">An Azure account.</span></span> <span data-ttu-id="12f94-124">Дополнительные сведения см. на странице с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="12f94-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="12f94-125">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="12f94-125">A Media Services account.</span></span> <span data-ttu-id="12f94-126">разделе toocreate, [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="12f94-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="12f94-127">Регистрация в [программе разработки Apple](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="12f94-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="12f94-128">Apple требует hello владельца содержимого tooobtain hello [пакет развертывания](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="12f94-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="12f94-129">Состояние уже реализован модуль безопасности ключ (KSM) с помощью служб мультимедиа и запрашивается hello конечного пакета число кадров в Секунду.</span><span class="sxs-lookup"><span data-stu-id="12f94-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="12f94-130">Существуют инструкциям hello окончательного кадров в Секунду пакета toogenerate сертификации и получить hello секретный ключ приложения (ASK).</span><span class="sxs-lookup"><span data-stu-id="12f94-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="12f94-131">Используется, чтобы ЗАДАТЬ tooconfigure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="12f94-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="12f94-132">Пакет SDK служб мультимедиа Azure для .NET **3.6.0** или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="12f94-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="12f94-133">Привет, выполнив действия должно быть задано на стороне доставки ключей служб мультимедиа:</span><span class="sxs-lookup"><span data-stu-id="12f94-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="12f94-134">**Приложение Cert (AC)**: это PFX-файл, который содержит закрытый ключ hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="12f94-135">Создайте этот файл и зашифруйте его с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="12f94-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="12f94-136">При настройке политики доставки ключей, необходимо указать этот пароль и hello PFX-файл в формате Base64.</span><span class="sxs-lookup"><span data-stu-id="12f94-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="12f94-137">Привет, следующие шаги описывают, как toogenerate сертификата PFX-файла для FairPlay:</span><span class="sxs-lookup"><span data-stu-id="12f94-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="12f94-138">Установите OpenSSL со страницы https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="12f94-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="12f94-139">Go toohello папку, где сертификат FairPlay hello и другие файлы, доставленные Apple.</span><span class="sxs-lookup"><span data-stu-id="12f94-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="12f94-140">Выполните следующую команду из командной строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="12f94-141">Это преобразует hello .cer файл tooa PEM-файл.</span><span class="sxs-lookup"><span data-stu-id="12f94-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="12f94-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="12f94-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="12f94-143">Выполните следующую команду из командной строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="12f94-144">Это преобразует hello .pem файл tooa PFX-файл с закрытым ключом hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="12f94-145">затем Hello пароль для PFX-файл hello запрашивается с помощью OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="12f94-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="12f94-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="12f94-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="12f94-147">**Пароль сертификата приложения**: hello пароль для создания hello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="12f94-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="12f94-148">**Идентификатор пароля приложения Cert**: hello пароля, аналогично toohow, они отправляют других ключей служб мультимедиа, необходимо передать.</span><span class="sxs-lookup"><span data-stu-id="12f94-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="12f94-149">Используйте hello **ContentKeyType.FairPlayPfxPassword** hello tooget значение enum, службы мультимедиа по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="12f94-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="12f94-150">Это происходит, они должны toouse внутри hello параметр политики доставки ключей.</span><span class="sxs-lookup"><span data-stu-id="12f94-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="12f94-151">**iv** — случайное 16-байтовое значение.</span><span class="sxs-lookup"><span data-stu-id="12f94-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="12f94-152">Он должен соответствовать hello iv в hello политики доставки активов.</span><span class="sxs-lookup"><span data-stu-id="12f94-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="12f94-153">При создании hello вектора инициализации и поместить его в обоих местах: hello политики доставки активов и параметр политики доставки ключей hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="12f94-154">**ПОПРОСИТЕ**: при создании hello сертификации с помощью портала разработчиков Apple hello получения этого ключа.</span><span class="sxs-lookup"><span data-stu-id="12f94-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="12f94-155">Каждая группа разработчиков получает свой, уникальный ASK.</span><span class="sxs-lookup"><span data-stu-id="12f94-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="12f94-156">Сохранить копию hello ПОПРОСИТЕ и сохраните ее в надежном месте.</span><span class="sxs-lookup"><span data-stu-id="12f94-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="12f94-157">Понадобится tooconfigure ПОПРОСИТЕ как FairPlayAsk tooMedia службы позже.</span><span class="sxs-lookup"><span data-stu-id="12f94-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="12f94-158">**Идентификатор ASK** — этот идентификатор будет получен при отправке ASK в службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="12f94-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="12f94-159">ПОПРОСИТЕ необходимо передать с помощью hello **ContentKeyType.FairPlayAsk** значение перечисления.</span><span class="sxs-lookup"><span data-stu-id="12f94-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="12f94-160">Результат hello возвращается hello идентификатор служб мультимедиа, а это, следует использовать при задании параметра политики доставки ключей hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="12f94-161">Hello следующее должно быть задано при hello кадров в Секунду на стороне клиента:</span><span class="sxs-lookup"><span data-stu-id="12f94-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="12f94-162">**Приложение Cert (AC)**: это.cer/.der файл, содержащий открытый ключ hello, какая операционная система hello использует tooencrypt некоторые полезные данные.</span><span class="sxs-lookup"><span data-stu-id="12f94-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="12f94-163">Службы мультимедиа должно tooknow о нем, так как она затребована проигрывателя hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="12f94-164">Служба доставки ключей Hello расшифровывает его с помощью соответствующего закрытого ключа hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="12f94-165">tooplay резервное зашифрованный поток FairPlay, получать реальные ОБРАТИТЕСЬ в первую очередь, а затем создать реальный сертификат.</span><span class="sxs-lookup"><span data-stu-id="12f94-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="12f94-166">В результате этого процесса создаются три элемента:</span><span class="sxs-lookup"><span data-stu-id="12f94-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="12f94-167">DER-файл;</span><span class="sxs-lookup"><span data-stu-id="12f94-167">.der file</span></span>
  * <span data-ttu-id="12f94-168">PFX-файл;</span><span class="sxs-lookup"><span data-stu-id="12f94-168">.pfx file</span></span>
  * <span data-ttu-id="12f94-169">пароль для PFX-файл hello</span><span class="sxs-lookup"><span data-stu-id="12f94-169">password for hello .pfx</span></span>

<span data-ttu-id="12f94-170">Hello следующие клиенты поддерживают HLS с **CBC AES-128** шифрования: Safari на iOS, OS X, Apple TV.</span><span class="sxs-lookup"><span data-stu-id="12f94-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="12f94-171">Настройка общего динамического шифрования FairPlay и службы доставки лицензий</span><span class="sxs-lookup"><span data-stu-id="12f94-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="12f94-172">Hello ниже приведены общие шаги для защиты активов с FairPlay с помощью службы доставки лицензий Media Services hello, а также с помощью динамического шифрования.</span><span class="sxs-lookup"><span data-stu-id="12f94-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="12f94-173">Создание актива и отправка файлов в актив hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="12f94-174">Кодирование активов hello, содержащий hello файл toohello с адаптивной скоростью набор MP4.</span><span class="sxs-lookup"><span data-stu-id="12f94-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="12f94-175">Создание ключа контента и связать его с активом hello в кодировке.</span><span class="sxs-lookup"><span data-stu-id="12f94-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="12f94-176">Настройка политики авторизации hello ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="12f94-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="12f94-177">Укажите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="12f94-177">Specify hello following:</span></span>

   * <span data-ttu-id="12f94-178">способ доставки Hello (в данном случае FairPlay).</span><span class="sxs-lookup"><span data-stu-id="12f94-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="12f94-179">Конфигурация параметров политики FairPlay.</span><span class="sxs-lookup"><span data-stu-id="12f94-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="12f94-180">Дополнительные сведения о том, как tooconfigure FairPlay, в разделе hello **ConfigureFairPlayPolicyOptions()** метод в следующем примере hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="12f94-181">Как правило вам бы хотелось tooconfigure FairPlay политики параметры только один раз, у вас будет только один набор сертификации и ASK.</span><span class="sxs-lookup"><span data-stu-id="12f94-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="12f94-182">Ограничения (открытая авторизация или с помощью маркера).</span><span class="sxs-lookup"><span data-stu-id="12f94-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="12f94-183">Тип доставки ключей сведения о конкретных toohello, определяющий способ доставки ключа hello toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="12f94-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="12f94-184">Настройка политики доставки активов hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="12f94-185">Конфигурация политики доставки Hello включает:</span><span class="sxs-lookup"><span data-stu-id="12f94-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="12f94-186">протокол доставки Hello (HLS).</span><span class="sxs-lookup"><span data-stu-id="12f94-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="12f94-187">тип динамического шифрования (общее шифрование CBC) Hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="12f94-188">Hello приобретения URL-адрес лицензии.</span><span class="sxs-lookup"><span data-stu-id="12f94-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="12f94-189">Если вы хотите toodeliver поток, который зашифрован FairPlay и другой системой управления цифровыми правами (DRM), у вас есть tooconfigure доставки отдельные политики:</span><span class="sxs-lookup"><span data-stu-id="12f94-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="12f94-190">Один tooconfigure IAssetDeliveryPolicy динамической адаптивной потоковой передачи по HTTP (дефис) с помощью Common Encryption (CENC) (PlayReady + Widevine), а также Smooth с помощью PlayReady</span><span class="sxs-lookup"><span data-stu-id="12f94-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="12f94-191">Другой IAssetDeliveryPolicy tooconfigure FairPlay для HLS</span><span class="sxs-lookup"><span data-stu-id="12f94-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="12f94-192">Создание указателя OnDemand tooget URL-адрес потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="12f94-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="12f94-193">Использование доставки ключей FairPlay приложениями проигрывателей</span><span class="sxs-lookup"><span data-stu-id="12f94-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="12f94-194">Можно разрабатывать приложения проигрывателя с помощью hello iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="12f94-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="12f94-195">toobe может tooplay FairPlay содержимое, у вас есть лицензии exchange tooimplement hello протокола.</span><span class="sxs-lookup"><span data-stu-id="12f94-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="12f94-196">Этот протокол не указывается компанией Apple.</span><span class="sxs-lookup"><span data-stu-id="12f94-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="12f94-197">Он работает приложение tooeach способ доставки ключей toosend запросов.</span><span class="sxs-lookup"><span data-stu-id="12f94-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="12f94-198">Служба доставки ключей Media Services FairPlay Hello ожидает hello SPC toocome в сообщении кодировке post www-form-url, hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="12f94-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="12f94-199">Azure Media Player не поддерживает воспроизведение FairPlay стандартной hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="12f94-200">Воспроизведение FairPlay tooget на MAC OS X, получить образец hello проигрывателя hello учетную запись разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="12f94-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="12f94-201">URL-адреса потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="12f94-201">Streaming URLs</span></span>
<span data-ttu-id="12f94-202">Если актива был зашифрован с более чем одной DRM, следует использовать тег шифрования в URL-адрес потоковой передачи hello: (format = «m3u8-aapl» шифрования = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="12f94-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="12f94-203">применить Hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="12f94-203">hello following considerations apply:</span></span>

* <span data-ttu-id="12f94-204">Можно указать только один тип шифрования или ни одного.</span><span class="sxs-lookup"><span data-stu-id="12f94-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="12f94-205">Тип шифрования Hello не toobe, указанный в URL-адрес hello, если только один шифрования был применен toohello активов.</span><span class="sxs-lookup"><span data-stu-id="12f94-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="12f94-206">Тип шифрования Hello без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="12f94-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="12f94-207">можно указать следующие типы шифрования Hello.</span><span class="sxs-lookup"><span data-stu-id="12f94-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="12f94-208">**cenc** — общее шифрование (Playready или Widevine);</span><span class="sxs-lookup"><span data-stu-id="12f94-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="12f94-209">**cbcs-aapl** — Fairplay;</span><span class="sxs-lookup"><span data-stu-id="12f94-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="12f94-210">**cbc** — шифрование конверта AES.</span><span class="sxs-lookup"><span data-stu-id="12f94-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="12f94-211">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="12f94-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="12f94-212">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="12f94-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="12f94-213">Добавьте следующие элементы слишком hello**appSettings** определенной в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="12f94-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="12f94-214">Пример</span><span class="sxs-lookup"><span data-stu-id="12f94-214">Example</span></span>

<span data-ttu-id="12f94-215">Следующий образец Hello демонстрирует возможности hello toouse toodeliver служб мультимедиа зашифрован FairPlay содержимого.</span><span class="sxs-lookup"><span data-stu-id="12f94-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="12f94-216">Эта возможность появилась в hello Azure Media Services SDK для .NET версии 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="12f94-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="12f94-217">Перезаписать hello код в файле Program.cs кодом hello, приведенные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="12f94-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="12f94-218">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="12f94-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="12f94-219">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="12f94-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="12f94-220">Чтобы узнать больше, ознакомьтесь с [этим](media-services-dotnet-manage-entities.md#limit-access-policies) разделом.</span><span class="sxs-lookup"><span data-stu-id="12f94-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="12f94-221">Сделайте том tooupdate переменных toopoint toofolders где расположены входные файлы.</span><span class="sxs-lookup"><span data-stu-id="12f94-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="12f94-222">Дальнейшие действия: схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="12f94-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="12f94-223">Отзывы</span><span class="sxs-lookup"><span data-stu-id="12f94-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
