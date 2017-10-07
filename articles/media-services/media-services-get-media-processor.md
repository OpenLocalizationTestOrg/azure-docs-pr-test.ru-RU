---
title: "Обработчик мультимедиа с помощью tooCreate aaaHow hello Azure Media Services SDK для .NET | Документы Microsoft"
description: "Узнайте, как toocreate tooencode компонента обработчика мультимедиа, преобразования формата, шифрования или расшифровки содержимого мультимедиа для служб мультимедиа Azure. Примеры кода на языке C# и используйте hello пакета SDK служб мультимедиа для .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>Получение экземпляра процессора мультимедиа
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Обзор
В службах мультимедиа обработчик мультимедиа является компонентом, который работает со специфическими задачами обработки, такими как кодирование, преобразование формата, шифрование или расшифровка мультимедийного контента. Обычно вы Создание обработчика мультимедиа при создании tooencode задачи, зашифровать или преобразовать формат hello мультимедийного содержимого.

## <a name="azure-media-processors"></a>Обработчики мультимедиа Azure 

Hello разделе представлен список обработчиков мультимедиа:

* [Кодировщики мультимедиа](scenarios-and-availability.md#encoding-media-processors)
* [Обработчики мультимедиа аналитики](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>Получение обработчика мультимедиа

Здравствуйте, как следующая показан метод tooget экземпляр обработчика мультимедиа. Hello примере кода предполагается, что используется hello переменную уровня модуля с именем **_контекста** tooreference hello server контекста, как описано в разделе "hello" [как: подключение службы программным образом tooMedia](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы знаете, как перейти tooget экземпляр обработчика мультимедиа toohello [как tooEncode актива](media-services-dotnet-encode-with-media-encoder-standard.md) раздела, в котором мы покажем, как toouse hello Media Encoder Стандартная tooencode актива.

