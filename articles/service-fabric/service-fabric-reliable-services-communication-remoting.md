---
title: "удаленное взаимодействие aaaService в Service Fabric | Документы Microsoft"
description: "Remoting Service Fabric позволяет клиентам и службам toocommunicate при помощи служб с помощью удаленного вызова процедуры."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a>Удаленное взаимодействие службы с Reliable Services
Для службы, не привязан протокол tooa определенной связи или стека, например WebAPI, Windows Communication Foundation (WCF) или другие, hello надежного обмена framework предоставляет механизм удаленного взаимодействия tooquickly и легко настроить удаленного вызова процедур для службы.

## <a name="set-up-remoting-on-a-service"></a>Настройка удаленного доступа в службе
Процесс настройки удаленного доступа для службы состоит из двух простых этапов.

1. Создайте интерфейс для tooimplement вашей службы. Этот интерфейс определяет hello методы, которые будут доступны для удаленного вызова процедур для службы. Hello методы должны быть возвращающий задачу асинхронный метод. должен быть реализован интерфейс Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal, hello службы имеет интерфейс удаленного взаимодействия.
2. Используйте прослушиватель удаленного взаимодействия в службе. Это реализация `ICommunicationListener` , которая предоставляет возможности удаленного взаимодействия. Hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` пространство имен содержит метод расширения`CreateServiceRemotingListener` без сохранения состояния и с отслеживанием состояния служб, не должен используется toocreate прослушивателя удаленного взаимодействия использовать протокол транспорта удаленного взаимодействия по умолчанию hello.

Примечание: hello `Remoting` пространство имен доступно как отдельный nuget пакету, вызываемому`Microsoft.ServiceFabric.Services.Remoting` 

Например hello следующей без сохранения состояния службы предоставляет один метод tooget «Hello World», через удаленный вызов процедуры.

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> Hello аргументы и hello возвращают типы в интерфейс службы hello может быть любой простой, сложных или пользовательских типов, но они должны быть сериализуемыми, hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Вызов удаленных методов службы
Вызов методов службы с помощью удаленного взаимодействия стека hello делается с помощью toohello локальный прокси-службы через hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` класса. Hello `ServiceProxy` метод создает локальный прокси-сервер, используя же интерфейс, hello службы реализует hello. С прокси-сервера можно просто вызвать методы интерфейса hello удаленно.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

Hello удаленного взаимодействия framework распространяет исключения на клиенте toohello hello службы. Поэтому обработка исключений логику на приветствия клиента с помощью `ServiceProxy` может напрямую обрабатывать исключения, которые hello служба вызывает исключение.

## <a name="service-proxy-lifetime"></a>Время существования ServiceProxy
Создание ServiceProxy — упрощенная операция, поэтому пользователь может создать столько прокси-серверов, сколько нужно. Прокси-сервер службы можно использовать повторно, если он нужен пользователю. Пользователь может повторно использовать hello один прокси-сервер при возникновении исключения. Каждый ServiceProxy содержит обменом данными сайтами клиента toosend сообщения по сети hello. При вызове API, у нас есть внутренняя проверка toosee Если связи клиента является допустимым. На основании этого результата, создаются заново hello связи клиента. Поэтому пользователь не обязательно serviceproxy toorecreate при возникновении исключения.

### <a name="serviceproxyfactory-lifetime"></a>Время существования ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) — это фабрика, которая создает прокси-сервер для различных интерфейсов удаленного взаимодействия. Если вы используете API ServiceProxy.Create для создания прокси-сервера, платформа создает hello singelton ServiceProxyFactory.
Это полезно toocreate один вручную при необходимости toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) свойства.
Создание фабрики — ресурсоемкая операция. ServiceProxyFactory хранит кэш клиента обмена данными.
Лучший способ — toocache ServiceProxyFactory то же время.

## <a name="remoting-exception-handling"></a>Обработка исключений удаленного взаимодействия
Все hello удаленного исключение, созданное API службы отправляются назад toohello клиента как AggregateException. RemoteExceptions в противном случае должны быть сериализуемыми DataContract [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) выдается прокси toohello API с Ошибка сериализации hello в нем.

ServiceProxy обрабатывать все исключения отработки отказа для раздела службы hello она создана для. Повторно разрешает hello конечных точек, если имеется вызов hello Exceptions(Non-Transient Exceptions) отработки отказа и повторные попытки с hello правильную конечную точку. Число повторных попыток для исключения отработки отказа не ограничено.
В случае TransientExceptions только повторяет вызов hello.

Параметры повтора по умолчанию определяются [OperationRetrySettings] (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Пользователь может настроить эти значения, передав конструктору tooServiceProxyFactory OperationRetrySettings объекта.

## <a name="next-steps"></a>Дальнейшие действия
* [Веб-API с OWIN в модели Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Взаимодействие WCF с Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Защита обмена данными для Reliable Services](service-fabric-reliable-services-secure-communication.md)
