---
title: "Надежные службы диагностики aaaStateful | Документы Microsoft"
description: "Диагностические функции для надежных служб с отслеживанием состояния"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Диагностические функции для надежных служб с отслеживанием состояния
выдает Hello надежного StatefulServiceBase служб с отслеживанием состояния класс [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) события, которые можно использовать toodebug Здравствуйте службы, получить представление о как операционной среды выполнения hello и помочь в устранении неполадок.

## <a name="eventsource-events"></a>События EventSource
Hello EventSource hello надежного StatefulServiceBase служб с отслеживанием состояния класс называется «Microsoft ServiceFabric Services». Из этого источника событий отображаются в [событий диагностики](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) окно hello службы, который [отладки в Visual Studio](service-fabric-debugging-your-application.md).

Для сбора и просмотра событий EventSource вы можете использовать такие средства и технологии, как [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [система диагностики Microsoft Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) и [библиотека Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>События
| Имя события | Идентификатор события | Уровень | Описание события |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Информация |Генерируется, когда запускается задача RunAsync службы. |
| StatefulRunAsyncCancellation |2 |Информация |Генерируется, когда отменяется задача RunAsync службы. |
| StatefulRunAsyncCompletion |3 |Информация |Генерируется, когда завершается выполнение задачи RunAsync службы. |
| StatefulRunAsyncSlowCancellation |4. |Предупреждение |Создается, когда службы RunAsync задачей занимает слишком много времени toocomplete отмены |
| StatefulRunAsyncFailure |5 |Ошибка |Генерируется, когда задача RunAsync службы вызывает исключение. |

## <a name="interpret-events"></a>Интерпретация событий
События StatefulRunAsyncInvocation, StatefulRunAsyncCompletion и StatefulRunAsyncCancellation являются полезным toohello службы модуля записи toounderstand hello жизненный цикл службы--, а также время hello при запуске, отменено или завершено службы . Это может быть полезно при отладке проблем службы или основные сведения о жизненном цикле услуги hello.

Записи с помощью службы следует уделять особое внимание tooStatefulRunAsyncSlowCancellation и StatefulRunAsyncFailure события, поскольку они указывают на проблемы со службой hello.

StatefulRunAsyncFailure создается каждый раз, когда задача RunAsync() hello службы создает исключение. Как правило исключение указывает на ошибку или ошибки в службе hello. Кроме того hello исключение вызывает toofail службы hello, поэтому перемещенный tooa другой узел. Это может быть ресурсоемкой операцией и может быть отложено входящие запросы, пока служба hello перемещается. Записи с помощью службы следует определить причину исключения hello hello и, если это возможно, устранить ее.

StatefulRunAsyncSlowCancellation создается каждый раз, когда запрос отмены для hello RunAsync задачи требуется больше времени чем четыре секунды. Когда службы занимает слишком много времени toocomplete отмены, оно влияет на возможность hello toobe службы hello быстро перезапускается на другом узле. Это может повлиять на общую доступность службы hello hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Поставщики EventSource в PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
