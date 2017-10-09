---
title: "aaaService удаленного взаимодействия в Azure Service Fabric | Документы Microsoft"
description: "Remoting Service Fabric позволяет клиентам и службам toocommunicate при помощи служб с помощью удаленного вызова процедуры."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a>Удаленное взаимодействие службы с Reliable Services
> [!div class="op_single_selector"]
> * [C# в Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java в Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

Платформа надежного обмена Hello предоставляет tooquickly механизм удаленного взаимодействия и легко настроить удаленного вызова процедур для службы.

## <a name="set-up-remoting-on-a-service"></a>Настройка удаленного доступа в службе
Процесс настройки удаленного доступа для службы состоит из двух простых этапов.

1. Создайте интерфейс для tooimplement вашей службы. Этот интерфейс определяет hello методы, которые доступны для удаленного вызова процедур для службы. Hello методы должны быть возвращающий задачу асинхронный метод. должен быть реализован интерфейс Hello `microsoft.serviceFabric.services.remoting.Service` toosignal, hello службы имеет интерфейс удаленного взаимодействия.
2. Используйте прослушиватель удаленного взаимодействия в службе. Это реализация `CommunicationListener` , которая предоставляет возможности удаленного взаимодействия. `FabricTransportServiceRemotingListener`можно использовать toocreate прослушивателя удаленного взаимодействия, используя протокол удаленного доступа по умолчанию hello.

Например hello следующей без сохранения состояния службы предоставляет один метод tooget «Hello World», через удаленный вызов процедуры.

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> аргументы Hello и hello возвращают типы в интерфейс hello службы может быть любой простой, сложных или пользовательских типов, но они должны быть сериализуемыми.
>
>

## <a name="call-remote-service-methods"></a>Вызов удаленных методов службы
Вызов методов службы с помощью удаленного взаимодействия стека hello делается с помощью toohello локальный прокси-службы через hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` класса. Hello `ServiceProxyBase` метод создает локальный прокси-сервер, используя же интерфейс, hello службы реализует hello. С прокси-сервера можно просто вызвать методы интерфейса hello удаленно.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

Hello удаленного взаимодействия framework распространяет исключения на клиенте toohello hello службы. Поэтому обработка исключений логику на приветствия клиента с помощью `ServiceProxyBase` может напрямую обрабатывать исключения, которые hello служба вызывает исключение.

## <a name="service-proxy-lifetime"></a>Время существования ServiceProxy
Создание ServiceProxy — упрощенная операция, поэтому пользователь может создать столько прокси-серверов, сколько нужно. Прокси-сервер службы можно использовать повторно, если он нужен пользователю. Пользователь может повторно использовать hello один прокси-сервер при возникновении исключения. Каждый ServiceProxy содержит сообщения toosend клиентом обмена данными по сети hello. При вызове API, у нас есть внутренняя проверка toosee Если связи клиента является допустимым. На основании этого результата, создаются заново hello связи клиента. Поэтому пользователь не обязательно serviceproxy toorecreate при возникновении исключения.

### <a name="serviceproxyfactory-lifetime"></a>Время существования ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) — это фабрика, которая создает прокси-сервер для различных интерфейсов удаленного взаимодействия. Если вы используете API `ServiceProxyBase.create` для создания прокси-сервера, то платформа создает `FabricServiceProxyFactory`.
Это полезно toocreate один вручную при необходимости toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) свойства.
Создание фабрики — ресурсоемкая операция. `FabricServiceProxyFactory` хранит кэш клиента обмена данными.
Лучший способ — toocache `FabricServiceProxyFactory` то же время.

## <a name="remoting-exception-handling"></a>Обработка исключений удаленного взаимодействия
Все hello удаленного исключение, созданное API службы, как RuntimeException или FabricException отправляются назад toohello клиента.

ServiceProxy обрабатывать все исключения отработки отказа для раздела службы hello она создана для. Повторно разрешает hello конечных точек, если имеется вызов hello Exceptions(Non-Transient Exceptions) отработки отказа и повторные попытки с hello правильную конечную точку. Число повторных попыток для исключения отработки отказа не ограничено.
В случае TransientExceptions только повторяет вызов hello.

Параметры повтора по умолчанию определяются [OperationRetrySettings] (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Пользователь может настроить эти значения, передав конструктору tooServiceProxyFactory OperationRetrySettings объекта.

## <a name="next-steps"></a>Дальнейшие действия
* [Защита обмена данными для Reliable Services](service-fabric-reliable-services-secure-communication.md)
