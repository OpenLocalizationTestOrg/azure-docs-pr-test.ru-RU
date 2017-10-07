---
title: "aaaProtect содержимого с помощью служб мультимедиа Azure | Документы Microsoft"
description: "В этой статье представлен обзор защиты содержимого с помощью служб мультимедиа."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Общие сведения о защите содержимого
Службы мультимедиа Microsoft Azure позволяет вам toosecure мультимедиа из hello раз, когда он покидает вашему компьютеру посредством хранения, обработки и доставки. Media Services позволяет toodeliver по требованию и динамического содержимого зашифрован динамически Advanced Encryption Standard (AES) (с помощью 128-битные ключи шифрования) или любой из hello основных DRMs: Microsoft PlayReady, Google Widevine и Apple FairPlay. Службы мультимедиа также предоставляют службу доставки ключей AES и управления цифровыми правами (PlayReady, Widevine и FairPlay) лицензирует tooauthorized клиентов. 

Следующие изображения Hello демонстрирует защиты содержимого hello рабочие процессы, которые поддерживает AMS. 

![Защита с помощью PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 

В этом разделе объясняется [основные понятия и терминология](media-services-content-protection-overview.md) соответствующие toounderstanding защиты содержимого с AMS. Hello раздел также содержит [ссылки](media-services-content-protection-overview.md#common-scenarios) tootopics, которые показывают, как tooachieve содержимого задач защиты. 

## <a name="dynamic-encryption"></a>Динамическое шифрование
Службы мультимедиа Microsoft Azure позволяет toodeliver содержимое шифруется динамически незащищенный ключ AES или шифрования DRM: Microsoft PlayReady, Google Widevine и Apple FairPlay.

В настоящее время можно зашифровать hello следующие форматы потоковой передачи: HLS, MPEG DASH и Smooth Streaming. Невозможно шифровать последовательно скачиваемые данные.

Если требуется для служб мультимедиа tooencrypt актива, требуется ключ шифрования (CommonEncryption и EnvelopeEncryption) tooassociate с ресурсом и также настроить политики авторизации для ключа hello.

Необходимо также политику доставки актива tooconfigure hello. Если необходимо toostream зашифрованного актива хранилища, убедитесь, что toospecify способ toodeliver его путем настройки политики доставки активов.

Когда проигрыватель запрашивает поток, службы мультимедиа используют указанный hello ключа toodynamically зашифровать ваш контент с помощью незащищенный ключ AES или шифрования DRM. поток toodecrypt hello, hello проигрыватель будет запрашивать ключ hello из службы доставки ключей hello. toodecide ли он hello авторизованных tooget hello ключ, hello служба оценивает политики авторизации hello, заданные для ключа hello.


## <a name="storage-encryption"></a>Шифрование хранилища
Использовать локально с помощью AES 256-разрядного шифрования незащищенного контента tooencrypt шифрования хранилища, а затем передать его tooAzure хранилища, где она хранится в зашифрованном виде. Активы, защищенные с помощью шифрования хранилища, автоматически дешифруются и помещаются в предыдущих tooencoding зашифрованный файл системы и при необходимости повторно зашифрован предыдущих toouploading возвращены в виде нового выходного актива. Hello основным случаем использования шифрования хранилища удобно, если нужно toosecure rest вашей высококачественных входных файлов мультимедиа с помощью строгого шифрования на диске.

В порядке toodeliver зашифрованного актива хранилища необходимо настроить политику доставки актива hello, службы мультимедиа получили информацию о способе toodeliver контента. Перед потоковой актива hello, потоковая передача контента с помощью hello шифрование хранилища сервера удаляет hello и потоки указан политики доставки (например, AES, общее шифрование или шифрование).

## <a name="common-encryption-cenc"></a>Общее шифрование (CENC)
Общее шифрование используется при шифровании содержимого с помощью PlayReady и (или) Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Использование шифрования cbcs-aapl
Cbcs-aapl используется при шифровании содержимого с помощью FairPlay.

## <a name="envelope-encryption"></a>Шифрование конверта
Используйте этот параметр, если требуется tooprotect контента с незащищенный ключ AES-128. Если требуется более высокий уровень защищенности, выберите одно из hello DRMs, перечисленных в этом разделе. 

## <a name="licenses-and-keys-delivery-service"></a>Служба доставки лицензий и ключей
Служба Media Services предоставляет услугу для доставки лицензии DRM (PlayReady, Widevine, FairPlay) и очистки клиентов tooauthorized ключей AES. Можно использовать [hello портал Azure](media-services-portal-protect-content.md), API-интерфейса REST или пакета SDK служб мультимедиа для .NET tooconfigure политики авторизации и проверки подлинности для лицензий и ключей.

## <a name="token-restriction"></a>Ограничение по маркеру
Hello политики авторизации ключа контента может иметь одно или несколько ограничений авторизации: открыть или маркер ограниченного использования программ. политика с ограничением токенов Hello должны сопровождаться маркера, выданного по токенов безопасности службы (STS). Службы мультимедиа поддерживают только токены в формате JSON Web Token (JWT) и формат hello простой веб-токены (SWT). Службы мультимедиа не предоставляют службы маркеров безопасности. Можно создать настраиваемую STS или использовать токены tooissue Microsoft Azure ACS. Hello STS должна быть настроенный toocreate токен, подписанным с hello указанный ключ и выдачи утверждений, которые указаны в конфигурации ограничения токенов hello. Службы мультимедиа Hello службы доставки ключей, то возвращается hello запрошенную ключей (или лицензий) клиента toohello, если токен hello действителен и hello утверждений в hello маркера соответствует настроенным ключей hello (или лицензий).

При настройке политики с ограничением токенов hello, необходимо указать hello основной ключ проверки, издателя и аудитории параметров. Hello основной ключ проверки содержит hello ключа, что был подписан токен hello, издателем является hello службой маркеров безопасности, выдает маркер hello. аудитория Hello (иногда называется область) описывает намерение hello hello маркера или hello ресурсов hello токен разрешает доступ. Hello служба доставки ключей Media Services проверяет, эти значения в токене hello соответствуют значениям hello в шаблоне hello.

## <a name="streaming-urls"></a>URL-адреса потоковой передачи
Если актива был зашифрован с более чем одной DRM, следует использовать тег шифрования в URL-адрес потоковой передачи hello: (format = «m3u8-aapl» шифрования = 'xxx').

применить Hello следующие вопросы:

* Можно указать только один тип шифрования или ни одного.
* Тип шифрования не имеет toobe, указанный в URL-адрес hello, если только один шифрования был применен toohello активов.
* Тип шифрования вводится без учета регистра.
* можно указать следующие типы шифрования Hello.  
  * **cenc**: общее шифрование (Playready или Widevine);
  * **cbcs-aapl**: Fairplay;
  * **cbc**: шифрование конверта AES.

## <a name="common-scenarios"></a>Распространенные сценарии
Hello следующих разделах демонстрируется tooprotect содержимое в хранилище, предоставляют динамически зашифрованные потоковой передачи мультимедиа, воспользуйтесь AMS служба доставки ключа/лицензий

* [Использование динамического шифрования AES-128 и службы доставки ключей](media-services-protect-with-aes128.md) 
* [Использование общего динамического шифрования PlayReady и (или) Widevine DRM ](media-services-protect-with-drm.md)
* [Использование служб мультимедиа Azure для потоковой передачи содержимого HLS, защищенного с помощью Apple FairPlay](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Дополнительные сценарии
* [Как службы toointegrate лицензий Azure PlayReady с собственного сервера или потоковой передачи шифратор](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [С помощью castLabs toodeliver DRM лицензий tooAzure служб мультимедиа](media-services-castlabs-integration.md)

>[!NOTE]
>Сценарий, в котором используется внешний сервер (технология) DRM и поток из AMS, в настоящее время не поддерживается.


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Представляем новые возможности служб мультимедиа Azure: функцию динамического шифрования AES и PlayReady как службу](http://mingfeiy.com/playready)

[Разъяснение ценовой политики для доставки лицензий PlayReady служб мультимедиа Azure](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Способ toodebug для AES-шифрования потока в службах мультимедиа Azure](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Аутентификация по токенам JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Интегрируйте приложение на основе OWIN MVC служб мультимедиа Azure с Azure Active Directory и ограничьте доставку ключей содержимого на основе утверждений JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Использовать токены Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
