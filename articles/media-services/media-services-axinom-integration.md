---
title: "aaaUsing Axinom toodeliver Widevine лицензий tooAzure Media Services | Документы Microsoft"
description: "В этой статье описывается, как можно использовать toodeliver служб мультимедиа Azure (AMS) поток, который зашифрован динамически AMS с помощью PlayReady и Widevine DRMs. лицензии PlayReady Hello поступают из сервера лицензий PlayReady служб мультимедиа и лицензии Widevine доставляется сервером лицензирования Axinom."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="35d24-104">С помощью Axinom toodeliver Widevine лицензий tooAzure служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="35d24-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35d24-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="35d24-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="35d24-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="35d24-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="35d24-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="35d24-107">Overview</span></span>
<span data-ttu-id="35d24-108">В службы мультимедиа Azure (AMS) добавлена динамическая защита Google Widevine (подробные сведения см. в [блоге Мингфей Ян (Mingfei Yan)](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)).</span><span class="sxs-lookup"><span data-stu-id="35d24-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="35d24-109">Кроме того, в Проигрыватель мультимедиа Azure (AMP) добавлена поддержка Widevine (подробные сведения см. в [документации по AMP](http://amp.azure.net/libs/amp/latest/docs/)).</span><span class="sxs-lookup"><span data-stu-id="35d24-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="35d24-110">Это большое достижение в потоковой передаче содержимого DASH, защищенного с помощью CENC с несколькими собственными технологиями DRM (PlayReady и Widevine) в современных браузерах, оснащенных MSE и EME.</span><span class="sxs-lookup"><span data-stu-id="35d24-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="35d24-111">Начиная с пакета SDK .NET служб мультимедиа версии 3.5.2 hello, Media Services позволяет вам tooconfigure Widevine шаблон лицензии и получить лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="35d24-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="35d24-112">Можно также использовать следующие toohelp партнеров AMS доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="35d24-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="35d24-113">В этой статье описывается, каким образом управляются Axinom сервера лицензий toointegrate и тестирования Widevine.</span><span class="sxs-lookup"><span data-stu-id="35d24-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="35d24-114">В частности, рассматриваются следующие операции:</span><span class="sxs-lookup"><span data-stu-id="35d24-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="35d24-115">настройка динамического стандартного шифрования с помощью нескольких технологий DRM (PlayReady и Widevine) с соответствующими URL-адресами для получения лицензии;</span><span class="sxs-lookup"><span data-stu-id="35d24-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="35d24-116">Создание токена JWT в порядке toomeet hello server требования к лицензиям;</span><span class="sxs-lookup"><span data-stu-id="35d24-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="35d24-117">разработка приложения Проигрывателя мультимедиа Azure, которое обрабатывает получение лицензий с помощью проверки подлинности маркеров JWT;</span><span class="sxs-lookup"><span data-stu-id="35d24-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="35d24-118">Здравствуйте всю систему и hello потока содержимого, которые идентификатор ключевые, ключевые, начальное значение ключа, маркер JTW и его утверждения может быть наилучшим образом описана hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="35d24-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH и CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="35d24-120">Система защиты содержимого</span><span class="sxs-lookup"><span data-stu-id="35d24-120">Content Protection</span></span>
<span data-ttu-id="35d24-121">Для настройки динамических защиты и доставки ключей политики, см. в разделе Мингфей в блоге: [как tooconfigure Widevine упаковку со службами мультимедиа Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="35d24-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="35d24-122">Можно настроить защиту динамического CENC с несколькими DRM для потоковой передачи, имеющих оба следующих hello ТИРЕ:</span><span class="sxs-lookup"><span data-stu-id="35d24-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="35d24-123">Защита PlayReady для MS Edge и IE11, в которой могут быть установлены ограничения авторизации маркеров.</span><span class="sxs-lookup"><span data-stu-id="35d24-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="35d24-124">Hello политики с ограничением токенов должна сопровождаться маркера, выданного по токенов безопасности службы (STS), таких как Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="35d24-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="35d24-125">Защита Widevine для Chrome (может потребоваться проверка подлинности маркера с помощью маркера, выданного другой службой STS).</span><span class="sxs-lookup"><span data-stu-id="35d24-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="35d24-126">В разделе [Создание маркеров JWT](media-services-axinom-integration.md#jwt-token-generation) объясняется, почему Azure Active Directory нельзя использовать в качестве службы маркеров безопасности для сервера лицензирования Widevine Axinom.</span><span class="sxs-lookup"><span data-stu-id="35d24-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="35d24-127">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="35d24-127">Considerations</span></span>
1. <span data-ttu-id="35d24-128">Необходимо использовать hello Axinom указать начальное значение ключа (8888000000000000000000000000000000000000) и созданного или выбранного ключа идентификатор toogenerate hello содержимого ключ для настройки службы доставки ключей.</span><span class="sxs-lookup"><span data-stu-id="35d24-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="35d24-129">Сервер лицензирования Axinom выдаст все лицензии, содержащий на основе ключей контента на hello ключ начальное значение, которое является допустимым для тестирования и производства.</span><span class="sxs-lookup"><span data-stu-id="35d24-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="35d24-130">Hello Widevine приобретения URL-адрес для тестирования: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="35d24-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="35d24-131">Допускается использование HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="35d24-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="35d24-132">Подготовка Проигрывателя мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="35d24-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="35d24-133">Проигрыватель AMP 1.4.0 поддерживает воспроизведение содержимого AMS, которое динамически упаковывается с помощью DRM PlayReady и Widevine.</span><span class="sxs-lookup"><span data-stu-id="35d24-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="35d24-134">Если сервер лицензирования Widevine не требует проверки подлинности маркера, отсутствуют дополнительные необходимые tootest toodo защищенного содержимого ТИРЕ, Widevine.</span><span class="sxs-lookup"><span data-stu-id="35d24-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="35d24-135">Например, группа hello AMP предоставляет простой [пример](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), где можно просмотреть его работа в Edge и IE11 с помощью PlayReady и хром с Widevine.</span><span class="sxs-lookup"><span data-stu-id="35d24-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="35d24-136">сервер лицензирования Widevine Hello, предоставляемые Axinom требует проверки подлинности маркера JWT.</span><span class="sxs-lookup"><span data-stu-id="35d24-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="35d24-137">токен JWT Hello должен toobe отправлено с запрос лицензии через заголовок HTTP «X AxDRM сообщение».</span><span class="sxs-lookup"><span data-stu-id="35d24-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="35d24-138">Для этой цели необходимо tooadd hello, следуя javascript на веб-странице hello размещение AMP перед hello источник параметров:</span><span class="sxs-lookup"><span data-stu-id="35d24-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="35d24-139">Hello остальной части кода AMP — Стандартная AMP API как документе AMP [здесь](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="35d24-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="35d24-140">Обратите внимание, что hello выше javascript для настраиваемого заголовка настраиваемой авторизации подход по-прежнему более короткий срок перед официальные hello выпуска долгосрочный подход в AMP параметра.</span><span class="sxs-lookup"><span data-stu-id="35d24-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="35d24-141">Создание маркеров JWT</span><span class="sxs-lookup"><span data-stu-id="35d24-141">JWT Token Generation</span></span>
<span data-ttu-id="35d24-142">Сервер лицензирования Widevine для тестирования, предоставляемый Axinom, требует проверки подлинности маркера JWT.</span><span class="sxs-lookup"><span data-stu-id="35d24-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="35d24-143">Кроме того один hello утверждений в токене JWT hello — сложный объект типа вместо примитивный тип данных.</span><span class="sxs-lookup"><span data-stu-id="35d24-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="35d24-144">К сожалению, Azure AD может выдавать маркеры JWT только примитивного типа.</span><span class="sxs-lookup"><span data-stu-id="35d24-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="35d24-145">Аналогично API .NET Framework (обработчик System.IdentityModel.Tokens.SecurityTokenHandler и JwtPayload) можно только tooinput сложный объект типа в виде утверждений.</span><span class="sxs-lookup"><span data-stu-id="35d24-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="35d24-146">Тем не менее hello утверждений по-прежнему будут сериализованы как строки.</span><span class="sxs-lookup"><span data-stu-id="35d24-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="35d24-147">Поэтому не удается использовать любой из двух hello для создания маркера JWT hello для запрос лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="35d24-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="35d24-148">Джон Sheehan [пакет JWT Nuget](https://www.nuget.org/packages/JWT) соответствует hello потребностей, мы будем toouse этот пакет Nuget.</span><span class="sxs-lookup"><span data-stu-id="35d24-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="35d24-149">Ниже приведен код hello для создания маркера JWT с hello необходимые утверждения, требуемые для сервера лицензирования Axinom Widevine для тестирования.</span><span class="sxs-lookup"><span data-stu-id="35d24-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

<span data-ttu-id="35d24-150">Сервер лицензирования Axinom Widevine</span><span class="sxs-lookup"><span data-stu-id="35d24-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="35d24-151">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="35d24-151">Considerations</span></span>
1. <span data-ttu-id="35d24-152">Хотя служба доставки лицензий AMS PlayReady требует наличия перед маркером проверки подлинности префикса Bearer=, сервер лицензирования Axinom Widevine не использует его.</span><span class="sxs-lookup"><span data-stu-id="35d24-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="35d24-153">Hello Axinom связи используется в качестве ключа подписи.</span><span class="sxs-lookup"><span data-stu-id="35d24-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="35d24-154">Обратите внимание, что разделу hello является шестнадцатеричную строку, однако он должен рассматриваться как последовательность байтов не является строкой при кодировании.</span><span class="sxs-lookup"><span data-stu-id="35d24-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="35d24-155">Это достигается с помощью метода hello ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="35d24-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="35d24-156">Получение идентификатора ключа</span><span class="sxs-lookup"><span data-stu-id="35d24-156">Retrieving Key ID</span></span>
<span data-ttu-id="35d24-157">Вы могли заметить, что в код создания JWT hello требуется идентификатор токена, ключевые.</span><span class="sxs-lookup"><span data-stu-id="35d24-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="35d24-158">Так как токен JWT hello должен toobe готовности перед загрузкой AMP проигрывателя, основные потребности идентификатор toobe, полученный в заказ маркера JWT toogenerate.</span><span class="sxs-lookup"><span data-stu-id="35d24-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="35d24-159">Конечно, существует несколько способов хранения tooget ключа по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="35d24-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="35d24-160">Например, идентификатор ключа может храниться вместе с метаданными содержимого в базе данных.</span><span class="sxs-lookup"><span data-stu-id="35d24-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="35d24-161">Также ключ можно извлечь из MPD-файла DASH.</span><span class="sxs-lookup"><span data-stu-id="35d24-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="35d24-162">Hello код предназначен для второй hello.</span><span class="sxs-lookup"><span data-stu-id="35d24-162">hello code below is for hello latter.</span></span>

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a><span data-ttu-id="35d24-163">Сводка</span><span class="sxs-lookup"><span data-stu-id="35d24-163">Summary</span></span>
<span data-ttu-id="35d24-164">С новейшей Widevine поддержки в Защита контента служб мультимедиа Azure и Azure Media Player, мы получаем доступ tooimplement потоковой передачи штриха + / native DRM (PlayReady + Widevine) с обе службы лицензий PlayReady в AMS и Widevine лицензии сервер Axinom для hello, следуя современных браузеров:</span><span class="sxs-lookup"><span data-stu-id="35d24-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="35d24-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="35d24-165">Chrome</span></span>
* <span data-ttu-id="35d24-166">Microsoft Edge под управлением Windows 10.</span><span class="sxs-lookup"><span data-stu-id="35d24-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="35d24-167">IE 11 под управлением Windows 8.1 и Windows 10.</span><span class="sxs-lookup"><span data-stu-id="35d24-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="35d24-168">(Desktop) Firefox и Safari на Mac (не операций ввода-вывода), также поддерживаются через Silverlight и hello же URL-адрес с помощью Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="35d24-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="35d24-169">Hello следующие параметры необходимы в сервер лицензий путем использования Axinom Widevine hello мини-решений.</span><span class="sxs-lookup"><span data-stu-id="35d24-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="35d24-170">За исключением ключ идентификатора, hello остальных параметров предоставляются на основе их настройки сервера Widevine Axinom.</span><span class="sxs-lookup"><span data-stu-id="35d24-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="35d24-171">Параметр</span><span class="sxs-lookup"><span data-stu-id="35d24-171">Parameter</span></span> | <span data-ttu-id="35d24-172">Использование</span><span class="sxs-lookup"><span data-stu-id="35d24-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="35d24-173">Идентификатор ключа обмена данными</span><span class="sxs-lookup"><span data-stu-id="35d24-173">Communication key ID</span></span> |<span data-ttu-id="35d24-174">Должен быть включен как значение утверждения hello «com_key_id» в токене JWT (см. [это](media-services-axinom-integration.md#jwt-token-generation) раздел).</span><span class="sxs-lookup"><span data-stu-id="35d24-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="35d24-175">Ключ обмена данными</span><span class="sxs-lookup"><span data-stu-id="35d24-175">Communication key</span></span> |<span data-ttu-id="35d24-176">Следует использовать как ключ подписи токена JWT hello (см. [это](media-services-axinom-integration.md#jwt-token-generation) раздел).</span><span class="sxs-lookup"><span data-stu-id="35d24-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="35d24-177">Начальное значение ключа</span><span class="sxs-lookup"><span data-stu-id="35d24-177">Key seed</span></span> |<span data-ttu-id="35d24-178">Ключ содержимого toogenerate используется с любым иметь содержимое ИД ключа (см. [это](media-services-axinom-integration.md#content-protection) раздел).</span><span class="sxs-lookup"><span data-stu-id="35d24-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="35d24-179">URL-адрес для приобретения лицензии Widevine</span><span class="sxs-lookup"><span data-stu-id="35d24-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="35d24-180">Должен использоваться при настройке политики доставки ресурсов-контейнеров для потоковой передачи DASH ([подробнее](media-services-axinom-integration.md#content-protection)).</span><span class="sxs-lookup"><span data-stu-id="35d24-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="35d24-181">Идентификатор ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="35d24-181">Content Key ID</span></span> |<span data-ttu-id="35d24-182">Должен быть включен в состав значение hello правах сообщение утверждения маркера JWT (см. [это](media-services-axinom-integration.md#jwt-token-generation) раздел).</span><span class="sxs-lookup"><span data-stu-id="35d24-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="35d24-183">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="35d24-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="35d24-184">Отзывы</span><span class="sxs-lookup"><span data-stu-id="35d24-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="35d24-185">Благодарности</span><span class="sxs-lookup"><span data-stu-id="35d24-185">Acknowledgments</span></span>
<span data-ttu-id="35d24-186">Мы хотели бы tooacknowledge hello, выполнив специалистами по созданию этого документа, влияющая: Kristjan Jõgi из Axinom, Yan Мингфей и Amit Rajput.</span><span class="sxs-lookup"><span data-stu-id="35d24-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

