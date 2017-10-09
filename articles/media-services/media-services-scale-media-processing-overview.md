---
title: "Общие сведения об обработке мультимедиа aaaScaling | Документы Microsoft"
description: "В этом разделе рассматривается масштабирование обработки мультимедиа с помощью служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Обзор масштабирования обработка мультимедиа
На этой странице приведены общие сведения о том, как и почему tooscale обработкой мультимедиа. 

## <a name="overview"></a>Обзор
Учетная запись служб мультимедиа связан с зарезервированным тип базового определяет hello скорость обработки задач обработки мультимедиа. Можно выбрать между hello следующие зарезервированные типы единиц измерения: **S1**, **S2**, или **S3**. Например, hello же кодированию выполняется быстрее при использовании hello **S2** тип зарезервированных единиц сравнить toohello **S1** типа. Дополнительные сведения см. в разделе hello [типы зарезервированных единиц](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

Кроме toospecifying hello зарезервировано тип единицы измерения, можно указать tooprovision вашей учетной записи зарезервированных единиц. Hello количество провизионированных зарезервированных единиц определяет hello количество мультимедийных задач, которые можно одновременно обрабатывать в данной учетной записи. Например если ваша учетная запись имеет пять зарезервированных единиц, то пять мультимедийных задач будет выполняться параллельно при условии, как существуют toobe задачи обработки. Hello оставшиеся задачи будут ожидать в очереди hello и будут извлекаться последовательно обработки после завершения выполняющихся задач. Если учетная запись не имеет подготовленных зарезервированных единиц, задачи будут отбираться последовательно. В этом случае hello время ожидания между один завершение задачи и hello началом будет зависеть от hello доступность ресурсов в системе hello.

## <a name="choosing-between-different-reserved-unit-types"></a>Выбор между разными типами зарезервированных единиц
в следующей таблице Hello помогает принятия решения при выборе между различные скорости кодирования. Оно также предоставляет несколько вариантов теста производительности и предоставляет URL-адреса SAS, который можно использовать toodownload видео, в которых можно выполнить собственное тестирование:

| Сценарии | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Предполагаемый вариант использования |Односкоростное кодирование. <br/>Файлы с разрешением SD или ниже, без учета времени, низкие затраты. |Односкоростное и многоскоростное кодирование.<br/>Обычное использование для кодирования SD и HD. |Односкоростное и многоскоростное кодирование.<br/>Видеоролики с разрешением Full HD и 4К. С учетом времени, более быстрое полное кодирование. |
| Тест производительности |[Входной файл: длительность — 5 минут; 640x360p, 29,97 кадра в секунду](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Кодировка файла tooa односкоростной MP4 в hello же разрешением занимает около 11 минут. |[Входной файл: длительность — 5 минут; 1280x720p, 29,97 кадра в секунду](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Кодирование с предустановкой H264 Single Bitrate 720p длится около 5 минут.<br/><br/>Кодирование с предустановкой H264 Multiple Bitrate 720p длится 11,5 минуты. |[Входной файл: длительность — 5 минут; 1920x1080p, 29,97 кадра в секунду](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>Кодирование с предустановкой H264 Single Bitrate 1080p длится 2,7 минуты.<br/><br/>Кодирование с предустановкой H264 Multiple Bitrate 1080p длится 5,7 минуты. |

## <a name="considerations"></a>Рекомендации
> [!IMPORTANT]
> Просмотрите рекомендации, приведенные в этом разделе.  
> 
> 

* Зарезервированные единицы работают для параллелизации всей обработки мультимедиа, включая задания индексирования с использованием индексатора мультимедийных данных Azure.  Однако в отличие от кодировки, задания индексирования не будут обрабатываться быстрее при использовании более производительных зарезервированных единиц.
* При использовании общих hello пула, то есть, без каких-либо зарезервированные единицы, а затем к задачам encode hello производительности с помощью S1 RUs. Однако нет времени toohello верхняя граница не могут проводить задач в состоянии в очереди, и в любой момент времени только одна задача будет выполняться.
* Hello, следуя центрах обработки данных, не обеспечивают hello **S2** зарезервировано тип единиц измерения: Южной Бразилии и Западная Индия.
* Hello следующие центра обработки данных не предлагает hello **S3** зарезервировано тип единиц измерения: Западная Индия.

## <a name="billing"></a>Выставление счетов

Цена зависит от фактического времени использования зарезервированных единиц мультимедиа. Подробное описание в разделе часто задаваемые вопросы о hello hello [цены Media Services](https://azure.microsoft.com/pricing/details/media-services/) страницы.   

## <a name="quotas-and-limitations"></a>Квоты и ограничения
Сведения о квотах и ограничениях и как увидеть tooopen обращение в службу поддержки, [квоты и ограничения](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Дальнейшие действия
Достичь hello масштабирование media обработки задачи с помощью одного из этих технологий. 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Портал](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

