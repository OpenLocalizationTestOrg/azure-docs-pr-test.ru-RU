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
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="c59bd-103">Удаленное взаимодействие службы с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c59bd-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="c59bd-104">Для службы, не привязан протокол tooa определенной связи или стека, например WebAPI, Windows Communication Foundation (WCF) или другие, hello надежного обмена framework предоставляет механизм удаленного взаимодействия tooquickly и легко настроить удаленного вызова процедур для службы.</span><span class="sxs-lookup"><span data-stu-id="c59bd-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="c59bd-105">Настройка удаленного доступа в службе</span><span class="sxs-lookup"><span data-stu-id="c59bd-105">Set up remoting on a service</span></span>
<span data-ttu-id="c59bd-106">Процесс настройки удаленного доступа для службы состоит из двух простых этапов.</span><span class="sxs-lookup"><span data-stu-id="c59bd-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="c59bd-107">Создайте интерфейс для tooimplement вашей службы.</span><span class="sxs-lookup"><span data-stu-id="c59bd-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="c59bd-108">Этот интерфейс определяет hello методы, которые будут доступны для удаленного вызова процедур для службы.</span><span class="sxs-lookup"><span data-stu-id="c59bd-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="c59bd-109">Hello методы должны быть возвращающий задачу асинхронный метод.</span><span class="sxs-lookup"><span data-stu-id="c59bd-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="c59bd-110">должен быть реализован интерфейс Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal, hello службы имеет интерфейс удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="c59bd-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="c59bd-111">Используйте прослушиватель удаленного взаимодействия в службе.</span><span class="sxs-lookup"><span data-stu-id="c59bd-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="c59bd-112">Это реализация `ICommunicationListener` , которая предоставляет возможности удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="c59bd-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="c59bd-113">Hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` пространство имен содержит метод расширения`CreateServiceRemotingListener` без сохранения состояния и с отслеживанием состояния служб, не должен используется toocreate прослушивателя удаленного взаимодействия использовать протокол транспорта удаленного взаимодействия по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c59bd-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="c59bd-114">Примечание: hello `Remoting` пространство имен доступно как отдельный nuget пакету, вызываемому`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="c59bd-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="c59bd-115">Например hello следующей без сохранения состояния службы предоставляет один метод tooget «Hello World», через удаленный вызов процедуры.</span><span class="sxs-lookup"><span data-stu-id="c59bd-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="c59bd-116">Hello аргументы и hello возвращают типы в интерфейс службы hello может быть любой простой, сложных или пользовательских типов, но они должны быть сериализуемыми, hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="c59bd-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="c59bd-117">Вызов удаленных методов службы</span><span class="sxs-lookup"><span data-stu-id="c59bd-117">Call remote service methods</span></span>
<span data-ttu-id="c59bd-118">Вызов методов службы с помощью удаленного взаимодействия стека hello делается с помощью toohello локальный прокси-службы через hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` класса.</span><span class="sxs-lookup"><span data-stu-id="c59bd-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="c59bd-119">Hello `ServiceProxy` метод создает локальный прокси-сервер, используя же интерфейс, hello службы реализует hello.</span><span class="sxs-lookup"><span data-stu-id="c59bd-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="c59bd-120">С прокси-сервера можно просто вызвать методы интерфейса hello удаленно.</span><span class="sxs-lookup"><span data-stu-id="c59bd-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="c59bd-121">Hello удаленного взаимодействия framework распространяет исключения на клиенте toohello hello службы.</span><span class="sxs-lookup"><span data-stu-id="c59bd-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="c59bd-122">Поэтому обработка исключений логику на приветствия клиента с помощью `ServiceProxy` может напрямую обрабатывать исключения, которые hello служба вызывает исключение.</span><span class="sxs-lookup"><span data-stu-id="c59bd-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="c59bd-123">Время существования ServiceProxy</span><span class="sxs-lookup"><span data-stu-id="c59bd-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="c59bd-124">Создание ServiceProxy — упрощенная операция, поэтому пользователь может создать столько прокси-серверов, сколько нужно.</span><span class="sxs-lookup"><span data-stu-id="c59bd-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="c59bd-125">Прокси-сервер службы можно использовать повторно, если он нужен пользователю.</span><span class="sxs-lookup"><span data-stu-id="c59bd-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="c59bd-126">Пользователь может повторно использовать hello один прокси-сервер при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="c59bd-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="c59bd-127">Каждый ServiceProxy содержит обменом данными сайтами клиента toosend сообщения по сети hello.</span><span class="sxs-lookup"><span data-stu-id="c59bd-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="c59bd-128">При вызове API, у нас есть внутренняя проверка toosee Если связи клиента является допустимым.</span><span class="sxs-lookup"><span data-stu-id="c59bd-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="c59bd-129">На основании этого результата, создаются заново hello связи клиента.</span><span class="sxs-lookup"><span data-stu-id="c59bd-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="c59bd-130">Поэтому пользователь не обязательно serviceproxy toorecreate при возникновении исключения.</span><span class="sxs-lookup"><span data-stu-id="c59bd-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="c59bd-131">Время существования ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="c59bd-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="c59bd-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) — это фабрика, которая создает прокси-сервер для различных интерфейсов удаленного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="c59bd-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="c59bd-133">Если вы используете API ServiceProxy.Create для создания прокси-сервера, платформа создает hello singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="c59bd-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="c59bd-134">Это полезно toocreate один вручную при необходимости toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) свойства.</span><span class="sxs-lookup"><span data-stu-id="c59bd-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="c59bd-135">Создание фабрики — ресурсоемкая операция.</span><span class="sxs-lookup"><span data-stu-id="c59bd-135">Factory is an expensive operation.</span></span> <span data-ttu-id="c59bd-136">ServiceProxyFactory хранит кэш клиента обмена данными.</span><span class="sxs-lookup"><span data-stu-id="c59bd-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="c59bd-137">Лучший способ — toocache ServiceProxyFactory то же время.</span><span class="sxs-lookup"><span data-stu-id="c59bd-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="c59bd-138">Обработка исключений удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="c59bd-138">Remoting Exception Handling</span></span>
<span data-ttu-id="c59bd-139">Все hello удаленного исключение, созданное API службы отправляются назад toohello клиента как AggregateException.</span><span class="sxs-lookup"><span data-stu-id="c59bd-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="c59bd-140">RemoteExceptions в противном случае должны быть сериализуемыми DataContract [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) выдается прокси toohello API с Ошибка сериализации hello в нем.</span><span class="sxs-lookup"><span data-stu-id="c59bd-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="c59bd-141">ServiceProxy обрабатывать все исключения отработки отказа для раздела службы hello она создана для.</span><span class="sxs-lookup"><span data-stu-id="c59bd-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="c59bd-142">Повторно разрешает hello конечных точек, если имеется вызов hello Exceptions(Non-Transient Exceptions) отработки отказа и повторные попытки с hello правильную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="c59bd-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="c59bd-143">Число повторных попыток для исключения отработки отказа не ограничено.</span><span class="sxs-lookup"><span data-stu-id="c59bd-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="c59bd-144">В случае TransientExceptions только повторяет вызов hello.</span><span class="sxs-lookup"><span data-stu-id="c59bd-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="c59bd-145">Параметры повтора по умолчанию определяются [OperationRetrySettings]</span><span class="sxs-lookup"><span data-stu-id="c59bd-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="c59bd-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Пользователь может настроить эти значения, передав конструктору tooServiceProxyFactory OperationRetrySettings объекта.</span><span class="sxs-lookup"><span data-stu-id="c59bd-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c59bd-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c59bd-147">Next steps</span></span>
* [<span data-ttu-id="c59bd-148">Веб-API с OWIN в модели Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c59bd-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c59bd-149">Взаимодействие WCF с Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c59bd-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="c59bd-150">Защита обмена данными для Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c59bd-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
