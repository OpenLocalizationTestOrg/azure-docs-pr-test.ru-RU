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
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>С помощью castLabs toodeliver Widevine лицензий tooAzure служб мультимедиа
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Обзор
В этой статье описывается, как можно использовать toodeliver служб мультимедиа Azure (AMS) поток, который зашифрован динамически AMS с помощью PlayReady и Widevine DRMs. лицензии PlayReady Hello поступают из сервера лицензий PlayReady служб мультимедиа и лицензии Widevine доставляется по **castLabs** сервера лицензирования.

tooplayback потоковой передачи содержимого, защищенного с CENC (PlayReady или Widevine), можно использовать [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Подробные сведения см. в [документе по AMP](http://amp.azure.net/libs/amp/latest/docs/).

Здравствуй, следующая диаграмма демонстрирует высокоуровневая архитектура Azure Media Services и castLabs интеграции.

![интеграция](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Настройка типичной системы
* Мультимедийное содержимое хранится в AMS.
* Идентификаторы ключей содержимого хранятся в castLabs и AMS.
* CastLabs и AMS имеют встроенную проверку подлинности маркеров. Привет, в следующих разделах рассматриваются токены проверки подлинности. 
* Когда клиент запрашивает видео toostream hello, содержимое hello динамически шифруется с **общее шифрование** (CENC) и динамического упаковать с AMS tooSmooth, потоковая передача и ТИРЕ. Для протокола потоковой передачи HLS предлагается также шифрование элементарного потока PlayReady M2TS.
* Лицензию PlayReady выдает сервер лицензирования AMS, а лицензию Widevine — сервер лицензирования castLabs. 
* Проигрыватель автоматически определяет, какие toofetch лицензии основании возможностей платформы клиента hello. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Создания маркеров проверки подлинности для получения лицензии
CastLabs и AMS поддерживает tooauthorize используется формат маркера JWT (веб-маркера JSON) лицензию. 

### <a name="jwt-token-in-ams"></a>Маркер JWT в AMS
Привет, в следующей таблице описываются маркера JWT в AMS. 

| Издатель | Строка поставщика из hello выбранной службы токенов безопасности (STS) |
| --- | --- |
| Аудитория |Строка аудитории из hello используется служба маркеров безопасности |
| Claims |Набор утверждений |
| NotBefore |Начало действия маркера hello |
| Expires |Окончания действия маркера hello |
| SigningCredentials |Hello ключ, который является общим для сервера лицензирования PlayReady, castLabs сервером лицензирования и STS, он может быть либо симметричный или асимметричный ключ. |

### <a name="jwt-token-in-castlabs"></a>Маркер JWT в castLabs
Привет, в следующей таблице описываются маркера JWT в castLabs. 

| Имя | Описание |
| --- | --- |
| optData |Строка JSON со сведениями о вас. |
| crt |Строка JSON, содержащий сведения о средстве hello, его лицензионных прав сведения и воспроизведения. |
| iat |Hello текущую дату и время в начала эпохи. |
| jti |Уникальный идентификатор о этот токен (каждый маркер может использоваться только один раз в системе castLabs hello). |

## <a name="sample-solution-set-up"></a>Настройка образца решения
Hello [образец решения](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) состоит из двух проектов:

* Консольное приложение, которое может быть используется tooset ограничения актива уже полученный DRM PlayReady и Widevine.
* Веб-приложение, которое передает маркеры, которые можно рассматривать как ОЧЕНЬ УПРОЩЕННУЮ версию службы маркеров безопасности.

Консольное приложение hello toouse:

1. Изменить учетные данные toosetup AMS app.config hello, castLabs учетные данные, конфигурации STS и общего ключа.
2. Отправьте файл в AMS.
3. Get hello UUID из hello отправлен активов и измените 32 строки в файл Program.cs hello.
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Используйте AssetId для hello активов в системе castLabs hello (44 строки в файл Program.cs hello).
   
   Необходимо задать AssetId для **castLabs**; он должен toobe уникальный буквенно-цифровую строку.
5. Запустите программу hello.

hello toouse веб-приложения (STS):

1. Изменение hello web.config toosetup castlabs merchant ID, конфигурации STS hello и hello общего ключа.
2. Развертывание tooAzure веб-сайтов.
3. Перейдите toohello веб-сайта.

## <a name="playing-back-a-video"></a>Воспроизведение видео
tooplayback видео зашифрован общее шифрование (PlayReady или Widevine), вы можете использовать hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). При запуске консольного приложения hello, передаются hello идентификатор ключа содержимого и hello URL-адрес манифеста.

1. Откройте новую вкладку и запустите службу маркеров безопасности: http://[имя_службы_маркеров_безопасности].azurewebsites.net/api/token/assetid/[ваш_AssetId_в_CastLabs]/contentkeyid/[идентификатор_ключа_содержимого].
2. Go слишком[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Вставьте URL-адрес потоковой передачи hello.
4. Нажмите кнопку hello **Дополнительно** флажок.
5. В hello **защиты** раскрывающийся список, выберите PlayReady и/или Widevine.
6. Вставьте токен hello, полученного от STS в текстовом поле токен hello. 
   
   сервер лицензирования castLab Hello не обязательно hello» носителя =» префикс перед маркером hello. Поэтому удалите, перед отправкой маркера hello.
7. Обновление проигрывателя hello.
8. должны играть Hello видео.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

