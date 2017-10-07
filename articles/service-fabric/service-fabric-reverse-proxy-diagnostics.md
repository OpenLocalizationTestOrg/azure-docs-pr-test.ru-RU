---
title: "aaaAzure Service Fabric обратного прокси-сервера диагностики | Документы Microsoft"
description: "Узнайте, как toomonitor и диагностики обработки запроса на hello обратного прокси-сервера."
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Мониторинг и диагностика обработки запроса на hello обратного прокси-сервера

Начиная с выпуска hello 5.7 Service Fabric, события обратного прокси-сервера, доступные для коллекции. Hello события доступны в двух каналов полноразмерных только события ошибок, связанных с toorequest сбоя обработки hello обратного прокси-сервера и второй канал, содержащий подробные события с записями для успешных и неудачных запросах.

См. слишком[собирать события обратного прокси-сервера](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable сбор событий из кластера Azure Service Fabric и локальной эти каналы.

## <a name="troubleshoot-using-diagnostics-logs"></a>Устранение неполадок с помощью журналов диагностики
Ниже приведены некоторые примеры на как общие журналы сбоя toointerpret hello такой могут столкнуться с:

1. Обратный прокси-сервер возвращает код состояния ответа 504 (превышено время ожидания).

    Одна из причин может быть вызвано сбоем службы toohello tooreply в течение времени ожидания запроса hello.
первое событие Hello ниже регистрирует подробности hello hello запроса, полученного на hello обратного прокси-сервера. Hello второе событие указывает, что hello не удалось выполнить запрос при tooservice переадресации, из-за слишком «Внутренняя ошибка = ERROR_WINHTTP_TIMEOUT» 

    полезные данные Hello включают:

    *  **числовое обозначение traceId**: этот идентификатор GUID можно использовать toocorrelate все события hello соответствующий tooa одного запроса. В hello ниже два события hello числовое обозначение traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, подразумевая, они принадлежат toohello того же запроса.
    *  **requestUrl**: hello URL-адрес (URL-адрес обратного прокси-сервера) toowhich hello запрос был отправлен.
    *  **verb**: HTTP-команда.
    *  **remoteAddress**: адрес клиента, отправив запрос hello.
    *  **resolvedServiceUrl**: служба конечной точки URL-адрес toowhich hello входящий запрос был разрешен. 
    *  **errorDetails**: Дополнительные сведения о сбое hello.

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. Обратный прокси-сервер возвращает код состояния ответа 404 (не найдено). 
    
    Ниже приведен пример события, где обратный прокси-сервер возвращает 404, поскольку ее не удалось toofind hello совпадения конечной точки службы.
    записи полезных данных Hello интересного являются:
    *  **processRequestPhase**: указывает фазу hello во время обработки запроса, когда произошел сбой hello, ***TryGetEndpoint*** т. е. При попытке toofetch hello службы конечной точки tooforward для. 
    *  **errorDetails**: перечислены критерии поиска hello конечной точки. Вы видите, listenerName hello указан = **FrontEndListener** в то время как hello реплики конечная точка содержит только прослушиватель с именем hello **OldListener**.
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    Другой пример, где обратный прокси-сервер может возвращать 404 — не найден: параметр конфигурации ApplicationGateway\Http **SecureOnlyMode** задаются tootrue hello обратный прокси-сервер прослушивает **HTTPS**, Однако все конечные точки реплики hello небезопасные (прослушивания HTTP).
    Обратный прокси-сервер возвращает 404, так как его не удалось найти конечную точку, прослушивающую на HTTPS-запрос tooforward hello. Анализ параметров hello в полезных данных события hello помогает toonarrow вниз hello проблемы:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Обратный прокси-сервер запрос toohello приведет к ошибке времени ожидания. 
    журналы событий Hello содержат события с сведения о запросе получен hello (здесь не показаны).
    Hello следующее событие показывает, что служба hello в ответе код состояния 404 и инициирует обратного прокси-сервера, заново разрешить. 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    При сбор всех событий, hello, можно увидеть обучение событий, показывающее все разрешения и прямой попытки.
    Hello последнее событие в серии hello показывает, что сбой обработки запроса hello с временем ожидания, вместе с hello число попыток успешно разрешения.
    
    > [!NOTE]
    > Его рекомендуется tookeep hello verbose канала сбора данных о событиях отключено по умолчанию и включить его для устранения неполадок на основе необходимость.

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    Если включен сбор только критические ошибки и события, может появиться одно событие с подробными сведениями о времени ожидания hello и hello число попыток разрешения. 
    
    Если служба hello Защищаемая toosend пользователь задней toohello код состояния 404, оно должно сопровождаться заголовок «X-ServiceFabric». После устранения это, вы увидите задней toohello клиента код состояния обратного прокси-сервера пересылает hello.  

4. Случаях, когда клиент hello отключен запрос hello.

    Hello ниже событие записывается в том случае, когда обратного прокси-сервера для переадресации tooclient hello ответа, но отключении hello клиента:

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> В настоящее время обработки запроса toowebsocket связанные события не регистрируются. Это будет добавлен в следующем выпуске hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Статистическая обработка и сбор событий с помощью системы диагностики Microsoft Azure](service-fabric-diagnostics-event-aggregation-wad.md) для обеспечения сбора журналов в кластерах Azure.
* события Service Fabric tooview в Visual Studio см. [монитор диагностики локально](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* См. слишком[настроить службы toosecure tooconnect обратного прокси-сервера](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) для диспетчера ресурсов Azure шаблона образцы tooconfigure безопасного обратного прокси-сервера с параметрами проверки сертификата другую службу hello.
* Чтение [Service Fabric обратный прокси-сервер](service-fabric-reverseproxy.md) toolearn дополнительные.
