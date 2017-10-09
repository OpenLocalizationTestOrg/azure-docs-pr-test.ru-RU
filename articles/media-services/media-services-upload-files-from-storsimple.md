---
title: "aaaUpload файлы в учетную запись служб мультимедиа Azure из Azure StorSimple | Документы Microsoft"
description: "В этой статье рассматривается использование диспетчера данных Azure StorSimple. статья Hello также связывает tootutorials, показывается, как данные tooextract из StorSimple и передать его как активы tooan учетная запись служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Отправка файлов в учетную запись служб мультимедиа Azure из Azure StorSimple

В этой статье рассматривается использование диспетчера данных Azure StorSimple. статья Hello также связывает tootutorials, показывается, как данные tooextract из StorSimple и передать эти данные как активы tooan учетной записи служб мультимедиа Azure (AMS).

> 
> [!NOTE]
> В настоящее время диспетчер данных Azure StorSimple доступен в качестве закрытой предварительной версии. 
> 

## <a name="overview"></a>Обзор

В службах мультимедиа цифровые файлы отправляются в актив. Hello актива может содержать видео, аудио, изображения, коллекции эскизов, текст отслеживает и титров файлов (и hello метаданные об этих файлах.) После загрузки файлов hello контент безопасно хранится в облаке hello для дальнейшей обработки и потоковой передачи.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) использует Облачное хранилище, а расширение hello локальное решение автоматически уровнями данных через hello локальное хранилище и Облачное хранилище. устройство StorSimple Hello dedupes и сжимает данные перед отправкой toohello облака, сделав его очень эффективен для отправки больших файлов toohello облака. Hello [данных StorSimple Manager](../storsimple/storsimple-data-manager-overview.md) служба предоставляет интерфейсы API, которые позволяют вам tooextract данные из StorSimple и представлять их как AMS активы.

## <a name="get-started"></a>Начало работы

1. [Создание учетной записи службы мультимедиа](media-services-portal-create-account.md) в которую будут tootransfer hello активы.
2. Зарегистрируйтесь диспетчер данных, как описано в hello [данных StorSimple Manager](../storsimple/storsimple-data-manager-overview.md) статьи.
3. Создайте учетную запись диспетчера данных StorSimple.
4. Создайте задание для преобразования данных, которое извлекает данные из устройства StorSimple, а затем переносит их в учетную запись AMS в качестве ресурсов. 

    В начале выполнения задания hello создается очередь хранилища. Эта очередь по мере готовности заполняется сообщениями о преобразованных больших двоичных объектах. имя этой очереди Hello hello совпадает с именем hello hello определения задания. Можно использовать этот toodetermine очереди при как ресурс — готовых и вызова к требуемой toorun операции служб мультимедиа. Например можно использовать этот очереди tootrigger функцию Azure, которая содержит в себе hello необходимый код для служб мультимедиа.

## <a name="see-also"></a>См. также

[Используйте hello .net SDK tootrigger заданий в диспетчер данных hello](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

Теперь можно закодировать отправленные ресурсы. Дополнительную информацию см. в статье, посвященной [кодированию ресурсов](media-services-portal-encode.md).
