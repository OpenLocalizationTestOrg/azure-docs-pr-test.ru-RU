---
title: "aaaGet работы с доставки VoD, с помощью hello портал Azure | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги hello реализации базовой службы доставки содержимого видео по запросу (VoD) с приложением служб мультимедиа Azure (AMS) с помощью портала Azure hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Приступая к работе с доставки содержимого по требованию с помощью портала Azure hello
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Этот учебник поможет выполнить шаги hello реализации базовой службы доставки содержимого видео по запросу (VoD) с приложением служб мультимедиа Azure (AMS) с помощью портала Azure hello.

## <a name="prerequisites"></a>Предварительные требования
Здесь представлены Hello необходимые toocomplete hello учебника:

* Учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Учетная запись служб мультимедиа. toocreate учетную запись служб носителей в разделе [как учетную запись служб мультимедиа tooCreate](media-services-portal-create-account.md).

Этот учебник включает hello следующие задачи:

1. Запуск конечной точки потоковой передачи.
2. Загрузка видеофайла.
3. Кодирование hello исходный файл в набор файлов MP4 с адаптивной скоростью.
4. Публикация активов hello и get потоковой передачи и URL-адресов прогрессивной загрузки.  
5. Воспроизведение содержимого.

## <a name="start-streaming-endpoints"></a>Запуск конечной точки потоковой передачи 

При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает видео через потоковой передачи с адаптивной скоростью. Служба Media Services предоставляет динамической упаковки, что позволяет вам toodeliver с адаптивным битрейтом MP4 кодируются содержимого в форматах, поддерживаемых служб мультимедиа (MPEG DASH, HLS, Smooth Streaming) just-in-time, без необходимости toostore упакована заранее потоковой передачи версии каждого из этих форматов потоковой передачи.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 

toostart Здравствуйте конечной точки потоковой передачи, hello следующие:

1. Войдите на hello [портал Azure](https://portal.azure.com/).
2. В окне "Параметры" hello щелкните конечных точек потоковой передачи. 
3. Щелкните конечную точку потоковой передачи по умолчанию hello. 

    Появится окно Hello по умолчанию потоковая передача сведений о конечной ТОЧКЕ.

4. Щелкните значок запуска hello.
5. Щелкните toosave кнопку hello сохранить изменения.

## <a name="upload-files"></a>Отправка файлов
toostream видео с помощью служб мультимедиа Azure, необходимо tooupload hello источник видео, кодировать несколько битрейтов и опубликуйте результат hello. Первым шагом Hello, описанные в этом разделе. 

1. В hello **параметр** окно, нажмите кнопку **активы**.
   
    ![Отправка файлов](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Нажмите кнопку hello **отправить** кнопки.
   
    Hello **отправить видео активов** появится окно.
   
   > [!NOTE]
   > Размер файлов неограничен.
   > 
   > 
3. Обзор toohello требуемого видео на компьютере, выберите его и нажмите ОК.  
   
    начнется загрузка Hello и следить за ходом hello в файле с именем hello можно.  

После завершения отправки hello, можно увидеть новый актив hello, перечисленные в hello **активы** окна. 

## <a name="encode-assets"></a>Кодирование ресурсов

При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает tooyour клиентам потоковой передачи с адаптивной скоростью. Службы мультимедиа поддерживают следующие технологии потоковой передачи с адаптивной скоростью hello: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare видео для потоковой передачи с адаптивной скоростью необходимо tooencode источника видео в файлы с разными скоростями. Следует использовать hello **Media Encoder Стандартная** tooencode кодировщик видео.  

Службы мультимедиа также предоставляют динамическую упаковку, позволяющий toodeliver вашей MP4-файлов с несколькими скоростями в hello следующие форматы потоковой передачи: MPEG DASH, HLS, Smooth Streaming, без необходимости toorepackage в такие форматы потоковой передачи. При использовании динамической упаковки достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа создает и обслуживает hello соответствующий ответ на основе запросов клиента.

tootake преимущества динамической упаковки необходимо tooencode файла исходного кода в набор MP4-файлов с несколькими скоростями (hello кодирования шаги демонстрируются позже в этом разделе).

### <a name="toouse-hello-portal-tooencode"></a>портала tooencode toouse hello
В этом разделе описывается hello может занять tooencode свое содержимое в стандартный кодировщик мультимедиа.

1. В hello **параметры** выберите **активы**.  
2. В hello **активы** окно, выберите hello активов, желательно tooencode.
3. Нажмите клавишу hello **Encode** кнопки.
4. В hello **закодировать ресурс** окно, выберите hello «Стандартный кодировщик мультимедиа» процессор и стиль. Дополнительные сведения о предустановках см. в статьях [Использование стандартной версии кодировщика мультимедиа Azure для автоматического создания схемы скоростей](media-services-autogen-bitrate-ladder-with-mes.md) и [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md). Если планируется использовать какие предустановку toocontrol, имейте в виду: важно tooselect hello стиль, лучше всего подходит для ввода видео. Например, если вы знаете, входной видео с разрешением 1920 x 1080 пикселей, затем можно использовать hello «H264 Multiple Bitrate 1080p» стиль. Если у вас есть видео с низким разрешением (640 x 360), не следует использовать предустановку H264 Multiple Bitrate 1080p.
   
   Чтобы упростить управление имеется возможность редактирования hello имя выходной актив hello и hello имя задания hello.
   
   ![Кодирование ресурсов](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. Нажмите кнопку **Создать**.

### <a name="monitor-encoding-job-progress"></a>Мониторинг хода выполнения задания кодирования
Щелкните toomonitor hello ход выполнения задания кодирования hello **параметры** (вверху hello hello страницы), а затем выберите **задания**.

![Задания](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>Публикация контента
tooprovide на пользователя с URL-адрес, который можно использовать toostream или загрузить содержимое, сначала требуется слишком «публикации» актива путем создания локатора. Локаторы предоставляют доступ toofiles, содержащиеся в ресурсе hello. Службы мультимедиа поддерживают два типа указателей: 

* Потоковая передача указателей (OnDemandOrigin), используемый для адаптивной потоковой передачи (например, toostream MPEG DASH, HLS или Smooth Streaming). toocreate указатель потоковой передачи актива должно содержать ISM-файла. 
* Последовательные указатели (SAS), используемые для доставки видео путем последовательного скачивания.

URL-адрес потоковой передачи имеет следующий формат hello и его можно использовать ресурсы Smooth Streaming tooplay.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

append toobuild на URL-адрес потоковой передачи HLS (format = m3u8-aapl) toohello URL-адрес.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Добавление toobuild на URL-адрес потоковой передачи MPEG DASH (формат = mpd время csf) toohello URL-адрес.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


URL-адрес SAS имеет следующий формат hello.

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> Указатели с датой окончания срока действия два года были созданы, при использовании портала toocreate локаторов hello до марта 2015 г.  
> 
> 

tooupdate дату окончания срока действия на указатель, используйте [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API-интерфейсы. При обновлении срок действия локатора SAS hello изменяет hello URL-адрес.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello портала toopublish актива
toouse hello портала toopublish актива, hello следующие:

1. Установите флажок **Параметры** > **Ресурсы-контейнеры**.
2. Выберите требуемый toopublish средство hello.
3. Нажмите кнопку hello **публикации** кнопки.
4. Выберите тип локатора hello.
5. Нажмите кнопку **Добавить**.
   
    ![Опубликовать](./media/media-services-portal-vod-get-started/media-services-publish1.png)

URL-адрес Hello добавляется список toohello **URL-адреса в опубликованные**.

## <a name="play-content-from-hello-portal"></a>Воспроизведение контента из портала hello
Hello портал Azure предоставляет проигрыватель контента, которые можно использовать tootest видео.

Выберите требуемого hello видео и нажмите кнопку hello **воспроизведение** кнопки.

![Опубликовать](./media/media-services-portal-vod-get-started/media-services-play.png)

Важные особенности

* toobegin потоковой передачи, запустить выполнение hello **по умолчанию** конечной точки потоковой передачи.
* Убедитесь, что опубликованный hello видео.
* Это **проигрыватель** воспроизводит контент из конечной точки потоковой передачи по умолчанию hello. Если требуется, чтобы tooplay из не по умолчанию потоковой передачи конечной точки, выберите URL-адрес toocopy hello и используйте другой проигрыватель. Например, [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

