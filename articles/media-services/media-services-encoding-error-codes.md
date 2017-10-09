---
title: "кодирование кодов ошибок служб мультимедиа aaaAzure | Документы Microsoft"
description: "В этом разделе перечислены коды ошибок, которые могут быть возвращены в случае, если произошла ошибка во время кодировки выполнения задачи hello..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a>Коды ошибок кодирования

Hello следующей таблице перечислены коды ошибок, которые могут быть возвращены в случае, если произошла ошибка во время hello кодировки выполнения задачи.  tooget сведения об ошибке в коде .NET, используйте hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) класса. использовать tooget сведения об ошибке в коде REST hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API-интерфейса REST.

| ErrorDetail.Code | Возможные причины ошибки |
| --- | --- |
| Unknown |Неизвестная ошибка при выполнении задачи hello |
| ErrorDownloadingInputAssetMalformedContent |Категория ошибок, охватывающая ошибки загрузки входного ресурса, такие как некорректное имя файлов, файлы нулевой длины, неправильное форматирование и т. д. |
| ErrorDownloadingInputAssetServiceFailure |Категория ошибок, рассматриваются проблемы на стороне службы hello - пример сети или хранилища ошибок при загрузке. |
| ErrorParsingConfiguration |Категория ошибок, где задач <see cref="MediaTask.PrivateData"/> (конфигурация) является недопустимым, например конфигурации hello не является допустимой системы конфигурации, или он содержит недопустимый XML. |
| ErrorExecutingTaskMalformedContent |Категория ошибок во время выполнения hello задачу hello, где вопросы внутри hello входных файлов мультимедиа к сбою. |
| ErrorExecutingTaskUnsupportedFormat |Категория ошибок, где обработчик мультимедиа hello не удается обработать предоставленных файлах hello - формата media не поддерживается или не соответствует конфигурации hello. Например при tooproduce только вывод актив, который содержит только видео |
| ErrorProcessingTask |Во время обработки hello hello задачи, которые связаны toocontent встретится категории других ошибок, которые hello обработчика мультимедиа. |
| ErrorUploadingOutputAsset |Категория ошибок при передаче hello выходной актив |
| ErrorCancelingTask |Категория ошибки toocover сбоев при hello toocancel задач |
| TransientError |Категория ошибки toocover временных проблем (например) (например, временные сетевые проблемы со службой хранилища Azure) |

Справка tooget из hello **Media Services** команды, откройте [обращение в службу поддержки](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Связанные статьи
* [Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа](media-services-custom-mes-presets-with-dotnet.md)
* [Квоты и ограничения](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
