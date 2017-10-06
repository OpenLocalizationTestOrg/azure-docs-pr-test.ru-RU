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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>С помощью Axinom toodeliver Widevine лицензий tooAzure служб мультимедиа
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Обзор
В службы мультимедиа Azure (AMS) добавлена динамическая защита Google Widevine (подробные сведения см. в [блоге Мингфей Ян (Mingfei Yan)](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)). Кроме того, в Проигрыватель мультимедиа Azure (AMP) добавлена поддержка Widevine (подробные сведения см. в [документации по AMP](http://amp.azure.net/libs/amp/latest/docs/)). Это большое достижение в потоковой передаче содержимого DASH, защищенного с помощью CENC с несколькими собственными технологиями DRM (PlayReady и Widevine) в современных браузерах, оснащенных MSE и EME.

Начиная с пакета SDK .NET служб мультимедиа версии 3.5.2 hello, Media Services позволяет вам tooconfigure Widevine шаблон лицензии и получить лицензии Widevine. Можно также использовать следующие toohelp партнеров AMS доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

В этой статье описывается, каким образом управляются Axinom сервера лицензий toointegrate и тестирования Widevine. В частности, рассматриваются следующие операции:  

* настройка динамического стандартного шифрования с помощью нескольких технологий DRM (PlayReady и Widevine) с соответствующими URL-адресами для получения лицензии;
* Создание токена JWT в порядке toomeet hello server требования к лицензиям;
* разработка приложения Проигрывателя мультимедиа Azure, которое обрабатывает получение лицензий с помощью проверки подлинности маркеров JWT;

Здравствуйте всю систему и hello потока содержимого, которые идентификатор ключевые, ключевые, начальное значение ключа, маркер JTW и его утверждения может быть наилучшим образом описана hello следующие схемы.

![DASH и CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Система защиты содержимого
Для настройки динамических защиты и доставки ключей политики, см. в разделе Мингфей в блоге: [как tooconfigure Widevine упаковку со службами мультимедиа Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

Можно настроить защиту динамического CENC с несколькими DRM для потоковой передачи, имеющих оба следующих hello ТИРЕ:

1. Защита PlayReady для MS Edge и IE11, в которой могут быть установлены ограничения авторизации маркеров. Hello политики с ограничением токенов должна сопровождаться маркера, выданного по токенов безопасности службы (STS), таких как Azure Active Directory;
2. Защита Widevine для Chrome (может потребоваться проверка подлинности маркера с помощью маркера, выданного другой службой STS). 

В разделе [Создание маркеров JWT](media-services-axinom-integration.md#jwt-token-generation) объясняется, почему Azure Active Directory нельзя использовать в качестве службы маркеров безопасности для сервера лицензирования Widevine Axinom.

### <a name="considerations"></a>Рекомендации
1. Необходимо использовать hello Axinom указать начальное значение ключа (8888000000000000000000000000000000000000) и созданного или выбранного ключа идентификатор toogenerate hello содержимого ключ для настройки службы доставки ключей. Сервер лицензирования Axinom выдаст все лицензии, содержащий на основе ключей контента на hello ключ начальное значение, которое является допустимым для тестирования и производства.
2. Hello Widevine приобретения URL-адрес для тестирования: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). Допускается использование HTTP и HTTPS.

## <a name="azure-media-player-preparation"></a>Подготовка Проигрывателя мультимедиа Azure
Проигрыватель AMP 1.4.0 поддерживает воспроизведение содержимого AMS, которое динамически упаковывается с помощью DRM PlayReady и Widevine.
Если сервер лицензирования Widevine не требует проверки подлинности маркера, отсутствуют дополнительные необходимые tootest toodo защищенного содержимого ТИРЕ, Widevine. Например, группа hello AMP предоставляет простой [пример](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), где можно просмотреть его работа в Edge и IE11 с помощью PlayReady и хром с Widevine.
сервер лицензирования Widevine Hello, предоставляемые Axinom требует проверки подлинности маркера JWT. токен JWT Hello должен toobe отправлено с запрос лицензии через заголовок HTTP «X AxDRM сообщение». Для этой цели необходимо tooadd hello, следуя javascript на веб-странице hello размещение AMP перед hello источник параметров:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

Hello остальной части кода AMP — Стандартная AMP API как документе AMP [здесь](http://amp.azure.net/libs/amp/latest/docs/).

Обратите внимание, что hello выше javascript для настраиваемого заголовка настраиваемой авторизации подход по-прежнему более короткий срок перед официальные hello выпуска долгосрочный подход в AMP параметра.

## <a name="jwt-token-generation"></a>Создание маркеров JWT
Сервер лицензирования Widevine для тестирования, предоставляемый Axinom, требует проверки подлинности маркера JWT. Кроме того один hello утверждений в токене JWT hello — сложный объект типа вместо примитивный тип данных.

К сожалению, Azure AD может выдавать маркеры JWT только примитивного типа. Аналогично API .NET Framework (обработчик System.IdentityModel.Tokens.SecurityTokenHandler и JwtPayload) можно только tooinput сложный объект типа в виде утверждений. Тем не менее hello утверждений по-прежнему будут сериализованы как строки. Поэтому не удается использовать любой из двух hello для создания маркера JWT hello для запрос лицензии Widevine.

Джон Sheehan [пакет JWT Nuget](https://www.nuget.org/packages/JWT) соответствует hello потребностей, мы будем toouse этот пакет Nuget.

Ниже приведен код hello для создания маркера JWT с hello необходимые утверждения, требуемые для сервера лицензирования Axinom Widevine для тестирования.

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

Сервер лицензирования Axinom Widevine

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Рекомендации
1. Хотя служба доставки лицензий AMS PlayReady требует наличия перед маркером проверки подлинности префикса Bearer=, сервер лицензирования Axinom Widevine не использует его.
2. Hello Axinom связи используется в качестве ключа подписи. Обратите внимание, что разделу hello является шестнадцатеричную строку, однако он должен рассматриваться как последовательность байтов не является строкой при кодировании. Это достигается с помощью метода hello ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Получение идентификатора ключа
Вы могли заметить, что в код создания JWT hello требуется идентификатор токена, ключевые. Так как токен JWT hello должен toobe готовности перед загрузкой AMP проигрывателя, основные потребности идентификатор toobe, полученный в заказ маркера JWT toogenerate.

Конечно, существует несколько способов хранения tooget ключа по идентификатору. Например, идентификатор ключа может храниться вместе с метаданными содержимого в базе данных. Также ключ можно извлечь из MPD-файла DASH. Hello код предназначен для второй hello.

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

## <a name="summary"></a>Сводка
С новейшей Widevine поддержки в Защита контента служб мультимедиа Azure и Azure Media Player, мы получаем доступ tooimplement потоковой передачи штриха + / native DRM (PlayReady + Widevine) с обе службы лицензий PlayReady в AMS и Widevine лицензии сервер Axinom для hello, следуя современных браузеров:

* Chrome
* Microsoft Edge под управлением Windows 10.
* IE 11 под управлением Windows 8.1 и Windows 10.
* (Desktop) Firefox и Safari на Mac (не операций ввода-вывода), также поддерживаются через Silverlight и hello же URL-адрес с помощью Azure Media Player

Hello следующие параметры необходимы в сервер лицензий путем использования Axinom Widevine hello мини-решений. За исключением ключ идентификатора, hello остальных параметров предоставляются на основе их настройки сервера Widevine Axinom.

| Параметр | Использование |
| --- | --- |
| Идентификатор ключа обмена данными |Должен быть включен как значение утверждения hello «com_key_id» в токене JWT (см. [это](media-services-axinom-integration.md#jwt-token-generation) раздел). |
| Ключ обмена данными |Следует использовать как ключ подписи токена JWT hello (см. [это](media-services-axinom-integration.md#jwt-token-generation) раздел). |
| Начальное значение ключа |Ключ содержимого toogenerate используется с любым иметь содержимое ИД ключа (см. [это](media-services-axinom-integration.md#content-protection) раздел). |
| URL-адрес для приобретения лицензии Widevine |Должен использоваться при настройке политики доставки ресурсов-контейнеров для потоковой передачи DASH ([подробнее](media-services-axinom-integration.md#content-protection)). |
| Идентификатор ключа содержимого |Должен быть включен в состав значение hello правах сообщение утверждения маркера JWT (см. [это](media-services-axinom-integration.md#jwt-token-generation) раздел). |

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Благодарности
Мы хотели бы tooacknowledge hello, выполнив специалистами по созданию этого документа, влияющая: Kristjan Jõgi из Axinom, Yan Мингфей и Amit Rajput.

