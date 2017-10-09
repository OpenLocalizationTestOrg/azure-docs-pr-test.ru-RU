---
title: "грани aaaRedact с медиа-аналитика Azure Пошаговое руководство | Документы Microsoft"
description: "В этом разделе показано пошаговые инструкции о том, как toorun полного исправления рабочего процесса с помощью обозревателя служб мультимедиа Azure (AMSE) и Azure Media Redactor визуализатора (средство с открытым исходным кодом)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Пошаговое руководство скрытия лиц с помощью аналитики мультимедиа Azure

## <a name="overview"></a>Обзор

**Azure Media Redactor** — [медиа-аналитика Azure](media-services-analytics-overview.md) обработчик мультимедиа (MP), который предлагает исправления масштабируемой лицевой стороны в облаке hello. Исправления лицевой стороны позволяет вам toomodify видео в гранях tooblur порядок выбранных сотрудников. Вы можете toouse hello начертания исправления службы в общих сценариях безопасности и новости мультимедиа. Через несколько минут, содержащий несколько начертаний материал может занять tooredact часы вручную, но с этой службы hello начертания процесс исправления потребуется всего несколько простых шагов. Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-redactor/).

Дополнительные сведения о **Redactor мультимедиа Azure**, hello в разделе [Обзор исправления лицевой](media-services-face-redaction.md) раздела.

В этом разделе показано пошаговые инструкции о том, как toorun полного исправления рабочего процесса с помощью обозревателя служб мультимедиа Azure (AMSE) и Azure Media Redactor визуализатора (средство с открытым исходным кодом).

Hello **Redactor мультимедиа Azure** MP в настоящее время находится в предварительной версии. Он доступен во всех общедоступных регионах Azure, а также в центрах обработки данных для государственных организаций США и для Китая. В настоящее время эта предварительная версия предоставляется бесплатно. В текущем выпуске hello отсутствует ограничение по 10-минутного обработанные продолжительность видео.

Дополнительную информацию см. в [этом](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) блоге.

## <a name="azure-media-services-explorer-workflow"></a>Рабочий процесс Azure Media Services Explorer

Hello tooget простой способ работы с Redactor — средство AMSE toouse hello открытым исходным кодом на сайте github. Можно запустить упрощенный рабочего процесса через **вместе** режим, если не требуется доступ к toohello заметки json или hello начертания изображений jpg.

### <a name="download-and-setup"></a>Скачивание и установка

1. Загрузите средство AMSE hello из [здесь](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Войдите в tooyour учетная запись служб мультимедиа с помощью ключа службы.

    Здравствуйте tooobtain имя учетной записи и сведения о ключе, последовательно выберите toohello [портал Azure](https://portal.azure.com/) и выберите свою учетную запись AMS. Последовательно выберите "Параметры" > "Ключи". ключи windows Hello управление показывает имя учетной записи hello и отображается hello первичного и вторичного ключей. Скопируйте значения hello имя учетной записи и первичный ключ hello.

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>Первый цикл — режим анализа

1. Передайте файл мультимедиа, щелкнув "Ресурс-контейнер" > "Отправить" или перетащив его. 
1. Щелкните правой кнопкой мыши файла мультимедиа и обработайте его, выбрав "Media Analytics" (Медиа-аналитика) > "Azure Media Redactor" > "Analyze mode" (Режим анализа). 


![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

Hello результат будет включать файл json заметки с данными расположение лицевой стороны, а также jpg каждого обнаруженного гарнитур. 

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>Второй цикл — режим скрытия

1. Отправка исходного toohello видео активов выходные данные из первого этапа hello и задайте в качестве основного средства. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (Необязательно) Отправьте файл «Dance_idlist.txt», который включает список hello идентификаторы, которые вы хотите tooredact перехода на новую строку с разделителями. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (Необязательно) Сделайте любые изменения toohello annotations.json файл как увеличение hello ограничивающего границы рамки. 
4. Щелкните правой кнопкой мыши hello выходной ресурс из первого этапа hello hello Redactor и запускать с hello **Redact** режим. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. Загрузите или совместно использовать hello окончательный размер выходного актива. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Инструмент с открытым кодом Azure Media Redactor Visualizer

Открытой [средство визуализатор](https://github.com/Microsoft/azure-media-redactor-visualizer) — разработчики спроектированный toohelp только начиная с hello формат заметки с синтаксический анализ и применение предложения output hello.

После клонирования репозитория hello, в порядке toorun hello проекта, необходимо будет toodownload FFMPEG из их [официальный сайт](https://ffmpeg.org/download.html).

Если вы являетесь разработчиком попытки hello tooparse заметки данных JSON, поиск внутри Models.MetaData примеры кода для образца.

### <a name="set-up-hello-tool"></a>Настройка средства hello

1.  Загрузить и построить все решение hello. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Скачайте компонент FFMPEG [отсюда](https://ffmpeg.org/download.html). Данный проект первоначально был разработан с использованием версии be1d324 (2016-10-04) со статическим связыванием. 
3.  Скопируйте ffmpeg.exe и ffprobe.exe toohello AzureMediaRedactor.exe папке выходных данных. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. Запустите AzureMediaRedactor.exe. 

### <a name="use-hello-tool"></a>Используйте средство hello

1. Обрабатывать видео в учетную запись служб мультимедиа Azure с hello Redactor MP режим анализа. 
2. Загрузка исходного файла видео hello и выходные данные hello hello исправления - анализ задания. 
3. Выберите файлы hello выше и приложение hello визуализатора. 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Воспользуйтесь предварительным просмотром файла. Укажите, какие стороной хотел tooblur через hello боковой панели на hello вправо. 
    
    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  hello начертания идентификаторы будут обновлены Hello нижней текстовое поле. Создайте файл idlist.txt, содержащий эти идентификаторы в виде списка, разделенного символами новой строки. 

    >[!NOTE]
    > Hello idlist.txt должен быть сохранен в формате ANSI. Можно использовать Блокнот toosave в ANSI.
    
6.  Отправьте этот файл toohello выходной актив из шага 1. Hello исходного видео toothis средства также загрузить и установить в качестве основного средства. 
7.  Запустите задание исправления этого актива с «Redact» tooget hello окончательный размер видео в режиме. 

## <a name="next-steps"></a>Дальнейшие действия 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Связанные ссылки
[Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md)

[Демонстрационные материалы для медиааналитики Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Announcing Face Redaction for Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/) (Анонс функции скрытия лиц с помощью медиа-аналитики Azure)
