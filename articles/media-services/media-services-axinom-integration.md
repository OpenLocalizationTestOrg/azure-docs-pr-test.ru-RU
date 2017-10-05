---
title: "Использование Axinom для предоставления лицензий Widevine для служб мультимедиа Azure | Документация Майкрософт"
description: "В этой статье описывается использование служб мультимедиа Azure (AMS) для доставки потока, который зашифрован динамически службой AMS, с помощью лицензий DRM PlayReady и Widevine. Лицензию PlayReady выдает сервер лицензирования служб мультимедиа PlayReady, а лицензию Widevine — сервер лицензирования Axinom."
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
ms.openlocfilehash: 64e8d4a88ea78e0de065e5a2c12dba4885e08bad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-axinom-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="bf75a-104">Использование Axinom для доставки лицензий Widevine в службы мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="bf75a-104">Using Axinom to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf75a-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="bf75a-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="bf75a-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="bf75a-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bf75a-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="bf75a-107">Overview</span></span>
<span data-ttu-id="bf75a-108">В службы мультимедиа Azure (AMS) добавлена динамическая защита Google Widevine (подробные сведения см. в [блоге Мингфей Ян (Mingfei Yan)](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="bf75a-109">Кроме того, в Проигрыватель мультимедиа Azure (AMP) добавлена поддержка Widevine (подробные сведения см. в [документации по AMP](http://amp.azure.net/libs/amp/latest/docs/)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="bf75a-110">Это большое достижение в потоковой передаче содержимого DASH, защищенного с помощью CENC с несколькими собственными технологиями DRM (PlayReady и Widevine) в современных браузерах, оснащенных MSE и EME.</span><span class="sxs-lookup"><span data-stu-id="bf75a-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="bf75a-111">Начиная с версии 3.5.2 пакета SDK служб мультимедиа для .NET, службы мультимедиа позволяют настраивать шаблоны лицензии Widevine и получать лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf75a-111">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="bf75a-112">Для доставки лицензий Widevine можно использовать следующих партнеров AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="bf75a-112">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="bf75a-113">В этой статье описывается интеграция и тестирование сервера лицензирования Widevine под управлением Axinom.</span><span class="sxs-lookup"><span data-stu-id="bf75a-113">This article describes how to integrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="bf75a-114">В частности, рассматриваются следующие операции:</span><span class="sxs-lookup"><span data-stu-id="bf75a-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="bf75a-115">настройка динамического стандартного шифрования с помощью нескольких технологий DRM (PlayReady и Widevine) с соответствующими URL-адресами для получения лицензии;</span><span class="sxs-lookup"><span data-stu-id="bf75a-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="bf75a-116">создание маркера JWT для удовлетворения требований сервера лицензирования;</span><span class="sxs-lookup"><span data-stu-id="bf75a-116">Generating a JWT token in order to meet the license server requirements;</span></span>
* <span data-ttu-id="bf75a-117">разработка приложения Проигрывателя мультимедиа Azure, которое обрабатывает получение лицензий с помощью проверки подлинности маркеров JWT;</span><span class="sxs-lookup"><span data-stu-id="bf75a-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="bf75a-118">Описание всей системы и процесса передачи ключа содержимого, идентификатора ключа, начального значения, маркера JTW и соответствующих утверждений представлено на следующей схеме.</span><span class="sxs-lookup"><span data-stu-id="bf75a-118">The complete system and the flow of content key, key ID, key seed, JTW token and its claims can be best described by the following diagram.</span></span>

![DASH и CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="bf75a-120">Система защиты содержимого</span><span class="sxs-lookup"><span data-stu-id="bf75a-120">Content Protection</span></span>
<span data-ttu-id="bf75a-121">Сведения о настройке динамической защиты и политики доставки ключей см. в блоге Мингфей Ян (Mingfei Yan) [Как настроить упаковку Widevine с помощью служб мультимедиа Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="bf75a-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How to configure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="bf75a-122">Вы можете настроить динамическую защиту CENC c помощью нескольких технологий DRM для потоковой передачи DASH при наличии двух следующих типов защиты.</span><span class="sxs-lookup"><span data-stu-id="bf75a-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of the following:</span></span>

1. <span data-ttu-id="bf75a-123">Защита PlayReady для MS Edge и IE11, в которой могут быть установлены ограничения авторизации маркеров.</span><span class="sxs-lookup"><span data-stu-id="bf75a-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="bf75a-124">При ограничении по маркеру к политике должен прилагаться маркер, выданный службой маркеров безопасности (STS), например Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf75a-124">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="bf75a-125">Защита Widevine для Chrome (может потребоваться проверка подлинности маркера с помощью маркера, выданного другой службой STS).</span><span class="sxs-lookup"><span data-stu-id="bf75a-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="bf75a-126">В разделе [Создание маркеров JWT](media-services-axinom-integration.md#jwt-token-generation) объясняется, почему Azure Active Directory нельзя использовать в качестве службы маркеров безопасности для сервера лицензирования Widevine Axinom.</span><span class="sxs-lookup"><span data-stu-id="bf75a-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="bf75a-127">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="bf75a-127">Considerations</span></span>
1. <span data-ttu-id="bf75a-128">Чтобы создать ключ содержимого для настройки службы доставки ключей, необходимо использовать заданное начальное значение Axinom (8888000000000000000000000000000000000000) и созданный или выбранный идентификатор ключа.</span><span class="sxs-lookup"><span data-stu-id="bf75a-128">You must use the Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID to generate the content key for configuring key delivery service.</span></span> <span data-ttu-id="bf75a-129">Сервер лицензирования Axinom будет выдавать все лицензии, содержащие ключи содержимого на основе одного начального значения, которое является допустимым как для тестирования, так и для рабочих задач.</span><span class="sxs-lookup"><span data-stu-id="bf75a-129">Axinom license server will issue all licenses containing content keys based on the same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="bf75a-130">URL-адрес для получения лицензии Widevine для тестирования: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="bf75a-130">The Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="bf75a-131">Допускается использование HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf75a-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="bf75a-132">Подготовка Проигрывателя мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="bf75a-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="bf75a-133">Проигрыватель AMP 1.4.0 поддерживает воспроизведение содержимого AMS, которое динамически упаковывается с помощью DRM PlayReady и Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf75a-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="bf75a-134">Если сервер лицензирования Widevine не требует проверки подлинности маркера, для тестирования содержимого DASH, защищенного с помощью Widevine, не требуются никакие дополнительные действия.</span><span class="sxs-lookup"><span data-stu-id="bf75a-134">If Widevine license server does not require token authentication, there is nothing additional you need to do to test a DASH content protected by Widevine.</span></span> <span data-ttu-id="bf75a-135">Например, группа разработчиков для AMP предоставляет простой [пример](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), где можно просмотреть его работу в Edge и IE11 с PlayReady и в Chrome с Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf75a-135">For an example, the AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="bf75a-136">Сервер лицензирования Widevine, предоставляемый Axinom, требует проверки подлинности маркера JWT.</span><span class="sxs-lookup"><span data-stu-id="bf75a-136">The Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="bf75a-137">Маркер JWT должен передаваться с запросом лицензии через заголовок HTTP X-AxDRM-Message.</span><span class="sxs-lookup"><span data-stu-id="bf75a-137">The JWT token needs to be submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="bf75a-138">Для этого перед тем, как задавать источник, на веб-страницу, где размещается AMP, необходимо добавить следующий код JavaScript:</span><span class="sxs-lookup"><span data-stu-id="bf75a-138">For this purpose, you need to add the following javascript in the web page hosting AMP before setting the source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="bf75a-139">Остальная часть кода AMP — стандартный API-интерфейс AMP, как в приведенном [здесь](http://amp.azure.net/libs/amp/latest/docs/)документе по AMP.</span><span class="sxs-lookup"><span data-stu-id="bf75a-139">The rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="bf75a-140">Обратите внимание, что указанный выше код JavaScript для настройки пользовательского заголовка авторизации все же является временным решением, которое будет действовать до выпуска официального постоянного решения для AMP.</span><span class="sxs-lookup"><span data-stu-id="bf75a-140">Note that the above javascript for setting custom authorization header is still a short term approach before the official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="bf75a-141">Создание маркеров JWT</span><span class="sxs-lookup"><span data-stu-id="bf75a-141">JWT Token Generation</span></span>
<span data-ttu-id="bf75a-142">Сервер лицензирования Widevine для тестирования, предоставляемый Axinom, требует проверки подлинности маркера JWT.</span><span class="sxs-lookup"><span data-stu-id="bf75a-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="bf75a-143">Кроме того, одно из утверждений в маркере JWT является объектом сложного типа, а не данными примитивного типа.</span><span class="sxs-lookup"><span data-stu-id="bf75a-143">In addition, one of the claims in the JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="bf75a-144">К сожалению, Azure AD может выдавать маркеры JWT только примитивного типа.</span><span class="sxs-lookup"><span data-stu-id="bf75a-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="bf75a-145">Аналогично API .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler и JwtPayload) позволяет использовать в качестве входных данных только утверждения сложного типа.</span><span class="sxs-lookup"><span data-stu-id="bf75a-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you to input complex object type as claims.</span></span> <span data-ttu-id="bf75a-146">При этом утверждения по-прежнему сериализуются как строка.</span><span class="sxs-lookup"><span data-stu-id="bf75a-146">However, the claims are still serialized as string.</span></span> <span data-ttu-id="bf75a-147">Поэтому мы не можем использовать ни один из этих типов, чтобы создать маркер JWT по запросу лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf75a-147">Therefore we cannot use any of the two for generating the JWT token for Widevine license request.</span></span>

<span data-ttu-id="bf75a-148">Мы будем использовать [пакет NuGet JWT](https://www.nuget.org/packages/JWT) Джона Шиэна (John Sheehan), так как он соответствует требованиям.</span><span class="sxs-lookup"><span data-stu-id="bf75a-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets the needs so we are going to use this Nuget package.</span></span>

<span data-ttu-id="bf75a-149">Ниже приведен код для создания маркера JWT с утверждениями, которые требуются для тестирования сервером лицензирования Axinom Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf75a-149">Below is the code for generating JWT token with the needed claims as required by Axinom Widevine license server for testing:</span></span>

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
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string to byte[] Note: Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string to byte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "The binary key cannot have an odd number of digits: {0}", hexString));
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

<span data-ttu-id="bf75a-150">Сервер лицензирования Axinom Widevine</span><span class="sxs-lookup"><span data-stu-id="bf75a-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="bf75a-151">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="bf75a-151">Considerations</span></span>
1. <span data-ttu-id="bf75a-152">Хотя служба доставки лицензий AMS PlayReady требует наличия перед маркером проверки подлинности префикса Bearer=, сервер лицензирования Axinom Widevine не использует его.</span><span class="sxs-lookup"><span data-stu-id="bf75a-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="bf75a-153">В качестве ключа подписи используется ключ обмена данными Axinom.</span><span class="sxs-lookup"><span data-stu-id="bf75a-153">The Axinom communication key is used as signing key.</span></span> <span data-ttu-id="bf75a-154">Обратите внимание, что этот ключ представляет собой шестнадцатеричную строку, однако при кодировании его следует рассматривать как последовательность байтов, а не как строку.</span><span class="sxs-lookup"><span data-stu-id="bf75a-154">Note that the key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="bf75a-155">Это возможно при использовании метода ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="bf75a-155">This is achieved by the method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="bf75a-156">Получение идентификатора ключа</span><span class="sxs-lookup"><span data-stu-id="bf75a-156">Retrieving Key ID</span></span>
<span data-ttu-id="bf75a-157">Вы могли заметить, что в коде, создающем маркер JWT, идентификатор ключа является обязательным.</span><span class="sxs-lookup"><span data-stu-id="bf75a-157">You may have noticed that in the code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="bf75a-158">Поскольку маркер JWT должен быть создан до загрузки проигрывателя AMP, вам сначала необходимо получить идентификатор ключа.</span><span class="sxs-lookup"><span data-stu-id="bf75a-158">Since the JWT token needs to be ready before loading AMP player, key ID needs to be retrieved in order to generate JWT token.</span></span>

<span data-ttu-id="bf75a-159">Это можно сделать несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="bf75a-159">Of course there are multiple ways to get hold of key ID.</span></span> <span data-ttu-id="bf75a-160">Например, идентификатор ключа может храниться вместе с метаданными содержимого в базе данных.</span><span class="sxs-lookup"><span data-stu-id="bf75a-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="bf75a-161">Также ключ можно извлечь из MPD-файла DASH.</span><span class="sxs-lookup"><span data-stu-id="bf75a-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="bf75a-162">В следующем фрагменте кода реализован второй способ.</span><span class="sxs-lookup"><span data-stu-id="bf75a-162">The code below is for the latter.</span></span>

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

## <a name="summary"></a><span data-ttu-id="bf75a-163">Сводка</span><span class="sxs-lookup"><span data-stu-id="bf75a-163">Summary</span></span>
<span data-ttu-id="bf75a-164">В систему защиты содержимого служб мультимедиа Azure и Проигрыватель мультимедиа Azure недавно добавлена поддержка Widevine. Благодаря этому мы смогли реализовать потоковую передачу DASH и нескольких собственных технологий DRM (PlayReady + Widevine) со службой лицензий PlayReady в AMS и сервером лицензирования Widevine от Axinom для следующих современных браузеров:</span><span class="sxs-lookup"><span data-stu-id="bf75a-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able to implement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for the following modern browsers:</span></span>

* <span data-ttu-id="bf75a-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="bf75a-165">Chrome</span></span>
* <span data-ttu-id="bf75a-166">Microsoft Edge под управлением Windows 10.</span><span class="sxs-lookup"><span data-stu-id="bf75a-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="bf75a-167">IE 11 под управлением Windows 8.1 и Windows 10.</span><span class="sxs-lookup"><span data-stu-id="bf75a-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="bf75a-168">Проигрыватель мультимедиа Azure также поддерживает браузеры Firefox (классический) и Safari под управлением Mac OS (не iOS) посредством Silverlight и того же URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="bf75a-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and the same URL with Azure Media Player</span></span>

<span data-ttu-id="bf75a-169">Для мини-решения, в котором используется сервер лицензирования Axinom Widevine, требуются следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="bf75a-169">The following parameters are required in the mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="bf75a-170">Все параметры, кроме ключа идентификатора, предоставляются Axinom в соответствии с настройками сервера Widevine.</span><span class="sxs-lookup"><span data-stu-id="bf75a-170">Except for key ID, the rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="bf75a-171">Параметр</span><span class="sxs-lookup"><span data-stu-id="bf75a-171">Parameter</span></span> | <span data-ttu-id="bf75a-172">Использование</span><span class="sxs-lookup"><span data-stu-id="bf75a-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="bf75a-173">Идентификатор ключа обмена данными</span><span class="sxs-lookup"><span data-stu-id="bf75a-173">Communication key ID</span></span> |<span data-ttu-id="bf75a-174">Должен быть включен в качестве значения утверждения com_key_id в маркере JWT ([подробнее](media-services-axinom-integration.md#jwt-token-generation)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-174">Must be included as value of the claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="bf75a-175">Ключ обмена данными</span><span class="sxs-lookup"><span data-stu-id="bf75a-175">Communication key</span></span> |<span data-ttu-id="bf75a-176">Должен использоваться в качестве ключа подписывания маркера JWT ([подробнее](media-services-axinom-integration.md#jwt-token-generation)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-176">Must be used as the signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="bf75a-177">Начальное значение ключа</span><span class="sxs-lookup"><span data-stu-id="bf75a-177">Key seed</span></span> |<span data-ttu-id="bf75a-178">Должно использоваться для создания ключа содержимого с любым заданным идентификатором ключа содержимого ([подробнее](media-services-axinom-integration.md#content-protection)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-178">Must be used to generate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="bf75a-179">URL-адрес для приобретения лицензии Widevine</span><span class="sxs-lookup"><span data-stu-id="bf75a-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="bf75a-180">Должен использоваться при настройке политики доставки ресурсов-контейнеров для потоковой передачи DASH ([подробнее](media-services-axinom-integration.md#content-protection)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="bf75a-181">Идентификатор ключа содержимого</span><span class="sxs-lookup"><span data-stu-id="bf75a-181">Content Key ID</span></span> |<span data-ttu-id="bf75a-182">Должен быть включен в значение утверждения сообщения об обслуживании маркера JWT ([подробнее](media-services-axinom-integration.md#jwt-token-generation)).</span><span class="sxs-lookup"><span data-stu-id="bf75a-182">Must be included as part of the value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="bf75a-183">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="bf75a-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bf75a-184">Отзывы</span><span class="sxs-lookup"><span data-stu-id="bf75a-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="bf75a-185">Благодарности</span><span class="sxs-lookup"><span data-stu-id="bf75a-185">Acknowledgments</span></span>
<span data-ttu-id="bf75a-186">Мы выражаем признательность тем, кто помог нам в составлении этого документа — это Кристьян Йоджи (Kristjan Jõgi) из Axinom, Мингфей Ян (Mingfei Yan) и Амит Раджпут (Amit Rajput).</span><span class="sxs-lookup"><span data-stu-id="bf75a-186">We would like to acknowledge the following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

