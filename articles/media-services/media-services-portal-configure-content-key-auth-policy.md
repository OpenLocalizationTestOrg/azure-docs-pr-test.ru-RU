---
title: "с помощью содержимого политики авторизации ключа aaaConfigure hello портал Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure политику авторизации для ключа контента."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Настройка политики авторизации ключа содержимого
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Обзор
Службы мультимедиа Microsoft Azure позволяет toodeliver MPEG-DASH, Smooth Streaming и HTTP-Live-Streaming (HLS) потоки, защищенных с помощью Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования) или [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS также позволяет вам toodeliver ТИРЕ потоки зашифрован Widevine DRM. PlayReady и Widevine шифруются на hello спецификации общее шифрование (CENC ISO/IEC 23001-7).

Службы мультимедиа также предоставляют **служба доставки ключа/лицензий** из которых клиенты могут получить ключи AES или PlayReady или Widevine лицензий tooplay hello зашифрованное содержимое.

В этом разделе показано, как toouse hello политики авторизации ключа контента hello Azure tooconfigure портала. Впоследствии можно будет использовать ключ Hello toodynamically шифрования контента. Обратите внимание, что в настоящее время можно зашифровать hello следующие форматы потоковой передачи: HLS, MPEG DASH и Smooth Streaming. Невозможно шифровать последовательно скачиваемые данные.

Когда проигрыватель запрашивает поток, который имеет значение toobe динамически зашифрованы, Media Services использует hello настроен ключа toodynamically шифрования контента с помощью шифрования AES или DRM. поток toodecrypt hello, hello проигрыватель будет запрашивать ключ hello из службы доставки ключей hello. toodecide ли он hello авторизованных tooget hello ключ, hello служба оценивает политики авторизации hello, заданные для ключа hello.

Если требуется планирование toohave нескольких ключей контента или toospecify **служба доставки ключа/лицензий** URL-адрес, отличный от hello служба доставки ключей Media Services, используйте Media Services .NET SDK или API REST.

[Настройка политики авторизации ключей содержимого с помощью пакета .NET SDK служб мультимедиа](media-services-dotnet-configure-content-key-auth-policy.md)

[Настройка политики авторизации ключей содержимого с помощью интерфейсов REST API служб мультимедиа](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Важные особенности
* При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. toostart вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования, потоковой передачи конечной точки потоковой передачи имеет toobe в hello **под управлением** состояния. 
* Ресурс должен содержать набор MP4-файлов с адаптивной скоростью или файлов Smooth Streaming с адаптивной скоростью. Дополнительные сведения см. в статье о [кодировании ресурсов](media-services-encode-asset.md).
* Hello служба доставки ключей кэширует ContentKeyAuthorizationPolicy и связанные объекты (параметры политики и ограничения) в течение 15 минут.  Если создать политику ContentKeyAuthorizationPolicy и укажите toouse ограничения «Token», а затем проверить его, а затем обновить политику hello слишком «открыть» ограниченного использования программ, займет примерно 15 минут, прежде чем hello политики коммутаторы toohello версию «Open» политики hello.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Как: Настройка политики авторизации ключа hello
Политика авторизации ключа hello tooconfigure, выберите hello **защиты СОДЕРЖИМОГО** страницы.

Службы мультимедиа поддерживают несколько способов аутентификации пользователей, которые запрашивают ключи. политики авторизации ключа контента Hello есть **откройте**, **маркера**, или **IP** ограничений авторизации (**IP** могут быть настроены REST или .NET SDK).

### <a name="open-restriction"></a>Ограничение открытого типа
Hello **откройте** ограничение означает hello система будет предоставлять tooanyone ключа hello, выполняющий запрос ключа. Это ограничение подходит для тестирования.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Ограничение по маркеру
токен hello toochoose ограниченной политики, нажмите клавишу hello **МАРКЕРА** кнопки.

Hello **маркера** политики с ограничением должен сопровождаться маркера, выданного **службы токенов безопасности** (STS). Службы мультимедиа поддерживают только токены в hello **токенов SWT** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) формат и **веб-маркера JSON** формате. Дополнительные сведения см. в статье, посвященной [проверке подлинности по маркерам JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Службы мультимедиа не предоставляют **службы маркеров безопасности**. Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS. Hello STS должна быть настроенный toocreate токен, подписанным с hello указанный ключ и выдачи утверждений, которые указаны в конфигурации ограничения токенов hello. Hello служба доставки ключей Media Services возвратит клиент toohello ключа шифрования hello Если hello маркер является допустимым и hello утверждения маркера hello соответствуют настроенным для ключа контента hello. Дополнительные сведения см. в разделе [токены ACS Azure используйте tooissue](http://mingfeiy.com/acs-with-key-services).

При настройке hello **МАРКЕРА** ограничить доступ, необходимо задать значение для **ключ проверки**, **издателя** и **аудитории**. Hello основной ключ проверки содержит hello ключа, что был подписан токен hello, издателем является hello службой маркеров безопасности, выдает маркер hello. аудитория Hello (иногда называется область) описывает намерение hello hello маркера или hello ресурсов hello токен разрешает доступ. Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello.

### <a name="playready"></a>PlayReady
При защите контента с **PlayReady**одно hello сведения, необходимые toospecify в политике авторизации является XML-строку, определяющий шаблон лицензии PlayReady hello. По умолчанию используется значение hello следующие политики:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"> <LicenseTemplates> <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>Nonpersistent</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>Allowed</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates> </PlayReadyLicenseResponseTemplate>

Можно щелкнуть hello **импорта политики xml** кнопку и укажите другой XML, который соответствует toohello XML-схемой, определенной [здесь](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

