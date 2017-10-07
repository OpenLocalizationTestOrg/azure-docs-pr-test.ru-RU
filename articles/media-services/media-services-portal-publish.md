---
title: "AAA» публиковать содержимое посредством hello портал Azure | Документы Microsoft»"
description: "Этот учебник поможет выполнить шаги для публикации содержимого с портала Azure hello hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a>Публиковать содержимое посредством hello портал Azure
> [!div class="op_single_selector"]
> * [Портал](media-services-portal-publish.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [REST](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a>Обзор
> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

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

Дополнительные сведения см. в [обзоре доставки содержимого](media-services-deliver-content-overview.md).

> [!NOTE]
> Указатели с датой окончания срока действия два года были созданы, при использовании портала toocreate локаторов hello до марта 2015 г.  
> 
> 

tooupdate дату окончания срока действия на указатель, используйте [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API-интерфейсы. Обратите внимание, что при обновлении срок действия локатора SAS hello hello URL-адрес изменяется.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello портала toopublish актива
toouse hello портала toopublish актива, hello следующие:

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. Установите флажок **Параметры** > **Ресурсы-контейнеры**.
3. Выберите требуемый toopublish средство hello.
4. Нажмите кнопку hello **публикации** кнопки.
5. Выберите тип локатора hello.
6. Нажмите кнопку **Добавить**.
   
    ![Опубликовать](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Hello URL-адрес будет добавлен список toohello **URL-адреса в опубликованные**.

## <a name="play-content-from-hello-portal"></a>Воспроизведение контента из портала hello
Hello портал Azure предоставляет проигрыватель контента, которые можно использовать tootest видео.

Выберите требуемого hello видео и нажмите кнопку hello **воспроизведение** кнопки.

![Опубликовать](./media/media-services-portal-vod-get-started/media-services-play.png)

Важные особенности

* Убедитесь, что опубликованный hello видео.
* Это **проигрыватель** воспроизводит контент из конечной точки потоковой передачи по умолчанию hello. Если требуется, чтобы tooplay из не по умолчанию потоковой передачи конечной точки, выберите URL-адрес toocopy hello и используйте другой проигрыватель. Например, [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
* Привет, из которого потоковой передачи конечной точки потоковой передачи должна быть запущена.  

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

