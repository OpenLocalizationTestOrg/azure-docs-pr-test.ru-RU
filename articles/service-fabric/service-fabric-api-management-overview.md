---
title: "aaaAzure Service Fabric с Обзор API управления | Документы Microsoft"
description: "Эта статья содержит введение toousing API управления Azure как приложения Service Fabric tooyour шлюза."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Общие сведения о Service Fabric со службой управления API Azure

Облачные приложения обычно требуется tooprovide интерфейса шлюза единый вход для пользователей, устройств или других приложений. В Service Fabric в качестве шлюза может выступать любая служба без отслеживания состояния, например [приложение ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), или другая служба, предназначенная для обработки входящего трафика, например [концентраторы событий](https://docs.microsoft.com/azure/event-hubs/), [Центр Интернета вещей](https://docs.microsoft.com/azure/iot-hub/) или [служба управления API Azure](https://docs.microsoft.com/azure/api-management/).

Эта статья содержит введение toousing API управления Azure как приложения Service Fabric tooyour шлюза. Управление API напрямую интегрируется с Service Fabric, позволяя toopublish API-интерфейсы с широким набором правил tooyour серверной части Service Fabric службы маршрутизации. 

## <a name="architecture"></a>Архитектура
Общая архитектура Service Fabric использует одной страницы веб-приложении, который выполнит вызовы HTTP tooback служб, которые предоставляют интерфейсы API HTTP. Hello [пример начала работы приложения Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) приведен пример такой архитектуры.

В этом сценарии без отслеживания состояния веб-службы служит шлюзом hello в hello приложения Service Fabric. Этот подход требует toowrite веб-службу, которая может прокси-сервера HTTP запросы служб tooback, как показано в hello, следующая схема:

![Обзор топологии Service Fabric со службой управления API Azure][sf-web-app-stateless-gateway]

По мере роста сложности приложения таким образом hello шлюзов, которые должен представить API перед множество серверными службами. Azure API Management — спроектированный toohandle сложных API-интерфейсы с правилами маршрутизации, управления доступом, ограничение скорости, мониторинг, ведение журнала событий и кэширование ответов с минимальными действий с вашей стороны. Управления API Azure поддерживает обнаружение службы Service Fabric, разрешения раздела и маршрута toointelligently Выбор реплики непосредственно запрашивает tooback служб в Service Fabric, поэтому не нужно toowrite без сохранения состояния шлюза API. 

В этом сценарии веб-hello пользовательского интерфейса по-прежнему обслуживаться через веб-службу, во время вызовов HTTP API управляются и маршрутизируются через API управления Azure, как показано в hello, следующая схема:

![Обзор топологии Service Fabric со службой управления API Azure][sf-apim-web-app]

## <a name="application-scenarios"></a>Сценарии приложений

На платформе Service Fabric могут размещаться как службы с отслеживанием состояния, так и службы без отслеживания состояния. Их секционирование осуществляется на основе одной из трех схем: одноэлементное, по диапазонам значений Int64 и по именам. Разрешение конечной точки службы требует определения отдельного раздела конкретного экземпляра службы. При разрешении конечной точки службы, оба hello имя экземпляра службы (например, `fabric:/myapp/myservice`) также должен быть задан определенный раздел hello hello службы, за исключением случая hello одноэлементный секции.

Служба управления API Azure поддерживает любое сочетание служб без отслеживания состояния, служб с отслеживанием состояния, а также любые схемы секционирования.

## <a name="send-traffic-tooa-stateless-service"></a>Отправка трафика tooa без сохранения состояния службы

В простейшем случае hello трафик перенаправляется tooa экземпляра службы без отслеживания состояния. tooachieve по этой операции управления API, содержит политику обработки входящего с Service Fabric серверной части, сопоставляющий tooa экземпляра без сохранения состояния службы в серверной части Service Fabric hello. Запросы, отправленные службе toothat отправляются tooa случайных реплики экземпляра службы без отслеживания состояния hello.

#### <a name="example"></a>Пример
В следующие сценарии hello, приложения Service Fabric содержит без сохранения состояния службы с именем `fabric:/app/fooservice`, который обеспечивает доступ к внутренним HTTP API. Имя экземпляра службы Hello хорошо известен и может быть жестко непосредственно в hello политики обработки входящего управления API. 

![Обзор топологии Service Fabric со службой управления API Azure][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Отправка трафика tooa с отслеживанием состояния службы

Аналогичный сценарий toohello службы без отслеживания состояния, трафик могут перенаправляться tooa экземпляра службы с отслеживанием состояния. В этом случае операции управления API, содержит политику обработки входящего с Service Fabric серверной части, соответствующий определенной секции tooa запроса конкретного *с отслеживанием состояния* экземпляра службы. Hello секции toomap toois каждый запрос вычисляется посредством метода лямбда-выражение, с помощью некоторых данных, вводимых hello входящего HTTP-запроса, например к значению в hello URL-адрес. Hello политики может быть настроенный toosend запросов toohello первичной реплики только или tooa случайных реплику для операций чтения.

#### <a name="example"></a>Пример

В следующие сценарии hello, приложения Service Fabric содержит секционированные службы с отслеживанием состояния с именем `fabric:/app/userservice` , обеспечивает доступ к внутренним HTTP API. Имя экземпляра службы Hello хорошо известен и может быть жестко непосредственно в hello политики обработки входящего управления API.  

Hello служба секционируется с использованием схемы секционирования hello Int64 с двумя разделами и ключевой диапазон, охватывающий `Int64.MinValue` слишком`Int64.MaxValue`. Hello внутренней политики вычисляет ключа секции в пределах диапазона, преобразуя hello `id` значение, указанное в hello URL-адрес запроса путь tooa 64-разрядное целое, несмотря на то, что любой алгоритм может быть ключа раздела используется здесь toocompute hello. 

![Обзор топологии Service Fabric со службой управления API Azure][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Отправлять трафик toomultiple службы без сохранения состояния

В более сложных сценариев можно определить операции управления API, maps запрашивает toomore от одной службы экземпляра. В этом случае каждая операция содержит политику, которая сопоставляет запросы tooa экземпляра службы на основании значений из hello входящего HTTP-запроса, такие как строки URL-путь или запрос hello и в случае hello служб с отслеживанием состояния, секции в пределах экземпляра служба hello . 

tooachieve это управления API, операция содержит политику обработки входящего с Service Fabric серверной части, соответствующий экземпляр службы без отслеживания состояния tooa в hello Service Fabric серверной части на основе значений, полученных из hello входящего HTTP-запроса. Экземпляр службы tooa запросы отправляются tooa случайных реплики экземпляра службы hello.

#### <a name="example"></a>Пример

В этом примере создается новый экземпляр службы без отслеживания состояния для каждого пользователя приложения динамически создаваемых именем с помощью hello следующую формулу:
 
 - `fabric:/app/users/<username>`

 Каждая служба имеет уникальное имя, но имена hello не известны авансовых так hello службы создаются в ответ toouser admin ввода и поэтому не может быть жестко закодирована в APIM политики или правила маршрутизации. Вместо этого имя hello hello службы toowhich toosend запрос создается в определении внутренней политики hello из hello `name` значение, указанное в пути запроса hello URL-адрес. Например:

  - Объект запроса слишком`/api/users/foo` перенаправленное tooservice экземпляр`fabric:/app/users/foo`
  - Объект запроса слишком`/api/users/bar` перенаправленное tooservice экземпляр`fabric:/app/users/bar`

![Обзор топологии Service Fabric со службой управления API Azure][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Отправлять трафик toomultiple служб с отслеживанием состояния

Аналогичный пример toohello службы без отслеживания состояния, API управления, можно сопоставить операция запрашивает toomore, чем один **с отслеживанием состояния** экземпляру службы, в этом случае также необходимо разрешение tooperform секции для каждой службы с отслеживанием состояния экземпляр.

tooachieve это управления API, операция содержит политику обработки входящего с Service Fabric серверной части, сопоставляющий tooa экземпляра службы с отслеживанием состояния в hello Service Fabric серверной части на основе значений, полученных из hello входящего HTTP-запроса. Кроме toomapping экземпляр службы toospecific запроса, запрос hello можно также сопоставленных tooa определенной секции в пределах экземпляра службы hello и при необходимости tooeither hello первичной реплики или случайное вторичной реплики в секции hello.

#### <a name="example"></a>Пример

В этом примере создается новый экземпляр службы с отслеживанием состояния для каждого пользователя приложения hello динамически создаваемых именем с помощью hello следующую формулу:
 
 - `fabric:/app/users/<username>`

 Каждая служба имеет уникальное имя, но имена hello не известны авансовых так hello службы создаются в ответ toouser admin ввода и поэтому не может быть жестко закодирована в APIM политики или правила маршрутизации. Вместо этого имя hello hello службы toowhich toosend запрос создается в определении внутренней политики hello из hello `name` путь запроса URL-адрес hello указанное значение. Например:

  - Объект запроса слишком`/api/users/foo` перенаправленное tooservice экземпляр`fabric:/app/users/foo`
  - Объект запроса слишком`/api/users/bar` перенаправленное tooservice экземпляр`fabric:/app/users/bar`

Каждый экземпляр службы также секционируется с использованием схемы секционирования hello Int64 с двумя разделами и ключевой диапазон, охватывающий `Int64.MinValue` слишком`Int64.MaxValue`. Hello внутренней политики вычисляет ключа секции в пределах диапазона, преобразуя hello `id` значение, указанное в hello URL-адрес запроса путь tooa 64-разрядное целое, несмотря на то, что любой алгоритм может быть ключа раздела используется здесь toocompute hello. 

![Обзор топологии Service Fabric со службой управления API Azure][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Дальнейшие действия

Выполните hello [краткого руководства по](service-fabric-api-management-quick-start.md) tooset копирование вашего первого Service Fabric кластер с API управления и поток запросов через tooyour службы управления API.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png