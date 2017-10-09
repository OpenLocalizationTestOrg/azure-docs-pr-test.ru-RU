---
title: "исключения, aaaCommon FabricClient | Документы Microsoft"
description: "Описывает общие исключения hello и ошибок, которые могут создаваться hello FabricClient интерфейсы API при выполнении операций управления приложения и кластера."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Общие исключения и ошибки при работе с API-интерфейсы FabricClient hello
Hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API позволяют кластера и приложения администраторы tooperform административных задач в приложения, службы или кластера Service Fabric. Например развертывание приложения, обновлению и удалению, проверка работоспособности hello кластера или тестирования службы. Разработчикам и администраторам кластера воспользуйтесь средствами toodevelop hello FabricClient API-интерфейсы для управления кластера Service Fabric hello и приложениями.

С помощью FabricClient можно выполнять операции различных типов.  Каждый метод может создавать исключения для ошибки из-за ввода tooincorrect, ошибки времени выполнения или проблемы с временными инфраструктуры.  См. в документации toofind hello API ссылка, какие исключения создаются с помощью определенного метода. При этом некоторые исключения могут выдаваться различными интерфейсами API [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient). Hello следующей таблице перечислены hello исключения, которые являются общими для hello FabricClient API-интерфейсы.

| Исключение | Вызывается, когда |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) объект находится в закрытом состоянии. Удалить hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) объекта используется и создания нового экземпляра [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) объекта. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |Истекло время ожидания операции Hello. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) возвращается, если операция hello принимает более чем MaxOperationTimeout toocomplete. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Сбой проверки доступа Hello hello операции. Возвращается E_ACCESSDENIED. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |При выполнении операции hello произошла ошибка времени выполнения. Любой из методов FabricClient hello потенциально может вызывать [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) свойство указывает причину исключения hello hello. Коды ошибок определяются в hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) перечисления. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |не удалось выполнить операцию Hello из-за условия временная ошибка tooa какого-либо. Например, операция может завершиться ошибкой, так как кворум реплик временно недоступен. Временные исключения соответствуют toofailed операций, которые могут быть повторены. |

Некоторые самые распространенные ошибки [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode), которые могут быть возвращены в [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), включают:

| Ошибка | Условие |
| --- |:--- |
| CommunicationError |В результате ошибки связи toofail hello операции, операции повтора hello. |
| InvalidCredentialType |Недопустимый тип учетных данных Hello. |
| InvalidX509FindType |Hello X509FindType является недопустимым. |
| InvalidX509StoreLocation |указано недопустимое расположение хранилища Hello X509. |
| InvalidX509StoreName |Недопустимое имя Hello X509 хранилища. |
| InvalidX509Thumbprint |Недопустимая строка отпечаток сертификата Hello X509. |
| InvalidProtectionLevel |Недопустимый уровень защиты Hello. |
| InvalidX509Store |не удается открыть хранилище сертификатов Hello X509. |
| InvalidSubjectName |Недопустимое имя субъекта Hello. |
| InvalidAllowedCommonNameList |Недопустимый формат Hello общие строки имени списка. Это должен быть список с разделителями-запятыми. |

