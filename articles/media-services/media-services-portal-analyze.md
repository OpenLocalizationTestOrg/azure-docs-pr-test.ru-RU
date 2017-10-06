---
title: "aaaAnalyze носителя с помощью hello портал Azure | Документы Microsoft"
description: "В этом разделе рассматриваются как tooprocess мультимедиа с помощью обработчиков мультимедиа медиа-аналитика (MP) с помощью hello портал Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Анализ мультимедиа с помощью портала Azure hello
> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Обзор
Azure Media Services Analytics — это коллекция речи и представление компонентов (на корпоративном уровне соответствия, безопасности и глобальный доступ), упрощают процесс принятия решений tooderive предприятия и организации их видеофайлов. Подробные сведения об аналитике служб мультимедиа Azure см. в [этой статье](media-services-analytics-overview.md). 

В этом разделе рассматриваются как tooprocess мультимедиа с помощью обработчиков мультимедиа медиа-аналитика (MP) с помощью hello портал Azure. Обработчики мультимедийных данных служб медиааналитики создают файлы в формате MP4 или JSON. Если обработчик мультимедиа созданы MP4-файл, можно загрузить файл hello постепенно. Если обработчик мультимедиа созданы JSON-файл, можно загрузить файл hello из hello хранилище больших двоичных объектов. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Выберите средства, которые должны tooanalyze
1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. В hello **параметры** выберите **активы**.  
   .
    ![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Выберите hello активов, которые будут tooanalyze и нажмите клавишу hello **анализ** кнопки.
   
    ![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. В hello **процесса актив мультимедиа с медиа-аналитика** окно, выберите hello процессора. 
   
    Hello оставшейся части статьи hello объясняется, почему и как toouse каждого процессора. 
5. Нажмите клавишу **создать** toohello запуска задания.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Hello **индексатора мультимедиа Azure** обработчик мультимедиа позволяет toomake файлы и контент мультимедиа с возможностью поиска, а также создавать дорожек со скрытыми субтитрами. В этих разделах подробно описываются некоторые сведения о параметрах, которые можно указать для обработчика мультимедиа.

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Язык
Здравствуйте, распознаваемые в файл мультимедиа hello toobe естественного языка. например английский или испанский. 

### <a name="captions"></a>Субтитры
Вы можете выбрать формат субтитров, который будет создаваться из контента. Задание индексирования можно создать файлы титров hello следующие форматы:  

* **SAMI**
* **TTML**
* **WebVTT**

Закрытых субтитров (CC) файлов в этих форматах можно использовать toomake аудио и видео файлы доступны toopeople возможностями слуха.

### <a name="aib-file"></a>Файл AIB
Выберите этот параметр, если вы бы как файл toogenerate hello аудио индекс большого двоичного объекта, для использования с hello пользовательский фильтр IFilter SQL Server. Дополнительную информацию см. в [этом](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) блоге.

### <a name="keywords"></a>Ключевые слова
Выберите этот параметр, если вы хотите toogenerate файл XML ключевые слова. Этот файл содержит ключевые слова, извлеченные из голосового содержимого hello, с частотой и сведения о смещении.

### <a name="job-name"></a>Имя задания
Понятное имя, позволяющее определить задания hello. [Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello. 

### <a name="output-file"></a>Выходной файл
Понятное имя, позволяющее определить hello выходных данных. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure Media Hyperlapse — это обработчик мультимедиа, который создает плавное замедленное видео от первого лица или контент, характерный для экшн-камер.  Дополнительные сведения см. в [этой статье](media-services-hyperlapse-content.md). В этих разделах подробно описываются некоторые сведения о параметрах, которые можно указать для обработчика мультимедиа.

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Speed
Укажите скорость hello с какой toospeed hello входного видео. Hello выводится представление hello входное видео в стабилизации и промежуток времени.

### <a name="job-name"></a>Имя задания
Понятное имя, позволяющее определить задания hello. [Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello. 

### <a name="output-file"></a>Выходной файл
Понятное имя, позволяющее определить hello выходных данных. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
Hello **детектор лицевой стороны Azure Media** обработчик мультимедиа (MP) позволяет toocount, перемещений отслеживания и даже участие аудитории датчика и реакция через выражения лица. В этой службе реализованы две функции: 

* **Обнаружение лиц**
  
    Функция обнаружения лиц используется для обнаружения и отслеживания человеческих лиц на видео. Несколько фрагментов могут быть обнаружены и впоследствии отслеживаются перемещения, с hello времени и расположение метаданных, возвращаемых в файле JSON. Во время отслеживания, он попытается toogive согласованного toohello идентификатор же сталкиваются при hello пользователь перемещается на экране, даже в том случае, если они являются действия или кратко оставьте hello кадра.
  
  > [!NOTE]
  > Эта служба не поддерживает распознавание лиц. Лицо, которое отправляется hello кадра или становится действия для слишком долго получает новый идентификатор при подключении.
  > 
  > 
* **Определение эмоций**
  
    Обнаружение эмоций — это необязательный компонент hello обработчик мультимедиа обнаружения начертания, возвращающий анализа на несколько атрибутов этому из hello гарнитуры обнаружено, включая счастье, sadness, опасаясь, anger и многое другое. 

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Режим распознавания
Можно использовать один из следующих режимов hello обработчиком hello:

* обнаружение лиц;
* распознавание эмоций отдельных лиц;
* распознавание общих эмоций.

### <a name="job-name"></a>Имя задания
Понятное имя, позволяющее определить задания hello. [Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello. 

### <a name="output-file"></a>Выходной файл
Понятное имя, позволяющее определить hello выходных данных. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
Hello **Детектор движения Azure Media** media процессора (MP) позволяет вам tooefficiently указывают разделы интерес в видео, в противном случае длинные и процедура. Обнаружение движения может использоваться с камеры статических материал tooidentify разделами видео hello которой происходит движения. Он создает JSON-файл, содержащий метаданные с метки времени и hello, ограничивающий область, где произошло событие hello.

Ориентирован видео безопасности веб-каналы, эта технология является движения может toocategorize в соответствующие события и ложных положительных результатов, такие как изменение освещения и тени. Это позволяет toogenerate оповещений системы безопасности из каналов камеры без личного веб-узла с событиями бесконечные значения, не может tooextract моменты процент от видео с очень длинными наблюдения.

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Этот процессор помогают создавать сводки по видеофайлов большого размера, выбрав автоматически интересные фрагменты hello источника видео. Это полезно при необходимости tooprovide краткий обзор какие tooexpect в длинного видео. Подробные сведения и примеры см. в разделе [tooCreate используйте Azure Media Video эскизы сводку видео](media-services-video-summarization.md)

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>Имя задания
Понятное имя, позволяющее определить задания hello. [Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello. 

### <a name="output-file"></a>Выходной файл
Понятное имя, позволяющее определить hello выходных данных. 

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

