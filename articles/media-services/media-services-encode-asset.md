---
title: "aaaOverview и сравнение Azure на требование кодировщики мультимедиа | Документы Microsoft"
description: "В этой статье приводится обзор и сравнение кодировщиков мультимедиа Azure по запросу."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Обзор и сравнение кодировщиков мультимедиа Azure по запросу
## <a name="encoding-overview"></a>Общие сведения о Службе кодирования
Службы мультимедиа Azure предоставляют несколько параметров для кодирования hello носителя в облаке hello.

При запуске с помощью служб мультимедиа, это важно toounderstand hello разницу между кодеками и форматами файлов.
Кодеки — hello программное обеспечение, которое реализует hello алгоритмы сжатия и распаковки, тогда как форматы файлов являются контейнерами, содержащими hello сжатия видео.

Служба Media Services предоставляет динамической упаковки, позволяющий toodeliver с адаптивным битрейтом MP4 или Smooth Streaming кодировке содержимого в потоковом форматы, поддерживаемые службами мультимедиа (MPEG DASH, HLS, Smooth Streaming) без необходимости toore-package в такие Потоковая передача форматы.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. преимущества tootake [динамической упаковки](media-services-dynamic-packaging-overview.md), требуется toodo hello следующее:
>
>Кроме того кодирование файла исходного кода в набор файлов MP4 с адаптивной скоростью или файлы Smooth Streaming с адаптивной скоростью (hello кодирования действия приведены далее в этом учебнике).

Службы мультимедиа поддерживают следующие hello по запросу кодировщиков, описанных в этой статье:

* [Стандартный кодировщик служб мультимедиа](media-services-encode-asset.md#media-encoder-standard)
* [Рабочий процесс Media Encoder Premium](media-services-encode-asset.md#media-encoder-premium-workflow)

В этой статье предоставляет краткий обзор по запросу мультимедиа кодировщиков и предоставляет tooarticles ссылки, которая позволяет получить более подробные сведения. Hello раздел также содержит сравнения кодировщиков hello.

>[!NOTE]
>По умолчанию каждая учетная запись служб мультимедиа может выполнять одну активную задачу кодирования в текущий момент. Можно зарезервировать единицы кодирования, которые позволят вам toohave несколько задачи кодирования параллельно; одна для зарезервированную единицу кодирования приобретения. Дополнительные сведения см. в статье [Обзор масштабирования обработка мультимедиа](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Стандартный кодировщик служб мультимедиа
### <a name="how-toouse"></a>Как toouse
[Как tooencode стандарту кодировщика мультимедиа](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Форматы
[Форматы и кодеки](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Предустановки
Стандартный кодировщик мультимедиа настраивается с помощью одного из описанных предустановки кодировщика hello [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Входные и выходные метаданные
Hello входных метаданных кодировщики описан [здесь](media-services-input-metadata-schema.md).

Hello кодировщики выходные метаданные описан [здесь](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Создание эскизов
Сведения см. в разделе [как эскизы toogenerate, с помощью Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>Усечение видео (обрезка)
Сведения см. в разделе [как tootrim видео, с помощью Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Создание наложений
Сведения см. в разделе [как toocreate слои с помощью Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>См. также
[Блог Hello служб мультимедиа](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Расширенный рабочий процесс кодировщика мультимедиа
### <a name="overview"></a>Обзор
[Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Как toouse
Рабочий процесс Premium кодировщика мультимедиа настраивается с помощью сложных рабочих процессов. Файлы рабочего процесса может быть создан и обновлен с использованием hello [конструктора рабочих процессов](media-services-workflow-designer.md) средства.

[Как tooUse расширенной кодировки в службах мультимедиа Azure](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Известные проблемы
Если входной видео не содержит титров, hello выходной ресурс по-прежнему будет содержать пустой файл TTML.


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Связанные статьи
* [Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа](media-services-custom-mes-presets-with-dotnet.md)
* [Квоты и ограничения](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
