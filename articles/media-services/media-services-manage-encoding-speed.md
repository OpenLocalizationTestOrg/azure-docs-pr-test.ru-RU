---
title: "скорость управление AAA и параллелизм кодирования с помощью служб мультимедиа Azure | Документы Microsoft"
description: "В этой статье вкратце описывается, как можно управлять скоростью и параллелизмом кодирования заданий и задач с помощью служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Управление скоростью и параллелизмом кодирования

В этой статье вкратце описывается, как можно управлять скоростью и параллелизмом кодирования заданий и задач.

## <a name="overview"></a>Обзор

В службах мультимедиа **тип зарезервированных единиц** определяет hello скорость обработки задач обработки мультимедиа. Можно выбрать между hello следующие зарезервированные типы единиц измерения: **S1**, **S2**, или **S3**. Например, hello же кодированию выполняется быстрее при использовании hello **S2** тип зарезервированных единиц сравнить toohello **S1** типа. Hello [масштабирование единиц кодирования](media-services-scale-media-processing-overview.md) разделе показана таблица, которая поможет принять решение, при выборе между различные скорости кодирования.

Кроме toospecifying hello зарезервировано тип единицы измерения, можно указать tooprovision свою учетную запись с **зарезервированных единиц**. Hello количество провизионированных зарезервированных единиц определяет hello количество мультимедийных задач, которые можно одновременно обрабатывать в данной учетной записи. Например если ваша учетная запись имеет пять зарезервированных единиц, то пять мультимедийных задач будет выполняться параллельно при условии, как существуют toobe задачи обработки. Hello оставшиеся задачи будут ожидать в очереди hello и будут извлекаться последовательно обработки после завершения выполняющихся задач. Если учетная запись не имеет подготовленных зарезервированных единиц, задачи будут отбираться последовательно. В этом случае hello время ожидания между один завершение задачи и hello началом будет зависеть от hello доступность ресурсов в системе hello.

Подробные сведения и примеры где показано, как tooscale единицы кодирования, в разделе [это](media-services-scale-media-processing-overview.md) раздела.

## <a name="next-step"></a>Дальнейшие действия

[Масштабирование единиц кодирования](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

