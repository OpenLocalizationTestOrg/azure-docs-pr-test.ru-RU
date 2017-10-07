---
title: "aaaAzure Media Services часто задаваемые вопросы | Документы Microsoft"
description: "Часто задаваемые вопросы (FAQ)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

В этой статье рассматриваются часто задаваемые вопросы hello сообщества пользователей служб мультимедиа Azure (AMS).

## <a name="general-ams-faqs"></a>Общие часто задаваемые вопросы об AMS и ответы на них
Вопрос. Как осуществляется масштабирование индексирования?

Ответ hello зарезервированных единиц hello же для кодировки и задачи индексирования. Следуйте инструкциям на [как кодирование зарезервированных единиц tooScale](media-services-scale-media-processing-overview.md). **Обратите внимание**, что производительность индексирования не зависит от типа зарезервированных единиц.

Вопрос. Видео отправлено, закодировано и опубликовано. Было бы hello причина hello видео не воспроизводится при попытке toostream его?

Ответ один из hello, чаще всего причин, по которой необходимо hello, из которого вы пытаетесь tooplayback в hello конечной точки потоковой передачи **под управлением** состояния.  

Вопрос. Можно ли объединять видео в динамическом потоке?

Ответ компоновка на обновляющиеся потоки в настоящее время не содержится в Azure Media Services, потребовалось бы toopre-составлено на локальном компьютере.

Вопрос. Можно ли использовать Azure CDN с динамической потоковой передачей?

Ответ Media Services позволяет интегрировать сети доставки Содержимого Azure (Дополнительные сведения см. в разделе [как tooManage потоковые конечные точки в учетную запись служб мультимедиа](media-services-portal-manage-streaming-endpoints.md)).  Вы можете использовать динамическую потоковую передачу с CDN. Службы мультимедиа Azure предоставляют выходные данные в форматах Smooth Streaming, HLS и MPEG-DASH. Все они используют протокол HTTP для передачи данных, а также кэширование HTTP. В динамической потоковой передачи фактических данных аудио/видео разделенная toofragments и это отдельные фрагменты помещаться в CDN. Только данные потребностей toobe обновленные данные hello манифеста. CDN периодически обновляет данные манифеста.

Вопрос. Службы мультимедиа Azure поддерживают хранение изображений?

Ответ, если требуется просто toostore JPEG или PNG-изображений, следует хранить в хранилище больших двоичных объектов Azure. Нет не tooputting преимущество, их в службах мультимедиа учетной записи, если не требуется, чтобы tookeep их, связанной с видео или аудио активы. Или, если возможно toouse необходимость hello изображения как слои в кодировщик видео hello. Стандартный кодировщик мультимедиа поддерживает изображения наложения объектов поверх видео и, что перечислены JPEG или PNG, поддерживаемой форматы входных данных. Дополнительные сведения см. в статье [Создание наложений](media-services-advanced-encoding-with-mes.md#overlay).

Вопрос. как копировать ресурсы из одного tooanother учетной записи служб мультимедиа.

Ответ toocopy ресурсам с помощью одной учетной записи службы мультимедиа tooanother, с помощью .NET, используйте [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) метод расширения, доступные в hello [расширения SDK .NET служб мультимедиа Azure](https://github.com/Azure/azure-sdk-for-media-services-extensions/) репозитория. Дополнительные сведения см. в [этой теме форума](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices).

Вопрос. что hello поддерживаются символы для имен файлов, при работе с AMS?

Ответ службы мультимедиа использует значение hello hello свойство IAssetFile.Name при построении URL-адреса для hello, потоковая передача содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается. Здравствуйте, значение hello **имя** свойство не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []». Кроме того, может использоваться только один знак ".". для расширения имени файла hello.

Вопрос. как tooconnect с помощью REST?

Ответ для получения сведений о как tooconnect toohello AMS API, см. статью [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI. 

Вопрос. как поворот видео во время кодирования процесса hello.

Ответ Здравствуйте, [Media Encoder Стандартная](media-services-dotnet-encode-with-media-encoder-standard.md) поддерживает поворот по углы 90, 180 или 270. поведение по умолчанию Hello является «Auto», где она пытается toodetect hello поворота метаданных в файл MP4 или MOV входящих hello и компенсации для него. Включить следующие hello **источников** tooone элемент определен предустановок json hello [здесь](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
