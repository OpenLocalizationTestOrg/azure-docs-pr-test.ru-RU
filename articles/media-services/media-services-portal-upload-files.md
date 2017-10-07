---
title: "AAA» передавать файлы в учетную запись служб мультимедиа с помощью hello портал Azure | Документы Microsoft»"
description: "Этот учебник поможет вам выполнить hello этапы загрузки файлов в учетную запись служб мультимедиа с помощью портала Azure hello"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Отправка файлов в учетную запись служб мультимедиа с помощью портала Azure hello
> [!div class="op_single_selector"]
> * [Портал](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


В службах мультимедиа цифровые файлы отправляются в актив. Hello актива может содержать видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.) После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.


## <a name="upload-files"></a>Отправка файлов

>[!NOTE]
>Имеется ограничение toohello максимальный размер файла поддерживается для обработки в службах мультимедиа. См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.
>

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. На hello **параметры** колонка, щелкните **активы**.
   
    ![Отправка файлов](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Нажмите кнопку hello **отправить** кнопки.
   
    Hello **отправить видео активов** появится окно.
   
   > [!NOTE]
   > Размер файлов неограничен.
   > 
   > 
4. Обзор toohello требуемого видео на компьютере, выберите его и нажмите ОК.  
   
    начнется загрузка Hello и следить за ходом hello в файле с именем hello можно.  

После завершения отправки hello, вы увидите новый актив hello, перечисленные в hello **активы** окна. 

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно закодировать отправленные ресурсы. Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).

Также можно использовать функции Azure tootrigger задание кодирования на основе файла, поступающих в контейнере hello настроен. Дополнительные сведения см. в [этом примере](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

