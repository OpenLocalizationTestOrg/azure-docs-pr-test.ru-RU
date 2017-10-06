---
title: "Логика aaaRetry hello пакета SDK служб мультимедиа для .NET | Документы Microsoft"
description: "Hello разделе приводится обзор логику повторных попыток в hello пакета SDK служб мультимедиа для .NET."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Повтора попыток hello пакета SDK служб мультимедиа для .NET
При работе со службами Microsoft Azure могут возникать временные сбои. Если возникает временная ошибка, в большинстве случаев после нескольких попыток hello операция завершается успешно. Hello пакета SDK служб мультимедиа для .NET реализует hello повтора логику toohandle временных ошибок, связанных с исключения и ошибки, вызванные веб-запросов, выполнение запросов, сохранение изменений и операций.  По умолчанию hello пакета SDK служб мультимедиа для .NET выполняет четырех повторных попыток перед повторной генерации tooyour приложения hello исключение. Hello в коде приложения затем должен правильно обрабатывать это исключение.  

 Hello ниже представлен краткие руководства веб-запросов, хранилища, запроса и SaveChanges политик:  

* Hello политики хранения используется для операции хранилища BLOB-объекта (передачи или загрузки файлов активов).  
* Hello политики веб-запросов используется для универсального веб-запросов (например, получение токена проверки подлинности и разрешения пользователей hello кластера конечной точки).  
* Hello политике запросов используется для выполнения запросов к сущностям из REST (например, mediaContext.Assets.Where(...)).  
* Hello SaveChanges политики используется для выполнение любых операций, что изменения данных в службе hello (например, при создании сущности обновление сущности, вызова функции службы для операции).  
  
  В этом разделе перечислены типы исключений и коды ошибок, которые обрабатываются hello пакета SDK служб мультимедиа для .NET логику повторных попыток.  

## <a name="exception-types"></a>Типы исключений
Hello Следующая таблица описывает исключения, hello пакета SDK служб мультимедиа для .NET дескрипторов или не обрабатывать для некоторых операций, которые могут вызвать временные сбои.  

| Исключение | Веб-запрос | Операции с хранилищем | Выполнение запросов | Сохранение изменений |
| --- | --- | --- | --- | --- |
| WebException<br/>Дополнительные сведения см. в разделе hello [коды состояния WebException](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) раздела. |Да |Да |Да |Да |
| DataServiceClientException<br/> Дополнительные сведения см. в разделе [Коды состояний ошибок HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Нет |Да |Да |Да |
| DataServiceQueryException<br/> Дополнительные сведения см. в разделе [Коды состояний ошибок HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Нет |Да |Да |Да |
| DataServiceRequestException<br/> Дополнительные сведения см. в разделе [Коды состояний ошибок HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Нет |Да |Да |Да |
| DataServiceTransportException |Нет |Нет |Да |Да |
| TimeoutException |Да |Да |Да |Нет |
| SocketException |Да |Да |Да |Да |
| StorageException |Нет |Да |Нет |Нет |
| IOException |Нет |Да |Нет |Нет |

### <a name="WebExceptionStatus"></a> Коды состояний WebException
Hello следующей таблице показаны для ошибки WebException реализована логика повторных попыток hello коды. Hello [не выполнен](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) перечисление определяет коды состояния hello.  

| Состояние | Веб-запрос | Операции с хранилищем | Выполнение запросов | Сохранение изменений |
| --- | --- | --- | --- | --- |
| ConnectFailure |Да |Да |Да |Да |
| NameResolutionFailure |Да |Да |Да |Да |
| ProxyNameResolutionFailure |Да |Да |Да |Да |
| SendFailure |Да |Да |Да |Да |
| PipelineFailure |Да |Да |Да |Нет |
| ConnectionClosed |Да |Да |Да |Нет |
| KeepAliveFailure |Да |Да |Да |Нет |
| UnknownError |Да |Да |Да |Нет |
| ReceiveFailure |Да |Да |Да |Нет |
| RequestCanceled |Да |Да |Да |Нет |
| Время ожидания |Да |Да |Да |Нет |
| ProtocolError <br/>Количество попыток Hello ошибка протокола контролируется обработку кода состояния HTTP hello. Дополнительные сведения см. в разделе [Коды состояний ошибок HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Да |Да |Да |Да |

### <a name="HTTPStatusCode"></a> Коды состояний ошибок HTTP
При операции запросов и SaveChanges throw DataServiceClientException, DataServiceQueryException или DataServiceQueryException, код состояния ошибки HTTP hello возвращается в hello StatusCode свойство.  Hello следующей таблице показаны коды ошибок, который реализуется hello логику повторных попыток.  

| Состояние | Веб-запрос | Операции с хранилищем | Выполнение запросов | Сохранение изменений |
| --- | --- | --- | --- | --- |
| 401 |Нет |Да |Нет |Нет |
| 403 |Нет |Да<br/>Обработка повторных попыток с увеличением времени ожидания. |Нет |Нет |
| 408 |Да |Да |Да |Да |
| 429 |Да |Да |Да |Да |
| 500 |Да |Да |Да |Нет |
| 502 |Да |Да |Да |Нет |
| 503 |Да |Да |Да |Да |
| 504 |Да |Да |Да |Нет |

См. Если требуется tootake рассмотрим hello фактическую реализацию hello пакета SDK служб мультимедиа для .NET логику повторных попыток, [azure sdk для media services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

