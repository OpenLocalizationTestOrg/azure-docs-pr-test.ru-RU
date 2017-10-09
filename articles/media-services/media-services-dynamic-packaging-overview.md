---
title: "Общие сведения о динамической упаковки служб мультимедиа aaaAzure | Документы Microsoft"
description: "раздел содержит Hello и общие сведения о динамической упаковки."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>Динамическая упаковка
## <a name="overview"></a>Обзор
Службы мультимедиа Microsoft Azure можно использовать toodeliver много media source форматы файлов, форматов потоковой передачи мультимедиа и защиты содержимого форматы tooa разных технологиях клиента (например, iOS, XBOX, Silverlight, Windows 8). Эти клиенты работают по разным протоколам: например, для iOS используется формат потоковой трансляции HTTP (HLS) V4, а для технологий Silverlight и Xbox необходимо использовать формат Smooth Streaming. Если у вас есть набор с адаптивной скоростью (с несколькими скоростями) MP4 файлов (ISO Base Media 14496-12) или набор файлов Smooth Streaming с адаптивной скоростью, которые должны tooclients tooserve понимают MPEG DASH, HLS или Smooth Streaming, следует воспользоваться преимуществами мультимедиа Динамическая упаковка служб.

С помощью динамической упаковки достаточно — toocreate актив, содержащий набор файлов MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью. Затем на основе заданного формата hello в манифесте hello или фрагмента запроса, hello server проверит Получение потока hello в протоколе hello, которую вы выбрали потоковой передачи по требованию. В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.

Hello следующей схеме показан hello традиционное кодирование и статическая упаковка рабочего процесса.

![Статическое кодирование](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Hello следующей диаграмме показан рабочий процесс hello динамической упаковки.

![Динамическое кодирование](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Стандартный сценарий
1. Отправьте входной файл (он также называется мезонинным). Например, H.264, MP4 или WMV (hello список поддерживаемых форматов см. [форматы, поддерживаемые Media Encoder Стандартная hello](media-services-media-encoder-standard-formats.md).
2. Закодируйте мезонинный файл tooH.264 MP4 с адаптивной скоростью наборов.
3. Опубликуйте hello актив, содержащий hello, создав локатор по запросу hello набор MP4 с адаптивной скоростью.
4. Построение hello tooaccess URL-адреса потоковой передачи и потоковую передачу контента.

## <a name="preparing-assets-for-dynamic-streaming"></a>Подготовка ресурсов для динамической потоковой передачи
tooprepare актива для динамической потоковой передачи можно использовать два варианта:

1. [Отправьте главный файл](media-services-dotnet-upload-files.md).
2. [Использовать hello Media Encoder стандартный кодировщик tooproduce H.264 MP4 с адаптивной скоростью наборы](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Выполните потоковую передачу содержимого](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Форматы, не поддерживаемые динамической упаковкой
Hello следующие форматы исходных файлов не поддерживаются для динамической упаковки.

* MP4-файлы в формате Dolby Digital.
* Файлы Smooth в формате Dolby Digital.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

